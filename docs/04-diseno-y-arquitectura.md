# Diseño y Arquitectura del Sistema

## 1. Introducción

Este documento describe la arquitectura general del sistema CraftFlow y las principales decisiones de diseño adoptadas para su implementación.

El diseño se basa en el modelo conceptual definido previamente y busca lograr un equilibrio entre simplicidad, escalabilidad y mantenibilidad, priorizando un enfoque pragmático acorde al tamaño y contexto del emprendimiento.

---

## 2. Arquitectura general

CraftFlow adopta una arquitectura de tipo cliente-servidor, separando responsabilidades entre:

- Interfaz de usuario (Frontend)
- Lógica de negocio (Backend)
- Persistencia de datos (Base de datos)

La comunicación entre el frontend y el backend se realiza mediante una API REST.

---

## 3. Componentes del sistema

### 3.1 Frontend

El frontend es responsable de la interacción con el usuario y la visualización del estado del sistema.

**Responsabilidades principales:**
- Registro y edición de pedidos
- Selección de plantillas de procesos
- Visualización de la planificación (Gantt simplificado)
- Visualización de alertas y riesgos
- Confirmación manual de pedidos con riesgo

**Características de diseño:**
- Aplicación web progresiva (PWA)
- Orientada a uso móvil
- Interfaz simple y centrada en tareas operativas

---

### 3.2 Backend

El backend implementa la lógica de negocio del sistema y expone una API REST para el frontend.

**Responsabilidades principales:**
- Gestión de pedidos y procesos productivos
- Generación de planificación sugerida
- Evaluación de riesgo de incumplimiento
- Emisión de alertas
- Autenticación y control de acceso

**Características de diseño:**
- Arquitectura modular
- Separación clara entre controladores, servicios y acceso a datos
- Validación de reglas de negocio centralizada

---

### 3.3 Base de datos

La base de datos almacena la información persistente del sistema.

**Responsabilidades principales:**
- Persistencia de pedidos, procesos, etapas y planificación
- Garantizar integridad y consistencia de los datos
- Soportar consultas temporales para planificación y visualización

---

## 4. Capas del backend (visión lógica)

El backend se organiza en las siguientes capas lógicas:

### 4.1 Capa de presentación (API)

- Controladores REST
- Recepción y validación de solicitudes
- Exposición de endpoints claros y consistentes

---

### 4.2 Capa de aplicación / servicios

- Implementación de casos de uso
- Orquestación de la lógica de planificación
- Evaluación de riesgo
- Coordinación entre entidades del dominio

---

### 4.3 Capa de dominio

- Representación de entidades y reglas del negocio
- Independencia de detalles técnicos
- Base conceptual del sistema

---

### 4.4 Capa de infraestructura

- Acceso a base de datos
- Integración con servicios externos
- Manejo de autenticación y seguridad

---

## 5. Flujo general de un pedido

1. El usuario registra un nuevo pedido
2. Selecciona una plantilla de proceso o define un proceso personalizado
3. El sistema genera una planificación sugerida
4. Se evalúa el nivel de riesgo asociado
5. El usuario revisa la planificación:
   - Si el riesgo es bajo, confirma el pedido
   - Si el riesgo es medio o alto, el sistema informa las causas y solicita confirmación manual
6. El pedido pasa a estado planificado
7. A medida que avanza la producción, el usuario actualiza el estado de las etapas
8. El sistema detecta desvíos y emite alertas cuando corresponde

---

## 6. Visualización de la planificación

La planificación se representa mediante un Gantt simplificado, que muestra:

- Pedidos activos
- Etapas por pedido
- Fechas estimadas de inicio y finalización
- Indicadores visuales de riesgo o atraso

El objetivo de esta visualización es facilitar la comprensión rápida del estado del trabajo sin complejidad excesiva.

---

## 7. Seguridad y acceso

- El acceso al sistema requiere autenticación
- Las credenciales se almacenan de forma segura
- La API restringe el acceso a operaciones sensibles

Dado el alcance del sistema, se adopta un esquema de seguridad simple, priorizando la protección de la información sin agregar complejidad innecesaria.

---

## 8. Consideraciones de escalabilidad y mantenimiento

- El sistema está diseñado para un único emprendimiento en su versión inicial
- La arquitectura permite extender funcionalidades de forma incremental
- La separación de capas facilita el mantenimiento y evolución del sistema

---

## 9. Justificación de decisiones

- Se adopta una arquitectura REST por su simplicidad y amplia adopción
- La separación frontend/backend permite independencia tecnológica
- La planificación se implementa como sugerencia y no como automatismo rígido
- Se prioriza la claridad del dominio por sobre optimizaciones prematuras

---

## 10. Alcance del documento

Este documento describe la arquitectura lógica y conceptual del sistema.

No incluye:
- Detalles de implementación
- Definición de endpoints específicos
- Diseño físico de la base de datos

Estos aspectos serán abordados en etapas posteriores del proyecto.

---
