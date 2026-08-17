#  Análisis de los sitemas

## Sistema 1 – Cyclic Scheduling

### Datos del sistema

| Tarea | C (WCET) | T (Período) | D (Deadline) |
| ----- | -------: | ----------: | -----------: |
| T1    |        1 |           4 |            4 |
| T2    |        2 |           5 |            5 |
| T3    |        5 |          20 |           20 |

En una planificación cíclica, el sistema se organiza mediante un calendario estático de ejecución. El período secundario se utiliza como unidad de planificación y las tareas deben poder ejecutarse respetando las restricciones temporales del sistema.

---

### 1. Factor de utilización

El factor de utilización de cada tarea se calcula como:

[
U_i = \frac{C_i}{T_i}
]

Por lo tanto:

**T1:**

[
U_1 = \frac{1}{4} = 0,25
]

**T2:**

[
U_2 = \frac{2}{5} = 0,40
]

**T3:**

[
U_3 = \frac{5}{20} = 0,25
]

El factor de utilización total es:

[
U = U_1 + U_2 + U_3
]

[
U = 0,25 + 0,40 + 0,25 = 0,90
]

Por lo tanto:

[
\boxed{U=0,90=90%}
]

El sistema utiliza el 90 % del tiempo disponible de CPU.

---

### 2. Hiperperíodo

El hiperperíodo es el mínimo común múltiplo de los períodos:

[
H = MCM(T_1,T_2,T_3)
]

[
H = MCM(4,5,20)
]

Como 20 es múltiplo de 4 y de 5:

[
\boxed{H=20}
]

Por lo tanto, el comportamiento global del sistema se repite cada 20 unidades de tiempo.

---

### 3. Período secundario

El período secundario se obtiene mediante el máximo común divisor de los períodos:

[
T_S = MCD(T_1,T_2,T_3)
]

[
T_S = MCD(4,5,20)
]

[
\boxed{T_S=1}
]

Por lo tanto, el ciclo secundario tiene una duración de 1 unidad de tiempo.

---

# Test de Garantía de Planificación Cíclica

Para determinar si el sistema puede ser planificado mediante Cyclic Scheduling se verifican las condiciones del test de garantía.

### Condición 1 – Cada tarea debe terminar en un único ciclo secundario

Para que una tarea pueda ejecutarse completamente dentro de un ciclo secundario debe cumplirse:

[
C_i \leq T_S
]

Como:

[
T_S=1
]

analizamos cada tarea.

**T1:**

[
C_1=1 \leq 1
]

Cumple.

**T2:**

[
C_2=2 \leq 1
]

No cumple.

**T3:**

[
C_3=5 \leq 1
]

No cumple.

Por lo tanto, existen tareas cuyo tiempo de ejecución es mayor que el período secundario.

[
\boxed{\text{Condición 1: NO CUMPLE}}
]

El sistema no puede ser planificado mediante Cyclic Scheduling con un período secundario de 1 unidad de tiempo.

---

### Condición 2 – Factor de utilización

El factor de utilización obtenido es:

[
U=0,90
]

Por lo tanto:

[
U<1
]

y la utilización total de CPU es menor al 100 %.

[
\boxed{\text{Condición 2: CUMPLE}}
]

Sin embargo, esta condición por sí sola no garantiza que exista una planificación cíclica válida. Es un chequeo de la carga total del procesador.

---

### Condición 3 – Hiperperíodo

El hiperperíodo calculado es:

[
H=20
]

El hiperperíodo permite representar un ciclo completo del comportamiento periódico del sistema, ya que:

[
\frac{H}{T_1}=\frac{20}{4}=5
]

[
\frac{H}{T_2}=\frac{20}{5}=4
]

[
\frac{H}{T_3}=\frac{20}{20}=1
]

Por lo tanto, dentro de un hiperperíodo se producen:

* 5 activaciones de T1
* 4 activaciones de T2
* 1 activación de T3

