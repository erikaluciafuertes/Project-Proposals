# Roadmap del Proyecto WhatsCourse

## Visión General

```mermaid
gantt
    title Roadmap WhatsCourse - Desarrollo por Fases
    dateFormat  YYYY-MM-DD
    section Fase 1 - Discovery
    Levantamiento de requisitos      :f1a, 2026-02-01, 5d
    Definición de alcance            :f1b, after f1a, 3d
    Validación con cliente           :f1c, after f1b, 2d
    
    section Fase 2 - MVP
    Configuración infraestructura    :f2a, after f1c, 5d
    Integración WhatsApp API         :f2b, after f2a, 7d
    Panel admin básico               :f2c, after f2a, 10d
    Bot de envío automático          :f2d, after f2b, 7d
    
    section Fase 3 - Evaluaciones
    Sistema de exámenes              :f3a, after f2d, 10d
    Calificación automática          :f3b, after f3a, 5d
    Reportes de progreso             :f3c, after f3b, 5d
    
    section Fase 4 - IA y Soporte
    Integración chatbot IA           :f4a, after f3c, 10d
    Escalamiento a tutores           :f4b, after f4a, 5d
    Bandeja de mensajes              :f4c, after f4a, 7d
    
    section Fase 5 - Lanzamiento
    Pruebas con usuarios reales      :f5a, after f4c, 10d
    Ajustes y correcciones           :f5b, after f5a, 7d
    Despliegue producción            :f5c, after f5b, 3d
```

---

## Detalle por Fase

### Fase 1: Discovery y Planificación (1.5 semanas)

**Stack tecnológico ya definido** (ver `whats-course.md` sección 3):
- **Backend:** Node.js + Express + PostgreSQL
- **Frontend:** React + TailwindCSS
- **WhatsApp:** Meta Cloud API
- **IA:** OpenAI GPT-4 / Claude
- **Infra:** Railway/Render + Cloudflare R2

```mermaid
flowchart LR
    A[Reunión inicial] --> B[Cuestionario cliente]
    B --> C[Validación de alcance]
    C --> D[Kick-off desarrollo]
```

| Entregable | Descripción |
|------------|-------------|
| Respuestas del cliente | Volumen, contenido, cuenta WhatsApp |
| Documento de alcance | Funcionalidades priorizadas |
| Ambiente de desarrollo | Repos, CI/CD, staging |

---

### Fase 2: MVP - Producto Mínimo Viable (4 semanas)

```mermaid
flowchart TB
    subgraph MVP["Alcance MVP"]
        M1[Registro de estudiantes]
        M2[Envío automático de contenido]
        M3[Panel admin básico]
        M4[Integración WhatsApp]
    end
    
    M1 --> M4
    M2 --> M4
    M3 --> M1
    M3 --> M2
```

**Funcionalidades del MVP:**
- Carga de estudiantes (manual + CSV)
- Creación de cursos con lecciones
- Programación de envío de contenido (drip)
- Vista de estudiantes por curso
- Conexión con WhatsApp Business API

**Criterio de éxito:** Un curso completo funcionando end-to-end con 10 estudiantes de prueba.

---

### Fase 3: Sistema de Evaluaciones (3 semanas)

```mermaid
flowchart LR
    A[Estudiante recibe examen] --> B[Responde por WhatsApp]
    B --> C[Sistema procesa respuestas]
    C --> D{Tipo de pregunta}
    D -->|Opción múltiple| E[Calificación automática]
    D -->|Respuesta abierta| F[IA evalúa o escala]
    E --> G[Actualiza progreso]
    F --> G
```

| Tipo de Evaluación | Prioridad | Fase |
|--------------------|-----------|------|
| Opción múltiple | Alta | 3 |
| Verdadero/Falso | Alta | 3 |
| Respuesta corta con IA | Media | 4 |
| Casos prácticos | Baja | Futuro |

---

### Fase 4: IA Conversacional y Soporte (3 semanas)

```mermaid
flowchart TB
    A[Mensaje de estudiante] --> B{Clasificación IA}
    B -->|Duda frecuente| C[Respuesta automática]
    B -->|Consulta compleja| D[Escala a tutor]
    B -->|Fuera de tema| E[Respuesta genérica]
    
    D --> F[Notificación en bandeja]
    F --> G[Tutor responde]
    G --> H[Mensaje al estudiante]
```

**Componentes:**
- Chatbot basado en LLM (GPT-4 / Claude)
- Base de conocimiento por curso
- Sistema de escalamiento inteligente
- Bandeja unificada para tutores

---

### Fase 5: Pruebas y Lanzamiento (3 semanas)

```mermaid
flowchart LR
    A[Beta cerrada] --> B[Feedback usuarios]
    B --> C[Iteración]
    C --> D[Beta abierta]
    D --> E[Go-live]
    E --> F[Monitoreo post-lanzamiento]
```

| Actividad | Duración | Participantes |
|-----------|----------|---------------|
| Beta cerrada | 1 semana | 1 empresa, 20 usuarios |
| Ajustes | 1 semana | Equipo desarrollo |
| Lanzamiento | 3 días | Cliente + soporte |

---

## Estimación de Tiempos Total

```mermaid
pie title Distribución de Tiempo por Fase
    "Discovery" : 1.5
    "MVP" : 4
    "Evaluaciones" : 3
    "IA y Soporte" : 3
    "Lanzamiento" : 3
```

| Fase | Duración | Acumulado |
|------|----------|-----------|
| Discovery | 1.5 semanas | 1.5 semanas |
| MVP | 4 semanas | 5.5 semanas |
| Evaluaciones | 3 semanas | 8.5 semanas |
| IA y Soporte | 3 semanas | 11.5 semanas |
| Lanzamiento | 3 semanas | **14.5 semanas** |

**Tiempo total estimado: ~3.5 meses**

---

## Dependencias Críticas

| Dependencia | Responsable | Impacto si falta |
|-------------|-------------|------------------|
| Cuenta WhatsApp Business verificada | Cliente | Bloquea Fase 2 |
| Contenido de cursos (videos/PDFs) | Cliente | Bloquea pruebas |
| Definición de evaluaciones | Cliente | Bloquea Fase 3 |
| Acceso a tutores para pruebas | Cliente | Bloquea Fase 4 |

---

## Próximos Pasos

1. Completar cuestionario del cliente (`client-questions.md`)
2. Validar presupuesto y tiempos
3. Firmar contrato / orden de trabajo
4. Kick-off del proyecto
