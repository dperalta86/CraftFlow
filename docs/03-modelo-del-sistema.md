# Modelo del Sistema

## 1. Introducción

Este documento describe el modelo conceptual del sistema CraftFlow, identificando las principales entidades del dominio, sus responsabilidades y las relaciones entre ellas.

El modelo fue definido a partir del análisis del problema y los requerimientos funcionales, y sirve como base para el diseño de la arquitectura, el modelo de datos y la implementación del sistema.

---

## 2. Visión general del dominio

CraftFlow se orienta a la gestión de pedidos artesanales bajo un esquema de producción por etapas.  
Cada pedido representa un compromiso de entrega que debe ser planificado considerando tiempos, capacidad y riesgos operativos.

El sistema no toma decisiones finales, sino que asiste al usuario mediante planificación sugerida, visualización del avance y alertas.

---

## 3. Entidades principales

### 3.1 Pedido

Representa un pedido realizado por un cliente y comprometido para una fecha de entrega determinada.

**Responsabilidades:**
- Almacenar la información general del pedido
- Asociar un proceso productivo
- Mantener el estado general del pedido
- Registrar el nivel de riesgo asociado a la planificación

**Atributos principales:**
- Identificador
- Cliente
- Fecha de entrega
- Cantidad
- Nivel de complejidad
- Observaciones
- Estado del pedido (planificado, en curso, finalizado, con riesgo)
- Planificación confirmada (sí / no)

---

### 3.2 Proceso Productivo

Define el conjunto de etapas necesarias para completar un pedido.

Un proceso productivo puede ser reutilizado como plantilla para distintos pedidos.

**Responsabilidades:**
- Definir la secuencia de etapas
- Establecer duraciones estimadas
- Servir como base para la planificación

**Atributos principales:**
- Identificador
- Nombre
- Tipo (plantilla / personalizado)
- Conjunto de etapas asociadas

---

### 3.3 Etapa

Representa una unidad de trabajo dentro de un proceso productivo.

**Responsabilidades:**
- Definir una actividad concreta del proceso
- Registrar su estado de avance
- Contribuir al cálculo de la planificación y riesgo

**Atributos principales:**
- Identificador
- Nombre
- Orden dentro del proceso
- Duración estimada
- Estado (pendiente, en curso, finalizada)
- Fecha estimada de inicio
- Fecha estimada de finalización

---

### 3.4 Planificación

Representa la asignación temporal de las etapas de un pedido.

La planificación puede ser sugerida automáticamente por el sistema y luego confirmada o ajustada por el usuario.

**Responsabilidades:**
- Calcular fechas de inicio y fin de cada etapa
- Evaluar factibilidad temporal
- Identificar desvíos respecto al plan

**Atributos principales:**
- Identificador
- Pedido asociado
- Fecha de generación
- Estado (sugerida, confirmada, ajustada)
- Conjunto de etapas planificadas

---

### 3.5 Riesgo

Representa el nivel de probabilidad de incumplimiento de la fecha de entrega de un pedido según su planificación.

**Responsabilidades:**
- Clasificar el nivel de riesgo del pedido
- Explicar las causas del riesgo
- Servir como base para alertas y confirmaciones manuales

**Atributos principales:**
- Nivel de riesgo (bajo, medio, alto)
- Descripción del riesgo
- Etapas críticas involucradas

---

### 3.6 Capacidad Productiva

Representa la disponibilidad de trabajo del emprendimiento en un período determinado.

**Responsabilidades:**
- Definir límites de producción por día
- Servir como restricción para la planificación
- Apoyar el cálculo de factibilidad

**Atributos principales:**
- Capacidad diaria estimada
- Días no laborables
- Excepciones (fechas especiales)

---

## 4. Relaciones entre entidades

- Un **Pedido** tiene asociado un **Proceso Productivo**
- Un **Proceso Productivo** está compuesto por una o más **Etapas**
- Un **Pedido** tiene una **Planificación**
- Una **Planificación** organiza temporalmente las **Etapas**
- Un **Pedido** puede tener asociado un **Riesgo**
- La **Capacidad Productiva** condiciona la **Planificación**

---

## 5. Estados del sistema (visión simplificada)

### Estados de un pedido

- Registrado
- Planificado
- En curso
- Con riesgo
- Finalizado

---

### Estados de una etapa

- Pendiente
- En curso
- Finalizada

---

## 6. Consideraciones de diseño

- El modelo prioriza la claridad y simplicidad sobre la automatización excesiva
- Las decisiones finales recaen siempre en el usuario
- El sistema debe permitir ajustes manuales en cualquier etapa del proceso
- El modelo está diseñado para ser extensible a otros tipos de producción artesanal

---

## 7. Alcance del modelo

Este modelo conceptual sirve como base para:
- Diseño de la arquitectura del sistema
- Definición del modelo de datos
- Implementación del backend y frontend
- Diseño de casos de prueba

No contempla detalles técnicos de implementación ni decisiones específicas de tecnología.

---
