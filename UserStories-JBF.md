Aquí tienes las **user stories** para los casos de uso de **LTI**, priorizadas según su impacto y necesidad.  

---

### **User Stories - Caso de Uso 1: Publicación de una Vacante**

#### **1. Como Reclutador, quiero crear una vacante con toda la información relevante para que los candidatos puedan postularse de manera efectiva.**  
**Criterios de Aceptación:**
- El sistema permite ingresar título, descripción, requisitos y beneficios del puesto.
- La interfaz es intuitiva y fácil de usar.
- Se pueden adjuntar archivos relevantes (PDFs, imágenes, etc.).

#### **2. Como Reclutador, quiero publicar la vacante en múltiples plataformas desde un solo lugar para maximizar su visibilidad.**  
**Criterios de Aceptación:**
- La vacante se puede distribuir automáticamente en LinkedIn, Indeed, y otras bolsas de empleo configuradas.
- Se confirma la publicación y se muestra un historial de envíos.
- Si una plataforma requiere autenticación, el sistema notifica y guía al usuario.

#### **3. Como Reclutador, quiero recibir notificaciones sobre la publicación de mi vacante para asegurarme de que se realizó correctamente.**  
**Criterios de Aceptación:**
- Se genera una notificación en el sistema cuando la vacante es publicada exitosamente.
- Se envía un correo electrónico de confirmación con un enlace a la vacante publicada.

---

### **User Stories - Caso de Uso 2: Evaluación de Candidatos**

#### **4. Como Reclutador, quiero crear evaluaciones personalizadas para cada vacante para medir las habilidades de los candidatos de manera efectiva.**  
**Criterios de Aceptación:**
- Se pueden definir preguntas de opción múltiple, respuestas abiertas y ejercicios prácticos.
- Se permite configurar el tiempo límite y la ponderación de cada pregunta.
- Se pueden reutilizar evaluaciones previas o modificar plantillas existentes.

#### **5. Como Reclutador, quiero enviar evaluaciones automáticamente a los candidatos para optimizar el proceso de selección.**  
**Criterios de Aceptación:**
- El sistema permite asignar pruebas a candidatos individuales o en grupo.
- Se notifica automáticamente a los candidatos por correo electrónico con un enlace de acceso.
- Se genera un registro de envíos para rastrear qué candidatos han recibido la evaluación.

#### **6. Como Reclutador, quiero visualizar los resultados de las evaluaciones de los candidatos en un formato claro para tomar decisiones informadas.**  
**Criterios de Aceptación:**
- Los resultados se muestran en un tablero con gráficos y puntuaciones detalladas.
- Se permite exportar los resultados en formato PDF o Excel.
- Se pueden agregar comentarios o notas sobre los resultados de los candidatos.

---

### **Priorización de las User Stories**

| Prioridad | User Story |
|-----------|------------|
| 🟢 **Alta** | **(1)** Creación de una vacante con información relevante |
| 🟢 **Alta** | **(2)** Publicación de la vacante en múltiples plataformas |
| 🟢 **Alta** | **(4)** Creación de evaluaciones personalizadas |
| 🟡 **Media** | **(5)** Envío automático de evaluaciones a los candidatos |
| 🟡 **Media** | **(6)** Visualización y análisis de resultados de evaluaciones |
| 🟡 **Media** | **(3)** Notificación de publicación de vacantes |

---

### **Justificación de la Prioridad**
1. **Las historias (1) y (2) son esenciales**, ya que sin la creación y publicación de vacantes, el sistema no cumple su propósito principal.  
2. **La historia (4) es prioritaria**, porque la evaluación es un paso clave en la selección de candidatos.  
3. **Las historias (5) y (6) son de prioridad media**, ya que complementan el proceso de evaluación pero no impiden la operación del sistema si no están implementadas desde el inicio.  
4. **La historia (3) tiene menor prioridad**, ya que es una funcionalidad informativa que mejora la experiencia del usuario pero no es crítica para el funcionamiento del sistema.  

---
Tickets tecnicos
---

Aquí tienes los **tickets técnicos** necesarios para la **User Story 1: Creación de una vacante con información relevante**, divididos en **Front-End** y **Back-End**.

---

## **🔹 Backlog Técnico para la Creación de una Vacante**

### **🔹 BACK-END (BE)**