[
\boxed{\text{Condición 3: CUMPLE}}
]

---

### Condición 4 – Los períodos deben ser múltiplos enteros del período secundario

Debe cumplirse:

[
\frac{T_i}{T_S}\in\mathbb{N}
]

Como:

[
T_S=1
]

tenemos:

**T1:**

[
\frac{4}{1}=4
]

**T2:**

[
\frac{5}{1}=5
]

**T3:**

[
\frac{20}{1}=20
]

Todos los resultados son números enteros.

[
\boxed{\text{Condición 4: CUMPLE}}
]

---

### Condición 5 – Cada tarea debe terminar antes de su nueva activación

Para cada tarea debe cumplirse que su ejecución pueda completarse antes de la siguiente activación:

[
C_i \leq T_i
]

Analizamos:

**T1:**

[
1 \leq 4
]

Cumple.

**T2:**

[
2 \leq 5
]

Cumple.

**T3:**

[
5 \leq 20
]

Cumple.

Por lo tanto:

[
\boxed{\text{Condición 5: CUMPLE}}
]

---

## Resumen del Test de Garantía

| Condición                                          | Resultado   |
| -------------------------------------------------- | ----------- |
| 1. Cada tarea termina en un único ciclo secundario | ❌ No cumple |
| 2. Factor de utilización                           | ✅ Cumple    |
| 3. Hiperperíodo                                    | ✅ Cumple    |
| 4. Períodos múltiplos de TS                        | ✅ Cumple    |
| 5. Tareas terminan antes de una nueva activación   | ✅ Cumple    |

### Conclusión

El sistema tiene un factor de utilización del 90 %, por lo que la carga total de CPU es menor al 100 %. Sin embargo, **no puede garantizarse una planificación mediante Cyclic Scheduling**, debido a que el período secundario calculado es:

[
T_S=1
]

y las tareas T2 y T3 requieren tiempos de cómputo de 2 y 5 unidades de tiempo respectivamente:

[
C_2=2>T_S
]

[
C_3=5>T_S
]

Por lo tanto, no es posible ejecutar dichas tareas completamente dentro de un único ciclo secundario.

En consecuencia:

[
\boxed{\text{Sistema 1: NO PLANIFICABLE MEDIANTE CYCLIC SCHEDULING}}
]

No se puede construir un Diagrama de Gantt válido que cumpla todas las condiciones del test de garantía con estos parámetros.

---
## Sistema 2 – Cyclic Scheduling

### Datos

| Tarea |  C | T = D |
| ----- | -: | ----: |
| T1    |  1 |     6 |
| T2    |  2 |    10 |
| T3    |  2 |    18 |

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

```math
H = MCM(6,10,18) = 90
```

```math
H = 90
```

### Período secundario

```math
T_S = MCD(6,10,18) = 2
```

```math
T_S = 2
```

---

## Test de Garantía

### 1. Cada tarea debe terminar en un único ciclo secundario

Debe cumplirse:

```math
C_i \leq T_S
```

* T1: `1 ≤ 2` → ✅
* T2: `2 ≤ 2` → ✅
* T3: `2 ≤ 2` → ✅

**Condición 1: CUMPLE.**

### 2. Factor de utilización

```math
U = 0,478 < 1
```

**Condición 2: CUMPLE.**

### 3. Hiperperíodo

```math
H = 90
```

Dentro de un hiperperíodo:

```math
90/6 = 15
```

```math
90/10 = 9
```

```math
90/18 = 5
```

Todas las tareas se ejecutan un número entero de veces.

**Condición 3: CUMPLE.**

### 4. Los períodos deben ser múltiplos del período secundario

```math
6/2 = 3
```

```math
10/2 = 5
```

```math
18/2 = 9
```

Todos los resultados son enteros.

**Condición 4: CUMPLE.**

### 5. Cada tarea debe terminar antes de su próxima activación

Debe cumplirse:

```math
C_i \leq T_i
```

