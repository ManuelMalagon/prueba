# prueba

```mermaid
erDiagram
    TRABAJADOR {
        int id_trabajador PK
        string nombre
        string apellidos
        string dni UK
        date fecha_nacimiento
        string direccion
        date fecha_alta
    }
    ADMINISTRATIVO {
        int id_trabajador PK, FK
    }
    MONITOR {
        int id_trabajador PK, FK
    }
    VETERINARIO {
        int id_trabajador PK, FK
        string num_colegiado UK
    }
    MONITOR_DISPONIBILIDAD {
        int id_monitor PK, FK
        string dia_semana PK "CHECK lunes a viernes"
    }
    RECINTO {
        int id_recinto PK
        string nombre
        string ubicacion
        int cap_maxima
        string tipo_animal
        boolean es_hospital
    }
    ANIMAL {
        int id_animal PK
        string codigo_registro UK "CHAR(15)"
        string especie
        string raza "nullable"
        string nombre
        int edad
        string estado_salud "SANO o REQUIERE_ATENCION"
        date fecha_fallecimiento "nullable"
        int id_recinto FK
    }
    HISTORIAL_CLINICO {
        int id_historial PK
        int id_animal FK, UK
        int id_veterinario FK
    }
    INGRESO {
        int id_ingreso PK
        int id_historial FK
        int id_recinto_origen FK
        date fecha_ingreso
        date fecha_salida "nullable"
        string medicacion
    }
    ADOPTANTE {
        int id_adoptante PK
        string dni UK
        string nombre
        string apellidos
        string direccion
        date fecha_nacimiento
        string telefono
    }
    ADOPCION {
        int id_adopcion PK
        int id_animal FK
        int id_adoptante FK
        int id_administrativo FK
        date fecha_adopcion
        boolean activa
    }
    CENTRO_EDUCATIVO {
        string codigo_centro PK "CHAR(8)"
        string nombre
        string direccion
        string profesor_nombre
        string profesor_apellidos
        string profesor_email
    }
    SOLICITUD_VISITA {
        int id_solicitud PK
        string codigo_centro FK
        int num_estudiantes
        string nivel_educativo "INFANTIL, PRIMARIA, SECUNDARIA"
        string estado "PENDIENTE, ASIGNADA, FINALIZADA"
    }
    SOLICITUD_DIAS {
        int id_solicitud PK, FK
        string dia_semana PK
    }
    ASIGNACION_VISITA {
        int id_asignacion PK
        int id_solicitud FK, UK
        int id_monitor FK
        string dia_asignado
    }

    TRABAJADOR ||--o| ADMINISTRATIVO : "es"
    TRABAJADOR ||--o| MONITOR : "es"
    TRABAJADOR ||--o| VETERINARIO : "es"
    MONITOR ||--o{ MONITOR_DISPONIBILIDAD : "tiene disponibilidad"
    RECINTO ||--o{ ANIMAL : "aloja"
    ANIMAL ||--o| HISTORIAL_CLINICO : "posee"
    VETERINARIO ||--o{ HISTORIAL_CLINICO : "es responsable de"
    HISTORIAL_CLINICO ||--o{ INGRESO : "registra"
    RECINTO ||--o{ INGRESO : "es recinto origen de"
    ANIMAL ||--o{ ADOPCION : "participa en"
    ADOPTANTE ||--o{ ADOPCION : "realiza"
    ADMINISTRATIVO ||--o{ ADOPCION : "gestiona"
    CENTRO_EDUCATIVO ||--o{ SOLICITUD_VISITA : "solicita"
    SOLICITUD_VISITA ||--|{ SOLICITUD_DIAS : "prefiere"
    SOLICITUD_VISITA ||--o| ASIGNACION_VISITA : "recibe"
    MONITOR ||--o{ ASIGNACION_VISITA : "ejecuta"
```

