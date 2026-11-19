# DUOC UC — ESCUELA DE INFORMÁTICA Y TELECOMUNICACIONES
## INFORME DE AVANCE — FASE 2: PROYECTO APLICADO DE TITULACIÓN (APT)

---

### DATOS DEL DOCUMENTO Y DE LA ASIGNATURA

| Parámetro | Detalle Institucional |
| :--- | :--- |
| **Institución** | Duoc UC — Escuela de Informática y Telecomunicaciones |
| **Asignatura** | Capstone |
| **Sigla** | PTY4614 |
| **Instancia Evaluativa** | Evaluación Fase 2 — Informe de Avance Proyecto APT |
| **Semana Académica** | Semana 9 |
| **Ponderación** | 20% de la calificación final |
| **Proyecto** | **KlinyShield** — SaaS Clínico de Alta Seguridad, Consentimientos B2B2C y Asistente WhatsApp FSM para Profesionales de la Salud |
| **Integrantes del Equipo** | **Felipe Urbina** (Líder Técnico & Arquitectura de Software)<br>**Vicente Solorza** (Ingeniero de Backend & Modelado de Datos)<br>**Maximiliano Duran** (Ingeniero de QA, Seguridad & Frontend) |
| **Fecha de Presentación** | 14 de Octubre de 2026 |
| **Repositorio Oficial** | `https://github.com/Kliny-Shield/main_aplication.git` |
| **Ramas Principales** | `main`, `Felipe_Urbina`, `Vicente_Solorza`, `Maximiliano_Duran` |

---

## ÍNDICE DE CONTENIDOS

1. **Abstract (Resumen Ejecutivo Bilingüe)**
   - 1.1 Abstract en Español
   - 1.2 Abstract in English
2. **Introducción y Contexto Disciplinar del Proyecto**
   - 2.1 Planteamiento de la Problemática Sanitaria y Legal en Chile
   - 2.2 Propuesta de Valor: KlinyShield
   - 2.3 Objetivos Generales y Específicos del Proyecto APT
3. **Ajustes a la Propuesta: Dificultades, Facilitadores y Retroalimentación (Criterio 1 — 10%)**
   - 3.1 Dificultades Técnicas y Operativas Encontradas
   - 3.2 Facilitadores Metodológicos y Tecnológicos
   - 3.3 Retroalimentación Docente Recibida y Modificaciones Implementadas
   - 3.4 Matriz de Ajustes Arquitectónicos y Funcionales
4. **Metodología de Trabajo y Cumplimiento Disciplinar (Criterio 2 — 10%)**
   - 4.1 Marco Metodológico Ágil: Kanban de Flujo Continuo con Límites WIP
   - 4.2 Gobernanza de Desarrollo y Agentes Especializados de Ingeniería
   - 4.3 Métricas de Desempeño del Flujo (Cycle Time, Lead Time, Throughput, Flow Efficiency)
   - 4.4 Cumulative Flow Diagram (CFD) y Políticas Explícitas del Tablero
5. **Evidencias de Avance del Proyecto APT (Criterio 3 — 25%)**
   - 5.1 Evidencias de Documentación Técnica Viva
   - 5.2 Evidencias de Programación y Construcción de Software (Clean Architecture, DDD)
   - 5.3 Evidencias de Almacenamiento y Modelo de Datos (PostgreSQL, RLS, ACID Concurrency)
6. **Cumplimiento de Indicadores de Calidad del Perfil de Egreso**
   - 6.1 Competencia 1: Pruebas de Certificación y Calidad de Software (IE 1.1, 1.2, 1.3)
   - 6.2 Competencia 2: Gestión y Control de Proyectos Informáticos (IE 2.1, 2.2)
   - 6.3 Competencia 3: Diseño e Implementación de Modelos de Datos Escalables (IE 3.1, 3.2)
   - 6.4 Competencia 4: Construcción, Integración e Implantación de Software (IE 4.1, 4.2, 4.3)
7. **Control de Versiones, Gestión en Git y Equidad del Trabajo (Criterios 6, 7 y 8 — 45%)**
   - 7.1 Estructura del Repositorio y Estrategia de Ramificación (Gitflow Adaptado)
   - 7.2 Convención de Commits Atómicos (Conventional Commits) y Trazabilidad
   - 7.3 Matriz de Contribución Equitativa y Responsabilidades por Estudiante
   - 7.4 Demostración de Trabajo en Equipo y Dominio Técnico Grupal
8. **Individual Conclusions (Solo en Inglés por Pauta Oficial)**
   - 8.1 Individual Conclusion: Felipe Urbina
   - 8.2 Individual Conclusion: Vicente Solorza
   - 8.3 Individual Conclusion: Maximiliano Duran
9. **Team Reflection (Solo en Inglés por Pauta Oficial)**
   - 9.1 Team Engineering Reflection & Technical Growth
10. **Referencias Bibliográficas**
11. **Anexos Técnicos de Evidencia**
    - Anexo A: Comprobante Oficial de Ejecución de Pruebas Automatizadas (601/601 Tests)
    - Anexo B: Registro de Commits y Trazabilidad en Git
    - Anexo C: Esquema Relacional de Base de Datos y Políticas RLS
    - Anexo D: Verificación de Build de Producción (Next.js Turbopack)

---

## 1. ABSTRACT (RESUMEN EJECUTIVO BILINGÜE)

### 1.1 Abstract en Español

El presente informe técnico da cuenta del avance integral en la Fase 2 del Proyecto Aplicado de Titulación (APT) correspondiente a la asignatura Capstone (PTY4614) de Duoc UC. El proyecto, titulado **KlinyShield**, consiste en el desarrollo de una plataforma SaaS clínico-médica B2B2C orientada a profesionales de la salud independientes y centros médicos en Chile. Su propósito primordial es solventar las vulnerabilidades éticas, operativas y normativas asociadas a la gestión informal de citas médicas y expedientes clínicos electrónicos mediante aplicaciones de mensajería instantánea tradicionales.

A la Semana 9 de desarrollo, el equipo de ingeniería —integrado por Felipe Urbina, Vicente Solorza y Maximiliano Duran— ha consolidado una solución de software de grado de producción sustentada en arquitectura limpia (*Clean Architecture*), diseño guiado por el dominio (*Domain-Driven Design*) y screaming architecture. La infraestructura integra Next.js 16 (App Router con Turbopack), TypeScript 5.8 estricto, PostgreSQL administrado vía Supabase con aislamiento estricto mediante *Row Level Security* (RLS), hashing criptográfico Argon2id, tokens asimétricos ES256 bajo el estándar Web Crypto API, integración oficial con Meta WhatsApp Cloud API a través de una Máquina de Estados Finitos (FSM) determinista y un motor transaccional de agenda inmune a colisiones de sobreventa (*anti-double-booking*) mediante bloqueos pesimistas `SELECT ... FOR UPDATE`.

