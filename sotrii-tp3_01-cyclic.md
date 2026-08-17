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


