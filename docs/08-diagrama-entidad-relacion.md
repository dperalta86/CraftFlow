# Diagrama Entidad–Relación (DER)

## 1. Introducción

Este documento describe el Diagrama Entidad–Relación del sistema CraftFlow.

El DER representa el modelo lógico de datos, basado en el modelo conceptual y los casos de uso previamente definidos, y sirve como base para la implementación de la base de datos relacional.

---

## 2. Alcance del DER

El diagrama incluye:

- Entidades principales del sistema
- Atributos relevantes
- Claves primarias (PK)
- Claves foráneas (FK)
- Relaciones y cardinalidades

Quedan fuera del alcance:

- Tipos de datos específicos del motor de base de datos
- Índices y optimizaciones
- Detalles de implementación física

---

## 3. Entidades incluidas

### Usuario
- id (PK)
- nombre
- email
- password_hash
- rol
- activo
- fecha_creacion

---

### Emprendimiento
- id (PK)
- nombre
- descripcion
- tipo_actividad
- activo
- fecha_creacion

---

### Usuario_Emprendimiento
*(entidad intermedia)*

- usuario_id (PK, FK)
- emprendimiento_id (PK, FK)

---

### Cliente
- id (PK)
- nombre
- contacto
- notas
- fecha_creacion

---

### Pedido
- id (PK)
- fecha_entrega
- estado
- riesgo
- observaciones
- fecha_creacion
- cliente_id (FK)
- emprendimiento_id (FK)

---

### Proceso_Productivo
- id (PK)
- nombre
- descripcion
- orden
- estado
- fecha_inicio_estimada
- fecha_fin_estimada
- fecha_inicio_real
- fecha_fin_real
- pedido_id (FK)

---

### Etapa
- id (PK)
- nombre
- duracion_estimada
- duracion_real
- estado
- orden
- proceso_id (FK)

---

### Plantilla_Proceso
- id (PK)
- nombre
- descripcion
- activo
- fecha_creacion
- emprendimiento_id (FK)

---

### Plantilla_Etapa
*(entidad intermedia)*

- plantilla_id (PK, FK)
- nombre
- duracion_estimada
- orden

---

### Alerta
- id (PK)
- tipo
- mensaje
- nivel
- leida
- fecha_creacion
- pedido_id (FK)

---

## 4. Relaciones y cardinalidades

- Usuario ↔ Emprendimiento  
  **N a N**, mediante Usuario_Emprendimiento

- Emprendimiento → Cliente  
  **1 a N**

- Cliente → Pedido  
  **1 a N**

- Emprendimiento → Pedido  
  **1 a N**

- Pedido → Proceso_Productivo  
  **1 a N**

- Proceso_Productivo → Etapa  
  **1 a N**

- Emprendimiento → Plantilla_Proceso  
  **1 a N**

- Plantilla_Proceso → Plantilla_Etapa  
  **1 a N**

- Pedido → Alerta  
  **1 a N**

---

## 5. Consideraciones de diseño

- Se utilizan entidades intermedias para resolver relaciones N–N
- Las entidades reflejan conceptos del negocio y no decisiones técnicas
- El modelo prioriza trazabilidad y flexibilidad
- El diseño permite incorporar nuevos tipos de procesos y actividades

---

## 6. Representación gráfica

El DER del sistema se encuentra disponible en el siguiente archivo: [diagrama DER](docs/diagrams/der.png)

