# Actividad 0: Equipo e ideas de producto

## Equipo

| Nombre y apellidos | Usuario de GitHub |
| --- | --- |
| Nerea Núñez Zarza | nernunnzar |
| Alberto Dávila de los Ríos | albertodavila95-byte |
| Manuel Valero Cayón | manu-valero |

Repositorio: <https://github.com/manu-valero/Proyecto-evolve>

---

## Idea 1: Verificador de ahorros energéticos (nombre provisional)

### Título y descripción
Herramienta que calcula cuánta energía ha ahorrado realmente un edificio tras una reforma de eficiencia energética. Estima cuánto habría consumido el edificio sin la reforma, según el clima y el uso, lo compara con el consumo real y traduce la diferencia a kWh, euros y CO₂, generando un informe de verificación.

### Problema y usuario
- Usuario principal: técnicos de empresas de servicios energéticos (ESE) que firman contratos en los que cobran según el ahorro conseguido. Necesitan demostrar ese ahorro a su cliente de forma objetiva. [Hipótesis: pendiente de validar con 1–2 profesionales del sector]
- Usuario secundario: gestores de edificios (ayuntamientos, universidades, empresas) que quieren comprobar si el ahorro que les facturan es real.
- Necesidad: *Cuando termino una reforma de eficiencia en un edificio, necesito calcular de forma objetiva cuánto ha ahorrado para facturar a mi cliente y justificarlo sin discusiones.*
- Cómo lo resuelve hoy: el ahorro no se puede medir directamente, porque hay que estimar cuánto habría consumido el edificio sin la reforma, y el clima de un año a otro distorsiona la comparación. Se suele hacer con hojas de cálculo y regresiones manuales, lo que es lento, poco reproducible y fuente de discrepancias entre empresa y cliente.

### Uso y valor
**Situación de uso:** una ESE cambió en enero la climatización de un edificio de oficinas. Seis meses después, el técnico carga en la herramienta el consumo horario del edificio y la fecha de la reforma. La herramienta entrena un modelo con el año anterior a la reforma, estima cuánto habría consumido el edificio desde enero con el clima real de esos meses y lo compara con el consumo medido. El técnico obtiene el ahorro en kWh, euros y CO₂, un gráfico de consumo real frente al esperado y un informe redactado que entrega al cliente.

**Valor para el usuario:** convierte un cálculo manual y discutible en un proceso reproducible y explicado, que separa el efecto de la reforma del efecto del clima. Reduce el tiempo de elaboración de informes y las discrepancias en la facturación. [Hipótesis] El tiempo ahorrado y la fiabilidad frente al método actual se validarán con profesionales del sector. El sistema de Certificados de Ahorro Energético distingue entre actuaciones estandarizadas, cuyo ahorro se calcula con una fórmula del catálogo oficial, y actuaciones singulares, que requieren justificar el ahorro con una metodología propia; la herramienta se dirige a estas últimas y a cualquier contrato en el que el ahorro deba medirse con datos reales.

