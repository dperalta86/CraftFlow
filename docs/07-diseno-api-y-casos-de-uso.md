# Diseño de API y Casos de Uso

## 1. Introducción

Este documento describe los principales casos de uso del sistema CraftFlow y el diseño inicial de su API REST.

El objetivo es definir cómo interactúan los usuarios con el sistema y qué operaciones expone el backend, sirviendo como base para la implementación técnica.

---

## 2. Principios de diseño de la API

La API del sistema se diseña bajo los siguientes principios:

- Arquitectura REST
- Separación clara de responsabilidades
- Endpoints orientados a casos de uso reales
- Simplicidad y legibilidad
- Evitar acoplamiento innecesario con el frontend

---

## 3. Actores del sistema

- **Usuario**: persona que gestiona el emprendimiento artesanal
- **Sistema**: lógica interna que planifica, evalúa riesgos y genera alertas

---

## 4. Casos de uso principales

### CU-01 – Gestión de usuarios

**Descripción:**  
Permite registrar, autenticar y gestionar usuarios del sistema.

**Operaciones:**
- Registrar usuario
- Iniciar sesión
- Obtener perfil

---

### CU-02 – Gestión de emprendimiento

**Descripción:**  
Permite crear y administrar un emprendimiento artesanal.

**Operaciones:**
- Crear emprendimiento
- Obtener datos del emprendimiento
- Asociar usuarios al emprendimiento

---

### CU-03 – Gestión de clientes

**Descripción:**  
Permite administrar clientes finales.

**Operaciones:**
- Crear cliente
- Listar clientes
- Actualizar datos de cliente

---

### CU-04 – Creación de pedido

**Descripción:**  
Permite registrar un pedido y evaluar su viabilidad.

**Flujo principal:**
1. El usuario registra un pedido con fecha de entrega
2. Selecciona una plantilla o define un proceso manualmente
3. El sistema genera una planificación automática
4. El sistema evalúa la capacidad y el riesgo

**Resultados posibles:**
- Pedido planificado sin riesgo
- Pedido con riesgo que requiere confirmación manual

---

### CU-05 – Confirmación manual de pedido con riesgo

**Descripción:**  
Permite al usuario aceptar un pedido aun cuando exista riesgo de incumplimiento.

**Flujo:**
1. El sistema informa el riesgo detectado
2. El usuario confirma o cancela el pedido
3. El sistema registra la decisión

---

### CU-06 – Seguimiento de pedidos

**Descripción:**  
Permite visualizar el avance de los pedidos y sus procesos.

**Operaciones:**
- Listar pedidos
- Ver detalle de un pedido
- Actualizar estado de procesos y etapas

---

### CU-07 – Gestión de plantillas de proceso

**Descripción:**  
Permite crear y reutilizar procesos productivos.

**Operaciones:**
- Crear plantilla
- Listar plantillas
- Editar plantilla

---

### CU-08 – Gestión de alertas

**Descripción:**  
Permite visualizar y gestionar alertas generadas por el sistema.

**Operaciones:**
- Listar alertas
- Marcar alerta como leída

---

## 5. Diseño de endpoints (propuesta inicial)

### Autenticación

- `POST /auth/register`
- `POST /auth/login`
- `GET /auth/me`

---

### Emprendimiento

- `POST /business`
- `GET /business/{id}`

---

### Clientes

- `POST /clients`
- `GET /clients`
- `PUT /clients/{id}`

---

### Pedidos

- `POST /orders`
- `GET /orders`
- `GET /orders/{id}`
- `POST /orders/{id}/confirm`

---

### Procesos y etapas

- `PUT /processes/{id}`
- `PUT /stages/{id}`

---

### Plantillas

- `POST /templates`
- `GET /templates`
- `PUT /templates/{id}`

---

### Alertas

- `GET /alerts`
- `PUT /alerts/{id}/read`

---

## 6. Consideraciones de diseño

- La evaluación de riesgo es responsabilidad exclusiva del backend
- El sistema nunca rechaza pedidos automáticamente
- Toda decisión crítica requiere acción explícita del usuario
- La API prioriza claridad por sobre optimización prematura

---

## 7. Próximos pasos

A partir de este diseño de API se podrá:

- Refinar el modelo de datos
- Construir el DER
- Definir DTOs y contratos
- Implementar controladores y servicios
- Escribir pruebas alineadas a los casos de uso

---
