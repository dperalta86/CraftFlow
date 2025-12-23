# Modelado de Datos del Sistema

## 1. Introducción

Este documento describe el modelo de datos del sistema CraftFlow, identificando las entidades principales, sus atributos y relaciones.

El objetivo del modelado es representar de forma clara el dominio del problema, sirviendo como base para el diseño de la base de datos y la implementación posterior.

---

## 2. Principios del modelado

El modelo de datos se basa en los siguientes principios:

- Representar conceptos del negocio, no decisiones técnicas
- Mantener flexibilidad para distintos tipos de artesanos
- Evitar sobreespecialización en un rubro puntual
- Permitir evolución futura del sistema

---

## 3. Entidades principales

### 3.1 Usuario

Representa a la persona que utiliza el sistema.

**Atributos:**
- id
- nombre
- email
- password_hash
- rol
- fecha_creacion
- activo

**Observaciones:**
- Un usuario puede gestionar uno o varios emprendimientos
- El rol permite futuras extensiones (admin, operador, etc.)

---

### 3.2 Emprendimiento

Representa un negocio artesanal que utiliza el sistema.

**Atributos:**
- id
- nombre
- descripcion
- tipo_actividad
- fecha_creacion
- activo

**Relaciones:**
- Un emprendimiento tiene uno o más usuarios
- Un emprendimiento tiene pedidos, procesos y plantillas

---

### 3.3 Cliente

Representa al cliente final que realiza pedidos.

**Atributos:**
- id
- nombre
- contacto
- notas
- fecha_creacion

**Relaciones:**
- Un cliente puede tener múltiples pedidos

---

### 3.4 Pedido

Representa un encargo realizado por un cliente.

**Atributos:**
- id
- fecha_entrega
- estado
- riesgo
- observaciones
- fecha_creacion

**Relaciones:**
- Un pedido pertenece a un cliente
- Un pedido pertenece a un emprendimiento
- Un pedido tiene uno o más procesos productivos

---

### 3.5 Proceso Productivo

Representa el flujo de trabajo asociado a un pedido.

**Atributos:**
- id
- nombre
- descripcion
- orden
- estado
- fecha_inicio_estimada
- fecha_fin_estimada
- fecha_inicio_real
- fecha_fin_real

**Relaciones:**
- Un proceso pertenece a un pedido
- Un proceso tiene una o más etapas

---

### 3.6 Etapa

Representa una unidad mínima de trabajo dentro de un proceso.

**Atributos:**
- id
- nombre
- duracion_estimada
- duracion_real
- estado
- orden

**Relaciones:**
- Una etapa pertenece a un proceso

---

### 3.7 Plantilla de Proceso

Representa un proceso reutilizable basado en experiencias anteriores.

**Atributos:**
- id
- nombre
- descripcion
- activo
- fecha_creacion

**Relaciones:**
- Una plantilla tiene una o más etapas
- Una plantilla pertenece a un emprendimiento

---

### 3.8 Alerta

Representa una notificación generada por el sistema.

**Atributos:**
- id
- tipo
- mensaje
- nivel
- fecha_creacion
- leida

**Relaciones:**
- Una alerta puede estar asociada a un pedido

---

## 4. Relaciones principales (resumen)

- Usuario ↔ Emprendimiento (N a N)
- Emprendimiento → Pedido (1 a N)
- Cliente → Pedido (1 a N)
- Pedido → Proceso Productivo (1 a N)
- Proceso Productivo → Etapa (1 a N)
- Emprendimiento → Plantilla de Proceso (1 a N)
- Pedido → Alerta (1 a N)

---

## 5. Estados relevantes

### Pedido
- creado
- planificado
- confirmado
- en_proceso
- en_riesgo
- finalizado

### Proceso / Etapa
- pendiente
- en_progreso
- completado
- retrasado

---

## 6. Consideraciones de diseño

- El sistema prioriza la trazabilidad del pedido
- Las duraciones estimadas y reales permiten análisis posteriores
- El riesgo se maneja como un estado explícito
- Las plantillas reducen la carga operativa del usuario

---

## 7. Próximos pasos

A partir de este modelo de datos se podrá:

- Definir el esquema lógico de la base de datos
- Diseñar la API REST
- Implementar las reglas de negocio
- Escribir pruebas basadas en entidades reales

---