### Datos
| Fuente | Enlace | Qué aporta | Estado |
| --- | --- | --- | --- |
| Building Data Genome Project 2 (BDG2): consumos | https://github.com/buds-lab/building-data-genome-project-2 | Consumo horario de 3.053 contadores (electricidad, frío, calor, agua…) de 1.636 edificios no residenciales, años 2016–2017 | [Confirmado 03/11/2026: repositorio público accesible; licencia CC BY-SA 4.0. Pendiente descargar y revisar los ficheros de consumo] |
| BDG2: metadatos de edificios y meteorología | Mismo repositorio (data/metadata y data/weather) | Uso del edificio, superficie, año de construcción, contadores disponibles y ubicación del emplazamiento; meteorología horaria de cada emplazamiento | [Confirmado 03/11/2026: metadata.csv revisado (una fila por edificio, coordenadas a nivel de emplazamiento, muchos campos vacíos). Meteorología pendiente de revisar] |
| Datos reales de un edificio en España (por ejemplo, vía Datadis) | Por concretar | Consumo real de un edificio con una reforma conocida | [Hipótesis: requiere autorización del titular; solo viable si el equipo consigue acceso] |
| Sistema de Certificados de Ahorro Energético (CAE, MITECO) | https://www.miteco.gob.es/es/prensa/ultimas-noticias/2024/julio/el-miteco-amplia-el-catalogo-de-medidas-de-eficiencia-energetica.html | Marco normativo del ahorro certificable: catálogo de 114 fichas estandarizadas (36 del sector terciario) con ahorro calculado por fórmula, y actuaciones singulares que requieren justificar el ahorro (Orden TED/815/2023). Contexto para el informe generado | [Confirmado 03/11/2026: nota de prensa oficial. Pendiente revisar la Orden TED/815/2023 sobre actuaciones singulares] |
| Factores de emisión de CO₂ (MITECO, Registro de huella de carbono) | https://www.miteco.gob.es/es/cambio-climatico/temas/registro-huella.html | Factor oficial (kg CO₂/kWh) para convertir los kWh ahorrados en emisiones evitadas | [Confirmado 03/11/2026: publicados los factores de emisión 2007–2025. Pendiente descargar el fichero] |
| Precio de la electricidad para consumidores no domésticos (Eurostat, nrg_pc_205) | https://ec.europa.eu/eurostat/databrowser/view/nrg_pc_205/default/table?lang=en | Precio real facturado (€/kWh) por país, tramo de consumo anual (IA–IG) y nivel de impuestos, semestral; valor por defecto para convertir el ahorro a euros, sustituible por la tarifa real del contrato | [Confirmado 03/11/2026: conjunto de datos disponible, actualizado el 19/10/2026. Pendiente descargar la serie de España y elegir tramo de consumo] |
| Meteorología de España (AEMET OpenData) | https://opendata.aemet.es | Temperatura y otras variables por estación meteorológica, necesarias para aplicar el modelo a un edificio español | [Confirmado 03/11/2026: portal accesible, con consulta web y API para desarrolladores; la API requiere solicitar una clave gratuita. Solo necesaria si se usan datos de un edificio español] |

Restricciones de uso y privacidad: BDG2 se publica con licencia Creative Commons Reconocimiento-CompartirIgual 4.0 (CC BY-SA 4.0), que permite usarlo y transformarlo citando a los autores (Miller et al., 2020, Scientific Data), indicando los cambios realizados y distribuyendo los datos derivados con la misma licencia; no afecta al código. Los edificios aparecen anonimizados y su ubicación solo se conoce a nivel de emplazamiento. Los datos de un edificio real serían confidenciales: solo se usarían con autorización del titular y no se subirían al repositorio. Los factores de CO₂ y los precios españoles se aplicarían como parámetros configurables, ya que los edificios de BDG2 no están en España. Los factores de emisión (MITECO), los precios (Eurostat) y la meteorología (AEMET) son datos públicos que se reutilizarían citando la fuente y la fecha de los datos.

### Primera versión (MVP)
**Incluye:**
1. Selección de un edificio y de una fecha de reforma.
2. Modelo que estima el consumo esperado sin reforma a partir del clima y del calendario (hora, día de la semana, festivos), entrenado con el periodo anterior a la reforma.
3. Cálculo del ahorro en kWh, euros y CO₂, con un gráfico de consumo real frente a consumo esperado.
4. Informe de verificación redactado automáticamente a partir de los resultados calculados.

**Queda fuera por ahora:** cálculo de Certificados de Ahorro Energético (CAE), detección de consumos anómalos, varios contadores o edificios a la vez, conexión directa con distribuidoras y cuentas de usuario.

**Qué mostraríamos funcionando:** el usuario elige un edificio y la fecha de la reforma y obtiene el consumo esperado frente al real, el ahorro en kWh, euros y CO₂, y un informe descargable que lo explica.

### Viabilidad y dudas
- Principal incertidumbre: los datos abiertos disponibles (BDG2) no incluyen reformas reales documentadas. Para demostrar el cálculo de ahorro habría que simular una reforma (por ejemplo, reducir el consumo un porcentaje conocido a partir de una fecha) y comprobar si la herramienta recupera ese ahorro.
- Cómo la comprobaríamos: descargar BDG2, entrenar un primer modelo con 2016 y medir su error al predecir 2017 en edificios sin cambios. Si el error es mayor que el ahorro que se quiere medir, la herramienta no sería fiable.
- Otras dudas:
  - Los datos son de 2016–2017 y no se actualizan, lo que limita la parte de actualización automática del producto (actividad 7). Lo resolvería contar con datos reales de un edificio.
  - Los edificios de BDG2 no están en España. El método no depende de ello, porque el modelo se entrena con los datos de cada edificio antes de su reforma; BDG2 sirve para desarrollarlo y validarlo en edificios y climas variados. Para aplicarlo a un edificio español harían falta sus consumos, la meteorología local (AEMET) y los festivos españoles, y no podremos comprobar su comportamiento con clima mediterráneo sin datos de un edificio español.