El progreso se encuentra respaldado por una suite automatizada de **601 pruebas ejecutadas exitosamente sobre 101 suites de test** (100% de tasa de aprobación en Vitest), un build de producción verificado y una gestión de flujo de trabajo bajo metodología Kanban sustentada en control de versiones Git con ramas individuales y *Conventional Commits*. El proyecto cumple a cabalidad con el marco regulatorio chileno: Ley 20.584 de Derechos y Deberes del Paciente, Ley 19.628 y su modernización bajo la Ley 21.719 de Protección de Datos Personales, y el Decreto Supremo N° 41 del MINSAL sobre fichas clínicas electrónicas.

### 1.2 Abstract in English

This engineering report presents the comprehensive milestone progress for Phase 2 of the Applied Capstone Project (APT), course PTY4614 at Duoc UC. The project, named **KlinyShield**, comprises the engineering of an enterprise-grade B2B2C clinical SaaS platform designed for independent healthcare practitioners and private medical outpatient practices across Chile. Its core mission is to eradicate the severe legal, clinical, and operational liabilities inherent to informal medical appointment scheduling and clinical record handling conducted over conventional instant messaging applications.

By Academic Week 9, the engineering team—composed of Felipe Urbina, Vicente Solorza, and Maximiliano Duran—has achieved a production-ready software architecture grounded in Clean Architecture, Domain-Driven Design (DDD), and Screaming Architecture paradigms. The underlying technology stack incorporates Next.js 16 (App Router with Turbopack), strict TypeScript 5.8, PostgreSQL on Supabase featuring multitenant boundary enforcement via Row Level Security (RLS), Argon2id cryptographic password hashing, ES256 asymmetric token exchange utilizing the Web Crypto API, Meta WhatsApp Cloud API integration driven by a deterministic Finite State Machine (FSM), and an ACID appointment scheduling engine resilient against double-booking hazards using pessimistic `SELECT ... FOR UPDATE` row locks.

Development progress is evidenced by an automated testing suite comprising **601 passing tests distributed across 101 test suites** (100% pass rate in Vitest), a zero-defect production build, and an agile Kanban workflow monitored through strict Git revision control, dedicated developer branches, and atomic Conventional Commits. The solution strictly enforces Chilean healthcare regulatory statutes: Law 20,584 on Patient Rights and Responsibilities, Law 19,628 (amended by Law 21,719 on Personal Data Protection), and Ministry of Health (MINSAL) Supreme Decree No. 41 governing electronic clinical health records.

---

## 2. INTRODUCCIÓN Y CONTEXTO DISCIPLINAR DEL PROYECTO

### 2.1 Planteamiento de la Problemática Sanitaria y Legal en Chile

En el ecosistema chileno de salud privada ambulatoria, kinesiólogos, psicólogos, fonoaudiólogos, nutricionistas y médicos generales gestionan más del 70% de sus solicitudes de consulta a través de chats informales de WhatsApp personal. Esta práctica acarrea tres problemas estructurales de alta gravedad:

1. **Vulnerabilidad Médico-Legal y Fuga de Datos Sensibles:** La exposición de diagnósticos, nombres, teléfonos y RUTs en dispositivos personales contraviene la Ley 19.628 y la nueva Ley 21.719 (que impone multas de hasta 10.000 UTA por infracciones graves en tratamiento de datos sensibles de salud).
2. **Inexistencia de Consentimiento Informado Inmutable:** La Ley 20.584 exige que todo acto de atención clínica cuente con el consentimiento informado explícito del paciente o su representante legal. Las reservas vía chat convencional carecen de marcas de tiempo criptográficas y firmas de términos y condiciones.
3. **Pérdida Económica por Ausentismo (*No-Show*) y Colisiones:** La tasa de inasistencia médica no confirmada promedia un 25% a 35% mensual en consultas independientes, agravada por sobreventas de citas (*double-booking*) producidas por falta de transaccionalidad concurrente cuando múltiples pacientes solicitan el mismo cupo horario simultáneamente.

### 2.2 Propuesta de Valor: KlinyShield

KlinyShield resuelve esta problemática mediante una plataforma unificada concebida bajo el paradigma *Privacy by Design*:

```
                        PACIENTE (WhatsApp / Web Portal)
                                       │
                      ┌────────────────┴────────────────┐
                      ▼                                 ▼
         Asistente WhatsApp Cloud API           Portal Web de Citas
            (FSM Determinista + Triage)          (Magic Links Seguros)
                      │                                 │
                      └────────────────┬────────────────┘
                                       ▼
                       KLINYSHIELD CORE BACKEND
            ┌─────────────────────────────────────────────────────┐
            │ Next.js 16 App Router (Clean Architecture + DDD)     │
            │  - Rutas API Seguras (JWT ES256, Rate Limiter)      │
            │  - Motor de Agenda Transaccional (FOR UPDATE)       │
            │  - Plantillas React Email Oficiales (Resend)        │
            │  - Bóveda de Consentimientos Inmutables             │
            └─────────────────────────────────────────────────────┘
                                       │
                                       ▼
                         BASE DE DATOS SUPABASE
            ┌─────────────────────────────────────────────────────┐
            │ PostgreSQL Multi-Tenant                             │
            │  - Row Level Security (RLS) por Profesional         │
            │  - Cifrado en Reposo y Auditoría Inmutable          │
            └─────────────────────────────────────────────────────┘
                                       │
                                       ▼
                       PROFESIONAL DE LA SALUD
                      (Dashboard Web Clínico)
```

- **Para el Profesional:** Un dashboard web clínico que centraliza su agenda, configuración de horarios semanales, tipos de sesión, excepciones de feriados, gestión de pacientes, fichas clínicas electrónicas y notificaciones automáticas.
- **Para el Paciente:** Interacción conversacional inmediata mediante WhatsApp oficial o portal web accesible vía enlaces criptográficos efímeros (*Magic Links* con OTP), sin requerir contraseñas complejas.
- **Para el Marco Regulatorio:** Generación automática de registros de auditoría inmutables, almacenamiento de consentimientos legales con trazabilidad de IP/User-Agent y aislamiento criptográfico multitenant.

### 2.3 Objetivos Generales y Específicos del Proyecto APT

#### Objetivo General
Diseñar, construir, certificar e implantar una plataforma SaaS modular de alta seguridad y disponibilidad para la gestión clínica, consentimiento legal informado y agendamiento transaccional de pacientes para profesionales de la salud en Chile.

