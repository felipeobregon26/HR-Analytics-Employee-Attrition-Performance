# Marco Teórico — Rotación Laboral Voluntaria
## Fundamentos Psicológicos y Organizacionales

**Felipe Obregón Ochoa** · Psicólogo UCN  
*Proyecto: IBM HR Analytics Employee Attrition & Performance*

---

## 1. Introducción

La rotación laboral voluntaria constituye uno de los fenómenos más estudiados
en psicología organizacional, dada su relevancia tanto para el bienestar de los
trabajadores como para la sostenibilidad operativa de las organizaciones. El
presente marco teórico integra perspectivas clásicas y contemporáneas para
fundamentar los hallazgos empíricos identificados en el análisis exploratorio
del dataset IBM HR Analytics, con especial atención a los patrones de rotación
diferenciada según antigüedad laboral.

---

## 2. Modelos Clásicos de Rotación Voluntaria

Los primeros modelos sistemáticos de rotación laboral adoptaron una lógica
secuencial y determinista. Mobley (1977) propuso que la rotación voluntaria
seguía una cadena causal lineal: la insatisfacción laboral precedía la
intención de búsqueda de empleo alternativo, la cual a su vez antecedía la
decisión de abandono. Este modelo, aunque influyente, presentó limitaciones
explicativas importantes: los estudios que lo evaluaron reportaron que los
predictores tradicionales —incluyendo la satisfacción laboral— explicaban
entre un 5% y un 25% de la varianza en rotación voluntaria (Hom & Griffeth,
1995, citado en Mitchell et al., 2001), sugiriendo que el fenómeno obedece a
dinámicas considerablemente más complejas.

Price y Mueller (1981) ampliaron el modelo de Mobley incorporando variables
estructurales como la centralización organizacional, las oportunidades de
promoción y los salarios como antecedentes de la satisfacción laboral.
Esta extensión anticipó desarrollos teóricos posteriores que reconocerían
el papel de las condiciones organizacionales objetivas —no solo las
percepciones subjetivas— en la decisión de permanencia o salida.

---

## 3. El Modelo de Despliegue de la Rotación Voluntaria

Lee y Mitchell (1994) propusieron una reformulación radical del paradigma
dominante mediante el *Unfolding Model of Voluntary Turnover*. Su argumento
central sostenía que no existe una única trayectoria hacia la rotación, sino
al menos cuatro vías diferenciadas según la naturaleza del proceso cognitivo
y emocional que desencadena la decisión de salida:

- **Vía 1:** Un evento disruptivo (*shock*) desencadena la salida sin
  deliberación extensa (ej. reducción salarial unilateral, cambio de jefatura).
- **Vía 2:** Un evento disruptivo activa una comparación deliberada con
  alternativas laborales disponibles.
- **Vía 3:** La percepción de violación del contrato psicológico motiva
  la búsqueda activa de alternativas.
- **Vía 4:** Sin evento detonante específico, el empleado abandona por
  inercia o desalineación gradual con la organización.

Este modelo tiene implicancias directas para la interpretación de los datos
analizados. El **Perfil 1** de rotación temprana (años 1-3) es consistente
con las Vías 2 y 3: empleados jóvenes cuyas expectativas iniciales no son
confirmadas por la experiencia organizacional real. El **Perfil 2** de
rotación media (años 5-7) es más compatible con las Vías 1 y 4: empleados
con mayor antigüedad que experimentan un evento detonante específico
(como la ausencia de promoción esperada) o una desalineación acumulada
que eventualmente supera su umbral de tolerancia.

---

## 4. El Efecto Honeymoon-Hangover

Boswell et al. (2005) modelaron la evolución intraindividual de la satisfacción
laboral en función de los patrones de cambio de empleo, identificando el
denominado *honeymoon-hangover effect*. Este efecto describe tres fases
secuenciales en la trayectoria actitudinal del empleado:

1. **Deterioración:** caída progresiva de la satisfacción en el empleo anterior,
   que antecede temporalmente la decisión de cambio.
2. **Honeymoon:** incremento súbito de la satisfacción laboral inmediatamente
   posterior al cambio de empleo, explicado por la confluencia de expectativas
   positivas proyectadas por el empleado y la tendencia de las organizaciones
   a presentar una imagen idealizadade sí mismas durante el proceso de
   incorporación.
3. **Hangover:** decline gradual de la satisfacción de vuelta a —o por debajo
   de— la línea base previa al cambio.