---

## Idea 2: ¿Reposto hoy? (nombre provisional)

### Título y descripción
Herramienta que ayuda a autónomos y pequeñas empresas a decidir cuándo y dónde repostar. Además de mostrar las gasolineras más baratas de su zona, estima si el precio subirá o bajará en los próximos días y recomienda repostar hoy o esperar.

### Problema y usuario
- Usuario principal: autónomos y pequeñas empresas con vehículos de trabajo que repostan varias veces por semana (reparto, comerciales, instaladores, técnicos de mantenimiento). Para ellos el combustible es un gasto fijo relevante y repostan dentro de una zona conocida. [Hipótesis: pendiente de validar con 2–3 profesionales]
- Usuario secundario: conductores particulares que usan el coche a diario para ir al trabajo.
- Necesidad: *Cuando planifico mis desplazamientos de la semana, necesito saber dónde y cuándo repostar para reducir el gasto en combustible sin desviarme ni perder tiempo.*
- Cómo lo resuelve hoy: reposta en la gasolinera habitual o en la que pilla de camino, o consulta el precio del momento en apps o en el Geoportal del Ministerio. Estas herramientas muestran el precio actual y su histórico, pero no le indican si le conviene esperar uno o dos días.

### Uso y valor
**Situación de uso:** el lunes por la mañana, un repartidor de Sevilla con furgoneta diésel abre la herramienta antes de empezar la ruta. Elige su zona y su carburante y ve las gasolineras más baratas de su zona hoy. Recibe además un aviso: «Probabilidad alta de bajada en tu zona en los próximos 2 días». Decide echar solo lo necesario hoy y llenar el depósito el miércoles en la estación recomendada.

**Valor para el usuario:** le ayuda a decidir dónde y cuándo repostar sin tener que comparar precios manualmente, y a evitar llenar el depósito justo antes de una bajada. Para un profesional que reposta varias veces por semana, pequeñas diferencias por litro se acumulan en un ahorro mensual apreciable; para un particular el ahorro es menor, por eso no es el usuario principal. [Hipótesis] En una primera consulta de los datos (Sevilla, 01/10/2026) se observan diferencias de precio apreciables entre estaciones de un mismo municipio; cuantificaremos esa dispersión y el ahorro posible en la actividad 1.

### Datos
| Fuente | Enlace | Qué aporta | Estado |
| --- | --- | --- | --- |
| Precios de carburantes en gasolineras españolas (Ministerio para la Transición Ecológica) | https://sedeaplicaciones.minetur.gob.es/ServiciosRESTCarburantes/PreciosCarburantes/help | Precio actual por estación y carburante, con ubicación, marca y horario (unas 11.500 estaciones); actualizado cada media hora | [Confirmado 02/11/2026] |
| Histórico de precios por fecha (servicio REST del Ministerio) | https://sedeaplicaciones.minetur.gob.es/ServiciosRESTCarburantes/PreciosCarburantes/help | Precios diarios por estación y carburante desde el 01/01/2007, filtrables por provincia y producto (una fecha por consulta) | [Confirmado 02/11/2026: probado con Sevilla (ID 41) para 01/01/2007 y 01/10/2026] |
| Precio diario del petróleo Brent (EIA, Agencia de Información Energética de EE. UU.) | https://www.eia.gov/dnav/pet/hist/RBRTED.htm | Coste de la materia prima: sus variaciones suelen trasladarse al precio en gasolinera con unos días de retraso | [Confirmado 03/11/2026: serie diaria en dólares por barril, descargable en Excel. Datos de origen Thomson Reuters: pendiente revisar condiciones de uso. Sin datos en fines de semana] |
| Tipo de cambio euro/dólar de referencia (Banco Central Europeo) | https://www.ecb.europa.eu/stats/policy_and_exchange_rates/euro_reference_exchange_rates/html/index.es.html | Convierte el Brent a euros; un euro más débil encarece el combustible | [Confirmado 03/11/2026: publicación diaria en días laborables; uso informativo] |
| Calendario: día de la semana y festivos nacionales y autonómicos (BOE) | https://www.boe.es/diario_boe/txt.php?id=BOE-A-2025-21667 | Patrones semanales (como el «efecto lunes» documentado por la CNMC en 2007–2012) y periodos festivos | [Confirmado 03/11/2026: resolución anual de fiestas laborales (enlace de 2026); se necesita una por cada año analizado. El día de la semana se calcula a partir de la fecha] |

