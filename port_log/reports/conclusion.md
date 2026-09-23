# Conclusión

El dataset heredado requirió una etapa de limpieza y normalización antes de poder analizarse de forma confiable. Durante ese proceso se detectaron valores nulos en campos críticos, fechas y horas inválidas, formatos inconsistentes en matrículas y muelles, y valores atípicos en tonelaje y velocidad. Como resultado de la limpieza por calidad de datos se descartó aproximadamente el 12.13% de los registros originales. Entre los problemas que permanecen identificables mediante los valores centinela, las horas inválidas representan el 15.40% de las infracciones y las fechas inválidas el 12.03%.

En los patrones de infracción, el turno con mayor cantidad de casos fue Madrugada con 134 infracciones. El muelle con mayor concentración fue MUELLED con 87 registros, mientras que el tipo de carga más frecuente fue CONTENEDORES con 71 infracciones, equivalente al 14.98% del total.

Incorporar los datos al nuevo sistema sin una limpieza previa podría producir resultados incorrectos, especialmente en el cálculo de tiempos de estadía, la asignación de infracciones por turno o mes y la detección de excesos de velocidad. Además, los formatos inconsistentes podrían fragmentar una misma categoría en varios valores y afectar los indicadores obtenidos.

Como mejora concreta, se propone validar los datos en el momento de la carga: exigir campos críticos obligatorios, aplicar controles de formato para fechas y horas, utilizar listas cerradas para muelles y tipos de carga, y validar automáticamente rangos numéricos como velocidad y tonelaje. Esto reduciría errores desde el origen y mejoraría la calidad de la información disponible para futuros análisis.