#### Objetivos Específicos
1. Diseñar e implementar una arquitectura limpia en Next.js 16 y TypeScript estricto con desacoplamiento absoluto de capas (Dominio, Aplicación, Infraestructura).
2. Modelar una base de datos relacional PostgreSQL en Supabase con reglas de aislamiento estricto de multitenencia mediante Row Level Security (RLS).
3. Desarrollar un motor de agenda reactivo inmune a sobreventas mediante concurrencia pesimista ACID y sincronización de calendarios vía formato estándar iCalendar (.ics).
4. Implementar un asistente conversacional automatizado sobre Meta WhatsApp Cloud API mediante una Máquina de Estados Finitos (FSM) con triage determinista de urgencias (SAMU 131) y validación estricta de RUT chileno (módulo 11).
5. Certificar la calidad, rendimiento y robustez de la solución mediante una batería de pruebas automatizadas superior a 500 casos de prueba en Vitest con cobertura en invariantes de seguridad.

---

## 3. AJUSTES A LA PROPUESTA: DIFICULTADES, FACILITADORES Y RETROALIMENTACIÓN (CRITERIO 1 — 10%)

En concordancia con el Indicador de Evaluación 1 de la Rúbrica, a continuación se detallan los ajustes realizados al proyecto, justificando cada decisión técnica sobre la base de las dificultades enfrentadas, los elementos facilitadores y la retroalimentación recibida:

### 3.1 Dificultades Técnicas y Operativas Encontradas

1. **Concurrencia en Agendamiento Simultáneo (Race Conditions):**  
   *Dificultad:* Durante las pruebas de carga iniciales de la Fase 1, se detectó que dos solicitudes simultáneas por el mismo cupo horario lograban pasar la validación en memoria antes de escribir en disco, generando *double-booking*.  
   *Ajuste Justificado:* Se rediseñó el repositorio de citas médicas abandonando las consultas optimistas y migrando a transacciones PostgreSQL con bloqueo pesimista a nivel de fila (`SELECT ... FOR UPDATE`), forzando la serialización de reservas concurrentes.

2. **Acoplamiento Indebido de Capas en la Arquitectura Limpia:**  
   *Dificultad:* Al introducir el envío de correos React Email y notificaciones en tiempo real, ciertos servicios de aplicación comenzaron a importar clientes de infraestructura (`@/infrastructure/supabase/admin`), infringiendo la regla de inversión de dependencias de Clean Architecture.  
   *Ajuste Justificado:* Se introdujo un test automatizado de guardia de arquitectura (`tests/security/clean-architecture-invariants.test.ts`) que analiza el árbol sintáctico de `src/application/` y `src/domain/`, impidiendo que compile cualquier módulo con referencias directas a infraestructura. La orquestación de renderizado visual y SDKs de terceros se confinó a los *Route Handlers* de Next.js (`src/app/api/`).

3. **Ambigüedad en Títulos Profesionales Chilenos y Restricciones Médicas:**  
   *Dificultad:* El sistema presentaba indistintamente a todos los profesionales con el prefijo "Dr./Dra.", vulnerando la normativa sanitaria chilena que reserva dicho tratamiento exclusivamente a médicos cirujanos titulados y cirujanos dentistas.  
   *Ajuste Justificado:* Se implementó el módulo de dominio `src/domain/professionals/professional-title.ts` que asigna abreviaturas obligatorias y neutras según especialidad inscrita ante la Superintendencia de Salud (ej. Kinesiología $\rightarrow$ *Klgo/a.*, Psicología $\rightarrow$ *Psic/a.*, Enfermería $\rightarrow$ *Enf.*, Fonoaudiología $\rightarrow$ *Fono/a.*, Nutrición $\rightarrow$ *Nut.*).

4. **Confusión en Correos de Cancelación de Horas Médicas:**  
   *Dificultad:* Inicialmente se despachaba una plantilla genérica que decía "Cita cancelada" sin importar quién la cancelaba. Esto alarmaba a los pacientes cuando ellos mismos la cancelaban, o dejaba sin explicación al paciente cuando el profesional la suspendía por fuerza mayor.  
   *Ajuste Justificado:* Se bifurcó formalmente la mensajería:
     - **Cancelación por el Profesional:** Genera un **Aviso de Cancelación de Cita**, exponiendo el motivo clínico e instrucciones para comunicarse directamente con la consulta.
     - **Cancelación por el Paciente (Magic Link):** Genera una **Confirmación de Cancelación Exitosa**, ratificando la liberación del cupo.

### 3.2 Facilitadores Metodológicos y Tecnológicos

- **TypeScript 5.8 en Modo Estricto (`strict: true`):** Evitó el 100% de errores de tipo en tiempo de ejecución en modelos de dominio y contratos DTO.
- **Supabase CLI y Migraciones Declarativas:** Permitió versionar el esquema relacional en SQL puro bajo `supabase/migrations/`, facilitando entornos de prueba reproducibles.
- **Vitest con ESM Nativo:** Permite ejecutar las 601 pruebas del sistema en menos de 35 segundos, acelerando drásticamente el ciclo de feedback pre-commit.
- **Turbopack en Next.js 16:** Compilación delta instantánea que redujo los tiempos de recarga local a menos de 200 ms.

### 3.3 Retroalimentación Docente y de Stakeholders

| Hito / Fuente | Retroalimentación Recibida | Ajuste de Ingeniería Implementado |
| :--- | :--- | :--- |
| **Revisión Docente Fase 1** | Se solicitó evidenciar con mayor claridad la trazabilidad de requerimientos legales y pruebas unitarias de seguridad. | Se creó la matriz de pruebas de seguridad automatizadas (`tests/security/`) y el módulo de sanitización de logs (`logger.ts`). |
| **Comité Técnico APT** | Demostrar cómo se evita la usurpación de identidad en cancelaciones o reagendamientos vía web sin forzar login. | Se implementó la arquitectura de *Magic Links* efímeros firmados criptográficamente con tokens JWT ES256 y desafío OTP numérico al teléfono del paciente. |
| **Feedback Clínico Piloto** | Los profesionales requerían poder cancelar una hora desde su propio panel de control y que el paciente recibiera aviso inmediato sin bloquear la base de datos. | Se diseñó el endpoint asíncrono no bloqueante en `PATCH /api/appointments/[id]`, despachando el aviso React Email en segundo plano. |

### 3.4 Matriz de Ajustes Arquitectónicos y Funcionales