Restricciones de uso y privacidad: los precios los comunican obligatoriamente las estaciones al Ministerio para la Transición Ecológica (Orden ITC/2308/2007). Su reutilización se rige por las condiciones generales de datos.gob.es (Ley 37/2007 y RD 1495/2011, aviso legal: https://datos.gob.es/es/aviso-legal), que permiten el uso comercial y no comercial, incluida la modificación y combinación con otras fuentes, siempre que no se desnaturalice la información, se cite la fuente y la fecha de última actualización y no se sugiera que el organismo respalda el producto. El Ministerio indica que la información es meramente informativa y no certifica precios de venta. El histórico guarda el precio vigente a las 23:59 de cada día. No contiene datos personales, solo direcciones de instalaciones. Hay reportes de caídas puntuales del servicio, por lo que la descarga deberá tolerar fallos y reintentos.

### Primera versión (MVP)
**Incluye:**
1. Selección de zona (inicialmente la provincia de Sevilla) y tipo de carburante.
2. Ranking de las gasolineras más baratas de la zona hoy, en lista y mapa.
3. Predicción de si el precio de cada estación subirá o bajará en los próximos días, con su nivel de confianza.
4. Recomendación «repostar hoy» o «esperar», acompañada de una explicación breve en lenguaje natural.

**Queda fuera por ahora:** cálculo de rutas, alertas y notificaciones, app móvil, cobertura de toda España, puntos de recarga eléctrica y cuentas de usuario.

**Qué mostraríamos funcionando:** el usuario elige zona y carburante y obtiene las estaciones más baratas, la predicción para los próximos días y la recomendación de repostar hoy o esperar, con su explicación.

### Viabilidad y dudas
- Principal incertidumbre: si el precio a uno o dos días se puede predecir mejor que con la regla sencilla «mañana costará lo mismo que hoy». Si no se supera esa referencia, la recomendación no aporta valor frente a las apps existentes.
- Cómo la comprobaríamos: descargar al menos un año de histórico de la provincia, medir con qué frecuencia y cuánto cambian los precios de cada estación y comparar una primera predicción sencilla con esa regla.
- Otras dudas:
  - El mercado ha cambiado mucho desde 2007 (precios más dispersos, nuevas marcas de bajo coste), por lo que probablemente usaremos solo los años recientes.
  - Las series del Brent y del tipo de cambio no tienen datos en fines de semana; habrá que decidir cómo rellenar esos días.
  - Estabilidad del servicio REST y si el ahorro real compensa al usuario (a validar hablando con 2–3 profesionales).

---

## Idea 3: ConsultorIA Medioambiental - Asistencia en normativa medioambiental y análisis de riesgo (nombre provisional)

### Título y descripción
Herramienta que presta asesoramiento en normativa medioambiental y análisis de riesgo para empresas en España. La herramienta combina un panel cuantitativo sobre la probabilidad y gravedad de expedientes sancionadores basándose en datos históricos oficiales con un asistente conversacional conectado a la legislación vigente del BOE para orientar a las empresas en su cumplimiento legal.

### Problema y usuario
- Usuario principal: responsables de medioambiente, responsables de sostenibilidad, gestores ambientales, directores de operaciones y asesores jurídicos en PyMEs e industrias que necesitan conocer qué obligaciones normativas les aplican y evaluar sus riesgos de sanción. [Validado por experiencia profesional propia.]
- Usuario secundario: consultores externos de cumplimiento normativo que buscan agilizar el análisis de impacto regulatorio para sus clientes.
- Necesidad: *Cuando una empresa desarrolla su actividad industrial, necesito identificar de forma precisa qué requisitos legales ambientales le afectan y cuál es su exposición real a sanciones para evitar incumplimientos.*
- Cómo lo resuelve hoy: la legislación ambiental española es muy amplia, dispersa y compleja. Actualmente se resuelve contratando consultorías costosas, realizando búsquedas manuales tediosas en boletines oficiales de forma reactiva o tras sufrir inspecciones.

### Uso y valor
**Situación de uso:** el responsable de medioambiente de una empresa introduce los parámetros básicos de su actividad (sector de actividad, volumen de residuos, tipo de vertidos o ubicación). La herramienta le devuelve un diagnóstico cuantitativo del riesgo sancionador basado en estadísticas oficiales del MITECO y del SEPRONA, mostrándole los tipos de infracciones y rangos de multa más habituales en su sector. Además, mediante el asistente RAG, puede consultar dudas específicas sobre la aplicación de las leyes y obtener resúmenes precisos con la normativa exacta del BOE, además de determinar que requisitos legales que no habían contemplado pueden ser de aplicación para su actividad. 

**Valor para el usuario:** unifica la consulta legal automatizada con el análisis analítico de riesgos, reduciendo la dependencia de costosos informes de consultoría y minimizando el riesgo de sanciones por desconocimiento normativo. Supone un ahorro de tiempo frente a la búsqueda manual. El sistema se centra en la legislación ambiental general de ámbito nacional, facilitando la auditoría preventiva de requisitos legales aplicables.

### Datos
| Fuente | Enlace | Qué aporta | Estado |
| --- | --- | --- | --- |
| API del Boletín Oficial del Estado (BOE) | https://www.boe.es/datosabiertos/api/api.php | Textos íntegros de leyes, reales decretos y normativas ambientales de España para alimentar la base de conocimiento del LLM (RAG) | Confirmado: API pública y gratuita disponible |
| Memorias Estadísticas del MITECO | https://www.datosabiertos.miteco.gob.es/es.html | Métricas e informes de inspección ambiental y expedientes sancionadores resueltos por tipología de norma | Confirmado: informes institucionales públicos y accesibles |
| Memorias Anuales del SEPRONA (Guardia Civil) | https://web.guardiacivil.es/es/institucional/conocenos/especialidades/Medio_ambiente/ | Datos cuantitativos oficiales sobre infracciones medioambientales detectadas, desglosadas por gravedad y normativa | Confirmado: memorias anuales públicas disponibles |
| Estadísticas del INE | https://www.ine.es/dynt3/inebase/index.htm?padre=54&capsel=3920 | Datos demográficos e industriales por sectores económicos (CNAE) para cruzar con las variables de actividad de las empresas | Confirmado: tablas descargables en formato CSV. Pendiente selección de variables sectoriales |

Restricciones de uso y privacidad: los textos del BOE, las estadísticas del MITECO, del SEPRONA y del INE son de dominio público institucional, por lo que su reutilización está permitida citando las fuentes y fechas correspondientes. Los datos operativos específicos introducidos por las empresas para su autoevaluación serán confidenciales, procesados localmente y excluidos por completo del repositorio público de GitHub.

### Primera versión (MVP)
**Incluye:**
1. Selección del sector de la empresa y características operativas de la misma.  
2. Mediante el modelo predictivo, basándose en los datos obtenidos de las estadísticas de las sanciones, clasificará el nivel de riesgo de sanción y, en la medida de lo posible, los riesgos o artículos de ley a vigilar por la empresa por mayor riesgo y probabilidad de incumplimiento. 
3. Los datos se mostrarán en un Dashboard interactivo que visualice los datos de riesgo normativo.
4. Un asistente conversacional (RAG) integrado en la interfaz que responda consultas sobre legislación ambiental citando la normativa oficial del BOE.

**Queda fuera por ahora:** la cobertura de normativas autonómicas o locales específicas de cada comunidad autónoma, y la automatización de trámites administrativos o presentación directa de solicitudes ante la administración.

**Qué mostraríamos funcionando:** el usuario introduce los datos de su actividad; la plataforma le muestra un diagnóstico visual del riesgo sancionador basado en datos oficiales y le permite chatear con un asistente que resuelve sus dudas legales extrayendo la información directamente del BOE.

### Viabilidad y dudas
- Principal incertidumbre: la complejidad técnica asociada al parsing (extracción de datos desde PDFs o informes institucionales) de las tablas estadísticas del SEPRONA y el MITECO para estructurarlas limpiamente en SQL.
- Cómo la comprobaríamos: validar en la Actividad 1 si la muestra de datos extraída de las memorias oficiales genera suficientes registros tabulares limpios y consistentes para alimentar los modelos de Machine Learning y los análisis estadísticos.
- Otras dudas:
  - La variabilidad y el formato no estandarizado de los informes anuales antiguos pueden dificultar la automatización completa de la ingesta (Actividad 7), lo cual se resolverá acotando el rango temporal de los datos analizados a los años más recientes y homogéneos.


## Preferencia del equipo (opcional)
...