Boswell et al. (2009) examinaron los factores moderadores de este efecto,
identificando que la profundidad del *hangover* era significativamente mayor
en empleados con menor satisfacción en el empleo anterior y menor grado de
socialización organizacional en el nuevo cargo. Este hallazgo tiene especial
relevancia para el contexto analizado: la variable `JobSatisfaction` del
dataset puede interpretarse como un indicador del momento en que el empleado
se encuentra dentro de esta curva actitudinal.

La distribución de `YearsAtCompany` identificada en el análisis exploratorio
—con una concentración de rotación en los primeros 1-3 años— es
empíricamente consistente con la fase *hangover* descrita por Boswell et al.
(2005): el período en que las expectativas iniciales colisionan con la
realidad organizacional y la satisfacción decae hacia su nivel de equilibrio.

---

## 5. La Teoría del Job Embeddedness

Mitchell et al. (2001) propusieron una reorientación conceptual significativa:
en lugar de preguntar exclusivamente *por qué los empleados se van*, plantearon
la pregunta complementaria *por qué los empleados se quedan*. Su respuesta fue
el constructo de *job embeddedness* —traducible como arraigo laboral—, definido
como el conjunto de fuerzas que "atrapan" al empleado en su posición actual,
análogas a una red o tejido de conexiones que dificultan el movimiento.

El constructo se articula en tres dimensiones:

**Fit (compatibilidad):** grado en que el empleado percibe que sus valores,
metas y planes de carrera son compatibles con la cultura organizacional y
el entorno comunitario. En el dataset analizado, las variables
`JobSatisfaction`, `EnvironmentSatisfaction` y `WorkLifeBalance` operan
como indicadores proximales de esta dimensión.

**Links (vínculos):** conexiones formales e informales entre el empleado
y otras personas o instituciones dentro y fuera de la organización.
`YearsWithCurrManager` y `YearsAtCompany` capturan parcialmente esta
dimensión al reflejar la profundidad del vínculo construido con la
jefatura directa y el tejido relacional interno.

**Sacrifice (sacrificio):** recursos tangibles e intangibles que el
empleado perdería al abandonar la organización. `MonthlyIncome` y
`StockOptionLevel` son los indicadores más directos de esta dimensión
en el dataset: a mayor compensación y participación en los resultados
organizacionales, mayor el costo percibido de la salida.

Estudios metaanalíticos posteriores (Jiang et al., 2012) confirmaron que
el *job embeddedness* predice la rotación voluntaria con mayor precisión
que la satisfacción laboral, el compromiso organizacional y la
disponibilidad de alternativas laborales considerados de forma aislada.
Este hallazgo tiene implicancias directas para el diseño de intervenciones
de retención: incrementar el arraigo organizacional —mediante vínculos,
compatibilidad y valor percibido del sacrificio— puede ser más efectivo
que intervenir exclusivamente sobre la satisfacción laboral.

---

## 6. El Contrato Psicológico como Hilo Conductor

Rousseau (1989, 1995) introdujo el concepto de contrato psicológico para
referirse al conjunto de creencias individuales sobre las obligaciones mutuas
implícitas en la relación laboral. A diferencia del contrato formal, el
contrato psicológico no está escrito ni explicitado — emerge de promesas
percibidas durante el reclutamiento, la socialización y las interacciones
cotidianas con la organización.

La *ruptura del contrato psicológico* (*psychological contract breach*)
ocurre cuando el empleado percibe que la organización no ha cumplido
con las obligaciones que le atribuía. Morrison y Robinson (1997)
distinguieron entre **breach** (percepción cognitiva de incumplimiento)
y **violation** (respuesta emocional intensa ante dicho incumplimiento),
siendo esta última la que más consistentemente predice la rotación
voluntaria.

El proceso típico que sigue a una ruptura no percibida es gradual:

```
Breach percibido
      ↓
Período de observación y espera ("quizás se corrija")
      ↓
Deterioro del compromiso organizacional
      ↓
Activación de búsqueda de alternativas
      ↓
Rotación voluntaria
```

Este proceso temporal explica con precisión el **Perfil 2** identificado
en el análisis: empleados con 5-7 años de antigüedad que no rotaron en
los primeros años —período en que aún confiaban en que sus expectativas
serían cumplidas— pero que eventualmente abandonaron la organización
cuando la evidencia acumulada de incumplimiento resultó insostenible.
La variable `YearsWithCurrManager` adquiere especial relevancia aquí:
una jefatura estable y de calidad puede funcionar como amortiguador del
breach, mientras que su ausencia o deterioro puede precipitar la ruptura.

---

## 7. Integración Teórica y Síntesis

Los marcos teóricos revisados no son modelos competitivos sino
**perspectivas complementarias** que iluminan distintos aspectos del
mismo fenómeno:

| Marco Teórico | Pregunta que responde | Variable proxy en el dataset |
|---|---|---|
| Mobley (1977) | ¿La insatisfacción precede la salida? | `JobSatisfaction` |
| Lee & Mitchell (1994) | ¿Por qué trayectoria sale el empleado? | `OverTime`, eventos disruptivos |
| Boswell et al. (2005) | ¿Cuándo cae la satisfacción después del ingreso? | `YearsAtCompany` (1-3 años) |
| Mitchell et al. (2001) | ¿Qué ancla al empleado? | `MonthlyIncome`, `YearsWithCurrManager` |
| Rousseau (1989) | ¿Qué promesa implícita fue rota? | `YearsAtCompany` (5-7 años) |

La distribución multimodal de `YearsAtCompany` identificada en el
análisis exploratorio —con peaks de rotación en los años 1-3 y 5-7—
es consistente con la operación simultánea de estos mecanismos en
distintos segmentos de la fuerza laboral. No se trata de un único
perfil de empleado que rota, sino de al menos dos trayectorias
diferenciadas que requieren intervenciones igualmente diferenciadas.

---

## 8. Implicancias para la Intervención Organizacional

La integración de estos marcos sugiere que las estrategias de retención
más efectivas son aquellas que actúan sobre múltiples dimensiones
simultáneamente:

**Para el Perfil 1 (rotación temprana, años 1-3):**
Intervenciones orientadas a gestionar activamente el *honeymoon-hangover*
mediante onboarding extendido, confirmación temprana de expectativas y
construcción deliberada de *links* organizacionales (Mitchell et al., 2001).
El objetivo es sostener la satisfacción inicial más allá del período
de luna de miel mediante experiencias organizacionales que confirmen
—en lugar de desconfirmar— las expectativas de ingreso.

**Para el Perfil 2 (rotación media, años 5-7):**
Intervenciones orientadas a prevenir y reparar rupturas del contrato
psicológico mediante *stay interviews* proactivas, revisión de
estructuras de carrera y señales organizacionales explícitas de
inversión en el desarrollo del empleado. El objetivo es incrementar
el *sacrifice* percibido (Mitchell et al., 2001) y reparar el breach
antes de que derive en violation (Rousseau, 1995).

---

## Referencias

Boswell, W. R., Boudreau, J. W., & Tichy, J. (2005). The relationship
between employee job change and job satisfaction: The honeymoon-hangover
effect. *Journal of Applied Psychology, 90*(5), 882–892.
https://doi.org/10.1037/0021-9010.90.5.882

Boswell, W. R., Shipp, A. J., Payne, S. C., & Culbertson, S. S. (2009).
Changes in newcomer job satisfaction over time: Examining the pattern of
honeymoons and hangovers. *Journal of Applied Psychology, 94*(4), 844–858.
https://doi.org/10.1037/a0014975

Jiang, K., Liu, D., McKay, P. F., Lee, T. W., & Mitchell, T. R. (2012).
When and how is job embeddedness predictive of turnover? A meta-analytic
investigation. *Journal of Applied Psychology, 97*(5), 1077–1096.
https://doi.org/10.1037/a0028610

Lee, T. W., & Mitchell, T. R. (1994). An alternative approach: The unfolding
model of voluntary employee turnover. *Academy of Management Review, 19*(1),
51–89. https://doi.org/10.2307/258835

Mitchell, T. R., Holtom, B. C., Lee, T. W., Sablynski, C. J., & Erez, M.
(2001). Why people stay: Using job embeddedness to predict voluntary turnover.
*Academy of Management Journal, 44*(6), 1102–1121.
https://doi.org/10.2307/3069391

Mobley, W. H. (1977). Intermediate linkages in the relationship between job
satisfaction and employee turnover. *Journal of Applied Psychology, 62*(2),
237–240. https://doi.org/10.1037/0021-9010.62.2.237

Morrison, E. W., & Robinson, S. L. (1997). When employees feel betrayed:
A model of how psychological contract violation develops. *Academy of
Management Review, 22*(1), 226–256. https://doi.org/10.2307/259230

Price, J. L., & Mueller, C. W. (1981). A causal model of turnover for nurses.
*Academy of Management Journal, 24*(3), 543–565.
https://doi.org/10.2307/255574

Rousseau, D. M. (1989). Psychological and implied contracts in organizations.
*Employee Responsibilities and Rights Journal, 2*(2), 121–139.
https://doi.org/10.1007/BF01384942

Rousseau, D. M. (1995). *Psychological and organizational contracts.*
Sage Publications.
