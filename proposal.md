# Propuesta TP DSW

## Grupo

### Integrantes

* 52665 - Mistraletti, Alejo
* 54449 - Martinez, Ramiro
* legajo - Apellido(s), Nombre(s)
* legajo - Apellido(s), Nombre(s)

### Repositorios

* [frontend app](http://hyperlinkToGithubOrGitlab)
* [backend app](http://hyperlinkToGithubOrGitlab)

## Tema

### Descripción

Sistema de gestión para un gimnasio que permite administrar socios, membresías,
actividades e instructores. Los socios pueden consultar su estado de membresía
y acceder a rutinas de entrenamiento personalizadas creadas por los instructores.
El personal administrativo gestiona altas, pagos y la asignación de rutinas.

### Modeloo de dominio
Aca agregue la fotro

## Alcance Funcional

### Alcance Mínimo

Regularidad:

| Req | Detalle |
| --- | --- |
| CRUD simple | 1. CRUD Socio  2. CRUD Actividad  3. CRUD Instructor  4. CRUD Plan de Membresía |
| CRUD dependiente | 1. CRUD Membresía {depende de} CRUD Socio y CRUD Plan  2. CRUD Turno {depende de} CRUD Actividad y CRUD Instructor |
| Listado + detalle | 1. Listado de turnos filtrado por actividad y/o día de la semana, muestra actividad, instructor, horario y cupo disponible => detalle muestra datos completos del turno y socios inscriptos  2. Listado de socios filtrado por estado de membresía (activo/vencido) y/o nombre, muestra nombre, DNI y estado => detalle muestra datos del socio, membresía vigente y rutinas asignadas |
| CUU/Epic | 1. Registrar nuevo socio y asignarle un plan de membresía  2. Inscribir un socio a un turno de clase |

Adicionales para Aprobación:

| Req | Detalle |
| --- | --- |
| CRUD | 1. CRUD Socio  2. CRUD Actividad  3. CRUD Instructor  4. CRUD Plan de Membresía  5. CRUD Membresía  6. CRUD Turno  7. CRUD Rutina (con sus ejercicios) |
| CUU/Epic | 1. Registrar nuevo socio y asignarle un plan de membresía  2. Inscribir un socio a un turno de clase (valida cupo y membresía vigente)  3. Crear una rutina de entrenamiento y asignarla a un socio  4. Registrar pago de membresía y renovar vencimiento |

### Alcance Adicional Voluntario

| Req | Detalle |
| --- | --- |
| Listados | 1. Agenda del día: listado de todos los turnos del día filtrado por fecha, muestra actividad, instructor, socios inscriptos y cupo restante  2. Socios con membresía próxima a vencer (en los próximos 7 días) |
| CUU/Epic | 1. Registrar asistencia de socios a un turno  2. Cancelar inscripción a un turno |
| Otros | 1. Panel del socio: vista donde el socio logueado puede ver su membresía vigente, próximos turnos inscriptos y rutinas asignadas |
