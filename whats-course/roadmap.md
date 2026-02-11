# Roadmap del Proyecto WhatsApp Learning

## Visión General

```mermaid
gantt
    title Roadmap WhatsApp Learning - Desarrollo por Fases
    dateFormat  YYYY-MM-DD
    
    section Fase 1 - Discovery
    Levantamiento de requisitos      :f1a, 2026-02-01, 5d
    Validación de alcance            :f1b, after f1a, 3d
    Aprobación cliente               :f1c, after f1b, 2d
    
    section Fase 2 - MVP
    Configuración VPS + Keycloak     :f2a, after f1c, 5d
    Integración WhatsApp API         :f2b, after f2a, 7d
    Panel admin (Angular)            :f2c, after f2b, 10d
    Sistema envío programado         :f2d, after f2c, 5d
    Pruebas internas MVP             :f2e, after f2d, 3d
    
    section Fase 3 - Evaluaciones
    Editor de exámenes               :f3a, after f2e, 5d
    Calificación automática          :f3b, after f3a, 5d
    Reportes de notas                :f3c, after f3b, 3d
    
    section Fase 4 - IA y Soporte
    Integración OpenAI/Claude        :f4a, after f3c, 7d
    Chatbot conversacional           :f4b, after f4a, 5d
    Bandeja para tutores             :f4c, after f4b, 5d
    Evaluación respuestas con IA     :f4d, after f4c, 3d
    
    section Fase 5 - QA y Lanzamiento
    Pruebas integrales               :f5a, after f4d, 5d
    Beta con usuarios reales         :f5b, after f5a, 7d
    Ajustes y corrección bugs        :f5c, after f5b, 5d
    Despliegue producción            :f5d, after f5c, 3d
    
    section Buffer
    Contingencia (+15%)              :f6a, after f5d, 10d
```

---

## Stack Tecnológico

### Decisiones Técnicas

| Componente | Decisión | Justificación |
|------------|----------|---------------|
| **WhatsApp API** | Meta Cloud API | Oficial de Meta, sin intermediarios, mejor precio a escala (~$0.05/conversación) |
| **Backend** | Node.js + Express | Async nativo, ideal para webhooks y eventos en tiempo real |
| **Base de datos** | PostgreSQL | Relacional, robusto, soporte JSON para flexibilidad |
| **Panel Admin** | Angular + TailwindCSS | Framework robusto, tipado fuerte, arquitectura escalable |
| **Colas/Tareas** | pg-boss (PostgreSQL) | Usa la misma DB, sin servicio extra, suficiente para este volumen |
| **IA Conversacional** | OpenAI GPT-4 / Claude | Mejor calidad de respuesta para contexto educativo (alternativas más baratas: Mistral, Llama 3) |
| **Infraestructura** | VPS en OVH | Control total, costo fijo predecible, sin vendor lock-in |
| **Almacenamiento** | Backblaze B2 o Cloudflare R2 | Cloud especializado, económico (~$0.005/GB), CDN incluido, compatible S3 |
| **Autenticación** | Keycloak | SSO, gestión de roles, escalable a múltiples empresas cliente, estándar enterprise |

### Arquitectura

```mermaid
flowchart TB
    subgraph VPS["VPS OVH"]
        subgraph FRONTEND["Frontend (Angular)"]
            F1[Panel Admin]
        end
        
        subgraph BACKEND["Backend (Node.js)"]
            B1[API REST]
            B2[Webhook Handler]
            B3[Queue Worker - pg-boss]
            B4[IA Service]
        end
        
        subgraph DATA["Datos"]
            D1[(PostgreSQL + pg-boss)]
            D2[Keycloak]
        end
    end
    
    subgraph EXTERNAL["Servicios Externos"]
        E1[Meta Cloud API]
        E2[OpenAI / Claude API]
        E3[Backblaze B2 / Cloudflare R2]
    end
    
    F1 --> D2
    F1 --> B1
    B1 --> D1
    B1 --> E3
    B2 <--> E1
    B3 --> D1
    B3 --> E1
    B4 --> E2
```

