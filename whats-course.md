# Propuesta de Proyecto: Plataforma de Cursos vía WhatsApp ("WhatsCourse")

## 1. Resumen Ejecutivo
Esta propuesta detalla el desarrollo de una plataforma educativa innovadora que utiliza WhatsApp como el canal principal de entrega de contenido. El objetivo es aprovechar la alta tasa de apertura de WhatsApp para ofrecer micro-aprendizaje (micro-learning) mediante videos, audios y PDFs, combinando la escalabilidad de la automatización con la calidez del soporte humano.

## 2. Modelos de Negocio Propuestos
Se presentan dos modelos viables para presentar al cliente. La plataforma soportará ambos técnicamente.

### Opción A: Modelo de Suscripción (Recurrente)
*   **Concepto:** "Netflix de Cursos". El usuario paga una mensualidad para acceder a una biblioteca de cursos o a una "comunidad premium".
*   **Ventajas:** Ingresos predecibles, mayor retención de usuarios (LTV), ideal para contenido continuo (ej. "Inglés diario", "Tips de finanzas semanales").
*   **Desventajas:** Requiere generación constante de contenido nuevo para evitar cancelaciones.

### Opción B: Pago por Curso (Venta Única)
*   **Concepto:** Venta tradicional. El usuario compra "Curso de Cocina Italiana" y recibe el contenido durante X semanas.
*   **Ventajas:** Ticket promedio más alto por venta, menor presión de crear contenido infinito, modelo mental familiar para el usuario.
*   **Desventajas:** Necesidad constante de captar nuevos clientes (tráfico) para cada lanzamiento.

**Recomendación:** Iniciar con **Opción B (Pago Único)** para validar el mercado con un producto específico, y evolucionar a suscripción si se logra una base de usuarios leales.

## 3. Modelo de Interacción: Híbrido
Para garantizar la calidad educativa sin perder escalabilidad:

*   **Entrega de Contenido (Automatizada):** Un "Bot" o sistema programado se encarga de enviar las lecciones puntualmente (ej. todos los días a las 8:00 AM).
    *   *Ejemplo:* "¡Buenos días! Aquí tienes la lección de hoy sobre 'Finanzas Personales' 📄 [PDF] + 🎥 [Video]"
*   **Soporte y Dudas (Humano):**
    *   Los alumnos pueden responder a los mensajes del bot.
    *   Un panel de administración centraliza estos mensajes para que *tutores humanos* respondan dudas específicas.
    *   Esto justifica un precio premium comparado con un curso 100% grabado.

## 4. Solución Técnica: El "Centro de Mando"
La clave del éxito para escalar este negocio no es el contenido en sí, sino la infraestructura que permite gestionar cientos de alumnos sin volverse loco. "WhatsCourse" actúa como un cerebro central que orquesta todo.

### 4.1. ¿Por qué se necesita una plataforma?
Sin una plataforma, la gestión es manual y propensa a errores: guardar contactos uno a uno, enviar archivos a mano, verificar transferencias.
**Con WhatsCourse:**
*   El profesor sube el contenido **una sola vez**.
*   El sistema trabaja 24/7 inscribiendo alumnos y enviando clases.
*   Puede escalar de 10 a 10.000 alumnos sin trabajo extra para el equipo.

### 4.2. Flujo de Usuario (Paso a Paso)
Así vive la experiencia un alumno desde que se interesa hasta que aprende:

1.  **Atracción:** El usuario ve un anuncio en redes y hace clic.
2.  **Pago (Automático):** Llega a una página de venta, ingresa sus datos y paga (Tarjeta/PayPal).
3.  **Registro Inmediato:** El sistema detecta el pago y automáticamente agrega el número del usuario a la base de datos del curso.
4.  **Bienvenida Mágica:** En menos de 1 minuto, el usuario recibe un WhatsApp automático: *"¡Hola María! Bienvenida al curso. Aquí tienes tu acceso"*.
5.  **Goteo de Contenido (Drip):**
    *   *Día 1, 08:00 AM:* El sistema envía el Video 1.
    *   *Día 2, 08:00 AM:* El sistema envía el PDF de ejercicios.
    *   *Día 3...:* Y así sucesivamente hasta terminar.
6.  **Interacción:** Si María tiene una duda, responde al chat. Su mensaje llega a la **Bandeja de Entrada Unificada** donde un tutor humano le responde.

### 4.3. Componentes del Sistema
1.  **Panel de Administración (Web Admin):** Donde el dueño ve estadísticas, ingresos y sube los cursos.
2.  **Motor de Envíos (WhatsApp API):** La conexión oficial con Meta para asegurar que los mensajes lleguen y no sean marcados como spam.
3.  **Pasarela de Pagos:** Integración segura para cobrar sin intervención manual.

## 5. Roadmap de Implementación

1.  **Fase 1: Descubrimiento y Definición (Semana 1):** Definir alcance exacto con el cuestionario final.
2.  **Fase 2: Prototipo (MVP) (Semana 2-3):** Panel básico para programar mensajes manuales y probar la API de WhatsApp.
3.  **Fase 3: Desarrollo de Plataforma (Semanas 4-8):** Automatización completa, integración de pagos y panel de tutores.
4.  **Fase 4: Lanzamiento Beta (Semana 9):** Primer curso piloto con usuarios reales.

---

## 6. Anexo: Cuestionario para Levantamiento de Información (Para el Cliente)

Usa estas preguntas para obtener los requerimientos finos del cliente:

### Sobre el Negocio
1.  **¿Cuál es el "dolor" principal que resuelven tus cursos?** (Para entender la urgencia del alumno).
2.  **¿Qué volumen de alumnos esperas manejar en el primer año?** (50, 500, 5.000? Esto define la infraestructura técnica y costos de WhatsApp API).
3.  **¿Tienes ya contenido creado (videos/pdfs)?** ¿En qué formato están?

### Sobre la Operativa
4.  **¿Cuántos tutores o personas de soporte tendrán acceso al sistema para responder mensajes?**
5.  **¿Deseas que los alumnos interactúen entre ellos (Grupos) o que sea una comunicación privada 1-a-1 (Broadcast)?** *Nota: 1-a-1 es mejor para cursos premium.*
6.  **¿Necesitas emitir certificados automáticos al finalizar el curso?**

### Sobre Tecnología
7.  **¿Tienes ya una cuenta de WhatsApp Business verificada o número dedicado para esto?**
8.  **¿Qué métodos de pago son indispensables para tu público?** (Tarjeta, Transferencia, Efectivo, Cripto).