#### **1. BE - Diseño y Creación del Modelo de Datos para Vacantes**  
📌 **Descripción:** Definir la estructura de la base de datos para almacenar vacantes.  
📌 **Tareas:**
- Crear tabla `job_postings` con campos como `title`, `description`, `requirements`, `benefits`, `salary_range`, `location`, `created_at`, `updated_at`, etc.
- Configurar relaciones con otras tablas (`users`, `applications`, etc.).
- Implementar migraciones en la base de datos.

📌 **Criterios de Aceptación:**
✅ Se debe poder crear, actualizar y eliminar registros de vacantes en la base de datos.  
✅ La estructura debe permitir agregar más campos en el futuro sin afectar la compatibilidad.

---

#### **2. BE - Creación del Endpoint para Registrar una Nueva Vacante**  
📌 **Descripción:** Implementar un endpoint RESTful para que el front-end pueda enviar los datos de una nueva vacante.  
📌 **Tareas:**
- Crear el endpoint `POST /api/jobs` que reciba datos en JSON.
- Validar los datos de entrada (campos obligatorios, formato, etc.).
- Guardar la vacante en la base de datos.
- Retornar un código 201 con la información de la vacante creada.

📌 **Criterios de Aceptación:**
✅ Si los datos son correctos, el sistema responde con `201 Created` y los detalles de la vacante.  
✅ Si faltan datos obligatorios, se devuelve `400 Bad Request` con un mensaje de error.  
✅ Las validaciones aseguran que los datos ingresados sean correctos (ej. salario numérico, título con mínimo de caracteres, etc.).  

---

#### **3. BE - Implementación de Seguridad y Autenticación**  
📌 **Descripción:** Asegurar que solo usuarios autenticados puedan crear vacantes.  
📌 **Tareas:**
- Integrar autenticación con JWT o sesión para restringir el acceso.
- Solo los reclutadores pueden crear vacantes (verificación de roles).
- Manejo de permisos y control de acceso.

📌 **Criterios de Aceptación:**
✅ Un usuario no autenticado recibe un `401 Unauthorized`.  
✅ Un usuario sin permisos recibe un `403 Forbidden`.  

---

### **🔹 FRONT-END (FE)**

#### **4. FE - Creación del Formulario de Creación de Vacantes**  
📌 **Descripción:** Desarrollar un formulario en el front-end donde los reclutadores puedan ingresar los datos de la vacante.  
📌 **Tareas:**
- Crear una pantalla `/new-job` con un formulario para ingresar los datos.
- Incluir validaciones en los campos (campos obligatorios, longitud mínima, formatos, etc.).
- Implementar un botón de "Guardar" que envíe la solicitud al back-end.

📌 **Criterios de Aceptación:**
✅ La interfaz debe ser clara y fácil de usar.  
✅ Los campos deben validarse antes de enviar la solicitud.  
✅ Si la vacante se guarda correctamente, se muestra un mensaje de éxito.  
✅ Si hay un error, se muestra un mensaje adecuado al usuario.  

---

#### **5. FE - Llamado al Endpoint de Creación de Vacantes**  
📌 **Descripción:** Enviar los datos ingresados en el formulario al back-end.  
📌 **Tareas:**
- Conectar el formulario con el endpoint `POST /api/jobs`.
- Manejar respuestas del servidor (éxito y error).
- Mostrar un mensaje de éxito o error según la respuesta.

📌 **Criterios de Aceptación:**
✅ Si la vacante se guarda correctamente, redirigir a la página de detalles de la vacante.  
✅ Si hay un error, mostrar un mensaje claro al usuario.  

---

#### **6. FE - Diseño y Estilización de la Página**  
📌 **Descripción:** Aplicar estilos al formulario para que tenga un diseño atractivo y consistente con la UI/UX.  
📌 **Tareas:**
- Implementar estilos con TailwindCSS o CSS Modules.
- Asegurar que la UI sea responsive.
- Mantener la coherencia con la identidad visual de la plataforma.

📌 **Criterios de Aceptación:**
✅ El formulario es responsive y se adapta bien a móviles y escritorio.  
✅ Los elementos tienen un diseño limpio y profesional.  

---

### **🔹 Priorización de Tickets**

| Prioridad | Ticket Técnico |
|-----------|---------------|
| 🟢 **Alta** | BE - Diseño y Creación del Modelo de Datos |
| 🟢 **Alta** | BE - Creación del Endpoint para Registrar Vacantes |
| 🟢 **Alta** | FE - Creación del Formulario de Vacantes |
| 🟡 **Media** | FE - Llamado al Endpoint |
| 🟡 **Media** | FE - Diseño y Estilización de la Página |
| 🟡 **Media** | BE - Implementación de Seguridad y Autenticación |

---
