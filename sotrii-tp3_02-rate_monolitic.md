#  Parte 1 : Ánalisis de los sistemas
## Sistema 1 – Rate Monotonic

### Datos

| Tarea |  C | T = D | Prioridad |
| ----- | -: | ----: | --------: |
| T1    |  1 |     4 |         1 |
| T2    |  2 |     5 |         2 |
| T3    |  5 |    20 |         3 |

En Rate Monotonic, la prioridad se asigna según el período de la tarea: **a menor período, mayor prioridad**.

Por lo tanto:

```text
T1 > T2 > T3
```

### Factor de utilización

El factor de utilización de cada tarea es:

```math
U_i = \frac{C_i}{T_i}
```

```math
U_1 = \frac{1}{4} = 0,25
```

```math
U_2 = \frac{2}{5} = 0,40
```

```math
U_3 = \frac{5}{20} = 0,25
```

Por lo tanto:

```math
U = 0,25 + 0,40 + 0,25 = 0,90
```

```math
U = 90\%
```

### Hiperperíodo

El hiperperíodo se obtiene como el mínimo común múltiplo de los períodos:

```math
H = MCM(4,5,20)
```

```math
H = 20
```

### Período secundario

El período secundario corresponde al Cyclic Scheduling. Para Rate Monotonic **no se utiliza como parámetro de planificación**, ya que el planificador trabaja mediante prioridades.

Por lo tanto:

```text
Período secundario: no aplica
```

---

### Test de Garantía

#### 1. Prioridades

Las prioridades se asignan según el período:

* T1: `T = 4` → prioridad 1
* T2: `T = 5` → prioridad 2
* T3: `T = 20` → prioridad 3

Por lo tanto:

```text
T1 > T2 > T3
```

#### 2. Factor de utilización

```math
U = 0,90 < 1
```

**Condición de carga: CUMPLE.**

El factor de carga total es menor al 100%.

#### 3. Test de utilización de Rate Monotonic

Para `n = 3` tareas, el límite suficiente de utilización de Rate Monotonic es:

```math
U_{RM} = n(2^{1/n}-1)
```

```math
U_{RM} = 3(2^{1/3}-1)
```

```math
U_{RM} \approx 0,780
```

El sistema tiene:

```math
U = 0,90
```

Por lo tanto:

```math
0,90 > 0,780
```

El sistema **no cumple el test suficiente de utilización de Rate Monotonic**.

Esto no significa necesariamente que el sistema sea imposible de planificar. El test de utilización es una condición suficiente, no necesaria.

#### 4. Análisis de tiempos de respuesta

Para verificar si las tareas cumplen sus deadlines, se analiza el peor tiempo de respuesta considerando las tareas de mayor prioridad.

##### T1

Como T1 tiene la mayor prioridad:

```math
R_1 = C_1
```

```math
R_1 = 1
```

Comparando con su deadline:

```math
1 \leq 4
```

→ ✅

**T1 cumple.**

##### T2

Para T2 se considera la interferencia de T1:

```math
R_2 = C_2 + \left\lceil\frac{R_2}{T_1}\right\rceil C_1
```

Iterando:

```math
R_2^{(0)} = 2
```

```math
R_2^{(1)} = 2 + \left\lceil\frac{2}{4}\right\rceil 1 = 3
```

```math
R_2^{(2)} = 2 + \left\lceil\frac{3}{4}\right\rceil 1 = 3
```

Por lo tanto:

```math
R_2 = 3
```

Comparando con su deadline:

```math
3 \leq 5
```

→ ✅

**T2 cumple.**

##### T3

Para T3 se considera la interferencia de T1 y T2:

```math
R_3 = C_3 +
\left\lceil\frac{R_3}{T_1}\right\rceil C_1 +
\left\lceil\frac{R_3}{T_2}\right\rceil C_2
```

Iterando:

```math
R_3^{(0)} = 5
```

```math
R_3^{(1)} =
5 +
\left\lceil\frac{5}{4}\right\rceil 1 +
\left\lceil\frac{5}{5}\right\rceil 2
= 8
```

```math
R_3^{(2)} =
5 +
\left\lceil\frac{8}{4}\right\rceil 1 +
\left\lceil\frac{8}{5}\right\rceil 2
= 9
```

```math
R_3^{(3)} =
5 +
\left\lceil\frac{9}{4}\right\rceil 1 +
\left\lceil\frac{9}{5}\right\rceil 2
= 12
```