### Costos Estimados Mensuales

| Servicio | Costo | Notas |
|----------|-------|-------|
| VPS OVH (8GB RAM, 4 vCPU) | ~€25-40/mes | Keycloak requiere más RAM |
| Backblaze B2 / Cloudflare R2 | ~€5-15/mes | ~$0.005/GB, 10GB gratis en R2 |
| Meta WhatsApp API | Variable | ~$0.05-0.08 por conversación/24h |
| OpenAI API | $20-100/mes | Según volumen de consultas IA |
| Dominio + SSL | ~€10-15/año | Let's Encrypt gratuito |
| **Total estimado** | **€50-155/mes** | Para ~500 usuarios activos |

> **Nota:** Si el volumen de IA es alto, considerar Mistral o Llama 3 self-hosted para reducir costos.

---

## Detalle por Fase

### Fase 1: Discovery y Planificación (1.5 semanas)

```mermaid
flowchart LR
    A[Reunión inicial] --> B[Cuestionario cliente]
    B --> C[Validación de alcance]
    C --> D[Aprobación para iniciar]
```

**Entregables AL CLIENTE:**

| Entregable | Descripción |
|------------|-------------|
| Documento de alcance firmado | Funcionalidades confirmadas, lo que entra y lo que NO |
| Cronograma acordado | Fechas de entrega por fase |

**Configuración interna (no entregable):**
- Repositorios Git
- Pipeline CI/CD
- VPS staging

**Dependencias del cliente:**
- Respuestas al cuestionario (`client-questions.md`)
- Cuenta WhatsApp Business verificada
- Acceso a contenido de ejemplo (1 curso mínimo)

---

### Fase 2: MVP - Producto Mínimo Viable (5 semanas)

> **Nota:** En esta fase NO hay IA. Los mensajes de estudiantes llegan pero no se responden automáticamente hasta Fase 4.

```mermaid
flowchart TB
    subgraph MVP["Alcance MVP"]
        M1[Panel Admin]
        M2[Gestión de Cursos]
        M3[Gestión de Estudiantes]
        M4[Envío Programado]
        M5[Integración WhatsApp]
    end
    
    M1 --> M2
    M1 --> M3
    M2 --> M4
    M3 --> M5
    M4 --> M5
```

**Funcionalidades del MVP:**

| Funcionalidad | Descripción | Para quién |
|---------------|-------------|------------|
| Carga de estudiantes | Manual + importar CSV con números | Administrador del cliente |
| Creación de cursos | Subir videos, PDFs, audios, definir orden | Administrador del cliente |
| Envío programado ("drip") | Goteo de contenido: envía lección 1 el día 1, lección 2 el día 2, etc. | Automático |
| Vista de progreso | Ver qué estudiantes recibieron qué lección | Administrador del cliente |
| Integración WhatsApp | Conexión técnica: enviar mensajes, recibir confirmación de entrega | Sistema |

**Criterio de éxito:** Un curso completo enviado a 10 estudiantes de prueba, con registro de entregas.

**Qué NO incluye esta fase:**
- Responder mensajes de estudiantes (Fase 4)
- Exámenes (Fase 3)
- IA conversacional (Fase 4)

---

### Fase 3: Sistema de Evaluaciones (2.5 semanas)

> **Nota:** Solo evaluaciones automáticas (opción múltiple, V/F). La evaluación con IA de respuestas abiertas es Fase 4.

```mermaid
flowchart LR
    A[Admin crea examen] --> B[Sistema envía a estudiante]
    B --> C[Estudiante responde por WhatsApp]
    C --> D[Sistema califica automáticamente]
    D --> E[Actualiza progreso en panel]
```

**Funcionalidades:**

