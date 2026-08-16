                CYCLIC
                   │
                   ▼
          Calcular U_i = C_i/T_i
                   │
                   ▼
              Calcular H
             H = MCM(Ti)
                   │
                   ▼
              Calcular TS
             TS = MCD(Ti)
                   │
                   ▼
        ¿Cada tarea entra en TS?
             C_i ≤ TS
              /    \
            NO      SÍ
            │        │
            ▼        ▼
         FALLA    seguir test
                     │
                     ▼
             construir Gantt




              RATE MONOTONIC
                     │
                     ▼
             Calcular U_i
                     │
                     ▼
            Asignar prioridades
          menor T → mayor prioridad
                     │
                     ▼
        Test de utilización de RM
                     │
              ┌──────┴──────┐
             OK             NO
              │               │
              ▼               ▼
          Planificable    Test de
                         tiempo de respuesta
                               │
                               ▼
                         ¿R ≤ D?
