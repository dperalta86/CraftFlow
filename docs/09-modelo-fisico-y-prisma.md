# Modelo Físico y Prisma Schema

## 1. Introducción

Este documento describe el modelo físico de datos del sistema CraftFlow y su implementación mediante Prisma ORM sobre PostgreSQL.

El diseño se basa en el modelo conceptual, el DER y los casos de uso definidos previamente, manteniendo independencia del frontend y priorizando claridad, trazabilidad y mantenibilidad.

---

## 2. Convenciones generales

### 2.1 Identificadores
- Todas las entidades utilizan un identificador `id`
- Tipo: UUID
- Generados automáticamente

---

### 2.2 Nombres
- Tablas y modelos: PascalCase (Prisma)
- Campos: camelCase
- Tablas intermedias explícitas para relaciones N–N

---

### 2.3 Timestamps
- `createdAt`: fecha de creación
- `updatedAt`: fecha de última modificación (cuando aplica)

---

### 2.4 Soft delete
- Se utiliza el campo `active` en entidades principales
- Evita borrados físicos innecesarios

---

### 2.5 Estados
- Los estados se manejan mediante enums
- El riesgo se maneja como atributo independiente del estado

---

## 3. Enums del sistema

```prisma
enum UserRole {
  ADMIN
  USER
}

enum OrderStatus {
  CREATED
  PLANNED
  CONFIRMED
  IN_PROGRESS
  AT_RISK
  COMPLETED
}

enum ProcessStatus {
  PENDING
  IN_PROGRESS
  COMPLETED
  DELAYED
}

enum AlertLevel {
  INFO
  WARNING
  CRITICAL
}
```

## 4. Prisma Schema

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id           String   @id @default(uuid())
  name         String
  email        String   @unique
  passwordHash String
  role         UserRole
  active       Boolean  @default(true)
  createdAt    DateTime @default(now())

  businesses   UserBusiness[]
}

model Business {
  id            String   @id @default(uuid())
  name          String
  description   String?
  activityType  String
  active        Boolean  @default(true)
  createdAt     DateTime @default(now())

  users         UserBusiness[]
  clients       Client[]
  orders        Order[]
  templates     ProcessTemplate[]
}

model UserBusiness {
  userId     String
  businessId String

  user       User     @relation(fields: [userId], references: [id])
  business   Business @relation(fields: [businessId], references: [id])

  @@id([userId, businessId])
}

model Client {
  id           String   @id @default(uuid())
  name         String
  contact      String?
  notes        String?
  createdAt    DateTime @default(now())

  businessId   String
  business     Business @relation(fields: [businessId], references: [id])

  orders       Order[]
}

model Order {
  id            String      @id @default(uuid())
  deliveryDate  DateTime
  status        OrderStatus
  risk          Boolean     @default(false)
  notes         String?
  createdAt     DateTime    @default(now())

  clientId      String
  businessId    String

  client        Client      @relation(fields: [clientId], references: [id])
  business      Business    @relation(fields: [businessId], references: [id])

  processes     ProductionProcess[]
  alerts        Alert[]
}

model ProductionProcess {
  id               String        @id @default(uuid())
  name             String
  description      String?
  orderIndex       Int
  status           ProcessStatus

  estimatedStart   DateTime
  estimatedEnd     DateTime
  actualStart      DateTime?
  actualEnd        DateTime?

  orderId          String
  order            Order         @relation(fields: [orderId], references: [id])

  stages           Stage[]
}

model Stage {
  id               String        @id @default(uuid())
  name             String
  estimatedDuration Int
  actualDuration   Int?
  status           ProcessStatus
  orderIndex       Int

  processId        String
  process          ProductionProcess @relation(fields: [processId], references: [id])
}

model ProcessTemplate {
  id            String   @id @default(uuid())
  name          String
  description   String?
  active        Boolean  @default(true)
  createdAt     DateTime @default(now())

  businessId    String
  business      Business @relation(fields: [businessId], references: [id])

  stages        TemplateStage[]
}

model TemplateStage {
  id               String   @id @default(uuid())
  name             String
  estimatedDuration Int
  orderIndex       Int

  templateId       String
  template         ProcessTemplate @relation(fields: [templateId], references: [id])
}

model Alert {
  id           String     @id @default(uuid())
  type         String
  message      String
  level        AlertLevel
  read         Boolean    @default(false)
  createdAt    DateTime   @default(now())

  orderId      String
  order        Order      @relation(fields: [orderId], references: [id])
}
```