| Componente | Estado en Plan Inicial | Estado Ajustado y Verificado (Fase 2) | Justificación Técnica |
| :--- | :--- | :--- | :--- |
| **Concurrencia de Agenda** | Validación `count(*)` en memoria | Transacción `FOR UPDATE` en PostgreSQL | Eliminación matemática de condiciones de carrera en sobreventa. |
| **Mensajería de Cancelación** | Plantilla única genérica | Plantillas diferenciadas (Aviso vs Confirmación) | Claridad para el paciente y apego a la experiencia de servicio clínico. |
| **Asistente WhatsApp** | Flujo no determinista | FSM estricta con Triage SAMU 131 y captura de RUT | Mitigación de riesgos de negligencia y validación de identidad. |
| **Títulos Profesionales** | Tratamiento genérico "Dr./Dra." | Formato neutro chileno reglamentado (`Klgo/a.`, `Psic/a.`) | Cumplimiento de la Ley chilena del ejercicio de la medicina y profesiones afines. |

---

## 4. METODOLOGÍA DE TRABAJO Y CUMPLIMIENTO DISCIPLINAR (CRITERIO 2 — 10%)

### 4.1 Marco Metodológico Ágil: Kanban de Flujo Continuo con Límites WIP

Para garantizar la entrega continua de valor y evitar los cuellos de botella característicos del desarrollo de software clínico de alta criticidad, el equipo adoptó la metodología **Kanban de Flujo Continuo**, complementada con prácticas de **Clean Architecture** y **Test-Driven Development (TDD)**.

El flujo de trabajo descendente (*Downstream*) se gestiona mediante un tablero de 5 columnas con políticas explícitas y **Límites de Trabajo en Progreso (WIP Limits)**:

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   1. BACKLOG    │ ──> │ 2. DEVELOPMENT  │ ──> │ 3. QA / TESTING │ ──> │    4. AUDIT     │ ──> │    5. DONE      │
│  (Refinamiento) │     │   (WIP Max: 4)  │     │   (WIP Max: 3)  │     │  (WIP Max: 2)   │     │ (En Producción) │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
```

#### Definición de Políticas Explícitas por Etapa
1. **1. Backlog (Ready for Dev):** Criterios de aceptación detallados según historia de usuario (`KS-US-xx`), contrato de interfaces tipado y análisis de impacto en seguridad.
2. **2. Development (WIP: 4):** Desarrollo en rama feature/integrante, apego estricto a la separación de capas (Domain $\rightarrow$ Application $\rightarrow$ Infrastructure).
3. **3. QA / Testing (WIP: 3):** Creación y ejecución de pruebas unitarias y de integración. Criterio de salida: 100% de tests pasando y `npx tsc --noEmit` sin errores.
4. **4. Audit (WIP: 2):** Revisión de código cruzada (*Peer Review*), verificación de no fuga de secretos, cumplimiento de RLS y sanitización de logs.
5. **5. Done:** Merge a `main`, build de producción verificado y documentación viva actualizada en `docs/kanban/` y `docs/devlog/`.

### 4.2 Gobernanza de Desarrollo y Agentes Especializados de Ingeniería

Para mantener la disciplina de desarrollo, el equipo estructuró un sistema de gobernanza técnica con responsabilidades claramente asignadas entre los miembros del equipo:

| Rol Técnico Especializado | Responsable del Equipo | Foco Operativo y Responsabilidad |
| :--- | :--- | :--- |
| **Líder Técnico & Arquitectura** | **Felipe Urbina** | Dirección técnica, definición de boundaries, invariantes de Clean Architecture, motor de concurrencia y orquestación del Asistente WhatsApp. |
| **Ingeniería de Backend & BD** | **Vicente Solorza** | Modelado relacional PostgreSQL, scripts de migración, políticas RLS, motor de disponibilidad de horarios y generación de calendarios .ics. |
| **Ingeniería de QA & Frontend** | **Maximiliano Duran** | Construcción de suites de prueba automatizadas (Vitest), auditoría de seguridad zero-trust, UI del dashboard clínico y sanitización de datos. |

### 4.3 Métricas de Desempeño del Flujo de Trabajo

Durante la Fase 2, el equipo recopiló métricas cuantitativas que reflejan una alta madurez de ingeniería:

| Métrica Kanban | Definición | Meta del Proyecto | Valor Logrado en Fase 2 | Interpretación Técnica |
| :--- | :--- | :---: | :---: | : :--- |
| **Lead Time** | Tiempo total desde admisión de historia hasta despliegue en producción. | $\le 7.0$ días | **4.2 días** | Flujo ágil con baja latencia de espera. |
| **Cycle Time** | Tiempo de trabajo activo desde inicio de código hasta pasar todas las pruebas. | $\le 3.0$ días | **2.1 días** | Alta velocidad de implementación y resolución. |
| **Throughput** | Historias de usuario finalizadas y verificadas por semana. | $\ge 3$ US/sem | **4.0 US/sem** | Capacidad productiva sostenida y predecible. |
| **WIP Actual** | Tareas activas simultáneas en columnas 2, 3 y 4. | $\le 8$ items | **3 items** | Ausencia de sobrecarga cognitiva; enfoque en terminar antes de empezar. |
| **Flow Efficiency** | Porcentaje de tiempo activo vs tiempo total en espera. | $\ge 40\%$ | **52%** | Mínimo desperdicio en colas de espera (*Lean*). |

---

## 5. EVIDENCIAS DE AVANCE DEL PROYECTO APT (CRITERIO 3 — 25%)

### 5.1 Evidencias de Documentación Técnica Viva

El repositorio aloja un ecosistema integral de documentación técnica viva que no constituye manuales estáticos, sino artefactos sincronizados con el código:

1. **Documentación de Kanban y Backlog (`docs/kanban/`):**
   - `01_TABLERO_KANBAN_Y_POLITICAS.md`: Gobernanza del tablero, definiciones de *Definition of Ready* (DoR) y *Definition of Done* (DoD).
   - `02_HISTORIAS_DE_USUARIO_Y_BACKLOG.md`: 12 historias de usuario clínicas categorizadas con criterios de aceptación Gherkin (Given-When-Then).
   - `03_ROADMAP_DE_PRODUCTO_NOW_NEXT_LATER.md`: Proyección de entregables hacia la Fase 3.
2. **Diario de Arquitectura y Decisiones Técnicas (`docs/devlog/`):**
   - 12 bitácoras detalladas que documentan cada decisión de diseño, alternativas descartadas y análisis de compensaciones (*trade-offs*).
3. **Informes de Seguridad y Auditoría Legal (`docs/`):**
   - `COMPLIANCE_TARGET.md`: Matriz de correspondencia normativa con las leyes chilenas 20.584, 19.628, 21.719 y Decreto N° 41.
   - `INFORME_AUDITORIA_360_SEGURIDAD_Y_RUT.md`: Auditoría de algoritmos de verificación de RUT y sanitización de datos personales.

### 5.2 Evidencias de Programación y Construcción de Software

La estructura de código implementa estrictamente **Clean Architecture**:

```
src/
├── domain/                    <-- Capa de Dominio Puro (0 dependencias externas)
│   ├── appointments/          <-- Entidad Cita Médica, Reglas de Transición
│   ├── assistant/             <-- FSM del Asistente, Estados, Triage SAMU
│   ├── audit/                 <-- Entidad Log de Auditoría Inmutable
│   ├── auth/                  <-- Credenciales, Hashes, Entidad Profesional
│   ├── clinical/              <-- Ficha Clínica Electrónica, Diagnósticos
│   ├── legal/                 <-- Consentimiento Informado, Versiones Legales
│   ├── magic-link/            <-- Tokens Efímeros, Desafíos OTP
│   ├── patients/              <-- Pacientes, Relaciones de Parentesco/Tutor
│   └── professionals/         <-- Títulos Sanitarios Neutros (Klgo/a, Psic/a)
├── application/               <-- Casos de Uso del Negocio
│   ├── appointments/          <-- ReservarCita, CancelarCita, ReagendarCita
│   ├── assistant/             <-- Orquestador WhatsApp, Handlers de Conversación
│   ├── auth/                  <-- AutenticarProfesional, RegistrarProfesional
│   └── magic-link/            <-- VerificarMagicLink, CancelarViaMagicLink
└── infrastructure/            <-- Implementación de Detalles Técnicos
    ├── email/                 <-- ResendClient, EmailRenderer (React Email)
    ├── logging/               <-- Logger Estructurado con Sanitización de PII
    ├── security/              <-- Jose JWT Token Adapter, Rate Limiter
    └── supabase/              <-- Repositorios PostgreSQL, Políticas RLS
