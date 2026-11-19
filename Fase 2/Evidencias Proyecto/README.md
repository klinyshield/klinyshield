# KlinyShield — Software Clínico de Alta Seguridad & Asistente C2C/B2B2C

KlinyShield es un SaaS clínico de misión crítica diseñado para consultas médicas y de kinesiología en Chile, construido bajo los más estrictos estándares de **Zero-Knowledge Architecture**, cumplimiento normativo chileno (**Ley 20.584** de Derechos y Deberes del Paciente, **Ley 19.628 / 21.719** de Protección de Datos Personales) y **Clean Architecture / Screaming Architecture**.

---

## 🏛️ Principios Arquitectónicos

1. **Aislamiento Multi-Tenant Estricto:** Separación de datos por `tenant_id` y `professional_id` mediante políticas de seguridad a nivel de fila (Row Level Security - RLS) en PostgreSQL / Supabase.
2. **Autenticación Dual-Token (BFF + RLS):**
   - **Token 1:** JWT emitido en el BFF firmado asimétricamente con clave elíptica **ES256 (ECDSA P-256)**, almacenado en cookie segura `HttpOnly`, `SameSite=Lax`.
   - **Token 2:** JWT efímero derivado al vuelo (`Token Exchange`) con claims RLS (`auth.uid()`, `tenant_id`) y expiración corta (5 min).
   - **Dispositivos de Confianza (MFA):** Fingerprinting criptográfico SHA-256 de dispositivo con desafío OTP obligatorio al detectar navegadores nuevos.
3. **Guardrails de Seguridad en 4 Capas (Defensa en Profundidad):**
   - **Capa 1 (Triage de Urgencias Médicas):** Detección determinista instantánea (<0.2 ms) de modismos chilenos y emergencias vitales ("me dio la pálida", "cuesta respirar", dolor torácico) derivando a SAMU (131).
   - **Capa 2 (Safe Harbor / Anti-Fuga de Datos Privados):** Bloqueo de solicitudes de teléfonos personales, WhatsApps privados y contacto fuera de canal.
   - **Capa 3 (Anti-Prompt Injection & Jailbreak):** Clasificación semántica vectorial local (ONNX embeddings) e inspección de patrones de manipulación.
   - **Capa 4 (Sanitizador de Salida / Data Leak Prevention):** Filtro regex y de entropía previo a enviar la respuesta al paciente, previniendo fuga de credenciales, teléfonos o diagnósticos no autorizados.
4. **Asistente Híbrido FSM-Governed Tool-Calling (Google AI Studio + PostgreSQL ACID):**
   - NLU flexible impulsado por **Gemini 2.5 Flash** ejecutando *Function Calling* tipado (`searchAvailableSlots`, `preselectSlot`, `submitPatientOnboarding`, `confirmBookingWithConsent`).
   - Gobernanza estricta mediante Máquina de Estados Finitos (FSM: `IDLE` → `SELECTING_SPECIALIST` → `AWAITING_SLOT_SELECTION` → `AWAITING_PATIENT_ONBOARDING` → `AWAITING_LEGAL_CONSENT` → `CONFIRMED`).
   - Fallback offline determinista 100% operativo sin dependencias de red para tests y contingencias.
   - Prevención de *Double-Booking* mediante bloqueos pesimistas `SELECT ... FOR UPDATE` en PostgreSQL.
   - Onboarding obligatorio antes de agendar: Nombre, Apellido, Correo para Magic Link y Consentimiento Informado explícito (Ley 20.584).

---

## 🛠️ Stack Tecnológico

| Capa | Tecnologías |
| :--- | :--- |
| **Runtime & Framework** | Node.js v22+ LTS, Next.js 16.3.3 (App Router, React 19), TypeScript 5.0 (Strict) |
| **Base de Datos & Auth** | PostgreSQL 15+ (Supabase), Row Level Security (RLS), Migraciones SQL versionadas |
| **Criptografía & Hashing** | Argon2id (`@node-rs/argon2`), ES256 / HS256 (`jose`), SHA-256 (`node:crypto`) |
| **Inteligencia Artificial** | Google AI Studio SDK (`@google/genai`), Transformers.js / ONNX Runtime (`@xenova/transformers`) |
| **Frontend & UI** | Tailwind CSS, Framer Motion (`motion/react`), Lucide React |
| **Testing & Calidad** | Vitest 3.0, TypeScript typecheck (`tsc --noEmit`), ESLint |

---

## 🧪 Estado de Pruebas & Cobertura

El proyecto cuenta con una cobertura integral de tests unitarios y de integración de seguridad:

```bash
# Verificación de tipos TypeScript
npx tsc --noEmit

# Ejecución de la suite completa de pruebas
npx vitest run
```

- **Validación local del 29-10-2026:** 997 pruebas de la suite global pasando y 11 pruebas de integración con Supabase local pasando. Las pruebas de base de datos se activan por separado.
- **Latencia promedio de Guardrails:** < 0.20 ms.

---

## 📋 Gestión de Proyecto & Metodología Kanban