| Funcionalidad | Tiempo | Descripción |
|---------------|--------|-------------|
| Crear exámenes | 3 días | Editor de preguntas opción múltiple y V/F |
| Enviar exámenes | 2 días | Por WhatsApp, formato conversacional |
| Calificación automática | 3 días | Procesar respuestas, calcular nota |
| Reportes de notas | 2 días | Vista de aprobados/reprobados en panel |
| Reintentos | 2 días | Permitir repetir examen si reprueba |

**Tipos de evaluación en esta fase:**

| Tipo | Incluido | Calificación |
|------|----------|-------------|
| Opción múltiple | ✅ Sí | Automática |
| Verdadero/Falso | ✅ Sí | Automática |
| Respuesta abierta | ❌ Fase 4 | Con IA |
| Casos prácticos | ❌ Futuro | Manual |

---

### Fase 4: IA Conversacional y Soporte (4 semanas)

```mermaid
flowchart TB
    A[Mensaje de estudiante] --> B{Clasificación IA}
    B -->|Duda sobre contenido| C[Respuesta automática con contexto del curso]
    B -->|Consulta compleja| D[Escala a tutor humano]
    B -->|Fuera de tema| E[Respuesta genérica + redirección]
    
    D --> F[Notificación en bandeja]
    F --> G[Tutor responde desde panel]
    G --> H[Mensaje al estudiante vía WhatsApp]
```

**Funcionalidades:**

| Funcionalidad | Tiempo | Descripción |
|---------------|--------|-------------|
| Integración OpenAI/Claude | 7 días | Conexión API, manejo de tokens, retry logic |
| Chatbot conversacional | 5 días | Respuestas contextuales basadas en contenido del curso |
| Bandeja para tutores | 5 días | Vista de mensajes pendientes, asignación, respuesta |
| Evaluación respuestas abiertas | 3 días | IA califica respuestas de texto libre |

**Componentes técnicos:**
- LLM: OpenAI GPT-4 o Claude (configurable)
- RAG: Base de conocimiento por curso (PDFs indexados)
- Escalamiento: Reglas + clasificación IA
- Bandeja: Tiempo real con WebSockets

---

### Fase 5: QA y Lanzamiento (4 semanas)

```mermaid
flowchart LR
    A[Pruebas integrales] --> B[Beta cerrada]
    B --> C[Feedback]
    C --> D[Corrección bugs]
    D --> E[Go-live]
    E --> F[Monitoreo 1 semana]
```

| Actividad | Duración | Descripción |
|-----------|----------|-------------|
| Pruebas integrales | 5 días | QA interno: todos los flujos, casos borde |
| Beta cerrada | 7 días | 1 empresa cliente, 20-30 usuarios reales |
| Corrección bugs | 5 días | Fixes de issues encontrados en beta |
| Despliegue producción | 3 días | Migración, DNS, monitoreo |

---

## Estimación de Tiempos Total

```mermaid
pie title Distribución de Tiempo por Fase
    "Discovery" : 1.5
    "MVP" : 5
    "Evaluaciones" : 2.5
    "IA y Soporte" : 4
    "QA y Lanzamiento" : 4
    "Buffer" : 2
```

| Fase | Duración | Acumulado | Qué incluye |
|------|----------|-----------|-------------|
| Discovery | 1.5 semanas | 1.5 sem | Requisitos, alcance, aprobación |
| MVP | 5 semanas | 6.5 sem | Panel, cursos, envío WhatsApp |
| Evaluaciones | 2.5 semanas | 9 sem | Exámenes opción múltiple, notas |
| IA y Soporte | 4 semanas | 13 sem | Chatbot, bandeja tutores, IA eval |
| QA y Lanzamiento | 4 semanas | 17 sem | Pruebas, beta, fixes, deploy |
| **Buffer (+15%)** | 2 semanas | **19 sem** | Contingencia para imprevistos |

**Tiempo total estimado: ~4.5 meses (19 semanas)**

> ⚠️ **Importante:** El buffer es para imprevistos reales (bugs complejos, cambios de requisitos menores, retrasos del cliente). No es tiempo "extra" para agregar funcionalidades.

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