```math
R_3^{(4)} =
5 +
\left\lceil\frac{12}{4}\right\rceil 1 +
\left\lceil\frac{12}{5}\right\rceil 2
= 14
```

```math
R_3^{(5)} =
5 +
\left\lceil\frac{14}{4}\right\rceil 1 +
\left\lceil\frac{14}{5}\right\rceil 2
= 15
```

```math
R_3^{(6)} =
5 +
\left\lceil\frac{15}{4}\right\rceil 1 +
\left\lceil\frac{15}{5}\right\rceil 2
= 15
```

Como se alcanza un punto fijo:

```math
R_3 = 15
```

Comparando con su deadline:

```math
15 \leq 20
```

→ ✅

**T3 cumple.**

---

### Resumen

| Tarea | Prioridad |  C |  T | Tiempo de respuesta | Deadline | Resultado |
| ----- | --------: | -: | -: | ------------------: | -------: | --------- |
| T1    |         1 |  1 |  4 |                   1 |        4 | Cumple    |
| T2    |         2 |  2 |  5 |                   3 |        5 | Cumple    |
| T3    |         3 |  5 | 20 |                  15 |       20 | Cumple    |

### Conclusión

El Sistema 1 presenta un factor de utilización de:

```math
U = 90\%
```

El test suficiente de utilización de Rate Monotonic no se cumple:

```math
0,90 > 0,780
```

Sin embargo, mediante el análisis de tiempos de respuesta se obtiene:

```math
R_1 = 1 \leq 4
```

```math
R_2 = 3 \leq 5
```

```math
R_3 = 15 \leq 20
```

Por lo tanto, **las tres tareas cumplen sus respectivos deadlines y el sistema es planificable mediante Rate Monotonic**.

El hiperperíodo del sistema es:

```math
H = 20
```
### Diagrama de Gantt

El hiperperíodo del sistema es:

```math
H = MCM(4,5,20) = 20
```

Por lo tanto, se representa la planificación entre `t = 0` y `t = 20`.

Las prioridades son:

```text
T1 > T2 > T3
```

En cada instante se ejecuta la tarea de mayor prioridad que se encuentre lista. Si se activa una tarea de mayor prioridad mientras se está ejecutando una de menor prioridad, esta última es interrumpida.

El diagrama de Gantt para un hiperperíodo es:

```text
Tiempo:  0    1    3    4    5    6    8   10   11   12   14   15   16   17        20
         |----|----|----|----|----|----|----|----|----|----|----|----|----|----------|
Tarea:   | T1 | T2 | T3 | T1 | T3 | T2 | T3 | T1 | T3 | T2 | T3 | T1 | T3 |   Idle   |
```

La tarea T3 comienza su ejecución en `t = 3`, pero es interrumpida por T1 cuando esta se activa en `t = 4`. Luego T3 continúa su ejecución una vez que finalizan las tareas de mayor prioridad.

Dentro del hiperperíodo se completan todas las ejecuciones correspondientes a las activaciones de las tres tareas, sin superar sus respectivos deadlines.

Por lo tanto, el diagrama de Gantt confirma la planificación obtenida mediante Rate Monotonic para el Sistema 1.
---

## Sistema 2 – Rate Monotonic

### Datos

| Tarea | C | T = D | Prioridad |
| ----- | -: | ----: | --------: |
| T1    | 1 |     6 | 1 |
| T2    | 2 |    10 | 2 |
| T3    | 2 |    18 | 3 |

En Rate Monotonic,  **a menor período, mayor prioridad**.

Por lo tanto:

```text
T1 > T2 > T3
````

### Factor de utilización

El factor de utilización de cada tarea es:

```math
U_i = \frac{C_i}{T_i}
```

```math
U_1 = \frac{1}{6} = 0,167
```

```math
U_2 = \frac{2}{10} = 0,20
```

```math
U_3 = \frac{2}{18} = 0,111
```

Por lo tanto:

```math
U = 0,167 + 0,20 + 0,111 = 0,478
```

```math
U \approx 47,8\%
```

### Hiperperíodo

El hiperperíodo se obtiene como el mínimo común múltiplo de los períodos:

```math
H = MCM(6,10,18)
```

```math
H = 90
```

### Período secundario

El período secundario corresponde al Cyclic Scheduling. Para Rate Monotonic **no se utiliza como parámetro de planificación**, ya que el planificador trabaja mediante prioridades.

Por lo tanto:

```text
Período secundario: no aplica
```

---

### Test de Garantía

#### 1. Prioridades

Las prioridades se asignan según el período:

* T1: `T = 6` → prioridad 1
* T2: `T = 10` → prioridad 2
* T3: `T = 18` → prioridad 3

Por lo tanto:

```text
T1 > T2 > T3
```

#### 2. Factor de utilización

```math
U = 0,478 < 1
```

**Condición de carga: CUMPLE.**

El factor de carga total es menor al 100%.

#### 3. Test de utilización de Rate Monotonic

Para `n = 3` tareas, el límite suficiente de utilización de Rate Monotonic es:

```math
U_{RM} = n(2^{1/n}-1)
```

```math
U_{RM} = 3(2^{1/3}-1)
```

```math
U_{RM} \approx 0,780
```

El sistema tiene:

```math
U = 0,478
```

Por lo tanto:

```math
0,478 < 0,780
```

**Test de utilización: CUMPLE.**

Al cumplirse el límite suficiente de utilización, el sistema es planificable mediante Rate Monotonic.

---

### Análisis de tiempos de respuesta

#### T1

Como T1 tiene la mayor prioridad:

```math
R_1 = C_1
```

```math
R_1 = 1
```

Comparando con su deadline:

```math
1 \leq 6
```

→ ✅

**T1 cumple.**

#### T2

Para T2 se considera la interferencia de T1:

```math
R_2 =
C_2 +
\left\lceil\frac{R_2}{T_1}\right\rceil C_1
```

Iterando:

```math
R_2^{(0)} = 2
```

```math
R_2^{(1)}
= 2 + \left\lceil\frac{2}{6}\right\rceil 1
= 3
```

```math
R_2^{(2)}
= 2 + \left\lceil\frac{3}{6}\right\rceil 1
= 3
```

Por lo tanto:

```math
R_2 = 3
```

Comparando con su deadline:

```math
3 \leq 10
```

→ ✅

**T2 cumple.**

#### T3

Para T3 se considera la interferencia de T1 y T2:

```math
R_3 =
C_3 +
\left\lceil\frac{R_3}{T_1}\right\rceil C_1 +
\left\lceil\frac{R_3}{T_2}\right\rceil C_2
```

Iterando:

```math
R_3^{(0)} = 2
```

```math
R_3^{(1)}
= 2 +
\left\lceil\frac{2}{6}\right\rceil 1 +
\left\lceil\frac{2}{10}\right\rceil 2
= 5
```

```math
R_3^{(2)}
= 2 +
\left\lceil\frac{5}{6}\right\rceil 1 +
\left\lceil\frac{5}{10}\right\rceil 2
= 5
```

Por lo tanto:

```math
R_3 = 5
```

Comparando con su deadline:

```math
5 \leq 18
```

→ ✅

**T3 cumple.**

---

### Resumen

| Tarea | Prioridad |  C |  T | Tiempo de respuesta | Deadline | Resultado |
| ----- | --------: | -: | -: | ------------------: | -------: | --------- |
| T1    |         1 |  1 |  6 |                   1 |        6 | Cumple    |
| T2    |         2 |  2 | 10 |                   3 |       10 | Cumple    |
| T3    |         3 |  2 | 18 |                   5 |       18 | Cumple    |

### Conclusión

El Sistema 2 presenta un factor de utilización de:

```math
U \approx 47,8\%
```

El test suficiente de utilización de Rate Monotonic se cumple:

```math
0,478 < 0,780
```

Además, el análisis de tiempos de respuesta confirma que todas las tareas cumplen sus deadlines:

```math
R_1 = 1 \leq 6
```

```math
R_2 = 3 \leq 10
```

```math
R_3 = 5 \leq 18
```

Por lo tanto, **el Sistema 2 es planificable mediante Rate Monotonic**.

El hiperperíodo del sistema es:

```math
H = 90
```

---

### Diagrama de Gantt

El hiperperíodo del sistema es:

```math
H = MCM(6,10,18) = 90
```

Las prioridades son:

```text
T1 > T2 > T3
```

Para visualizar la planificación, se representa el comienzo del hiperperíodo:

```text
Tiempo:  0    1    3    6    7    9   10   12   13   18   19   20   22   24   25   30
         |----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|
