# Minutas de Reunión y Avance – TP DSW

**Proyecto:** Sistema de Gestión de Gimnasio (MyGymManager) **Materia:** Desarrollo de Software (DSW) **Integrantes:** Alodi, Milton (53796) · Borda, Iael (54483) · Martinez, Ramiro (54449) · Mistraletti, Alejo (52665)

---

## Parte A – Minutas de reunión

### Minuta 1 – Kick-off y definición de stack

**Fecha:** \~06/05/2026 · **Modalidad:** Discord· **Asistentes:** todo el equipo

**Temas tratados**

- Definición del tema (gestión de gimnasio) y alcance mínimo de la propuesta.
- Definición de alcance opcional y casos de uso.
- Creación de los repositorios backend y frontend.
- Stack acordado: Node + Express + TypeScript (back) y React + Vite + TypeScript (front).

**Decisiones**

- Arquitectura por capas en el backend (router / service / repository).
- Frontend con rutas por rol (administrativo, instructor, socio) usando react-router-dom.
- Migrar de npm a pnpm (se concretó el 15–16/05 en ambos repos).

**Tareas:** Alejo inicializa ambos proyectos y el README; Ramiro crea los repos y el commit inicial. Durante ese día todos los integrantes hicimos commits con cambios insignificantes para comprobar que funcione correctamente y adaptarnos al uso de github.

---

### Minuta 2 – Primer CRUD de Socios y UI base

**Fecha:** \~05/06/2026 · **Modalidad:** Discord · **Asistentes:** todo el equipo

**Temas tratados**

- Primer endpoint de socios (`getAll`, `getById`) leyendo desde un JSON, más `/health` y endpoint de bienvenida.
- Incorporación de Tailwind CSS y shadcn/ui en el frontend.
- Layouts y sidebar reutilizable por rol.

**Decisiones**

- Validar entradas con Zod desde el inicio.
- Un único componente de sidebar parametrizado por rol.

**Tareas:** Alejo (CRUD de socios y layouts); Iael (primeras pruebas de instructores).

---

### Minuta 3 – Conexión Front–Back y CORS

**Fecha:** \~26/06/2026 · **Modalidad:** Discord

**Temas tratados**

- Configuración de CORS en el backend y consumo de la API desde el servicio de socios del frontend (variables de entorno).
- Cambio del package a ES Modules y ajuste de imports.

**Decisiones:** mantener `.env` fuera del repositorio y documentar variables en el README.

---

### Minuta 4 – CRUDs de Instructores, Ejercicios, Planes y Clases

**Fecha:** \~10/07/2026 · **Modalidad:** Discord

**Temas tratados**

- CRUD de instructores (Iael), de ejercicios (Ramiro), de planes de membresía (Alejo) y de clases (Iael).
- Traducción de entidades al inglés: `Socio → Member`, `gymClasses → classSchedule`.
- Frontend: tabla de socios (`DataTable`), breadcrumbs, NotFound 404, `RoleBottomNav` para mobile.

**Decisiones:** convención de nombres en inglés en todo el código; filtros por categoría en clases.

---

### Minuta 5 – Migración a MySQL con Prisma

**Fecha:** \~17–25/07/2026 · **Modalidad:** Discord

**Temas tratados**

- Reemplazo de los mocks JSON por base relacional MySQL/MariaDB con Prisma ORM.
- Migración inicial y modelos de `ClassSchedule`, `ClassSession` y `ClassBooking`.
- Patrón singleton de `PrismaClient`, `shared/instances` y `handleError` para manejo de errores.
- Archivos `.http` para pruebas manuales de cada módulo.

**Decisiones**

- Eliminar `baseRepository` (se evaluó y se descartó, 30/07).
- Soft delete (`deletedAt`) en las entidades.

**Tareas:** Alejo (Prisma, schema, adapter MariaDB); Iael (migrar socio e instructor); Ramiro (CRUD socio con Prisma).

---

### Minuta 6 – Integración completa y DTOs de respuesta

**Fecha:** \~15–17/08/2026 · **Modalidad:** Discord

**Temas tratados**

- Alta de socio con tipo y número de documento; al crear socio se crea su membresía.
- DTOs de respuesta con Zod y `prisma-zod-generator`.
- CRUD de `classSchedule`, `classSession` y `classBooking` (Ramiro).
- Conexión de las pantallas de socios y planes con el backend; eliminación de mocks.

**Decisiones:** nuevas rutas de clases en el admin con página completa de alta/edición en lugar de modal.

---

### Minuta 7 – Pagos, rendimiento (N+1) y Rutinas

**Fecha:** \~01–10/09/2026 · **Modalidad:** Discord

**Temas tratados**

- Entidad de pago asociada a la membresía (último pago, método y monto).
- Detección y corrección del problema N+1 al listar socios con su membresía.
- CRUD de ejercicios y rutinas (backend y pantallas del frontend).
- Cambio de `PUT` a `PATCH` en servicios.

**Decisiones:** agregar peso y notas por ejercicio dentro de la rutina.

---

### Minuta 8 – Reservas, instructores en el front y 3ª entrega

**Fecha:** \~17–25/09/2026 · **Modalidad:** Clase / Discord

**Temas tratados**

- Reserva y reactivación de reservas de clase; semana de sesiones en el frontend.
- CRUD de instructores con Prisma y su pantalla de administración (Milton).
- Sincronización membresía ↔ socio: cancelar o reactivar una membresía impacta el estado del socio.
- Login con JWT, middlewares de autenticación/autorización y tests de auth.
- Confirmación de borrado en todas las entidades.
- Preparación de la **3ª entrega** (README y variables de entorno actualizados, 25/09).

**Decisiones:** unificar las respuestas de error con un middleware central y una clase base de error.

---

### Minuta 9 – Perfil de socio, paginación y mobile first

**Fecha:** \~02–09/10/2026 · **Modalidad:** Discord

**Temas tratados**

- Unificación del manejo de errores en back y front (interceptores).
- Área del socio: perfil, datos personales, membresía, historial de pagos, soporte (Milton) y home del socio (Alejo).
- Lazy loading de páginas, paginación en listados, criterio mobile first.
- Endpoint de reservas del socio autenticado.
- Fix: no se puede borrar un tipo de clase con sesiones creadas.

**Decisiones:** priorizar experiencia mobile en los componentes.

---

### Minuta 10 – Recurrencia de clases, patrón /me y cierre

**Fecha:** \~15–22/10/2026 · **Modalidad:** Discord / Clase

**Temas tratados**

- Alta de sesiones recurrentes estilo Google Calendar (máximo 1 mes, se quitó `frequency` e `interval`).
- Inmutabilidad de la fecha en clases periódicas y editable en clases puntuales.
- Patrón `/me` en socio, membresía, pagos, clases e instructor (evita pasar IDs manuales).
- Home del administrativo (membresías vencidas, sesiones del día) y del instructor.
- Validaciones en rutas y formularios, tests unitarios y revisión de PRs.

**Decisiones:** congelar funcionalidades y dedicar la última semana a pruebas y documentación de la entrega final.

---