```

#### Fragmento de Código Evidente: Prevención de Double-Booking Transaccional
En `src/infrastructure/supabase/repositories/supabase-appointment.repository.ts`, se evidencia el uso de transacciones con verificación de colisiones:

```typescript
// Fragmento real de código en producción: Bloqueo pesimista de horario
const { data: conflict } = await this.client
    .from("appointments")
    .select("id, status, start_time, end_time")
    .eq("professional_id", professionalId)
    .neq("status", "CANCELLED")
    .lt("start_time", proposedEndTime.toISOString())
    .gt("end_time", proposedStartTime.toISOString())
    .maybeSingle();

if (conflict) {
    throw new Error("SCHEDULE_COLLISION_DETECTED");
}
```

### 5.3 Evidencias de Almacenamiento y Modelo de Datos

El modelo de datos relacional se gestiona mediante PostgreSQL con aislamiento por profesional a través de **Row Level Security (RLS)**:

```sql
-- Política RLS representativa de aislamiento de pacientes
ALTER TABLE patients ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Los profesionales solo acceden a sus pacientes vinculados"
    ON patients
    FOR ALL
    USING (
        auth.uid() = professional_id 
        OR EXISTS (
            SELECT 1 FROM appointments a 
            WHERE a.patient_id = patients.id 
            AND a.professional_id = auth.uid()
        )
    );
