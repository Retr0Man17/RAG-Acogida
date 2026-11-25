# Proposito

• Propósito principal. Traducir la intención de negocio en requisitos técnicos concretos, verificables y sin ambigüedades para evitar que la IA "alucine" o improvise.
• Contenido habitual. Define las entradas y salidas de datos, flujos de usuario paso a paso, reglas de negocio, casos límite (edge cases), manejo de errores y criterios de aceptación.
• Audiencia y revisión. Es revisado por ingenieros y arquitectos de software antes de pasar a la fase de planificación (plan.md) y generación de código


backend/
├── src/
│   ├── config/
│   │   └── database.ts             # Configuración del cliente Prisma y conexión a PostgreSQL
│   ├── modules/
│   │   └── rag-fae/                # Módulo principal del negocio FAE
│   │       ├── controllers/
│   │       │   ├── chat.controller.ts       # Endpoints para streaming y chat
│   │       │   ├── auth.controller.ts       # Autenticación de duplas y familias (invitaciones)
│   │       │   └── backoffice.controller.ts # Gestión de corpus, duplas y panel de brechas
│   │       ├── routes/
│   │       │   └── rag.routes.ts            # Enrutador Express central
│   │       ├── services/
│   │       │   ├── orchestrator.service.ts      # Coordina flujo: Semáforo -> Recuperador -> Generador[cite: 11, 12]
│   │       │   ├── safety-classifier.service.ts # Semáforo (Verde, Amarillo, Rojo)[cite: 11, 13]
│   │       │   ├── vector-retriever.service.ts  # Búsqueda vectorial pura con pgvector y Prisma [$queryRaw][cite: 11]
│   │       │   ├── bridge.service.ts            # Generador de resumen anónimo para la dupla[cite: 4, 11]
│   │       │   └── generation.service.ts        # Integración con LLM y formateo de citas[cite: 12, 37]
│   │       │
│   │       └── models/
│   │           └── rag.types.ts
│   │
│   ├── shared/
│   │   ├── middleware/
│   │   │   ├── auth.middleware.ts        # Validación JWT, roles (Dupla, Curador, Admin) y 2FA[cite: 10, 34]
│   │   │   ├── rate-limiter.middleware.ts  # Protección contra abuso en modo abierto (RNF-14)[cite: 37]
│   │   │   └── privacy.middleware.ts     # Anonimización y exclusión de datos personales en logs[cite: 38]
│   │   └── errors/
│   │       └── custom-errors.ts
│   │
│   ├── app.ts                      # Configuración de Express y middlewares globales
│   └── server.ts                   # Inicialización del servidor Node.js
├── prisma/
│   ├── schema.prisma               # Modelos relacionales y tipo Vector para pgvector
│   └── migrations/                 # Migraciones SQL (incluyendo CREATE EXTENSION vector;)
└── package.json


frontend/
├── src/
│   ├── app/
│   │   ├── core/
│   │   │   ├── interceptors/
│   │   │   │   └── auth.interceptor.ts      # Inyección de tokens JWT para cuentas de familia y backoffice
│   │   │   └── services/
│   │   │       ├── api.service.ts           # Cliente HTTP centralizado
│   │   │       └── geolocation.service.ts   # Cálculo local de urgencias y zonas (nunca envía coordenadas)[cite: 22, 40]
│   │   │
│   │   ├── features/
│   │   │   └── rag-fae/
│   │   │       ├── components/
│   │   │       │   ├── chat-container/      # Contenedor de conversación en tiempo real (Streaming)[cite: 12, 36]
│   │   │       │   ├── chat-input/          # Barra de mensaje con botón de micrófono (dictado por voz)[cite: 29]
│   │   │       │   ├── message-bubble/      # Renderizado de respuestas con formato visual y tarjetas[cite: 12, 28]
│   │   │       │   ├── source-citations/    # Tarjetas desplegables con citas bibliográficas (Título, autor, año)[cite: 18, 41]
│   │   │       │   ├── safety-banner/       # Alertas de semáforo (Rojo/Amarillo) y canales de emergencia[cite: 13, 18, 20]
│   │   │       │   ├── bridge-generator/    # Vista previa del resumen anónimo para enviar a la dupla[cite: 4, 23]
│   │   │       │   ├── timeline-view/       # Línea de tiempo interactiva de la etapa de acogimiento[cite: 27]
│   │   │       │   └── emergency-locator/   # Buscador local de SAPU/SAR/Hospitales cercanos[cite: 21]
│   │   │       │
│   │   │       ├── pages/
│   │   │       │   ├── open-mode/           # Vista abierta (sin cuenta, captación, ruta de postulación)[cite: 8, 23]
│   │   │       │   ├── family-mode/         # Vista de familia (con cuenta, perfil de etapa, historial 90 días)[cite: 8, 25]
│   │   │       │   ├── auth-activation/     # Activación de cuenta mediante enlace único de la dupla[cite: 10, 24]
│   │   │       │   └── backoffice/          # Panel de gestión para Curadores, Duplas y Admin Técnico[cite: 8, 10]
│   │   │       │
│   │   │       └── models/
│   │   │           └── rag-fae.model.ts     # Interfaces TypeScript (Mensaje, Cita, Perfil, Semáforo)
│   │   │
│   │   ├── shared/
│   │   │   ├── components/                  # Botón flotante de ayuda inmediata y glosario desplegable[cite: 20, 28]
│   │   │   └── directives/
│   │   │
│   │   ├── app.component.ts
│   │   └── app.routes.ts                    # Enrutamiento principal de la aplicación Angular
│   │
│   ├── assets/
│   │   ├── images/                          # Infografías curadas por el Observatorio[cite: 29, 43]
│   │   └── i18n/
│   ├── index.html
│   └── main.ts
└── package.json


