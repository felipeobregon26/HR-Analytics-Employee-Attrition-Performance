# Interpretación — Perfil de Empleado en Riesgo de Rotación

> **Nota metodológica:** Los hallazgos descritos a continuación corresponden a
> análisis descriptivo y exploratorio. Las asociaciones identificadas no implican
> causalidad — su confirmación estadística se desarrolla en el notebook 03
> (modelo predictivo).

---

## Hallazgos cuantitativos base

| Variable | No rota | Sí rota | Diferencia |
|---|---|---|---|
| Ingreso mensual promedio | $6.833 | $4.787 | **-$2.046 (-30%)** |
| Edad promedio | 37.6 años | 33.6 años | **-4 años** |
| Antigüedad promedio | 7.4 años | 5.1 años | **-2.3 años** |

---

## Perfil 1 — Rotación temprana (años 1-3)

El segmento con mayor concentración de rotación corresponde a empleados
jóvenes con menor compensación económica. La brecha salarial de un 30%
respecto a quienes permanecen sugiere que la organización no logra sostener
la percepción de equidad interna durante el período de integración inicial.

Este patrón es consistente con literatura organizacional sobre el **período
de luna de miel** — una fase de alta motivación y expectativa que, de no ser
reforzada con señales concretas de desarrollo y reconocimiento, tiende a
erosionarse en los primeros 24-36 meses.

**Implicancia para intervención:**
Extender y sostener activamente ese período mediante acompañamiento
estructurado en los primeros dos años — onboarding prolongado, mentorías,
revisiones salariales tempranas y planes de carrera visibles desde el ingreso.

---

## Perfil 2 — Rotación media (años 5-7)

La distribución de `YearsAtCompany` muestra un patrón multimodal con un
segundo peak de rotación entre los 5 y 7 años de antigüedad. Este segmento
no corresponde a empleados nuevos — han invertido tiempo considerable en la
organización y conocen su funcionamiento.

La hipótesis más plausible es la presencia de **barreras de desarrollo
profesional** — momentos donde el crecimiento se estanca, la compensación
no avanza al ritmo esperado o las oportunidades de ascenso son percibidas
como limitadas o inequitativas. En contextos de alta demanda laboral
especializada — como la minería en la II Región — este perfil representa
un riesgo especialmente crítico dado el costo de reposición.

**Implicancia para intervención:**
Revisión de estructuras de carrera y bandas salariales en el tramo de
5-8 años de antigüedad. Identificación proactiva de empleados en ese
rango mediante entrevistas de permanencia (*stay interviews*) antes de
que la decisión de salida esté tomada.

---

## Síntesis ejecutiva

> El análisis sugiere que la rotación en esta organización no responde
> a un perfil único, sino a **dos momentos críticos diferenciados** en
> la trayectoria laboral: uno asociado a la consolidación del vínculo
> inicial y otro a barreras de desarrollo en la etapa intermedia.
> Ambos son prevenibles con intervenciones focalizadas y oportunas.

---

*Redactado por Felipe Obregón Ochoa — Psicólogo UCN*
*Basado en análisis exploratorio del IBM HR Analytics Dataset*
