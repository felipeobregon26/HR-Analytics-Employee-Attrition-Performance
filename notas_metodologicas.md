# 📋 Notas Metodológicas — HR Analytics Project
**Autor:** Felipe Obregón Ochoa · Psicólogo UCN  
**Repositorio:** github.com/felipeobregon26/HR-Analytics-Employee-Attrition-Performance  
**Stack:** R + RMarkdown + tidyverse + caret + randomForest  

> Este documento registra las decisiones metodológicas, criterios analíticos
> y fundamentos técnicos adoptados a lo largo del desarrollo del proyecto.
> Incluye justificaciones de cada decisión de preprocesamiento, modelado y
> visualización, conectadas con el dominio de RRHH y Bienestar Organizacional.

---

## Sesión 01 — 2026-05-30

### Contexto
Revisión línea a línea del notebook `03_modelo_predictivo.Rmd`.
Foco: comprensión significativa del código, no solo ejecución.

---

### 1. Verificación de dimensiones del dataset

**Código revisado:**
```r
cat("Filas:", nrow(df), "\n")
cat("Columnas:", ncol(df), "\n")
```

**Qué aprendí:**
- `nrow()` y `ncol()` verifican que el dataset cargó completo antes de cualquier análisis.
- `cat()` concatena texto y valores para mostrarlos en consola de forma legible.
- `"\n"` es una secuencia de escape que genera salto de línea — se escribe como dos caracteres (`\` + `n`) y R los interpreta juntos.
- Esta verificación no es decorativa: un dataset incompleto produce modelos silenciosamente incorrectos.

**Criterio analítico:**
> Antes de modelar, siempre confirmar que el número de filas coincide con el esperado.

---

### 2. Identificación y eliminación de variables de varianza cero

**Código revisado:**
```r
df %>%
  select(EmployeeCount, Over18, StandardHours) %>%
  distinct()
```

**Qué aprendí:**
- Una variable que no varía entre registros no aporta poder discriminatorio al modelo.
- `distinct()` no *descubre* que son constantes — **confirma** una decisión tomada previamente en el EDA.
- El flujo correcto es: detectar en EDA → decidir eliminar → verificar con `distinct()` → eliminar con `select(-variable)`.
- Las tres variables eliminadas (`EmployeeCount = 1`, `Over18 = "Y"`, `StandardHours = 80`) son artefactos administrativos del dataset IBM, no variables psicológicas ni organizacionales.

**Matiz importante — Gender como caso especial:**
Si en un dataset `Gender` aparece constante (ej: 100% "Male"), la decisión es doble:
- **Eliminar del modelo** (varianza cero → no aporta matemáticamente).
- **Reportar en el EDA y limitaciones** (es un hallazgo organizacional relevante — un dataset sin diversidad de género restringe la generalización de resultados).

> Un analista de datos elimina la variable. Un psicólogo organizacional además reporta lo que eso significa.

---

### 3. Diferencia entre `select()` y `group_by()`

**Qué aprendí:**

| Función | Actúa sobre | Para qué |
|---|---|---|
| `select()` | columnas | reducir el ancho del dataset |
| `group_by()` | filas | agrupar por categoría para calcular |

- `select()` es como ocultar columnas en Excel.
- `group_by()` + `summarise()` es como hacer una tabla dinámica.
- Se usan frecuentemente juntos en un mismo pipeline.

---

### 4. Lectura de pipelines con `%>%`

**Qué aprendí:**
- El pipe `%>%` se lee como **"y luego"**.
- Un pipeline se escribe y lee **de arriba hacia abajo** — como una receta.
- Para entender **qué pregunta responde** un pipeline, conviene leerlo **de abajo hacia arriba**.
- Estructura de lectura:

| Posición | Pregunta |
|---|---|
| Primera línea | ¿De qué dataset parto? |
| Líneas del medio | ¿Qué transformaciones aplico? |
| Última línea | ¿Qué resultado final produzco? |

**Ejemplo analizado:**
```r
df %>%
  filter(Attrition == "Yes") %>%
  select(Department, Age, MonthlyIncome) %>%
  arrange(desc(MonthlyIncome))
```
Resultado: tabla de 3 columnas con los empleados que rotaron, ordenados de mayor a menor ingreso. La primera fila es el empleado con **mayor** ingreso que se fue.

---

### 5. Tibble vs. DataFrame

**Qué aprendí:**
- Un tibble es un dataframe mejorado, nativo del ecosistema tidyverse.
- Las funciones de `dplyr` (`select`, `filter`, `distinct`, etc.) siempre devuelven tibbles.
- Diferencias prácticas relevantes:
  - El tibble muestra el tipo de cada columna (`<dbl>`, `<chr>`, `<int>`, `<fct>`) directamente en la consola.
  - No convierte strings a factor automáticamente.
  - Limita la impresión a 10 filas por defecto — más legible.
- Tipos de datos frecuentes en R:

| Tipo | Símbolo | Ejemplo |
|---|---|---|
| Número entero | `<int>` | `1`, `42` |
| Número decimal | `<dbl>` | `3.14`, `80.0` |
| Texto | `<chr>` | `"Yes"`, `"Sales"` |
| Factor | `<fct>` | categorías ordenadas |
| Lógico | `<lgl>` | `TRUE` / `FALSE` |

---

### 6. Variables ordinales y escalas Likert en R

**Qué aprendí:**
- `JobSatisfaction` tiene valores `1, 2, 3, 4` → R lo lee como `<int>`.
- Desde una perspectiva psicométrica, es una **escala ordinal** — hay orden, pero no distancias iguales entre niveles.
- En la práctica del modelado predictivo se trata como numérica (escala intervalar asumida), especialmente con 5+ puntos.
- Esta decisión debe **documentarse como limitación** del modelo, no ignorarse.

**Conexión con práctica profesional:**
Las escalas Likert — usadas en la mayoría de instrumentos de clima, satisfacción y bienestar organizacional — presentan exactamente este mismo problema. El debate ordinal vs. intervalar es estándar en psicometría aplicada a RRHH.

**Criterio adoptado en este proyecto:**
> `JobSatisfaction` y variables similares se tratan como numéricas (`<int>`) para el modelo predictivo, asumiendo escala intervalar. Esta decisión se documenta como limitación psicométrica en la sección de conclusiones del notebook 03.

---

### Resumen de conceptos clave — Sesión 01

| Concepto | Dominio | Estado |
|---|---|---|
| `nrow()`, `ncol()`, `cat()` | R base | ✅ Comprendido |
| Varianza cero y su impacto en modelos | Estadística | ✅ Comprendido |
| `select()` vs `group_by()` | tidyverse | ✅ Comprendido |
| Lectura de pipelines `%>%` | tidyverse | ✅ Comprendido |
| Tibble vs. DataFrame | tidyverse | ✅ Comprendido |
| Tipos de datos en R | R base | ✅ Comprendido |
| Escalas Likert como variables ordinales | Psicometría + R | ✅ Comprendido |
| Criterio analítico con fundamento psicológico | RRHH aplicado | ✅ En desarrollo |

---

*Próxima sesión: continuar revisión del notebook 03 — preprocesamiento, división train/test y manejo del desbalance de clases.*

---

## Sesión 02 — 2026-05-31

### Contexto
Revisión del notebook `02_visualizaciones.Rmd` y conceptos de ggplot2.
Foco: comprensión de la arquitectura de capas de ggplot2, transformación de datos para visualización y criterio analítico aplicado a RRHH.

---

### 1. Frecuencia absoluta y relativa con `count()` y `mutate()`

**Código revisado:**
```r
tabla_attrition <- df %>%
  count(Attrition) %>%
  mutate(
    porcentaje = n / sum(n) * 100,
    etiqueta   = paste0(round(porcentaje, 1), "%")
  )
```

**Qué aprendí:**
- `count()` es un atajo de `group_by() + summarise(n = n())` — cuenta filas por categoría y devuelve una columna llamada `n` automáticamente.
- `mutate()` agrega columnas nuevas sin eliminar las anteriores.
- `round(número, decimales)` redondea al número de decimales especificado — `round(16.326, 1)` → `16.3`.
- `paste0()` concatena texto sin espacios — `paste0(16.3, "%")` → `"16.3%"`.
- La columna `etiqueta` no es para el modelo — es para reutilizarla directamente en `geom_text()` del gráfico. Prepararla en la tabla mantiene el código del gráfico más limpio.

---

### 2. Arquitectura de capas en ggplot2

**Qué aprendí:**
- ggplot2 usa `+` en vez de `%>%` — cada `+` agrega una **capa** al gráfico, como acetatos transparentes apilados.
- Las capas no se ejecutan en secuencia — ggplot las **acumula todas** y construye el gráfico al final de una vez.
- Estructura estándar de un gráfico:

| Capa | Función | Responsabilidad |
|---|---|---|
| 1 | `ggplot()` | lienzo y mapeo de variables |
| 2 | `geom_*()` | geometría visual (barras, puntos, líneas) |
| 3 | `coord_*()` | sistema de coordenadas |
| 4 | `scale_*()` | escalas y colores |
| 5 | `theme_*()` | estilo visual |
| 6 | `labs()` | títulos y etiquetas — siempre al final |

**Por qué `labs()` va al final:**
Separación de responsabilidades — quien quiera cambiar un título no necesita tocar la lógica técnica del gráfico. Principio de parsimonia aplicado al código.

**`aes()` — aesthetics:**
Define el mapeo entre columnas del dataframe y dimensiones visuales (`x`, `y`, `fill`, `color`, `label`). No dibuja nada — solo declara qué variable va dónde.

---

### 3. `coord_flip()` — rotar coordenadas

**Qué aprendí:**
- `coord_flip()` voltea el sistema de coordenadas completo — todas las capas se adaptan automáticamente.
- Es preferible a intercambiar `x` e `y` en `aes()` porque no requiere revisar cada capa individualmente.
- Analogía: rotar la habitación entera vs. mover cada mueble uno por uno.

---

### 4. `pivot_longer()` — transformación de formato ancho a largo

**Código revisado:**
```r
vars_numericas %>%
  pivot_longer(everything(), names_to = "variable", values_to = "valor")
```

**Qué aprendí:**
- `pivot_longer()` transforma el formato del dataframe de **ancho** (muchas columnas) a **largo** (dos columnas: nombre y valor).
- ggplot2 necesita formato largo para graficar múltiples variables simultáneamente.
- `everything()` transforma todas las columnas — `-Attrition` excluye una columna específica del pivoteo.
- `names_to` define el nombre de la columna que recibirá los nombres de las columnas originales.
- `values_to` define el nombre de la columna que recibirá los valores.

**Diferencia clave entre dos usos:**
```r
pivot_longer(everything(), ...)      # transforma TODAS las columnas
pivot_longer(-Attrition, ...)        # transforma todas EXCEPTO Attrition
```
El `-` se usa cuando una variable es el ancla de comparación — debe mantenerse como columna fija.

---

### 5. `facet_wrap()` — subpaneles automáticos

**Código revisado:**
```r
facet_wrap(~ variable, scales = "free", ncol = 2)
```

**Qué aprendí:**
- `facet_wrap()` divide el gráfico en subpaneles, uno por cada valor de la variable especificada.
- `scales = "free"` da a cada panel su propio eje X e Y — necesario cuando las variables tienen rangos muy distintos.
- `scales = "free_y"` libera solo el eje Y — cuando el eje X es el mismo en todos los paneles (ej: "No" y "Yes").
- `ncol = 2` organiza los paneles en 2 columnas — `ncol = 1` los apila en una sola columna.

---

### 6. Boxplot — lectura e interpretación

**Qué aprendí:**

| Parte del boxplot | Qué representa |
|---|---|
| Línea del medio (Q2) | Mediana — 50% de datos arriba, 50% abajo |
| Borde izquierdo (Q1) | 25% más bajo |
| Borde derecho (Q3) | 75% más bajo |
| Ancho de la caja (RIC) | Donde vive el 50% central |
| Bigotes | Rango sin outliers |
| Puntos sueltos | Valores atípicos |

**Interpretación aplicada al dataset:**
Las 4 variables numéricas clave (Age, MonthlyIncome, YearsAtCompany, TotalWorkingYears) muestran diferencias visuales entre grupos "No" y "Yes" — los empleados que rotaron tienden a ser más jóvenes, con menor salario y menor antigüedad. Esta es una **asociación**, no causalidad — el modelo predictivo del notebook 03 responde la pregunta causal.

**Boxplot vs. Violín:**

| | Boxplot | Violín |
|---|---|---|
| Muestra cuartiles | ✅ Explícito | Con superposición |
| Muestra forma completa | ❌ | ✅ |
| Detecta subgrupos internos | ❌ | ✅ |
| Legible para no estadísticos | ✅ | ⚠️ |

Uso recomendado: boxplot para presentaciones a dirección; violín para análisis técnico cuando se sospecha distribución multimodal.

---

### 7. Hallazgo analítico — distribución multimodal en antigüedad

**Observación identificada:**
`YearsAtCompany` y `TotalWorkingYears` muestran distribución multimodal con picos alternos en los primeros años — muchos empleados en año 3, pocos en año 4, muchos en año 5. Patrón que sugiere **hitos críticos en la trayectoria laboral**.

**Hipótesis de RRHH:**
Los picos podrían corresponder a momentos de evaluación, promoción o vencimiento de contrato — puntos de decisión donde el empleado evalúa si permanecer o irse.

**Acción recomendada:**
Análisis inferencial complementario (Kruskal-Wallis) y visualización con `geom_violin()` para confirmar si el patrón existe diferencialmente entre grupos que rotaron y no rotaron.

---

### 8. Barras apiladas — `position` en `geom_col()`

**Qué aprendí:**

| `position` | Qué hace | Cuándo usarlo |
|---|---|---|
| `"stack"` | apila — valores absolutos | cuando importa el total |
| `"fill"` | apila al 100% — proporciones | cuando importa comparar entre grupos |
| `"dodge"` | barras lado a lado | cuando importa ver cada valor por separado |

**Criterio de parsimonia aplicado:**
`position = "fill"` es la opción más parsimonious para comparar tasas de rotación entre departamentos — una sola barra por grupo responde la pregunta sin ruido visual adicional. `position = "dodge"` obligaría al ojo a hacer el cálculo mentalmente.

---

### 9. `ungroup()` — buena práctica vs. necesidad

**Qué aprendí:**
- `group_by()` marca internamente el dataframe — esa marca persiste después del `mutate()`.
- `ungroup()` borra esa marca y devuelve el dataframe a estado normal.
- Sin `ungroup()`, cálculos posteriores se ejecutan por grupo aunque ya no sea la intención — error silencioso (el código corre sin avisar pero el número está mal).
- Regla adoptada: usar `ungroup()` siempre después de `group_by()`, aunque el pipeline termine ahí.

---

### 10. Matriz de correlación — `corrplot` y multicolinealidad

**Código revisado:**
```r
vars_cor <- df %>%
  select(where(is.numeric)) %>%
  bind_cols(Attrition_num = ifelse(df$Attrition == "Yes", 1, 0))
```

**Qué aprendí:**
- `where(is.numeric)` selecciona todas las columnas numéricas sin nombrarlas individualmente.
- `bind_cols()` pega columnas de un objeto externo al dataframe — distinto de `mutate()` que crea columnas desde dentro.
- `ifelse(condición, valor_si_true, valor_si_false)` — convierte `"Yes"/"No"` a `1/0` para incluir Attrition en el cálculo de correlación (operación matemática que requiere números).
- `colorRampPalette(c(color1, color2, color3))(200)` crea un gradiente continuo de 200 tonos entre tres colores.
- `type = "upper"` muestra solo el triángulo superior de la matriz — evita redundancia (principio de parsimonia).

**Multicolinealidad:**
Variables con correlación muy alta entre sí (r > 0.9) generan inestabilidad en los coeficientes de la regresión logística — el modelo no puede distinguir el efecto individual de cada una. Se detecta con VIF (Variance Inflation Factor):

| VIF | Interpretación |
|---|---|
| 1 | sin problema |
| 1-5 | aceptable |
| 5-10 | preocupante |
| >10 | problema grave |

**Decisión contextual — `YearsAtCompany` vs. `TotalWorkingYears`:**
La variable a conservar depende de la pregunta de negocio:
- **Reclutamiento** → `TotalWorkingYears` (experiencia acumulada como filtro de selección)
- **Retención** → `YearsAtCompany` (vínculo con esta organización — identifica grupos de riesgo internos)

> La estadística identifica la multicolinealidad. El criterio organizacional decide qué variable conservar.

---

### Resumen de conceptos clave — Sesión 02

| Concepto | Dominio | Estado |
|---|---|---|
| `count()`, `mutate()`, `round()`, `paste0()` | tidyverse | ✅ Comprendido |
| Arquitectura de capas ggplot2 | visualización | ✅ Comprendido |
| `aes()` y mapeo de variables | ggplot2 | ✅ Comprendido |
| `coord_flip()` | ggplot2 | ✅ Comprendido |
| `pivot_longer()` — formato ancho a largo | tidyverse | ✅ Comprendido |
| `facet_wrap()` — subpaneles | ggplot2 | ✅ Comprendido |
| Lectura e interpretación de boxplots | estadística | ✅ Comprendido |
| Boxplot vs. Violín | visualización | ✅ Comprendido |
| Distribución multimodal como hallazgo de RRHH | analítica aplicada | ✅ Identificado autónomamente |
| `position = "fill"` vs `"stack"` vs `"dodge"` | ggplot2 | ✅ Comprendido |
| `ungroup()` — buena práctica | tidyverse | ✅ Comprendido |
| `where()`, `bind_cols()`, `ifelse()` | tidyverse + R base | ✅ Comprendido |
| Multicolinealidad y VIF | estadística | ✅ Comprendido |
| Decisión de variable según pregunta de negocio | RRHH analítico | ✅ Criterio propio demostrado |

---

*Próxima sesión: subir archivos al repositorio GitHub + continuar con notebook 03 — preprocesamiento, división train/test y manejo del desbalance de clases.*