El ciclo de vida y entrega continua de KlinyShield se gestiona bajo el marco ágil de flujo continuo **Kanban**:
- **[Sistema Kanban & Políticas Operativas](file:///home/michimisimo/Programming/klinyshield/docs/kanban/README.md):** Tablero visual, límites WIP, políticas explícitas (DoR/DoD) y carriles de servicio (*Swimlanes*).
- **[Catálogo de Historias de Usuario](file:///home/michimisimo/Programming/klinyshield/docs/kanban/02_HISTORIAS_DE_USUARIO_Y_BACKLOG.md):** Especificaciones BDD Gherkin, RLS y trazabilidad legal chilena (Leyes 19.628, 20.584 y 21.719).
- **[Roadmap de Producto Now - Next - Later](file:///home/michimisimo/Programming/klinyshield/docs/kanban/03_ROADMAP_DE_PRODUCTO_NOW_NEXT_LATER.md):** Horizontes temporales orientados a valor clínico y gestión de riesgos.
- **[Guía y Plantillas de Presentación de Avances](file:///home/michimisimo/Programming/klinyshield/docs/kanban/04_GUIA_Y_PLANTILLAS_PRESENTACION_DE_AVANCES.md):** Métricas de flujo (Lead Time, Cycle Time, Throughput, CFD), informes ejecutivos RAG y guion para comités.

---

## 🚀 Puesta en Marcha Local

### 1. Requisitos

- Node.js 22+ y npm.
- Docker Desktop abierto, con motor Linux funcionando.
- No se requiere cuenta de Supabase ni acceso al proyecto remoto.

### 2. Levantar Supabase

Desde la raíz del repositorio, en PowerShell:

```powershell
npm.cmd install
npx.cmd --yes supabase@2.122.0 start
npx.cmd --yes supabase@2.122.0 status
```

El repositorio ya contiene `supabase/config.toml`; no ejecutar `supabase init` sobre él. El primer arranque descarga contenedores y aplica las migraciones. El Token 2 de intercambio local utiliza HS256 con el secreto de esta instancia. La regla previa para Token 1 exige ES256; el fallback de firma del código no equivale a una excepción autorizada. La revisión de conformidad del perfil y sus bloqueos se registra en `docs/devlog/19-revision-perfil-contra-linea-base.md`. No hay un seed general configurado; los catálogos se cargan desde las migraciones. La analítica local opcional está desactivada porque su recolector de logs requiere un endpoint de Docker que no está disponible en esta configuración de Docker Desktop.

| Servicio | URL |
|---|---|
| API Supabase | `http://127.0.0.1:54321` |
| Studio local | `http://127.0.0.1:54323` |
| PostgreSQL | `127.0.0.1:54322` |

### 3. Conectar la aplicación a la instancia local

Obtener las credenciales locales con `npx.cmd --yes supabase@2.122.0 status -o env` y configurar `.env.local` (ignorado por Git):

```dotenv
NEXT_PUBLIC_SUPABASE_URL="http://127.0.0.1:54321"
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY="<ANON_KEY local>"
SUPABASE_SERVICE_ROLE_KEY="<SERVICE_ROLE_KEY local>"
SUPABASE_JWT_SECRET="<JWT_SECRET local>"
```

El nombre que lee el cliente actual es `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`; para este entorno se utiliza la `ANON_KEY` local. El secreto JWT debe coincidir con el de esa instancia para comprobar RLS mediante los tokens efímeros. No reutilizar credenciales del proyecto remoto. Las variables de IA, correo y WhatsApp corresponden a otras integraciones y no son necesarias para las pruebas de publicación.

```powershell
npm.cmd run dev
```

Abrir `http://localhost:3000`. Si ya hay un servidor de este mismo proyecto abierto, utilizarlo o reiniciarlo al cambiar variables de entorno.

### 4. Pruebas reales del perfil público

Con Docker, Supabase y Next.js locales funcionando:

```powershell
npm.cmd run test:local:profile
```

El comando ejecuta `tests/integration/profile-publication.local.test.ts` contra PostgreSQL, RLS, repositorios y endpoints reales. Exige API `127.0.0.1:54321` y un contexto Docker con socket local; no apunta al proyecto alojado. `LOCAL_APP_URL` permite indicar otro puerto local para Next.js.

Comprueba migración con datos previos, borrador persistente, publicación y actualización, permisos, revisión optimista, rutas históricas, disponibilidad, reserva y retiro concurrente. El backfill se comprueba dentro de una transacción que termina en rollback. Los fixtures temporales se limpian por UUID; el fixture de reserva integral conserva sus consentimientos ficticios append-only y queda identificado como «Fixture Reserva Integral». No se invocan proveedores externos de notificaciones en esa prueba.

La suite habitual `npm.cmd test` omite estas pruebas de base de datos salvo activación explícita mediante el comando anterior. Para la primera carga del modelo semántico se verificó la suite global con `npm.cmd test -- --maxWorkers=2 --testTimeout=60000`, evitando saturar la máquina con múltiples inferencias simultáneas.

Para detener Supabase conservando sus datos:

```powershell
npx.cmd --yes supabase@2.122.0 stop
```

`supabase db reset --local --no-seed` reconstruye la instancia y elimina los datos locales; no es necesario para arrancar ni para ejecutar esta batería.

---
## 📄 Licencia y Cumplimiento
KlinyShield — Desarrollado conforme a la legislación sanitaria y de protección de datos de la República de Chile (Leyes 19.628, 20.584 y 21.719).

## Entrega del perfil profesional (#65)

El incremento mantiene borrador privado, publicación explícita y enlace canónico estable. La reserva pública acredita correo antes de consultar fichas. Véase [guía del líder](docs/infra/entrega-perfil-profesional.md) para las migraciones, configuración de correo y condiciones antes del merge: el workflow actual despliega el código de main, pero no migra Supabase Cloud. A01/A02 no forma parte del incremento.

`npm.cmd run test:local:profile` ejecuta 20 integraciones activadas explícitamente en un solo worker. `npm.cmd run test:local:profile:browser` comprueba Chrome contra Supabase, Next.js y SMTP exclusivamente locales; la guía describe las variables. No ejecutar el runner de navegador contra la nube.