* T1: `1 ≤ 6` → ✅
* T2: `2 ≤ 10` → ✅
* T3: `2 ≤ 18` → ✅

**Condición 5: CUMPLE.**

---

## Resumen

| Condición                  | Resultado |
| -------------------------- | --------- |
| 1. `C_i ≤ T_S`             | Cumple    |
| 2. `U < 1`                 | Cumple    |
| 3. Hiperperíodo            | Cumple    |
| 4. `T_i` múltiplo de `T_S` | Cumple    |
| 5. `C_i ≤ T_i`             | Cumple    |

### Conclusión

El Sistema 2 cumple todas las condiciones del test de garantía para Cyclic Scheduling, por lo que es posible construir una planificación cíclica válida.

```math
\boxed{\text{Sistema 2: PLANIFICABLE MEDIANTE CYCLIC SCHEDULING}}
```

El hiperperíodo es de **90 unidades de tiempo** y el período secundario es de **2 unidades de tiempo**.

## Diagrama de Gantt

Para el Sistema 2 se obtuvo:

```math
H = 90
```

```math
T_S = 2
```

Por lo tanto, el hiperperíodo de 90 unidades de tiempo se divide en ciclos secundarios de 2 unidades.

En Cyclic Scheduling se construye un calendario estático, determinando previamente en qué intervalo se ejecutará cada instancia de cada tarea. Cada tarea debe ejecutarse completamente dentro de un único ciclo secundario.

Las tareas del sistema son:

| Tarea |  C |  T |  D |
| ----- | -: | -: | -: |
| T1    |  1 |  6 |  6 |
| T2    |  2 | 10 | 10 |
| T3    |  2 | 18 | 18 |

### Diagrama

```text
Tiempo
 0    2    4    6    8   10   12   14   16   18   20   22   24   26   28   30   32   34   36   38   40   42   44   46   48   50   52   54   56   58   60   62   64   66   68   70   72   74   76   78   80   82   84   86   88   90
 |----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|
 | T2 | T3 | T1 | ID | T2 | T1 | ID | ID | T3 | T2 | T1 | T1 | ID | T2 | T1 | T3 | T1 | T2 | T1 | ID | T1 | T2 | T3 | T1 | T1 | T2 | T1 | T1 | T2 | ID | ID | T1 | T2 | T1 | T1 | T2 | T3 | T1 | T1 | T2 | T1 | ID | ID | T1 |
```

Cada bloque del diagrama representa un ciclo secundario de:

```math
T_S = 2
```

Cuando una tarea tiene un tiempo de cómputo menor que el ciclo secundario, el tiempo restante queda disponible para otra tarea o permanece en estado `IDLE`.

Por ejemplo, T1 tiene:

```math
C_1 = 1 < T_S
```

por lo que utiliza solamente 1 unidad dentro de su ciclo secundario y queda 1 unidad disponible.

En cambio, T2 y T3 tienen:

```math
C_2 = C_3 = T_S = 2
```

por lo que ocupan un ciclo secundario completo.

### Verificación de las activaciones

Durante el hiperperíodo se deben ejecutar:

```math
\frac{H}{T_1} = \frac{90}{6} = 15
```

instancias de T1,

```math
\frac{H}{T_2} = \frac{90}{10} = 9
```

instancias de T2 y

```math
\frac{H}{T_3} = \frac{90}{18} = 5
```

instancias de T3.

En el diagrama se encuentran las 15 ejecuciones de T1, las 9 ejecuciones de T2 y las 5 ejecuciones de T3.

Cada instancia se ejecuta después de su activación y finaliza antes de su deadline.

Por ejemplo, la primera instancia de T1 se ejecuta entre 4 y 5:

```math
0 \leq 4 < 5 \leq 6
```

La primera instancia de T2 se ejecuta entre 0 y 2:

```math
0 \leq 0 < 2 \leq 10
```

La primera instancia de T3 se ejecuta entre 2 y 4:

```math
0 \leq 2 < 4 \leq 18
```

