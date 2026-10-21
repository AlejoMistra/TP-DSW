# Propuesta TP DSW

## Grupo

### Integrantes

- 53796 - Alodi, Milton (com 301)
- 54483 - Borda, Iael (com 301)
- 54449 - Martinez, Ramiro (com 301)
- 52665 - Mistraletti, Alejo (com 303)

### Repositorios

- [frontend app](https://github.com/RamiroM04/Front-TP-DSW)
- [backend app](https://github.com/RamiroM04/Back-TP-DSW)

## Tema

Sistema de gestión para gimnasio.

### Descripción

Sistema de gestión para un gimnasio que permite administrar socios, membresías, clases e instructores.
Los instructores crean rutinas de entrenamiento y dictan clases.
Los socios pueden consultar el estado de su membresía, explorar rutinas para su entrenamiento diario, y reservar o cancelar cupos en las clases grupales disponibles.
El personal administrativo gestiona altas de socios, planes, instructores y cobro de cuotas.

### Diagrama de clases

```mermaid
classDiagram

class Member {
  +int id
  +string name
  +string surname
  +string idNumber
  +string email
  +string phone
  +Date joinDate
}

class MembershipPlan {
  +int id
  +string name
  +float price
  +int durationDays
  +string description
}

class Membership {
  +int id
  +Date startDate
  +Date endDate
  +string status
  +string lastPaymentMethod
  +float lastAmountPaid
}

class ClassSchedule {
  +int id
  +string name
  +string description
  +CategoriaClase category
  +int maxCapacity
  +int durationMinutes
}

class ClassSession {
  +int id
  +int classScheduleId
  +Date date
  +string startTime
  +int remainingCapacity
  +enum status
}

class ClassSessionRecurrence {
  +int id                 
  +RecurrenceFrequency frequency
  +string? daysOfWeek             
  +Date startDate  
  +Date endDate
}

class ClassBooking {
  +int id
  +int memberId
  +int classSessionId
  +Date bookingDate
  +enum status
}

class Instructor {
  +int id
  +string name
  +string surname
  +string email
}

class Routine {
  +int id
  +string name
  +string description
  +string level
  +Date createdDate
}

class Exercise {
  +int id
  +string name
  +string description
  +string muscleGroup
  +enum difficultyLevel
}

class RoutineExercise {
  +int sets
  +int repetitions
  +string notes
  +int order
}

%% RELATIONSHIPS

Exercise "1" --> "0..*" RoutineExercise : appears in

Member "1" --> "1" Membership : has
Membership "1" --> "1" MembershipPlan : corresponds to

ClassBooking "0..*" --> "1" Member : makes
ClassSession "1" --> "0..*" ClassBooking : has

ClassSchedule "1" --> "0..*" ClassSession : generates
ClassSchedule "0..*" --> "1" Instructor : teaches
ClassSession "0..*" --> "1" ClassSessionRecurrence : follows recurrence pattern


Member "0..*" --> "0..*" Routine : consults and follows
Routine "1" --> "1..*" RoutineExercise : contains

Instructor "1" --> "0..*" Routine : creates
Instructor "1" --> "0..*" Exercise : creates
```

## Alcance Funcional

### Alcance Mínimo

Regularidad:

| Req               | Detalle                                                                                                                                                                                                                                                                                                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CRUD simple       | 1. CRUD Socio<br>2. CRUD Plan de Membresía<br>3. CRUD Instructor<br>4. CRUD Ejercicio                                                                                                                                                                                                                                          |
| CRUD dependiente  | 1. CRUD Membresía {depende de} CRUD Socio y CRUD Plan de Membresía<br>2. CRUD Rutina {depende de} CRUD Instructor y CRUD Ejercicio                                                                                                                                                                                             |
| Listado + detalle | 1. Listado de socios filtrado por estado de membresía (activo/vencido) y/o nombre, muestra nombre, DNI y estado => detalle muestra datos del socio y membresía vigente<br>2. Listado de Rutinas filtrado por nivel => detalle muestra datos completos de los ejercicios                                                        |
| CUU/Epic          | 1. Registrar nuevo socio y asignarle un plan de membresía<br>2. Reserva y cancelación de cupo en clases por parte del socio: el socio consulta sesiones disponibles y reserva su cupo; el sistema valida disponibilidad y descuenta el cupo en tiempo real. El socio puede además cancelar su reserva restituyendo la vacante. |

Adicionales para Aprobación:

| Req      | Detalle                                                                                                                                                                                                                                                                                                                                               |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CRUD     | 1. CRUD Socio<br>2. CRUD Plan de Membresía<br>3. CRUD Instructor<br>4. CRUD Ejercicio<br>5. CRUD Horario y Sesión de Clase {depende de} CRUD Instructor<br>6. CRUD Membresía {depende de} CRUD Socio y CRUD Plan de Membresía<br>7. CRUD Rutina {depende de} CRUD Instructor y CRUD Ejercicio                                                         |
| CUU/Epic | 1. Registrar nuevo socio y asignarle un plan de membresía<br>2. Reserva y cancelación de cupo en clases por parte del socio con control de cupo en tiempo real<br>3. Crear y gestionar rutinas de catálogo con ejercicios parametrizados por parte del instructor<br>4. Registrar pago de membresía y renovar automáticamente la fecha de vencimiento |

### Alcance Adicional Voluntario

| Req      | Detalle                                                                                                                                                                                |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Listados | 1. Listado de actividades del día, muestra horarios, descripción, instructores, socios inscriptos y cupo restante<br>2. Socios con membresía próxima a vencer (en los próximos 7 días) |
| Otros    | 1. Integración con pasarela de pago externa (Mercado Pago / Stripe)                                                                                                                    |
