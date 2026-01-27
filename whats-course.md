# Propuesta de Proyecto: Plataforma de Cursos vía WhatsApp ("WhatsCourse")

## 1. Resumen Ejecutivo
Esta propuesta detalla el desarrollo de una plataforma educativa que utiliza WhatsApp como el canal principal de entrega de contenido. El objetivo es aprovechar la alta tasa de apertura de WhatsApp para ofrecer micro-aprendizaje (micro-learning) mediante videos, audios y PDFs, combinando la escalabilidad de la automatización con la calidez del soporte humano.

## 2. Modelo de Negocio
El cliente al que se le está preparando esta propuesta vende cursos y capacitaciones, por lo que va a una empresa y ofrece un curso o capacitacion y la empresa a la que va lecontrata un paquete para sus empleados (por ejemplo 30 empleados). Los que desde su whatsapp deben tener acceso a los cursos. 
Descartar la pasarela de pagos porque el cliente ya lo tiene resuelto.
Se debe constriuir una plataforma para seguimientob de los cursos para administradores de la empresa que ofrece el curso, para que sepan los emplados, cual es el curso, el progreso y si aprobo o no, por estudiante.
Se debe Ofrecer examenes tipo preguntas y respuestas para validar el conocimiento adquirido.
tambien prponer que mas se puede ofrecer como evaluaciones.
Tener la opcion de si desea hablar con un tutor humano en caso de que la interaccion con el bot le sea insuficiente. pero iniciallmente va a habla con una ia.
Hay que valorar si usamos herramientas como chatwoot, n8n, para la plataforma web administrativa o se construye todo desde cero.
Hay que hacer la parte tecnica si se necesita servidores, herramientas costos tiempo etc.
Hay que hacer un roadmap 

## 3. Modelo de Interacción: Híbrido
Para garantizar la calidad educativa sin perder escalabilidad:

*   **Entrega de Contenido (Automatizada):** Un "Bot" o sistema programado se encarga de enviar las lecciones puntualmente (ej. todos los días a las 8:00 AM).
    *   *Ejemplo:* "¡Buenos días! Aquí tienes la lección de hoy sobre 'Finanzas Personales' 📄 [PDF] + 🎥 [Video]"
*   **Soporte y Dudas (Humano):**
    *   Los alumnos pueden responder a los mensajes del bot.
    *   Un panel de administración centraliza estos mensajes para que *tutores humanos* respondan dudas específicas.

## 4. Solución Técnica: El "Centro de Mando"
La clave del éxito para escalar este negocio no es el contenido en sí, sino la infraestructura que permite gestionar cientos de alumnos sin volverse loco. "WhatsCourse" actúa como un cerebro central que orquesta todo.

### 4.1. ¿Por qué se necesita una plataforma?
Sin una plataforma, la gestión es manual y propensa a errores: guardar contactos uno a uno, enviar archivos a mano.
**Con WhatsCourse:**
*   El profesor sube el contenido **una sola vez**.
*   El sistema trabaja 24/7 inscribiendo alumnos y enviando clases.

### 4.2. Flujo de Usuario (Paso a Paso)
Así vive la experiencia un alumno desde que se interesa hasta que aprende:

3.  **Registro Inmediato:** Un adminstrador agrega el número del usuario a la base de datos del curso, puede ser manual o importando un archivo csv con los numeros.
4.  **Bienvenida Mágica:** En menos de 1 minuto, el usuario recibe un WhatsApp automático: *"¡Hola María! Bienvenida al curso. Aquí tienes tu acceso"*.
5.  **Goteo de Contenido (Drip):**
    *   *Día 1, 08:00 AM:* El sistema envía el Video 1.
    *   *Día 2, 08:00 AM:* El sistema envía el PDF de ejercicios.
    *   *Día 3...:* Y así sucesivamente hasta terminar.
6.  **Interacción:** Si María tiene una duda, escribe al whatsapp del curso.
    *   **Solución Low-Cost:** Los mensajes llegan a una **Bandeja Básica Integrada** en el mismo panel. Sin pagar herramientas externas extras. Simple y directo.


Entregables al Cliente
Cuestionario para Levantamiento de Información (Para el Cliente)
### Sobre el Negocio
2.  **¿Qué volumen de alumnos esperas manejar en el primer año?** (50, 500, 5.000? Esto define la infraestructura técnica y costos de WhatsApp API).
3.  **¿Tienes ya contenido creado (videos/pdfs)?** ¿En qué formato están?
### Sobre la Operativa
4.  **¿Cuántos tutores o personas de soporte tendrán acceso al sistema para responder mensajes?**
5.  **¿Deseas que los alumnos interactúen entre ellos (Grupos) o que sea una comunicación privada 1-a-1 (Broadcast)?** *Nota: 1-a-1 es mejor para cursos premium.*
6.  **¿Necesitas emitir certificados automáticos al finalizar el curso?**
### Sobre Tecnología
7.  **¿Tienes ya una cuenta de WhatsApp Business verificada o número dedicado para esto?**