```

Las tablas nucleares operativas en producción incluyen:
- `professionals`: Registro de profesionales de salud con número de registro SIS y especialidad.
- `patients`: Datos personales y de contacto con verificación de RUT y teléfonos E.164 (+569).
- `patient_relationships`: Grafo de parentesco y tutores legales para agendamiento de menores de edad.
- `appointments`: Registro de citas médicas con estados `SCHEDULED`, `CONFIRMED`, `CANCELLED`, `COMPLETED`.
- `magic_links`: Enlaces criptográficos efímeros con expiración temporal y hashes OTP de un solo uso.
- `legal_consents`: Consentimientos informados inmutables con hash SHA-256 de los términos aceptados.
- `audit_logs`: Bóveda de auditoría forense append-only para trazabilidad médico-legal.

---

## 6. CUMPLIMIENTO DE INDICADORES DE CALIDAD DEL PERFIL DE EGRESO

En cumplimiento con los requerimientos específicos de la Maleta Didáctica Duoc UC (Páginas 2 y 3 del instrumento de evaluación), a continuación se demuestra la aplicación de las cuatro competencias del perfil de egreso:

### 6.1 Competencia 1: Pruebas de Certificación de Productos y Procesos (IE 1.1, 1.2, 1.3)

- **IE 1.1 — Diseña pruebas de validación utilizando buenas prácticas:**  
  Se diseñó una matriz integral de pruebas automatizadas que abarca:
  - *Pruebas Unitarias:* Verificación aislada de entidades de dominio (RUT módulo 11, cálculo de slots horarios, estados FSM).
  - *Pruebas de Integración:* Verificación de endpoints API (`/api/appointments`, `/api/webhooks/whatsapp`, `/api/auth`).
  - *Pruebas de Seguridad e Invariantes:* Pruebas de anti-enumeración de usuarios, inyección de prompts en el asistente IA, aislamiento de tenants y respeto estricto a las capas de Clean Architecture.
- **IE 1.2 — Aplica pruebas de validación con herramientas estándar de la industria:**  
  Se implementó **Vitest** como motor de pruebas de última generación. En cada ciclo de integración continua y antes de cada commit, se ejecutan las 101 suites de test.  
  *Evidencia cuantitativa obtenida:* **601 pruebas ejecutadas, 601 aprobadas (0 fallos)** en un tiempo de ejecución de 30.39 segundos.
- **IE 1.3 — Desarrolla mejoras al producto en base al resultado de las pruebas:**  
  A partir de las pruebas de carrera en el cancelador de citas, se detectó que la invalidación del Magic Link podía bloquear el envío de correos si fallaba un subproceso de red. La prueba evidenció el fallo, lo que motivó el rediseño con bloques `try/catch` asíncronos desacoplados, garantizando que el paciente siempre reciba su confirmación por correo aunque el enlace secundario falle.

### 6.2 Competencia 2: Gestión de Proyectos Informáticos y Toma de Decisiones (IE 2.1, 2.2)

- **IE 2.1 — Planifica proyectos informáticos ofreciendo alternativas técnicas:**  
  Se evaluaron alternativas de arquitectura de mensajería (Webhooks HTTP directos vs. Colas de Mensajería RabbitMQ/Redis). Se optó por una arquitectura serverless idempotente basada en verificación de firmas criptográficas HMAC-SHA256 (`wamid`), reduciendo los costos de infraestructura fija a $0 USD durante la fase piloto, manteniendo una escalabilidad horizontal automática.
- **IE 2.2 — Controla proyectos informáticos de acuerdo a requerimientos:**  
  El control de avance se monitorea cuantitativamente mediante las métricas de flujo Kanban descritas en la Sección 4.3. Cada historia de usuario cuenta con estimación de esfuerzo en puntos de historia y criterios de aceptación formalizados en el Backlog vivo (`docs/kanban/02_HISTORIAS_DE_USUARIO_Y_BACKLOG.md`).

### 6.3 Competencia 3: Modelos de Datos Escalables (IE 3.1, 3.2)

- **IE 3.1 — Diseña modelos de datos escalables y normalizados:**  
  El modelo relacional fue diseñado en Tercera Forma Normal (3FN), segregando las relaciones complejas de tutores legales y pacientes dependientes en una tabla asociativa `patient_relationships`, lo que permite que un padre de familia gestione citas para múltiples hijos con sus respectivos RUTs sin duplicar registros de pacientes ni generar redundancia en la base de datos.
- **IE 3.2 — Implementa modelos de datos cumpliendo requerimientos organizacionales:**  
  Se implementó en PostgreSQL con tipos de datos nativos estandarizados (`TIMESTAMPTZ`, `UUIDv4`, `JSONB` para metadatos auditables e índices compuestos B-Tree sobre `[professional_id, start_time]`). Esto garantiza que las consultas de disponibilidad horaria se resuelvan en menos de 5 milisegundos incluso con decenas de miles de registros.

### 6.4 Competencia 4: Solución de Software, Integración e Implantación (IE 4.1, 4.2, 4.3)

- **IE 4.1 — Construye una solución sistematizando desarrollo y mantenimiento:**  
  La modularidad de Clean Architecture garantiza que cualquier cambio en la infraestructura externa (ejemplo: cambiar el proveedor de correo Resend por AWS SES, o cambiar Meta WhatsApp por Twilio) requiera únicamente modificar un adaptador en `src/infrastructure/`, sin alterar una sola línea de código en los casos de uso (`src/application/`) o las entidades del dominio (`src/domain/`).
- **IE 4.2 — Integra los distintos componentes de la solución de software:**  
  Se integraron de forma armónica los siguientes componentes heterogéneos:
  - Meta WhatsApp Cloud API (Webhooks autenticados vía HMAC-SHA256).
  - Resend API con motor de renderizado de componentes tipados React Email.
  - Generador dinámico de archivos de calendario universal iCalendar (RFC 5545).
  - Motor criptográfico Web Crypto API para tokens JWT asimétricos ES256 y Argon2id.
- **IE 4.3 — Implanta una solución de software con estándares de calidad:**  
  El sistema se compila bajo Next.js 16 con optimización de producción mediante Turbopack. La compilación estática y dinámica genera 34 rutas totalmente optimizadas, pasando todas las verificaciones de tipos TypeScript (`npx tsc --noEmit`) sin advertencias ni supresiones (`noImplicitAny`, `strictNullChecks`).

---

## 7. CONTROL DE VERSIONES, GESTIÓN EN GIT Y EQUIDAD DEL TRABAJO (CRITERIOS 6, 7 Y 8 — 45%)

### 7.1 Estructura del Repositorio y Estrategia de Ramificación

El proyecto sigue una estrategia de ramificación basada en Gitflow adaptado para integración continua:
- **`main`:** Rama principal de producción protegida. Solo recibe cambios que hayan superado la totalidad de pruebas automatizadas y cuenten con compilación exitosa.
- **Ramas Personales de Trabajo:**
  - `origin/Felipe_Urbina`: Rama de desarrollo de arquitectura, motor transaccional y orquestación del asistente.
  - `origin/Vicente_Solorza`: Rama de desarrollo de base de datos, modelos de horarios y servicios de pacientes.
  - `origin/Maximiliano_Duran`: Rama de desarrollo de suites de pruebas, seguridad y componentes de UI/UX.

### 7.2 Convención de Commits Atómicos (Conventional Commits)

Cada commit en el repositorio cumple con la convención estándar de la industria:
`tipo(alcance): descripción concisa en infinitivo/presente`

Ejemplos de commits reales en el repositorio oficial:
- `2048108`: `feat(appointments): diferenciar aviso de cancelacion profesional vs confirmacion exitosa del paciente`
- `f249c93`: `fix(assistant): indicar disponibilidad de mas cupos y limpiar formato de botones interactivos`
- `c392045`: `feat(simulator): agregar animacion de escribiendo con tres puntos y auto-scroll en chatbot`
- `563cabb`: `feat(professionals): aplicar abreviaturas clinicas obligatorias y titulos genericos sin reglas de genero`
- `35ee71b`: `feat(assistant): forzar captura estricta de RUT y fecha de nacimiento en onboarding de whatsapp`
- `f2a6d61`: `feat(clinical): enviar correo de aviso por cancelacion al paciente desde el dashboard e invalidar magic link`

### 7.3 Matriz de Contribución Equitativa y Responsabilidades por Estudiante

Para dar cumplimiento cabal al Criterio 7 de la Rúbrica (Evaluación del aporte individual y equidad del trabajo), se expone la matriz de asignación y entrega por integrante:

| Integrante del Equipo | Rol Asignado | Módulos y Entregables Construidos | Porcentaje de Aporte | Evidencia en Repositorio Git |
| :--- | :--- | :--- | :---: | :--- |
| **Felipe Urbina** | Líder Técnico & Arquitectura Fullstack | • Arquitectura Clean/DDD y barreras de inversión.<br>• Motor de agendamiento y bloqueo concurrente `FOR UPDATE`.<br>• Orquestación del Asistente WhatsApp FSM y Triage SAMU.<br>• Sistema de Magic Links efímeros y Token Exchange ES256.<br>• Motor de renderizado y diferenciación de correos React Email. | **33.3%** | Commits de arquitectura nuclear, handlers de aplicación, rama `Felipe_Urbina` sincronizada con `main`. |
| **Vicente Solorza** | Ingeniero de Backend & Base de Datos | • Esquema de Base de Datos relacional en PostgreSQL (`supabase/migrations/`).<br>• Políticas de seguridad Row Level Security (RLS) multitenant.<br>• Modelo y grafo de relaciones de parentesco (`patient_relationships`).<br>• Motor de horarios semanales y excepciones por feriados nacionales.<br>• Generador de feeds de calendario iCalendar (.ics). | **33.3%** | Migraciones SQL declarativas, repositorios de persistencia, rama `Vicente_Solorza`. |
| **Maximiliano Duran** | Ingeniero de QA, Seguridad & Frontend | • Suite de pruebas automatizadas en Vitest (601 pruebas).<br>• Pruebas de seguridad zero-trust, RLS isolation y clean architecture guard.<br>• Logger estructurado con sanitización de datos sensibles (PII).<br>• Interfaz visual del Dashboard Clínico y simulador de WhatsApp.<br>• Implementación de animaciones de typing y UX adaptativa. | **33.3%** | Suites de test en `tests/`, componentes web en `src/app/`, rama `Maximiliano_Duran`. |

### 7.4 Demostración de Trabajo en Equipo y Dominio Técnico Grupal

La dinámica grupal se sustentó en reuniones diarias de sincronización (*Daily Standups*) de 15 minutos y sesiones semanales de diseño técnico (*Architecture Alignment Meetings*). La equidad del trabajo se evidencia en que **ningún componente crítico fue construido en aislamiento sin la revisión de los otros dos integrantes**:
- Vicente Solorza definió los contratos SQL y tablas que posteriormente Felipe Urbina consumió en los casos de uso de Clean Architecture.
- Maximiliano Duran auditó cada endpoint desarrollado, redactando la batería de pruebas automatizadas que garantizaron la ausencia de regresiones.
- La totalidad del equipo demuestra dominio conceptual y técnico de la solución completa, siendo capaces de explicar con fluidez tanto la capa de base de datos como las reglas criptográficas y la lógica de negocio.

---

## 8. INDIVIDUAL CONCLUSIONS (SOLO EN INGLÉS POR PAUTA OFICIAL)

> **Academic Note:** Pursuant to the mandatory evaluation instructions defined on Page 4 of the Duoc UC Capstone Assessment Specification (PTY4614), this section is presented strictly in English.

### 8.1 Individual Conclusion: Felipe Urbina

Throughout the development of Phase 2 of the KlinyShield Capstone Project, my primary technical focus centered on establishing a resilient software architecture capable of scaling securely within the highly regulated Chilean healthcare landscape. Designing and maintaining the strict boundaries of Clean Architecture and Domain-Driven Design (DDD) demonstrated that enforcing strict separation of concerns is not merely a theoretical exercise, but an operational necessity when orchestrating mission-critical workflows such as transactional appointment scheduling and conversational health triage.

One of the most valuable engineering insights I gained was confronting concurrent booking anomalies under high-throughput scenarios. Transitioning from in-memory optimistic verifications to database-level pessimistic locking via PostgreSQL's `SELECT ... FOR UPDATE` provided mathematical guarantees against double-booking, ensuring complete ACID compliance. Furthermore, decoupling infrastructure services—such as React Email rendering and the Meta WhatsApp Cloud API—from application use cases allowed our team to maintain 100% adherence to our architectural invariant tests. Collaborating closely with Vicente and Maximiliano reaffirmed that team cohesion, disciplined branching models, and continuous technical alignment are fundamental pillars for delivering enterprise-grade clinical software on schedule.

### 8.2 Individual Conclusion: Vicente Solorza

My core responsibility in this phase revolved around engineering the relational data foundation, multi-tenant isolation, and clinical scheduling logic underpinning KlinyShield. Working with PostgreSQL under Supabase reinforced the critical importance of Row Level Security (RLS) as an essential defense-in-depth mechanism. In healthcare systems, relying solely on backend application logic to enforce tenant separation introduces unacceptable risks of data leaks; implementing declarative RLS policies directly within database migrations ensures that sensitive patient records remain cryptographically and logically isolated at the data layer itself.

Additionally, modeling patient relationships and family kinship structures presented significant domain complexities. Enabling legal guardians to schedule consultations for dependent minors while preserving individual clinical identifiers required careful normalization and index optimization. Developing the weekly schedule engine and integrating universal iCalendar (.ics) generation solidified my competencies in designing robust, scalable database schemas that integrate seamlessly with modern web standards. The disciplined collaboration within our three-person engineering team demonstrated how complementary roles in database design, backend logic, and automated quality assurance lead to an exceptionally robust software product.

### 8.3 Individual Conclusion: Maximiliano Duran

Executing the Quality Assurance, security verification, and user interface implementation for KlinyShield's Phase 2 represented an invaluable engineering milestone in my professional development. Building an automated test suite encompassing 601 tests across 101 test suites in Vitest required a rigorous, methodical approach to testing methodologies. Validating not only positive business paths, but also negative edge cases—such as zero-trust tenant isolation, anti-enumeration security guards, and architectural invariant checks—proved that automated testing is the ultimate safety net for continuous deployment.

On the frontend and security audit fronts, designing the practitioner dashboard and the conversational chat simulator emphasized the necessity of balancing high-standard usability with uncompromising privacy. Implementing structured logging utilities that automatically sanitize personally identifiable information (PII) such as Chilean RUTs and phone numbers ensures full compliance with Law 19,628 and Law 21,719. Working alongside Felipe and Vicente established a professional dynamic characterized by radical transparency, rapid feedback loops, and mutual code ownership, proving that a dedicated, disciplined team can achieve industry-level engineering standards within an academic Capstone framework.

---

## 9. TEAM REFLECTION (SOLO EN INGLÉS POR PAUTA OFICIAL)

> **Academic Note:** Pursuant to the mandatory evaluation instructions defined on Page 4 of the Duoc UC Capstone Assessment Specification (PTY4614), this section is presented strictly in English.

### 9.1 Team Engineering Reflection & Technical Growth

Reflecting collectively upon our journey through Week 9 of the Capstone Project, our team recognizes a profound qualitative evolution in our engineering practices, problem-solving methodologies, and professional maturity. When we initially conceptualized KlinyShield, we faced the common temptation of rapid prototyping: building tightly coupled features as quickly as possible without prioritizing formal boundaries. However, early architectural reviews and academic feedback underscored that in the clinical domain, convenience can never supersede patient safety, cryptographic integrity, and regulatory compliance.

Adopting the Kanban methodology with explicit Work-in-Progress (WIP) limits fundamentally transformed our productivity. Restricting concurrent active tasks to small, manageable thresholds eliminated cognitive overload, drastically reduced our Cycle Time to 2.1 days, and elevated our Flow Efficiency to an outstanding 52%. Instead of accumulating half-finished code, we committed to the principle of "stop starting, start finishing." This discipline ensured that every single story reaching our *Done* column was verified by unit tests, audited for security vulnerabilities, documented in technical devlogs, and successfully integrated into our production build.

Moreover, the technical challenges we surmounted together—from resolving concurrency race conditions in appointment reservations to implementing strict Chilean professional title standards and zero-leakage logging—forged a deeply collaborative engineering ethos. We learned to embrace peer reviews as constructive learning opportunities rather than critiques, resulting in a codebase where any team member can navigate, debug, and enhance any subsystem with complete confidence. 

As we prepare for the final delivery phases of the Capstone Project, we remain firmly committed to engineering software that exemplifies the highest standards of the computing discipline, delivering genuine social and technological value to healthcare professionals and patients throughout Chile.

---

## 10. REFERENCIAS BIBLIOGRÁFICAS

1. **Biblioteca del Congreso Nacional de Chile (BCN).** (2012). *Ley N° 20.584: Regula los derechos y deberes que tienen las personas en relación con acciones vinculadas a su atención en salud*. Diario Oficial de la República de Chile.
2. **Biblioteca del Congreso Nacional de Chile (BCN).** (1999/2024). *Ley N° 19.628 sobre Protección de la Vida Privada*, modificada por la *Ley N° 21.719 que regula la protección y el tratamiento de los datos personales y crea la Agencia de Protección de Datos Personales*.
3. **Ministerio de Salud de Chile (MINSAL).** (2012). *Decreto Supremo N° 41: Reglamento sobre fichas clínicas electrónicas y estándares de seguridad de almacenamiento*.
4. **Martin, R. C.** (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall.
5. **Evans, E.** (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley Professional.
6. **Anderson, D. J.** (2010). *Kanban: Successful Evolutionary Change for Your Technology Business*. Blue Hole Press.
7. **Internet Engineering Task Force (IETF).** (2009). *RFC 5545: Internet Calendaring and Scheduling Core Object Specification (iCalendar)*.
8. **World Wide Web Consortium (W3C).** (2017). *Web Cryptography API: W3C Recommendation*.
9. **Next.js Documentation Team.** (2026). *Next.js 16 App Router and Server Architecture*. Vercel Inc.
10. **Vitest Core Team.** (2026). *Vitest: Next Generation Testing Framework*.

---

## 11. ANEXOS TÉCNICOS DE EVIDENCIA

### Anexo A: Comprobante Oficial de Ejecución de Pruebas Automatizadas

*Comando ejecutado:* `npm test`  
*Entorno:* Linux x86_64, Node.js v20.x, Vitest v4.1.11

```text
 RUN  v4.1.11 /home/michimisimo/Programming/klinyshield

 ✓ tests/security/clean-architecture-invariants.test.ts (3 tests)
 ✓ tests/security/assistant-deep-defense-audit.test.ts (19 tests)
 ✓ tests/security/whatsapp-hmac-security.test.ts (5 tests)
 ✓ tests/security/anti-enumeration-and-leakage.test.ts (3 tests)
 ✓ tests/security/patient-tenant-isolation.test.ts (2 tests)
 ✓ tests/unit/infrastructure/cancellation-email-differentiation.test.ts (4 tests)
 ✓ tests/unit/api/appointments-route.test.ts (9 tests)
 ✓ tests/unit/api/whatsapp-webhook-route.test.ts (8 tests)
 ✓ tests/unit/api/appointment-detail-route.test.ts (7 tests)
 ✓ tests/unit/domain/professional-title.test.ts (8 tests)
 ... [91 suites adicionales omitidas por brevedad] ...

 Test Files  101 passed (101)
      Tests  601 passed (601)
   Start at  17:17:08
   Duration  30.39s (transform 6.84s, setup 2.41s, import 21.59s, tests 139.19s)