El mismo criterio se cumple para las restantes instancias durante todo el hiperperíodo.

### Conclusión

El Diagrama de Gantt permite verificar que todas las instancias de las tareas pueden ubicarse dentro del hiperperíodo de 90 unidades de tiempo, respetando sus períodos y deadlines.

---
## Sistema 3 – Cyclic Scheduling

### Datos

| Tarea |  C | T = D |
| ----- | -: | ----: |
| T1    |  1 |     8 |
| T2    |  3 |    15 |
| T3    |  4 |    20 |
| T4    |  6 |    22 |

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

Según las diapositivas, el período secundario se obtiene como el máximo común divisor de los períodos de las tareas.

```math
T_S = MCD(8,15,20,22)
```

```math
T_S = 1
```

---

## Test de Garantía

### 1. Cada tarea debe terminar en un único ciclo secundario

Debe cumplirse:

```math
C_i \leq T_S
```

Como:

```math
T_S = 1
```

tenemos:

* T1: `1 ≤ 1` → ✅
* T2: `3 ≤ 1` → ❌
* T3: `4 ≤ 1` → ❌
* T4: `6 ≤ 1` → ❌

**Condición 1: NO CUMPLE.**

Por lo tanto, las tareas T2, T3 y T4 no pueden terminar dentro de un único ciclo secundario.

### 2. Factor de utilización

```math
U = 0,798 < 1
```

**Condición 2: CUMPLE.**

El factor de carga del sistema es menor al 100%.

### 3. Hiperperíodo

```math
H = 1320
```

Dentro de un hiperperíodo:

```math
1320/8 = 165
```

```math
1320/15 = 88
```

```math
1320/20 = 66
```

```math
1320/22 = 60
```

Todas las tareas se ejecutan un número entero de veces.

**Condición 3: CUMPLE.**

### 4. El período de cada tarea debe ser múltiplo entero del ciclo secundario

Como:

```math
T_S = 1
```

tenemos:

```math
8/1 = 8
```

```math
15/1 = 15
```

```math
20/1 = 20
```

```math
22/1 = 22
```

Todos los resultados son enteros.

**Condición 4: CUMPLE.**

### 5. Cada tarea debe terminar antes de un nuevo período de activación

Debe cumplirse:

```math
C_i \leq T_i
```

* T1: `1 ≤ 8` → ✅
* T2: `3 ≤ 15` → ✅
* T3: `4 ≤ 20` → ✅
* T4: `6 ≤ 22` → ✅

**Condición 5: CUMPLE.**

---

## Resumen

| Condición                  | Resultado     |
| -------------------------- | ------------- |
| 1. `C_i ≤ T_S`             | **No cumple** |
| 2. `U < 1`                 | Cumple        |
| 3. Hiperperíodo            | Cumple        |
| 4. `T_i` múltiplo de `T_S` | Cumple        |
| 5. `C_i ≤ T_i`             | Cumple        |

### Conclusión

El Sistema 3 tiene un factor de utilización de:

```math
U \approx 79,8\%
```

un hiperperíodo de:

```math
H = 1320
```

y un período secundario de:

```math
T_S = 1
```

Sin embargo, **no cumple el Test de Garantía**, porque las tareas T2, T3 y T4 tienen un tiempo de ejecución mayor que el período secundario:

```math
C_2 = 3 > 1
```

```math
C_3 = 4 > 1
```

```math
C_4 = 6 > 1
```

Por lo tanto, **el Sistema 3 no puede ser planificado mediante Cyclic Scheduling sin segmentar las tareas**.

Las diapositivas indican que, cuando no es posible confeccionar un plan cíclico pero `U ≤ 1`, es posible recurrir a la **segmentación de tareas**, dividiendo una tarea en segmentos de tiempo de cómputo conocido.
---

## Sistema 4 – Cyclic Scheduling

### Datos