Tarea:   | T1 | T2 | T3 | T1 | T2 |Idle| T1 | T3 |Idle| T1 | T2 | T3 | T1 | T2 |Idle| ... |
```

#### Detalle de la planificación

En `t = 0` se activan las tres tareas. Se ejecuta primero T1 por tener la mayor prioridad:

```math
0 \rightarrow 1 : T1
```

Luego se ejecuta T2:

```math
1 \rightarrow 3 : T2
```

y posteriormente T3:

```math
3 \rightarrow 5 : T3
```

En `t = 6` se activa nuevamente T1:

```math
6 \rightarrow 7 : T1
```

Luego T2:

```math
7 \rightarrow 9 : T2
```

Entre `t = 9` y `t = 10` no hay tareas listas:

```math
9 \rightarrow 10 : Idle
```

En `t = 10` se activa T1 y luego T3:

```math
10 \rightarrow 11 : T1
```

```math
11 \rightarrow 13 : T3
```

Entre `t = 13` y `t = 18` el procesador queda libre.

En `t = 18` se activa nuevamente T1:

```math
18 \rightarrow 19 : T1
```

Luego T2:

```math
19 \rightarrow 21 : T2
```

y T3:

```math
21 \rightarrow 23 : T3
```

La misma lógica continúa durante el resto del hiperperíodo.

#### Resultado del Gantt

El Gantt muestra que el planificador ejecuta siempre la tarea de mayor prioridad que se encuentra lista:

```text
T1 > T2 > T3
```

Las tareas pueden ser interrumpidas por tareas de mayor prioridad cuando estas se activan.

De acuerdo con el análisis de tiempos de respuesta, todas las tareas cumplen sus respectivos deadlines.

Por lo tanto, **el Sistema 2 puede ser planificado mediante Rate Monotonic**.



---

## Sistema 3 – Rate Monotonic

### Datos

| Tarea |  C | T = D | Prioridad |
| ----- | -: | ----: | --------: |
| T1    |  1 |     8 |         1 |
| T2    |  3 |    15 |         2 |
| T3    |  4 |    20 |         3 |
| T4    |  6 |    22 |         4 |

En Rate Monotonic, la prioridad se asigna según el período de la tarea: **a menor período, mayor prioridad**.

Por lo tanto:

```text
T1 > T2 > T3 > T4
```

### Factor de utilización

El factor de utilización de cada tarea es:

```math
U_i = \frac{C_i}{T_i}
```

```math
U_1 = \frac{1}{8} = 0,125
```

```math
U_2 = \frac{3}{15} = 0,20
```

```math
U_3 = \frac{4}{20} = 0,20
```

```math
U_4 = \frac{6}{22} = 0,273
```

Por lo tanto:

```math
U = 0,125 + 0,20 + 0,20 + 0,273 = 0,798
```

```math
U \approx 79,8\%
```

### Hiperperíodo

El hiperperíodo se obtiene como el mínimo común múltiplo de los períodos:

```math
H = MCM(8,15,20,22)
```

```math
H = 1320
```

### Período secundario

El período secundario corresponde al Cyclic Scheduling. Para Rate Monotonic **no se utiliza como parámetro de planificación**, ya que el planificador trabaja mediante prioridades.

Por lo tanto:

```text
Período secundario: no aplica
```

---

## Test de Garantía

### 1. Prioridades

Las prioridades se asignan según el período:

* T1: `T = 8` → prioridad 1
* T2: `T = 15` → prioridad 2
* T3: `T = 20` → prioridad 3
* T4: `T = 22` → prioridad 4

Por lo tanto:

```text
T1 > T2 > T3 > T4
```

### 2. Factor de utilización

```math
U = 0,798 < 1
```

**Condición de carga: CUMPLE.**

El factor de carga total es menor al 100%.

### 3. Test de utilización de Rate Monotonic

Para `n = 4` tareas, el límite suficiente de utilización de Rate Monotonic es:

```math
U_{RM} = n(2^{1/n}-1)
```

```math
U_{RM} = 4(2^{1/4}-1)
```

```math
U_{RM} \approx 0,757
```

El sistema tiene:

```math
U = 0,798
```

Por lo tanto:

```math
0,798 > 0,757
```

**Test de utilización: NO CUMPLE.**

Esto no permite concluir por sí solo que el sistema sea imposible de planificar, por lo que se realiza el análisis de tiempos de respuesta.

---

## Análisis de tiempos de respuesta

### T1

Como T1 tiene la mayor prioridad:

```math
R_1 = C_1
```

```math
R_1 = 1
```

Comparando con su deadline:

```math
1 \leq 8
```

→ ✅

**T1 cumple.**

### T2

Para T2 se considera la interferencia de T1:

```math
R_2 =
C_2 +
\left\lceil\frac{R_2}{T_1}\right\rceil C_1
```

Iterando:

```math
R_2^{(0)} = 3
```

```math
R_2^{(1)}
= 3 + \left\lceil\frac{3}{8}\right\rceil 1
= 4
```

```math
R_2^{(2)}
= 3 + \left\lceil\frac{4}{8}\right\rceil 1
= 4
```

Por lo tanto:

```math
R_2 = 4
```

Comparando con su deadline:

```math
4 \leq 15
```

→ ✅

**T2 cumple.**

### T3

Para T3 se considera la interferencia de T1 y T2:

```math
R_3 =
C_3 +
\left\lceil\frac{R_3}{T_1}\right\rceil C_1 +
\left\lceil\frac{R_3}{T_2}\right\rceil C_2
```

Iterando:

```math
R_3^{(0)} = 4
```

```math
R_3^{(1)}
= 4 +
\left\lceil\frac{4}{8}\right\rceil 1 +
\left\lceil\frac{4}{15}\right\rceil 3
= 8
```

```math
R_3^{(2)}
= 4 +
\left\lceil\frac{8}{8}\right\rceil 1 +
\left\lceil\frac{8}{15}\right\rceil 3
= 8
```

Por lo tanto:

```math
R_3 = 8
```

Comparando con su deadline:

```math
8 \leq 20
```

→ ✅

**T3 cumple.**

### T4

Para T4 se considera la interferencia de T1, T2 y T3:

```math
R_4 =
C_4 +
\left\lceil\frac{R_4}{T_1}\right\rceil C_1 +
\left\lceil\frac{R_4}{T_2}\right\rceil C_2 +
\left\lceil\frac{R_4}{T_3}\right\rceil C_3
```

Iterando:

```math
R_4^{(0)} = 6
```

```math
R_4^{(1)}
= 6 +
\left\lceil\frac{6}{8}\right\rceil 1 +
\left\lceil\frac{6}{15}\right\rceil 3 +
\left\lceil\frac{6}{20}\right\rceil 4
= 14
```

```math
R_4^{(2)}
= 6 +
\left\lceil\frac{14}{8}\right\rceil 1 +
\left\lceil\frac{14}{15}\right\rceil 3 +
\left\lceil\frac{14}{20}\right\rceil 4
= 15
```

```math
R_4^{(3)}
= 6 +
\left\lceil\frac{15}{8}\right\rceil 1 +
\left\lceil\frac{15}{15}\right\rceil 3 +
\left\lceil\frac{15}{20}\right\rceil 4
= 15
```

Por lo tanto:

```math
R_4 = 15
```

Comparando con su deadline:

```math
15 \leq 22
```

→ ✅

**T4 cumple.**

---

## Resumen

| Tarea | Prioridad |  C |  T | Tiempo de respuesta | Deadline | Resultado |
| ----- | --------: | -: | -: | ------------------: | -------: | --------- |
| T1    |         1 |  1 |  8 |                   1 |        8 | Cumple    |
| T2    |         2 |  3 | 15 |                   4 |       15 | Cumple    |
| T3    |         3 |  4 | 20 |                   8 |       20 | Cumple    |
| T4    |         4 |  6 | 22 |                  15 |       22 | Cumple    |

### Conclusión

El Sistema 3 presenta un factor de utilización de:

```math
U \approx 79,8\%
```

El test suficiente de utilización de Rate Monotonic **no se cumple**:

```math
0,798 > 0,757
```

Sin embargo, el análisis de tiempos de respuesta muestra que todas las tareas cumplen sus respectivos deadlines:

```math
R_1 = 1 \leq 8
```

```math
R_2 = 4 \leq 15
```

```math
R_3 = 8 \leq 20
```

```math
R_4 = 15 \leq 22
```

Por lo tanto, **el Sistema 3 es planificable mediante Rate Monotonic**, a pesar de no cumplir el test suficiente de utilización.

El hiperperíodo del sistema es:

```math
H = 1320
```
## Diagrama de Gantt

El hiperperíodo del sistema es:

```math
H = MCM(8,15,20,22) = 1320
````
Las prioridades según Rate Monotonic son:

```text
T1 > T2 > T3 > T4
```

En cada instante se ejecuta la tarea de mayor prioridad que se encuentre lista. Si durante la ejecución de una tarea se activa otra de mayor prioridad, la tarea de menor prioridad es interrumpida.

Para visualizar la planificación, se representa el comienzo del hiperperíodo hasta `t = 80`.

```text
Tiempo:  0    1    4    8    9   15   16   17   19   20   24   25   30   32   33   34   35   40   41   45   48   49   55   56   57   60   63   64   65   68   72   80
         |----|----|----|----|------|----|----|----|----|----|----|-----|----|----|----|----|-----|----|----|----|----|-----|----|----|----|----|----|----|----|----|--------|
Tarea:   | T1 | T2 | T3 | T1 |  T4  | T2 | T1 | T2 |Idle| T3 | T1 | T4  | T2 | T1 | T2 | T4 |Idle | T1 | T3 | T2 | T1 | T4  |Idle| T1 |Idle| T2 | T3 | T1 | T3 | T4 | Idle   |
```

### Detalle de la planificación

En `t = 0` se activan las cuatro tareas. Se ejecuta primero T1 por tener la mayor prioridad:

```math
0 \rightarrow 1 : T1
```

Luego se ejecuta T2:

```math
1 \rightarrow 4 : T2
```