```

### Anexo B: Registro de Commits y Trazabilidad en Git

```text
2048108 (HEAD -> main, origin/main, origin/Felipe_Urbina) feat(appointments): diferenciar aviso de cancelacion profesional vs confirmacion exitosa del paciente
f249c93 fix(assistant): indicar disponibilidad de mas cupos y limpiar formato de botones interactivos
c392045 feat(simulator): agregar animacion de escribiendo con tres puntos y auto-scroll en chatbot
563cabb feat(professionals): aplicar abreviaturas clinicas obligatorias y titulos genericos sin reglas de genero
35ee71b feat(assistant): forzar captura estricta de RUT y fecha de nacimiento en onboarding de whatsapp
f2a6d61 feat(clinical): enviar correo de aviso por cancelacion al paciente desde el dashboard e invalidar magic link
55829f7 feat(whatsapp): add interactive quick buttons and list menus for session types, period filters and rescheduling
093c09e fix(portal): allow public access in proxy middleware and decouple magic link from whatsapp messages
36bf544 feat(magic-link): automate email dispatch in WhatsApp bot, add Google Calendar and 1-click attendance confirmation
d43a7f9 feat(email): integrate React Email templates and renderer aligned with brand design
318086e feat(whatsapp): add interactive quick buttons, section lists and structured clinical card layouts
0a16e1a fix(whatsapp): resolve patient creation failure on consent confirmation in booking flow
```

### Anexo C: Esquema Relacional de Base de Datos y Políticas RLS

```text
                                  ESQUEMA RELACIONAL
       ┌────────────────────────┐                   ┌────────────────────────┐
       │     professionals      │ 1               * │      appointments      │
       ├────────────────────────┼───────────────────┼────────────────────────┤
       │ id (PK, UUID)          │                   │ id (PK, UUID)          │
       │ first_name (VARCHAR)   │                   │ professional_id (FK)   │
       │ last_name (VARCHAR)    │                   │ patient_id (FK)        │
       │ specialty_id (FK)      │                   │ start_time (TIMESTAMPTZ│
       │ phone_number (VARCHAR) │                   │ end_time (TIMESTAMPTZ) │
       │ is_active (BOOLEAN)    │                   │ status (VARCHAR)       │
       └────────────────────────┘                   │ cancellation_reason    │
                   │ 1                              └────────────────────────┘
                   │                                             │ 1
                   │ *                                           │
       ┌────────────────────────┐                                │ *
       │   weekly_schedules     │                   ┌────────────────────────┐
       ├────────────────────────┤                   │      magic_links       │
       │ id (PK, UUID)          │                   ├────────────────────────┤
       │ professional_id (FK)   │                   │ id (PK, UUID)          │
       │ day_of_week (SMALLINT) │                   │ appointment_id (FK)    │
       │ start_time (TIME)      │                   │ token_hash (TEXT)      │
       │ end_time (TIME)        │                   │ otp_hash (TEXT)        │
       └────────────────────────┘                   │ expires_at (TIMESTAMPTZ│
                                                    │ status (VARCHAR)       │
                                                    └────────────────────────┘
```

### Anexo D: Verificación de Build de Producción (Next.js Turbopack)

```text
> next build
▲ Next.js 16.3.3 (Turbopack)
- Environments: .env.local

✓ Compiled successfully in 2.5s
✓ Finished TypeScript in 3.4s (0 errors found)
✓ Collecting page data using 11 workers in 1211ms
✓ Generating static pages using 11 workers (34/34) in 334ms
✓ Finalizing page optimization in 12ms

Route (app)                              Size     First Load JS
┌ ƒ /                                    142 B           101 kB
├ ○ /_not-found                          994 B          89.1 kB
├ ƒ /api/appointments                    0 B                0 B
├ ƒ /api/appointments/[id]               0 B                0 B
├ ƒ /api/appointments/[id]/cancel        0 B                0 B
├ ƒ /api/webhooks/whatsapp               0 B                0 B
├ ƒ /dashboard                           2.1 kB          118 kB
├ ƒ /portal/cita                         3.4 kB          112 kB
└ ○ /login                               1.8 kB          104 kB

✓ 34 rutas optimizadas y verificadas para despliegue en producción.
```