| Tarea |   C | T = D |
| ----- | --: | ----: |
| T1    | 0,5 |     4 |
| T2    |   1 |     5 |
| T3    |   2 |    10 |
| T4    |   9 |    24 |

### Factor de utilización

El factor de utilización de cada tarea es:

```math
U_i = \frac{C_i}{T_i}
```

```math
U_1 = \frac{0,5}{4} = 0,125
```

```math
U_2 = \frac{1}{5} = 0,20
```

```math
U_3 = \frac{2}{10} = 0,20
```

```math
U_4 = \frac{9}{24} = 0,375
```

Por lo tanto:

```math
U = 0,125 + 0,20 + 0,20 + 0,375 = 0,90
```

```math
U = 90\%
```

### Hiperperíodo

El hiperperíodo se obtiene como el mínimo común múltiplo de los períodos:

```math
H = MCM(4,5,10,24)
```

```math
H = 120
```

### Período secundario

Según las diapositivas, el período secundario se obtiene como el máximo común divisor de los períodos de las tareas.

```math
T_S = MCD(4,5,10,24)
```

```math
T_S = 1
```

---

## Test de Garantía

### 1. Cada tarea debe terminar en un único ciclo secundario

Debe cumplirse:

```math
C_i \leq T_S
```

Como:

```math
T_S = 1
```

tenemos:

* T1: `0,5 ≤ 1` → ✅
* T2: `1 ≤ 1` → ✅
* T3: `2 ≤ 1` → ❌
* T4: `9 ≤ 1` → ❌

**Condición 1: NO CUMPLE.**

Las tareas T3 y T4 no pueden terminar dentro de un único ciclo secundario.

### 2. Factor de utilización

```math
U = 0,90 < 1
```

**Condición 2: CUMPLE.**

El factor de carga del sistema es menor al 100%.

### 3. Hiperperíodo

```math
H = 120
```

Dentro de un hiperperíodo:

```math
120/4 = 30
```

```math
120/5 = 24
```

```math
120/10 = 12
```

```math
120/24 = 5
```

Todas las tareas se ejecutan un número entero de veces.

**Condición 3: CUMPLE.**

### 4. El período de cada tarea debe ser múltiplo entero del ciclo secundario

Como:

```math
T_S = 1
```

tenemos:

```math
4/1 = 4
```

```math
5/1 = 5
```

```math
10/1 = 10
```

```math
24/1 = 24
```

Todos los resultados son enteros.

**Condición 4: CUMPLE.**

### 5. Cada tarea debe terminar antes de un nuevo período de activación

Debe cumplirse:

```math
C_i \leq T_i
```

* T1: `0,5 ≤ 4` → ✅
* T2: `1 ≤ 5` → ✅
* T3: `2 ≤ 10` → ✅
* T4: `9 ≤ 24` → ✅

**Condición 5: CUMPLE.**

---

## Resumen

| Condición                  | Resultado     |
| -------------------------- | ------------- |
| 1. `C_i ≤ T_S`             | **No cumple** |
| 2. `U < 1`                 | Cumple        |
| 3. Hiperperíodo            | Cumple        |
| 4. `T_i` múltiplo de `T_S` | Cumple        |
| 5. `C_i ≤ T_i`             | Cumple        |

### Conclusión

El Sistema 4 tiene un factor de utilización de:

```math
U = 90\%
```

un hiperperíodo de:

```math
H = 120
```

y un período secundario de:

```math
T_S = 1
```

Sin embargo, **no cumple el Test de Garantía**, porque las tareas T3 y T4 tienen un tiempo de ejecución mayor que el período secundario:

```math
C_3 = 2 > 1
```

```math
C_4 = 9 > 1
```

Por lo tanto, **el Sistema 4 no puede ser planificado mediante Cyclic Scheduling sin segmentar las tareas**.

Las diapositivas indican que, cuando no es posible confeccionar un plan cíclico pero `U ≤ 1`, es posible utilizar **segmentación de tareas**, dividiendo una tarea en segmentos cuyo tiempo de cómputo sea conocido.
## Diagrama de Gantt

