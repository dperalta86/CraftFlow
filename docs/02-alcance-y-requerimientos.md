# Alcance y Requerimientos del Sistema

## 1. Objetivo del sistema

El objetivo de CraftFlow es asistir a emprendimientos artesanales en la planificación y gestión de pedidos realizados bajo un esquema de producción por etapas, permitiendo controlar la capacidad productiva, visualizar el avance de los pedidos y reducir el riesgo de incumplimiento de fechas de entrega.

El sistema actúa como herramienta de apoyo a la toma de decisiones, sin reemplazar el criterio del usuario.

---

## 2. Alcance del sistema

### 2.1 Incluido en el alcance

El sistema contempla las siguientes funcionalidades:

- Registro y administración de pedidos
- Definición de procesos productivos compuestos por etapas
- Uso de plantillas de procesos productivos reutilizables
- Planificación temporal de pedidos según capacidad estimada
- Evaluación automática de factibilidad y nivel de riesgo
- Visualización del avance de pedidos mediante un Gantt simplificado
- Emisión de alertas ante posibles desvíos
- Confirmación manual de pedidos con riesgo de incumplimiento
- Acceso desde dispositivos móviles mediante una aplicación web progresiva (PWA)

---

### 2.2 Fuera del alcance

Las siguientes funcionalidades quedan fuera del alcance de esta primera versión:

- Gestión contable o facturación
- Integración directa con plataformas de mensajería (ej. WhatsApp)
- Gestión de pagos o cobros
- Automatización de la producción
- Gestión avanzada de múltiples usuarios y roles
- Optimización automática basada en técnicas de aprendizaje automático

Estas funcionalidades podrán considerarse como posibles mejoras futuras.

---

## 3. Actores del sistema

### 3.1 Administrador

Corresponde al responsable del emprendimiento artesanal.  
Tiene control total sobre la configuración del sistema y la gestión de pedidos.

Funciones principales:
- Crear y modificar pedidos
- Seleccionar o definir procesos productivos
- Ajustar manualmente la planificación sugerida
- Visualizar la planificación general
- Recibir alertas y notificaciones
- Confirmar pedidos que presenten riesgo de incumplimiento

---

## 4. Requerimientos funcionales

### RF01 – Gestión de pedidos  
El sistema debe permitir registrar pedidos indicando, como mínimo:
- Cliente
- Fecha de entrega
- Cantidad solicitada
- Nivel de complejidad
- Observaciones adicionales

---

### RF02 – Definición de etapas productivas  
El sistema debe permitir definir procesos productivos compuestos por etapas.

Cada etapa deberá tener:
- Nombre
- Duración estimada
- Orden dentro del proceso

---

### RF03 – Uso de plantillas de procesos  
El sistema debe permitir definir y reutilizar plantillas de procesos productivos con etapas y duraciones predefinidas para agilizar la carga de nuevos pedidos.

---

### RF04 – Planificación temporal de pedidos  
El sistema debe generar una planificación temporal de los pedidos en función de:
- Fecha de entrega comprometida
- Duración estimada de las etapas
- Capacidad productiva disponible

La planificación generada tendrá carácter de sugerencia.

---

### RF05 – Evaluación de riesgo del pedido  
El sistema debe evaluar la planificación propuesta e identificar situaciones en las que exista riesgo de incumplimiento de la fecha de entrega.

El nivel de riesgo deberá ser informado de forma clara al usuario.

---

### RF06 – Confirmación manual de pedidos con riesgo  
Cuando se detecte un riesgo de incumplimiento, el sistema debe:
- Informar las causas del riesgo
- Sugerir alternativas (reprogramación, ajuste de cantidades, etc.)
- Permitir la confirmación manual del pedido bajo responsabilidad del usuario

---

### RF07 – Visualización del estado de los pedidos  
El sistema debe permitir visualizar el estado general de los pedidos y el avance de sus etapas mediante una representación gráfica tipo Gantt simplificado.

---

### RF08 – Actualización del estado de las etapas  
El sistema debe permitir marcar las etapas como:
- Pendiente
- En curso
- Finalizada

---

### RF09 – Detección de desvíos  
El sistema debe identificar desvíos respecto a la planificación prevista y reflejarlos en la visualización y alertas correspondientes.

---

### RF10 – Alertas y notificaciones  
El sistema debe emitir alertas cuando:
- Un pedido se encuentre en riesgo de atraso
- Una etapa crítica no haya sido iniciada o finalizada dentro del tiempo estimado

---

## 5. Requerimientos no funcionales

### RNF01 – Usabilidad  
El sistema debe ser intuitivo y de fácil uso para usuarios sin conocimientos técnicos, minimizando la carga manual de información repetitiva.

---

### RNF02 – Accesibilidad  
El sistema debe poder utilizarse desde dispositivos móviles y de escritorio.

---

### RNF03 – Persistencia de la información  
La información gestionada por el sistema debe persistir de forma segura en una base de datos.

---

### RNF04 – Rendimiento  
El sistema debe ofrecer tiempos de respuesta adecuados para la consulta y actualización de pedidos.

---

### RNF05 – Seguridad  
El sistema debe proteger el acceso a la información mediante mecanismos de autenticación.

---

## 6. Supuestos y restricciones

### Supuestos

- El emprendimiento cuenta con un único responsable de la producción
- Los tiempos estimados de cada etapa son definidos o ajustados por el usuario
- La producción se realiza bajo pedido y no en serie
- El usuario puede asumir riesgos operativos de forma consciente

---

### Restricciones

- El sistema no contempla múltiples plantas de producción
- La planificación se basa en estimaciones y no garantiza resultados exactos
- El sistema no toma decisiones finales, sino que actúa como apoyo a la planificación

---
