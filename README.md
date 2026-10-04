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

El símbolo $\overset{d}{=}$ indica que ambos vectores tienen la misma distribución conjunta. Aquí, $m$ es el número de observaciones consideradas, no el orden de un momento estadístico. Esto no significa que los valores observados sean iguales, sino que su comportamiento probabilístico no depende de cuándo se observen.

En muchas aplicaciones se utiliza una condición menos exigente, llamada **estacionariedad débil** o **de segundo orden**: la media y la varianza son constantes en el tiempo, y la covarianza entre dos observaciones depende solo de la distancia temporal entre ellas. En el análisis de frecuencia hidrológico clásico suele suponerse, de manera más general, que la distribución de los caudales máximos se mantiene estable durante el período analizado. La estacionariedad no implica independencia: una serie puede conservar estas propiedades y aun así presentar dependencia entre observaciones.

Los cambios en una distribución pueden describirse observando sus momentos estadísticos:

- **Primer momento:** media.
- **Segundo momento central:** varianza.
- **Tercer momento estandarizado:** asimetría.
- **Cuarto momento estandarizado:** curtosis.

Por ejemplo, si los caudales anuales pasan de fluctuar alrededor de 100 m³/s a hacerlo alrededor de 130 m³/s, la media ha cambiado; esto indica no estacionariedad en la media. Si, además, los caudales comienzan a mostrar una dispersión mayor, también ha cambiado la varianza, lo que indica no estacionariedad en la varianza. Cambios en la asimetría o la curtosis reflejarían modificaciones en otros aspectos de la forma de la distribución. Estas variaciones pueden estar asociadas, entre otros factores, al cambio climático o a cambios en el uso del suelo, pero su causa debe evaluarse con datos y análisis específicos.

En algunos contextos se habla de no estacionariedad de distinto orden para referirse a los momentos estadísticos afectados. Sin embargo, expresiones como “estacionariedad de segundo orden” también tienen un significado técnico específico, relacionado con la media y la covarianza. Para evitar ambigüedades, aquí es preferible indicar directamente si cambia la media, la varianza, la asimetría u otra característica estadística.


