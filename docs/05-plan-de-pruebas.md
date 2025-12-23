# Plan de Pruebas del Sistema

## 1. Introducción

Este documento define la estrategia de pruebas del sistema CraftFlow, estableciendo los objetivos, alcance y principales escenarios a validar.

El plan de pruebas se utiliza como guía para la implementación del sistema y como referencia para verificar que los requerimientos funcionales y no funcionales se cumplan correctamente.

---

## 2. Objetivos de las pruebas

Los objetivos principales del plan de pruebas son:

- Validar el correcto funcionamiento de las reglas de negocio
- Verificar la planificación y evaluación de riesgos
- Detectar desvíos y condiciones críticas
- Asegurar que el sistema asista adecuadamente al usuario en la toma de decisiones
- Reducir errores antes del despliegue

---

## 3. Alcance de las pruebas

### 3.1 Incluido en el alcance

- Pruebas de lógica de planificación
- Pruebas de evaluación de riesgo
- Pruebas de actualización de estados
- Pruebas de generación de alertas
- Pruebas de confirmación manual de pedidos con riesgo

---

### 3.2 Fuera del alcance

- Pruebas de carga y estrés
- Pruebas de seguridad avanzadas
- Pruebas de usabilidad con usuarios reales
- Pruebas de integración con sistemas externos

---

## 4. Tipos de pruebas

### 4.1 Pruebas unitarias

Validan funciones y servicios individuales, principalmente relacionados con:

- Cálculo de planificación
- Evaluación de capacidad
- Clasificación de riesgo

---

### 4.2 Pruebas de integración

Validan la interacción entre componentes del sistema, tales como:

- Creación de pedidos con procesos asociados
- Generación y confirmación de planificación
- Actualización de estados y detección de desvíos

---

### 4.3 Pruebas de aceptación

Validan que el sistema cumpla con los escenarios de uso esperados desde el punto de vista del usuario.

---

## 5. Escenarios de prueba principales

### Escenario 1 – Pedido con planificación factible

**Dado:**  
Un pedido con fecha de entrega y proceso productivo compatible con la capacidad disponible.

**Cuando:**  
El sistema genera la planificación.

**Entonces:**  
- El pedido se planifica sin riesgo
- No se requiere confirmación manual
- El pedido queda en estado planificado

---

### Escenario 2 – Pedido con riesgo de incumplimiento

**Dado:**  
Un pedido cuya planificación supera la capacidad disponible antes de la fecha de entrega.

**Cuando:**  
El sistema evalúa la planificación.

**Entonces:**  
- Se detecta riesgo de incumplimiento
- Se informa la causa del riesgo
- El sistema solicita confirmación manual

---

### Escenario 3 – Confirmación manual de pedido con riesgo

**Dado:**  
Un pedido marcado con riesgo de incumplimiento.

**Cuando:**  
El usuario confirma manualmente el pedido.

**Entonces:**  
- El pedido queda confirmado
- El riesgo queda registrado
- El sistema continúa el seguimiento del pedido

---

### Escenario 4 – Detección de desvío durante la ejecución

**Dado:**  
Un pedido planificado correctamente.

**Cuando:**  
Una etapa no se inicia o finaliza en el tiempo estimado.

**Entonces:**  
- El sistema detecta el desvío
- Se genera una alerta
- El pedido se marca como en riesgo

---

### Escenario 5 – Uso de plantillas de procesos

**Dado:**  
Una plantilla de proceso previamente definida.

**Cuando:**  
El usuario crea un nuevo pedido utilizando la plantilla.

**Entonces:**  
- El sistema precarga las etapas
- La planificación se genera automáticamente
- El usuario puede ajustar la planificación

---

## 6. Criterios de aceptación

- El sistema no rechaza pedidos de forma automática
- Toda situación de riesgo es informada de forma clara
- El usuario mantiene siempre la decisión final
- Las alertas se generan únicamente cuando corresponde
- La planificación puede ajustarse manualmente

---

## 7. Consideraciones finales

Este plan de pruebas será utilizado como referencia durante el desarrollo del sistema y podrá ampliarse a medida que se incorporen nuevas funcionalidades.

---
