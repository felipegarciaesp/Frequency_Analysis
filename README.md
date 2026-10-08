# Frequency Analysis

Código para realizar análisis de frecuencia de datos hidrológicos y notas de estudio relacionadas.

**Autor:** Felipe García  
**Correo:** [felipegarcia.esp@gmail.com](mailto:felipegarcia.esp@gmail.com)

## Notas respecto al análisis de frecuencia

### Referencias

1. Stowhas, Ludwig. *Fundamentos de Hidrología Aplicada*.
2. Searcy, J., Hardison, C. H. y Langbein, W. B. (1960). *Double-mass curves, with a section fitting curves to cyclic data*. U.S. Geological Survey, Water-Supply Paper 1541-B. [https://doi.org/10.3133/wsp1541B](https://doi.org/10.3133/wsp1541B).

### 1 Introducción

#### Estadística de variables hidrológicas

Se refiere al estudio estadístico de mediciones o registros de variables hidrológicas, como la evaporación, la precipitación y la escorrentía, entre otras series de tiempo.

#### Variables aleatorias

Una variable se considera aleatoria cuando no se conoce de manera determinista la magnitud que alcanzará en un instante o período de tiempo determinado. En hidrología, los registros de variables hidrológicas suelen modelarse como realizaciones de variables aleatorias debido a la incertidumbre asociada con su ocurrencia y magnitud.

#### Técnica del análisis de frecuencia

Es una herramienta de la estadística y de la teoría de probabilidades que permite determinar, de manera fundamentada, las magnitudes de diseño que deben adoptarse. Esta técnica estima la probabilidad de ocurrencia o de repetición de eventos hidrológicos futuros mediante la aplicación de modelos probabilísticos.

#### Serie de tiempo

Una serie de tiempo es un conjunto finito de observaciones de una variable, registradas secuencialmente y ordenadas de acuerdo con el tiempo. Desde el punto de vista estadístico, estas observaciones pueden interpretarse como una muestra finita de un proceso aleatorio o de una población de valores potencialmente mucho más amplia.

### 2 Tratamiento de Datos Hidrológicos para el Análisis de Frecuencia

Para que una serie de datos pueda ser tratada estadística y probabilísticamente, debe cumplir, idealmente, con las siguientes condiciones:

- Ser una muestra aleatoria y representativa de la población de la cual proviene.
- Contener valores homogéneos e independientes.
- Para aplicar métodos clásicos de análisis de frecuencia, suele suponerse que la serie es estacionaria.

**Una muestra será más representativa de la población a medida que aumente el número de datos disponibles. En general, se estima que se requiere una serie de al menos 30 años de longitud para lograr una representatividad adecuada. Sin embargo, esta referencia puede variar según la variable hidrológica estudiada, la calidad de los datos y el objetivo del análisis. Conviene extender estadísticas demasiado cortas antes de realizar análisis de frecuencia.**

En el análisis de frecuencia, la validez de los resultados depende tanto de la representatividad de los datos como de que se evalúen ciertos supuestos sobre su comportamiento. Entre ellos se encuentran la aleatoriedad, la homogeneidad, la independencia y la estacionariedad. Estos conceptos están relacionados, pero describen propiedades distintas; su importancia depende del método utilizado y de las características de la serie analizada.

#### Homogeneidad

En este contexto, una serie es homogénea cuando sus observaciones son comparables a lo largo del período analizado y pueden considerarse parte de una misma población o proceso, sin cambios no considerados que alteren la forma en que se generan o miden los datos. Cambios en la ubicación de una estación, los instrumentos o los procedimientos de medición pueden introducir discontinuidades en el registro. También pueden ocurrir cambios reales en el régimen hidrológico; estos deben analizarse, pues pueden afectar la estacionariedad de la serie.

Para revisar la consistencia de un registro puede utilizarse el método de la curva doble acumulada, que compara los valores acumulados de una estación con los de una serie de referencia construida a partir de estaciones cercanas. Un cambio en la pendiente puede señalar un cambio en la relación entre ambos registros y justificar una revisión de los datos y de sus metadatos. Sin embargo, este método es una herramienta de diagnóstico: por sí solo no demuestra que la serie sea homogénea ni identifica necesariamente la causa de una discontinuidad ([Searcy, Hardison y Langbein, 1960, USGS](https://pubs.usgs.gov/publication/wsp1541B)).

#### Independencia

Dos observaciones son independientes cuando conocer el valor de una no aporta información sobre el valor de la otra. En una serie temporal, esta condición puede verse afectada por dependencias espaciales o temporales, aunque su evaluación depende del tipo de análisis.

- **Dependencia espacial:** dos pluviógrafos cercanos pueden registrar precipitaciones correlacionadas porque están expuestos a los mismos sistemas meteorológicos. Esto no significa que midan exactamente lo mismo, pues cada estación representa una ubicación distinta. (De acuerdo con la Ref. 1, cuando se presenta esta dependencia, las observaciones deberán considerarse como un solo dato para el análisis.)
- **Dependencia temporal:** dos crecidas consecutivas pueden corresponder al mismo episodio meteorológico o estar relacionadas porque las condiciones de la cuenca tras la primera crecida influyen en la respuesta a la siguiente. En ese caso, los picos pueden no ser independientes. (De acuerdo con la Ref. 1, cuando se presenta esta dependencia, los valores deberán considerarse como un solo dato para el análisis.) La identificación de eventos dependientes debe realizarse según el criterio hidrológico y el método de análisis utilizados; por ejemplo, los análisis de máximos anuales consideran un máximo por año.

#### Estacionariedad

Una forma precisa de expresar la estacionariedad es mediante la invariancia ante desplazamientos del origen del tiempo. Si $X_t$ representa el caudal en el instante $t$, un proceso es **estrictamente estacionario** cuando, para cualquier número $m$ de observaciones, cualquier conjunto de instantes $t_1, t_2, \ldots, t_m$ y cualquier desplazamiento temporal $k$, se cumple que:

$$
(X_{t_1}, X_{t_2}, \ldots, X_{t_m}) \overset{d}{=} (X_{t_1+k}, X_{t_2+k}, \ldots, X_{t_m+k})
$$

El símbolo $\overset{d}{=}$ significa que ambos grupos tienen el mismo patrón probabilístico. En sencillo: si observamos los caudales de tres años seguidos, la forma en que se combinan valores altos y bajos debería tener las mismas probabilidades al observar otros tres años. Esto no significa que los caudales sean idénticos, sino que ese patrón no cambia al desplazar el período en el tiempo. En la fórmula, $m$ solo indica cuántas observaciones se comparan.

Los cambios en una distribución pueden describirse observando sus momentos estadísticos:

- **Primer momento:** media.
- **Segundo momento central:** varianza.
- **Tercer momento estandarizado:** asimetría.
- **Cuarto momento estandarizado:** curtosis.

Por ejemplo, si los caudales anuales pasan de fluctuar alrededor de 100 m³/s a hacerlo alrededor de 130 m³/s, la media ha cambiado; esto indica no estacionariedad en la media. Si, además, los caudales comienzan a mostrar una dispersión mayor, también ha cambiado la varianza, lo que indica no estacionariedad en la varianza. Cambios en la asimetría o la curtosis reflejarían modificaciones en otros aspectos de la forma de la distribución. Estas variaciones pueden estar asociadas, entre otros factores, al cambio climático o a cambios en el uso del suelo, pero su causa debe evaluarse con datos y análisis específicos.

En algunos contextos se habla de no estacionariedad de distinto orden para referirse a los momentos estadísticos afectados. Sin embargo, expresiones como “estacionariedad de segundo orden” también tienen un significado técnico específico, relacionado con la media y la covarianza. Para evitar ambigüedades, aquí es preferible indicar directamente si cambia la media, la varianza, la asimetría u otra característica estadística.

#### Procesos no estacionarios en la media

Los procesos no estacionarios más comunes que afectan al promedio de la serie son los de **tendencia**, **periodicidad** y **persistencia**.

##### Tendencia

Existe tendencia en una serie cuando el promedio móvil de sus características o parámetros muestra una variación sostenida, ya sea creciente o decreciente, en el tiempo. Por ejemplo, una serie de caudales anuales que exhibe una disminución progresiva asociada a un aumento sostenido de las extracciones de agua en la cuenca, o una serie de temperaturas que muestra un incremento gradual atribuible al cambio climático.

##### Periodicidad

La periodicidad es una característica intrínseca de muchas variables hidrológicas, ya que estas quedan sujetas a los ciclos climatológicos diurnos y anuales, habiéndose sugerido además la existencia de otros ciclos de período mayor. Por ejemplo, los caudales de un río de régimen nival presentan un ciclo anual marcado, con valores altos en los meses de deshielo y valores bajos en invierno; de manera similar, la evaporación diaria sigue un ciclo asociado a la radiación solar a lo largo del día.

##### Persistencia

La persistencia es la tendencia de algunas variables aleatorias a mantenerse sostenidamente en valores similares a los que las han precedido. Por ejemplo, en una serie de niveles de un embalse o de humedad de suelo, un valor alto en un período tiende a ir seguido de valores también altos en los períodos siguientes, reflejando la memoria o inercia del sistema hidrológico.

#### Detección y tratamiento

Se deben aplicar procedimientos y tests estadísticos para detectar la presencia de procesos no estacionarios. Si se detectan, **deben ser eliminados de la serie antes de someterla a análisis de frecuencia**.

> [!NOTE]
> ### ¿Cómo se maneja la periodicidad en la práctica, si es casi inherente a toda variable hidrológica?
>
> La periodicidad responde a ciclos físicos reales (estacionalidad climática, ciclo diario de radiación, etc.), por lo que no se "elimina" dato a dato como una tendencia espuria. En su lugar, se **controla mediante el diseño de la serie** que se somete al análisis de frecuencia:
>
> - **Trabajar con un valor por ciclo (lo más común):** extraer, por ejemplo, el **máximo anual** (crecidas), el **mínimo anual** (estiajes/sequías) o el **promedio anual**, según el fenómeno de interés. Al tomar un solo valor representativo por año, el ciclo intra-anual queda fuera de la serie resultante, y esta puede tratarse razonablemente como estacionaria frente al ciclo estacional.
> - **Trabajar por sub-período homogéneo:** analizar cada mes o estación del año por separado (por ejemplo, los caudales de enero de todos los años), evitando mezclar datos de ciclos distintos en una sola distribución.
> - **Remover el ciclo explícitamente:** ajustar un modelo del ciclo estacional (medias y desviaciones mensuales) y trabajar con las anomalías o residuos, o usar modelos tipo SARIMA. Esto es más propio del análisis de series de tiempo que del análisis de frecuencia clásico, pero es una alternativa si se requiere usar datos sub-anuales directamente.
>
> En resumen, no es necesario eliminar la periodicidad dato a dato: se elige una ventana de agregación (anual, mensual, estacional) que haga que deje de ser un factor dentro de la serie analizada. La elección entre máximo anual, mínimo anual o promedio anual depende del objetivo del estudio (diseño de obras de crecida → máximos; estudios de sequía o caudal ecológico → mínimos o promedios).

> [!NOTE]
> ### ¿Qué hacer si se detecta tendencia en la serie?
>
> Si un test estadístico (por ejemplo, Mann-Kendall, Spearman o una regresión lineal con test de significancia de la pendiente) confirma una tendencia significativa, las alternativas típicas son:
>
> 1. **Investigar y corregir la causa, si es antrópica y cuantificable:** por ejemplo, si la tendencia en caudales se debe a extracciones crecientes conocidas, se puede reconstruir una serie "naturalizada" (sumando de vuelta las extracciones a cada año) para obtener una serie más homogénea y estacionaria, representativa del régimen natural de la cuenca.
> 2. **Remover la tendencia (*detrending*):** ajustar una función de tendencia (lineal, polinómica, etc.) y trabajar con los **residuos** (serie menos tendencia). Esto estabiliza la media, pero complica la interpretación de los resultados, ya que luego hay que reincorporar la tendencia al resultado final (por ejemplo, proyectar el valor de diseño al año de interés sumando la tendencia estimada para ese año).
> 3. **Segmentar la serie:** si la tendencia refleja un cambio de régimen (por ejemplo, un antes y un después de la construcción de un embalse o un cambio abrupto de uso de suelo), puede ser más apropiado dividir la serie en dos períodos y analizar solo el más reciente y relevante para las condiciones actuales o futuras, en vez de forzar a toda la serie a ser estacionaria.
> 4. **Usar métodos no estacionarios (enfoque más moderno):** en vez de eliminar la tendencia, modelar directamente permitiendo que los parámetros de la distribución (p. ej. la media) varíen en el tiempo o en función de una covariable (como el año o un índice climático). Esto es lo que se conoce como **análisis de frecuencia no estacionario**, cada vez más usado en contextos de cambio climático, aunque requiere supuestos y metodologías adicionales respecto al AF clásico.
>
> En la práctica más tradicional, lo usual es detectar la causa, corregir o naturalizar la serie si es posible, y si no, remover la tendencia (*detrending*) antes del análisis de frecuencia, dejando el enfoque no estacionario como una alternativa más avanzada.