y posteriormente T3:

```math
4 \rightarrow 8 : T3
```

En `t = 8` se activa nuevamente T1, por lo que T3 ya finalizó su ejecución y se ejecuta T1:

```math
8 \rightarrow 9 : T1
```

Luego T4 utiliza el procesador:

```math
9 \rightarrow 15 : T4
```

En `t = 15` se activa T2:

```math
15 \rightarrow 16 : T2
```

En `t = 16` se activa T1:

```math
16 \rightarrow 17 : T1
```

T2 continúa:

```math
17 \rightarrow 19 : T2
```

Entre `t = 19` y `t = 20` no hay ninguna tarea lista:

```math
19 \rightarrow 20 : Idle
```

En `t = 20` se activa T3:

```math
20 \rightarrow 24 : T3
```

En `t = 24` se activa T1:

```math
24 \rightarrow 25 : T1
```

Luego T4 continúa su ejecución:

```math
25 \rightarrow 30 : T4
```

En `t = 30` se activa T2:

```math
30 \rightarrow 32 : T2
```

En `t = 32` se activa T1:

```math
32 \rightarrow 33 : T1
```

T2 continúa:

```math
33 \rightarrow 34 : T2
```

y luego T4:

```math
34 \rightarrow 35 : T4
```

Entre `t = 35` y `t = 40` el procesador queda libre:

```math
35 \rightarrow 40 : Idle
```

En `t = 40` se activa T1:

```math
40 \rightarrow 41 : T1
```

Luego se ejecuta T3:

```math
41 \rightarrow 45 : T3
```

En `t = 45` se activa T2:

```math
45 \rightarrow 48 : T2
```

En `t = 48` se activa T1:

```math
48 \rightarrow 49 : T1
```

Luego se ejecuta T4:

```math
49 \rightarrow 55 : T4
```

Entre `t = 55` y `t = 56` no hay tareas listas:

```math
55 \rightarrow 56 : Idle
```

En `t = 56` se ejecuta T1:

```math
56 \rightarrow 57 : T1
```

Entre `t = 57` y `t = 60` el procesador queda libre:

```math
57 \rightarrow 60 : Idle
```

En `t = 60` se activa T2:

```math
60 \rightarrow 63 : T2
```

T3 se ejecuta parcialmente:

```math
63 \rightarrow 64 : T3
```

En `t = 64` se activa T1, que tiene mayor prioridad:

```math
64 \rightarrow 65 : T1
```

Luego T3 continúa:

```math
65 \rightarrow 68 : T3
```

Finalmente se ejecuta T4:

```math
68 \rightarrow 72 : T4
```

Desde `t = 72` hasta `t = 80` no hay tareas pendientes:

```math
72 \rightarrow 80 : Idle
```

### Resultado del Gantt

El Gantt muestra que Rate Monotonic permite interrumpir una tarea de menor prioridad cuando se activa una tarea de mayor prioridad.

Por ejemplo, T3 comienza en:

```math
t = 63
```

pero es interrumpida en:

```math
t = 64
```

por la activación de T1. Luego T3 continúa en:

```math
t = 65
```

hasta completar su ejecución.

La planificación respeta las prioridades:

```text
T1 > T2 > T3 > T4
```

y, de acuerdo con el análisis de tiempos de respuesta, todas las tareas cumplen sus respectivos deadlines.

Por lo tanto, **el Sistema 3 es planificable mediante Rate Monotonic**.

---