Para el Sistema 4 se tiene:

```math
T_S = 1
```

Por lo tanto, cada ciclo secundario tiene una duración de `1` unidad de tiempo.

Las tareas tienen los siguientes tiempos de ejecución:

| Tarea |   C |
| ----- | --: |
| T1    | 0,5 |
| T2    |   1 |
| T3    |   2 |
| T4    |   9 |

T1 y T2 pueden ejecutarse dentro de un único ciclo secundario:

```text
Tiempo:  0    1    2    3    4    5    ...
         |----|----|----|----|----|----|
T1:      |0,5 |
T2:           |----|
```

Sin embargo, T3 necesita `2` unidades de tiempo y T4 necesita `9` unidades de tiempo:

```math
C_3 = 2 > T_S = 1
```

```math
C_4 = 9 > T_S = 1
```

Por lo tanto, ninguna de estas tareas puede ejecutarse completamente dentro de un único ciclo secundario.

El intento de planificación queda representado de forma esquemática como:

```text
Tiempo:  0    1    2    3    4    5    6    7    8    9
         |----|----|----|----|----|----|----|----|----|
         T_S  T_S  T_S  T_S  T_S  T_S  T_S  T_S  T_S

T1:      |0,5 |
T2:           |----|

T3:                |---------|
                   <--- 2 --->

T4:                           |-------------------------------------|
                              <----------- 9 ----------------------->
```

T3 y T4 ocupan más de un ciclo secundario, por lo que la planificación no cumple la primera condición del Test de Garantía.

### Resultado del Gantt

El diagrama permite visualizar el problema de planificación:

```math
C_3 > T_S
```

```math
C_4 > T_S
```

Por lo tanto, **no es posible construir un Gantt válido para el Sistema 4 utilizando el Cyclic Scheduling original sin segmentar las tareas**.

La segmentación de tareas podría utilizarse como alternativa, ya que el factor de utilización cumple:

```math
U = 0,90 \leq 1
```

pero dicha alternativa corresponde a una planificación diferente y no al Cyclic Scheduling original analizado en este sistema.

# Configuración de FreeRTOS para Cyclic Scheduling

Para implementar una planificación cíclica utilizando FreeRTOS se debe configurar un esquema **estático y cooperativo**, basado en un calendario de ejecución previamente definido.

El sistema debe utilizar el **tick de FreeRTOS** como referencia temporal para generar las activaciones de las tareas. El período secundario debe ser compatible con el tick del sistema:

```math
T_S = K \cdot Tick
```

Las tareas deben ejecutarse según el calendario establecido y utilizando un comportamiento **Run to Completion**: una vez que una tarea comienza su ejecución, debe finalizar antes de permitir la ejecución de otra tarea.

```text
Cyclic Scheduling → calendario fijo + tick + scheduler cooperativo + Run to Completion.
```

Por lo tanto, la configuración debe contemplar:

* un tick de sistema adecuado para representar el período secundario;
* un planificador cooperativo;
* tareas definidas estáticamente;
* activaciones periódicas según el calendario calculado;
* ejecución de las tareas **Run to Completion**;
* evitar la interrupción de una tarea por otra durante su ejecución.

Este tipo de configuración busca mantener el comportamiento **determinista y predecible** propio de los Sistemas Gobernados por Tiempo.

Sin embargo, **no resulta conveniente utilizar FreeRTOS para una planificación estrictamente cíclica**, ya que el calendario de ejecución puede definirse directamente de forma estática sin necesitar las capacidades generales de planificación y gestión de tareas que proporciona un RTOS. En este caso, un planificador cíclico dedicado sería una solución más simple y directa.

**Conclusión:** FreeRTOS puede configurarse para reproducir un esquema de Cyclic Scheduling mediante un planificador cooperativo, un tick adecuado y tareas *Run to Completion*, pero **no es la alternativa más conveniente cuando la planificación ya está completamente determinada de antemano**.
