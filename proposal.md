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

Sistema de gestión para un gimnasio que permite administrar socios, membresías,
rutinas e instructores. Los instructores pueden crear rutinas de entrenamiento
y asignarlas a los socios. Los socios pueden consultar el estado de su membresía
y acceder a rutinas de entrenamiento que les fueron asignadas por los instructores.
El personal administrativo gestiona altas, planes y pagos.

### Diagrama de clases

```mermaid
classDiagram

class Member {
  +int id
  +string name
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
  +float amountPaid
}

class Classes {
  +int id
  +string name
  +string description
  +int maxCapacity
  +int durationMinutes
}

class Instructor {
  +int id
  +string name
  +string specialty
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
}

class RoutineExercise {
  +int sets
  +int repetitions
  +string notes
  +int order
}

class Booking {
  +int id
  +Date date
  +string startTime
  +string endTime
}

%% RELATIONSHIPS

Exercise "1" --> "0..*" RoutineExercise : appears in

Member "1" --> "0..*" Membership : has
Membership "1" --> "1" MembershipPlan : corresponds to

Member "1" --> "0..*" Booking : books
Booking "0..*" --> "1" Activity : for

Instructor "1" --> "0..*" Activity : teaches

Member "1" --> "0..*" Routine : follows
Routine "1" --> "1..*" RoutineExercise : contains

Instructor "1" --> "0..*" Routine : creates
Instructor "1" --> "0..*" Exercise : creates
```

## Alcance Funcional

### Alcance Mínimo

Regularidad:

| Req               | Detalle                                                                                                                                                                                                                                                                                    |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CRUD simple       | 1. CRUD Socio<br>2. CRUD Plan de Membresía<br>3. CRUD Instructor<br>4. CRUD Ejercicio                                                                                                                                                                                                      |
| CRUD dependiente  | 1. CRUD Membresía {depende de} CRUD Socio y CRUD Plan de Membresía<br>2. CRUD Rutina {depende de} CRUD Ejercicio                                                                                                                                                                           |
| Listado + detalle | 1. Listado de socios filtrado por estado de membresía (activo/vencido) y/o nombre, muestra nombre, DNI y estado => detalle muestra datos del socio, membresía vigente y rutinas asignadas<br>2. Listado de Rutinas filtrado por nivel => detalle muestra datos completos de los ejercicios |
| CUU/Epic          | 1. Registrar nuevo socio y asignarle un plan de membresía<br>2. Solicitar y asignar una rutina de entrenamiento: el socio la solicita y el instructor la arma asignándole ejercicios                                                                                                       |

Adicionales para Aprobación:

| Req      | Detalle                                                                                                                                                                                                                                                                                                        |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CRUD     | 1. CRUD Socio<br>2. CRUD Plan de Membresía<br>3. CRUD Instructor<br>4. CRUD Ejercicio<br>5. CRUD Membresía {depende de} CRUD Socio y CRUD Plan de Membresía<br>6. CRUD Rutina {depende de} CRUD Ejercicio<br>7. CRUD Ejercicio<br>8. CRUD Rutina {depende de} CRUD Socio, CRUD Instructor y CRUD Ejercicio<br> |
| CUU/Epic | 1. Registrar nuevo socio y asignarle un plan de membresía<br>2. Solicitar y asignar una rutina de entrenamiento: el socio la solicita y el instructor la arma asignándole ejercicios<br>3. Registrar una nueva rutina con ejercicios<br>4. Registrar pago de membresía y renovar vencimiento                   |

### Alcance Adicional Voluntario

| Req      | Detalle                                                                                                                                                                                |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Listados | 1. Listado de actividades del dia, muestra horarios, descripcion, instructores, socios inscriptos y cupo restante<br>2. Socios con membresía próxima a vencer (en los próximos 7 días) |
| CUU/Epic | 1. Registrar reserva de cupo para un socio en una actividad<br>2. Cancelar reserva de cupo para un socio en una actividad                                                              |
| Otros    | 1. Integración con sistema de pago                                                                                                                                                     |
