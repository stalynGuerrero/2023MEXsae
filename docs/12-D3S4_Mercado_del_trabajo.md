# Día 3 - Sesión 4- Modelo de área para estadísticas del mercado de trabajo




La Encuesta Nacional de Ingresos y Gastos de los Hogares (ENIGH) 2020 es una encuesta representativa a nivel nacional que recopila información sobre los ingresos, gastos, características sociodemográficas y acceso a servicios de los hogares mexicanos. La encuesta se realizó del 27 de octubre al 30 de diciembre de 2020 y contó con una muestra de aproximadamente 100,000 viviendas.

La ENIGH recopila una amplia variedad de datos relacionados con el empleo en los hogares mexicanos. Algunos de los resultados y análisis asociados al empleo que se pueden derivar de la ENIGH incluyen:

  -   *Tasa de empleo*: Proporciona una estimación de la proporción de la población económicamente activa que está empleada.

  -   *Ingresos laborales*: La encuesta recopila información sobre los ingresos derivados del trabajo, incluidos salarios, sueldos, bonificaciones y otras compensaciones laborales.

  -   *Desempleo*: La ENIGH también puede proporcionar datos sobre la tasa de desempleo, que mide la proporción de la población económicamente activa que no tiene empleo y está buscando activamente trabajo.


## Definición del modelo multinomial

-   Sea $K$ el número de categorías de la variable de interés $𝑌\sim multinimial\left(\boldsymbol{\theta}\right)$, con $\boldsymbol{\theta}=\left(p_{1},p_{2},\dots ,p_{k}\right)$ y $\sum_{k=1}^{K}p_{k}=1$.

-   Sea $N_i$ el número de elementos en el i-ésiamo dominio y $N_{ik}$ el número de elementos que tienen la k-ésima categoría, note que $\sum_{k=1}^{K}N_{ik}=N_{i}$ y $p_{ik}=\frac{N_{ik}}{N_{i}}$.

-   Sea $\hat{p}_{ik}$ la estimación directa de $p_{ik}$ y $v_{ik}=Var\left(\hat{p}_{ik}\right)$ y denote el estimador de la varianza por $\hat{v}_{ik}=\widehat{Var}\left(\hat{p}_{ik}\right)$


Note que el efecto diseño cambia entre categoría, por tanto, lo primero será definir el tamaño de muestra efectivo por categoría. Esto es:

La estimación de $\tilde{n}$ esta dado por $\tilde{n}_{ik} = \frac{(\tilde{p}_{ik}\times(1-\tilde{p}_{ik}))}{\hat{v}_{ik}},$

$\tilde{y}_{ik}=\tilde{n}_{ik}\times\hat{p}_{ik}$

luego, $\hat{n}_{i} = \sum_{k=1}^{K}\tilde{y}_{ik}$

de donde se sigue que $\hat{y}_{ik} = \hat{n}_i\times \hat{p}_{ik}$


Sea $\boldsymbol{\theta}=\left(p_{1},p_{2}, p_{3}\right)^{T}=\left(\frac{N_{i1}}{N_{i}},\frac{N_{i2}}{N_{i}}\frac{N_{i3}}{N_{i}}\right)^{T}$, entonces el modelo multinomial para el i-ésimo dominio estaría dado por:

$$
\left(\tilde{y}_{i1},\tilde{y}_{i2},\tilde{y}_{i3}\right)\mid\hat{n}_{i},\boldsymbol{\theta}_{i}\sim multinomial\left(\hat{n}_{i},\boldsymbol{\theta}_{i}\right)
$$ 
Ahora, puede escribir $p_{ik}$ como :

$\ln\left(\frac{p_{i2}}{p_{i1}}\right)=\boldsymbol{X}_{i}^{T}\beta_{2} + u_{i2}$ y
$\ln\left(\frac{p_{i3}}{p_{i1}}\right)=\boldsymbol{X}_{i}^{T}\beta_{3}+ u_{i3}$



Dada la restricción $1 = p_{i1} + p_{i2} + p_{i3}$ entonces 
$$p_{i1} + p_{i1}(e^{\boldsymbol{X}_{i}^{T}\boldsymbol{\beta_{2}}}+  u_{i2})+p_{i1}(e^{\boldsymbol{X}_{i}^{T}\boldsymbol{\beta}_{3}} + u_{i3})$$ de donde se sigue que 

$$
p_{i1}=\frac{1}{1+e^{\boldsymbol{X}_{i}^{T}\boldsymbol{\beta_{2}}}+ u_{i2}+e^{\boldsymbol{X_{i}}^{T}\boldsymbol{\beta_{3}}}+ u_{i3}}
$$

Las expresiones para $p_{i2}$ y $p_{i3}$ estarían dadas por: 

$$
p_{i2}=\frac{e^{\boldsymbol{X}_{i}^{T}\boldsymbol{\beta}_{2}} + u_{i2}}{1+e^{\boldsymbol{X}_{i}^{T}\boldsymbol{\beta_{2}}}+ u_{i2}+e^{\boldsymbol{X_{i}}^{T}\boldsymbol{\beta_{3}}}+ u_{i3}}
$$

$$
p_{i3}=\frac{e^{\boldsymbol{X}_{i}^{T}\boldsymbol{\beta}_{3}}+ u_{i3}}{1+e^{\boldsymbol{X}_{i}^{T}\boldsymbol{\beta_{2}}}+ u_{i2}+e^{\boldsymbol{X_{i}}^{T}\boldsymbol{\beta_{3}}}+ u_{i3}}
$$

## Lectura de librerías.

  -   La librería `survey` es una herramienta de análisis estadístico en R que permite trabajar con datos de encuestas complejas, como las encuestas estratificadas, multietápicas o con pesos de muestreo. Ofrece funciones para estimación de parámetros, diseño de muestras, análisis de varianza y regresión, y cálculo de errores estándar.

  -   La librería `tidyverse` es un conjunto de paquetes de R que se utilizan para la manipulación y visualización de datos. Incluye las librerías `dplyr`, `ggplot2`, `tidyr` y otras, y se caracteriza por su enfoque en la programación `tidy` o ordenada, que facilita la exploración y análisis de datos.

  -   La librería `srvyr` es una extensión de la librería `survey` que permite integrar las funciones de `survey` con la sintaxis de `dplyr`, lo que facilita la manipulación de datos de encuestas complejas. Incluye funciones para agrupar, filtrar y resumir datos de encuestas utilizando la sintaxis `tidy`.

  -   La librería `TeachingSampling` es una herramienta de R que se utiliza para la enseñanza de métodos de muestreo estadístico. Incluye funciones para simular diferentes tipos de muestras, estimar parámetros, calcular errores estándar y construir intervalos de confianza, entre otras.

  -   La librería `haven` es una herramienta de R que permite importar y exportar datos en diferentes formatos, incluyendo SPSS, Stata y SAS. Permite trabajar con archivos de datos de encuestas, y ofrece funciones para etiquetar variables, codificar datos faltantes y convertir datos de diferentes formatos.

  -   La librería `bayesplot` es una herramienta de R que se utiliza para la visualización y diagnóstico de modelos Bayesianos. Incluye funciones para graficar distribuciones posteriores, diagnósticos de convergencia, gráficos de diagnóstico de residuos, y otros tipos de gráficos relacionados con el análisis Bayesianos.

  -   La librería `patchwork` es una herramienta de R que permite unir gráficos de manera sencilla y flexible. Esta librería facilita la creación de gráficos complejos al permitir la combinación de múltiples gráficos en una sola visualización, lo que resulta especialmente útil en análisis de datos y modelización.

  -   La librería `stringr` es una herramienta de R que se utiliza para la manipulación de cadenas de texto. Incluye funciones para la extracción, manipulación y modificación de cadenas de texto, lo que resulta especialmente útil en la limpieza y preparación de datos antes de su análisis.

  -   La librería `rstan` es una herramienta de R que se utiliza para la estimación de modelos Bayesianos mediante el método de cadenas de Markov Monte Carlo (MCMC). Esta librería permite la especificación y estimación de modelos complejos mediante un lenguaje sencillo y flexible, y ofrece diversas herramientas para el diagnóstico y visualización de resultados.


```r
library(survey)
library(tidyverse)
library(srvyr)
library(TeachingSampling)
library(haven)
library(bayesplot)
library(patchwork)
library(stringr)
library(rstan)
```

## Lectura de la encuesta y estimaciones directas 

En la primera línea se carga la encuesta desde un archivo RDS y se guarda en un objeto llamado `encuesta`. La segunda línea utiliza la función `transmute()` de la librería `dplyr` para seleccionar las variables de interés en la encuesta y crear nuevas variables a partir de ellas. Luego, se utiliza la variable `id_dominio` para identificar el dominio de estudio. En conjunto, estos pasos son fundamentales para preparar los datos de la encuesta para su posterior estimación del parámetro.



```r
encuesta <- readRDS('Recursos/Día3/Sesion4/Data/encuesta_empleo.rds')
## 
length_upm <- max(nchar(encuesta[["upm"]]))
length_estrato <- max(nchar(encuesta[["estrato"]]))

encuesta <-
  encuesta %>%
 transmute(
    dam, dam2,    
    upm = str_pad(string = `upm`, width = length_upm, pad = "0"),
    estrato = str_pad(string = `estrato`, width = length_estrato , pad = "0"),
    fep = `fep`, 
    empleo
  )
id_dominio <- "dam2"
```

El código presentado define el diseño muestral para el análisis de la encuesta "encuesta" en R. La primera línea establece una opción para el tratamiento de las PSU (unidades primarias de muestreo) solitarias, lo que indica que se deben aplicar ajustes en el cálculo de los errores estándar. La segunda línea utiliza la función "as_survey_design" de la librería "survey" para definir el diseño muestral. La función toma como argumentos la variable "encuesta" y los siguientes parámetros:

  -   `strata`: la variable que define las estratas de muestreo en la encuesta, en este caso la variable "estrato".

  -   `ids`: la variable que identifica las PSU en la encuesta, en este caso la variable "upm".

  -   `weights`: la variable que indica los pesos muestrales de cada observación, en este caso la variable "fep".

  -   `nest`: un parámetro lógico que indica si los datos de la encuesta están anidados o no. En este caso, se establece en "TRUE" porque los datos están anidados por dominio.
  
En conjunto, estos pasos permiten definir un diseño muestral que tenga en cuenta las características del muestreo y los pesos asignados a cada observación en la encuesta, lo que es necesario para obtener estimaciones precisas y representativas de los parámetros de interés.


```r
options(survey.lonely.psu= 'adjust' )
diseno <- encuesta %>%
  as_survey_design(
    strata = estrato,
    ids = upm,
    weights = fep,
    nest=T
  )
```

El código presentado es una operación que se realiza en el diseño muestral definido en el código anterior, con el objetivo de obtener un indicador del empleo por dominio. La primera línea define un objeto llamado "indicador_dam". En la segunda línea, se agrupa el diseño muestral según el dominio especificado en la variable "id_dominio". La tercera línea filtra los datos para quedarse con los individuos que tienen empleo (empleo igual a 1), están desempleados (empleo igual a 2) o son inactivos (empleo igual a 3).

A partir de la cuarta línea, se utilizan las funciones "summarise" y "survey_mean" para calcular las estadísticas descriptivas de interés. En particular, se calculan el número de personas ocupadas, desocupadas e inactivas en cada dominio, y la proporción de personas en cada una de estas categorías. La función "survey_mean" se utiliza para calcular la proporción de personas en cada una de estas categorías con sus respectivos errores estándar y efecto de diseño.


```r
indicador_dam <-
  diseno %>% group_by_at(id_dominio) %>% 
  filter(empleo %in% c(1:3)) %>%
  summarise(
    n_ocupado = unweighted(sum(empleo == 1)),
    n_desocupado = unweighted(sum(empleo == 2)),
    n_inactivo = unweighted(sum(empleo == 3)),
    Ocupado = survey_mean(empleo == 1,
      vartype = c("se",  "var"),
      deff = T
    ),
    Desocupado = survey_mean(empleo == 2,
                          vartype = c("se",  "var"),
                          deff = T
    ),
    Inactivo = survey_mean(empleo == 3,
                          vartype = c("se",  "var"),
                          deff = T
    )
  )
```

## Selección de dominios 

En la sección anterior, se llevó a cabo una estimación directa para cada categoría individualmente en cada municipio (dominio) presente en la muestra. Ahora, para evaluar la calidad de los resultados obtenidos. Se emplean varias medidas de calidad, entre ellas, se cuenta el número de dominios que tienen tres o más unidades primarias de muestreo (UPM), así como el efecto de diseño mayor a 0.7 el alguna de las categorías y las varianzas mayores a 0. Estas medidas nos permitirán determinar la fiabilidad de nuestros resultados y tomar decisiones informadas en función de ellos.

Después de realizar las validaciones anteriores se establece como regla incluir en el estudio los dominios que posean 

  - Tres o más UPM por dominio. 
  
  - Varianzas estimadas mayor a cero. 
  
  - Contar con un resultado en el efecto de diseño mayor a 0.7 en por lo menos una categoría.  


```r
indicador_dam <- encuesta %>% select(id_dominio, upm) %>%
  distinct() %>%
  group_by_at(id_dominio) %>%
  tally(name = "n_upm") %>%
  inner_join(indicador_dam, by = id_dominio)

saveRDS(indicador_dam,
        "Recursos/Día3/Sesion4/Data/indicador_dam.rds")

indicador_dam1 <- indicador_dam %>%
  filter(
    n_upm >= 3,
    Desocupado_var > 0,
    Ocupado_var > 0,
    Inactivo_var > 0,
    Desocupado_deff > 0.7 |
      Ocupado_deff > 0.7 |
      Inactivo_deff > 0.7
  ) %>%
  mutate(id_orden = 1:n())
saveRDS(object = indicador_dam1, "Recursos/Día3/Sesion4/Data/base_modelo.Rds")
```

<table class="table table-striped lightable-classic" style="width: auto !important; margin-left: auto; margin-right: auto; font-family: Arial Narrow; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> dam2 </th>
   <th style="text-align:right;"> n_upm </th>
   <th style="text-align:right;"> n_ocupado </th>
   <th style="text-align:right;"> n_desocupado </th>
   <th style="text-align:right;"> n_inactivo </th>
   <th style="text-align:right;"> Ocupado </th>
   <th style="text-align:right;"> Ocupado_se </th>
   <th style="text-align:right;"> Ocupado_var </th>
   <th style="text-align:right;"> Ocupado_deff </th>
   <th style="text-align:right;"> Desocupado </th>
   <th style="text-align:right;"> Desocupado_se </th>
   <th style="text-align:right;"> Desocupado_var </th>
   <th style="text-align:right;"> Desocupado_deff </th>
   <th style="text-align:right;"> Inactivo </th>
   <th style="text-align:right;"> Inactivo_se </th>
   <th style="text-align:right;"> Inactivo_var </th>
   <th style="text-align:right;"> Inactivo_deff </th>
   <th style="text-align:right;"> id_orden </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 01001 </td>
   <td style="text-align:right;"> 274 </td>
   <td style="text-align:right;"> 2560 </td>
   <td style="text-align:right;"> 151 </td>
   <td style="text-align:right;"> 1609 </td>
   <td style="text-align:right;"> 0.5927 </td>
   <td style="text-align:right;"> 0.0082 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 1.2035 </td>
   <td style="text-align:right;"> 0.0361 </td>
   <td style="text-align:right;"> 0.0032 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 1.3006 </td>
   <td style="text-align:right;"> 0.3712 </td>
   <td style="text-align:right;"> 0.0079 </td>
   <td style="text-align:right;"> 0.0001 </td>
   <td style="text-align:right;"> 1.1630 </td>
   <td style="text-align:right;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01003 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 238 </td>
   <td style="text-align:right;"> 18 </td>
   <td style="text-align:right;"> 194 </td>
   <td style="text-align:right;"> 0.5399 </td>
   <td style="text-align:right;"> 0.0158 </td>
   <td style="text-align:right;"> 2e-04 </td>
   <td style="text-align:right;"> 0.4575 </td>
   <td style="text-align:right;"> 0.0362 </td>
   <td style="text-align:right;"> 0.0075 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 0.7328 </td>
   <td style="text-align:right;"> 0.4239 </td>
   <td style="text-align:right;"> 0.0138 </td>
   <td style="text-align:right;"> 0.0002 </td>
   <td style="text-align:right;"> 0.3554 </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01005 </td>
   <td style="text-align:right;"> 27 </td>
   <td style="text-align:right;"> 619 </td>
   <td style="text-align:right;"> 25 </td>
   <td style="text-align:right;"> 298 </td>
   <td style="text-align:right;"> 0.6365 </td>
   <td style="text-align:right;"> 0.0182 </td>
   <td style="text-align:right;"> 3e-04 </td>
   <td style="text-align:right;"> 1.3637 </td>
   <td style="text-align:right;"> 0.0352 </td>
   <td style="text-align:right;"> 0.0077 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 1.6567 </td>
   <td style="text-align:right;"> 0.3283 </td>
   <td style="text-align:right;"> 0.0157 </td>
   <td style="text-align:right;"> 0.0002 </td>
   <td style="text-align:right;"> 1.0603 </td>
   <td style="text-align:right;"> 3 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01006 </td>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:right;"> 273 </td>
   <td style="text-align:right;"> 14 </td>
   <td style="text-align:right;"> 194 </td>
   <td style="text-align:right;"> 0.5801 </td>
   <td style="text-align:right;"> 0.0200 </td>
   <td style="text-align:right;"> 4e-04 </td>
   <td style="text-align:right;"> 0.7957 </td>
   <td style="text-align:right;"> 0.0264 </td>
   <td style="text-align:right;"> 0.0056 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 0.5836 </td>
   <td style="text-align:right;"> 0.3935 </td>
   <td style="text-align:right;"> 0.0180 </td>
   <td style="text-align:right;"> 0.0003 </td>
   <td style="text-align:right;"> 0.6536 </td>
   <td style="text-align:right;"> 4 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01007 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 334 </td>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:right;"> 225 </td>
   <td style="text-align:right;"> 0.6132 </td>
   <td style="text-align:right;"> 0.0312 </td>
   <td style="text-align:right;"> 1e-03 </td>
   <td style="text-align:right;"> 2.3457 </td>
   <td style="text-align:right;"> 0.0155 </td>
   <td style="text-align:right;"> 0.0059 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 1.3093 </td>
   <td style="text-align:right;"> 0.3714 </td>
   <td style="text-align:right;"> 0.0300 </td>
   <td style="text-align:right;"> 0.0009 </td>
   <td style="text-align:right;"> 2.2054 </td>
   <td style="text-align:right;"> 5 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01011 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 324 </td>
   <td style="text-align:right;"> 17 </td>
   <td style="text-align:right;"> 177 </td>
   <td style="text-align:right;"> 0.6359 </td>
   <td style="text-align:right;"> 0.0290 </td>
   <td style="text-align:right;"> 8e-04 </td>
   <td style="text-align:right;"> 1.9003 </td>
   <td style="text-align:right;"> 0.0298 </td>
   <td style="text-align:right;"> 0.0074 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 0.9842 </td>
   <td style="text-align:right;"> 0.3343 </td>
   <td style="text-align:right;"> 0.0319 </td>
   <td style="text-align:right;"> 0.0010 </td>
   <td style="text-align:right;"> 2.3912 </td>
   <td style="text-align:right;"> 6 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02001 </td>
   <td style="text-align:right;"> 73 </td>
   <td style="text-align:right;"> 1359 </td>
   <td style="text-align:right;"> 55 </td>
   <td style="text-align:right;"> 979 </td>
   <td style="text-align:right;"> 0.5488 </td>
   <td style="text-align:right;"> 0.0190 </td>
   <td style="text-align:right;"> 4e-04 </td>
   <td style="text-align:right;"> 3.5128 </td>
   <td style="text-align:right;"> 0.0230 </td>
   <td style="text-align:right;"> 0.0050 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 2.6845 </td>
   <td style="text-align:right;"> 0.4282 </td>
   <td style="text-align:right;"> 0.0181 </td>
   <td style="text-align:right;"> 0.0003 </td>
   <td style="text-align:right;"> 3.2195 </td>
   <td style="text-align:right;"> 7 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02002 </td>
   <td style="text-align:right;"> 141 </td>
   <td style="text-align:right;"> 2014 </td>
   <td style="text-align:right;"> 93 </td>
   <td style="text-align:right;"> 1644 </td>
   <td style="text-align:right;"> 0.5537 </td>
   <td style="text-align:right;"> 0.0113 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 1.9590 </td>
   <td style="text-align:right;"> 0.0221 </td>
   <td style="text-align:right;"> 0.0039 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 2.6821 </td>
   <td style="text-align:right;"> 0.4242 </td>
   <td style="text-align:right;"> 0.0110 </td>
   <td style="text-align:right;"> 0.0001 </td>
   <td style="text-align:right;"> 1.8694 </td>
   <td style="text-align:right;"> 8 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02003 </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:right;"> 519 </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:right;"> 379 </td>
   <td style="text-align:right;"> 0.5640 </td>
   <td style="text-align:right;"> 0.0293 </td>
   <td style="text-align:right;"> 9e-04 </td>
   <td style="text-align:right;"> 3.2058 </td>
   <td style="text-align:right;"> 0.0188 </td>
   <td style="text-align:right;"> 0.0072 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 2.5963 </td>
   <td style="text-align:right;"> 0.4172 </td>
   <td style="text-align:right;"> 0.0361 </td>
   <td style="text-align:right;"> 0.0013 </td>
   <td style="text-align:right;"> 4.9275 </td>
   <td style="text-align:right;"> 9 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02004 </td>
   <td style="text-align:right;"> 197 </td>
   <td style="text-align:right;"> 2077 </td>
   <td style="text-align:right;"> 116 </td>
   <td style="text-align:right;"> 1531 </td>
   <td style="text-align:right;"> 0.5577 </td>
   <td style="text-align:right;"> 0.0101 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 1.5357 </td>
   <td style="text-align:right;"> 0.0327 </td>
   <td style="text-align:right;"> 0.0041 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 1.9601 </td>
   <td style="text-align:right;"> 0.4096 </td>
   <td style="text-align:right;"> 0.0098 </td>
   <td style="text-align:right;"> 0.0001 </td>
   <td style="text-align:right;"> 1.4950 </td>
   <td style="text-align:right;"> 10 </td>
  </tr>
</tbody>
</table>

## Modelo programando en `STAN`

El código presenta la implementación de un modelo multinomial logístico de área de respuesta utilizando el lenguaje de programación `STAN`. En este modelo, se asume que la variable de respuesta en cada dominio sigue una distribución multinomial. Se asume que los parámetros que rigen la relación entre las variables predictoras y la variable de respuesta son diferentes en cada dominio y se modelan como efectos aleatorios.

La sección de *functions* define una función auxiliar llamada `pred_theta()`, que se utiliza para predecir los valores de la variable de respuesta en los dominios no observados. La sección de `data` contiene las variables de entrada del modelo, incluyendo el número de dominios, el número de categorías de la variable de respuesta, las estimaciones directas de la variable de respuesta en cada dominio, las covariables observadas en cada dominio y las covariables correspondientes a los dominios no observados.

La sección de *parameters* define los parámetros desconocidos del modelo, incluyendo la matriz de parámetros *beta*, que contiene los coeficientes que relacionan las covariables con la variable de respuesta en cada categoría. También se incluyen los desviaciones estándar de los efectos aleatorios.

En la sección de *transformed parameters* se define el vector de parámetros `theta`, que contiene las probabilidades de pertenencia a cada categoría de la variable de respuesta en cada dominio. Se utilizan los efectos aleatorios para ajustar los valores de `theta` en cada dominio.

En la sección de *model* se define la estructura del modelo y se incluyen las distribuciones a priori para los parámetros desconocidos. En particular, se utiliza una distribución normal para los coeficientes de la matriz beta. Finalmente, se calcula la función de verosimilitud de la distribución multinomial para las estimaciones directas de la variable de respuesta en cada dominio.

La sección de *generated quantities* se utiliza para calcular las predicciones de la variable de respuesta en los dominios no observados utilizando la función auxiliar definida previamente.


```r
functions {
  matrix pred_theta(matrix Xp, int p, matrix beta){
  int D1 = rows(Xp);
  real num1[D1, p];
  real den1[D1];
  matrix[D1,p] theta_p;
  
  for(d in 1:D1){
    num1[d, 1] = 1;
    num1[d, 2] = exp(Xp[d, ] * beta[1, ]' ) ;
    num1[d, 3] = exp(Xp[d, ] * beta[2, ]' ) ;
    
    den1[d] = sum(num1[d, ]);
  }
  
  for(d in 1:D1){
    for(i in 2:p){
    theta_p[d, i] = num1[d, i]/den1[d];
    }
    theta_p[d, 1] = 1/den1[d];
   }

  return theta_p  ;
  }
  
}

data {
  int<lower=1> D; // número de dominios 
  int<lower=1> P; // categorías
  int<lower=1> K; // cantidad de regresores
  int y_tilde[D, P]; // matriz de datos
  matrix[D, K] X_obs; // matriz de covariables
  int<lower=1> D1; // número de dominios 
  matrix[D1, K] X_pred; // matriz de covariables
}
  

parameters {
  matrix[P-1, K] beta;// matriz de parámetros 
  real<lower=0> sigma2_u1;       // random effects standard deviations
  real<lower=0> sigma2_u2;       // random effects standard deviations
  vector[D] u1;
  vector[D] u2;
  // declare L_u to be the Choleski factor of a 2x2 correlation matrix
          
}

transformed parameters {
  simplex[P] theta[D];// vector de parámetros;
  real num[D, P];
  real den[D];
  real<lower=0> sigma_u1;       // random effects standard deviations
  real<lower=0> sigma_u2;       // random effects standard deviations
  sigma_u1 = sqrt(sigma2_u1); 
  sigma_u2 = sqrt(sigma2_u2); 

  for(d in 1:D){
    num[d, 1] = 1;
    num[d, 2] = exp(X_obs[d, ] * beta[1, ]' + u1[d]) ;
    num[d, 3] = exp(X_obs[d, ] * beta[2, ]' + u2[d]) ;
    
    den[d] = sum(num[d, ]);
  }
  
  for(d in 1:D){
    for(p in 2:P){
    theta[d, p] = num[d, p]/den[d];
    }
    theta[d, 1] = 1/den[d];
  }
}

model {
 u1 ~ normal(0, sigma_u1);
 u2 ~ normal(0, sigma_u2);
 sigma2_u1 ~  inv_gamma(0.0001, 0.0001);
 sigma2_u2 ~  inv_gamma(0.0001, 0.0001);
  
  for(p in 2:P){
    for(k in 1:K){
      beta[p-1, k] ~ normal(0, 10000);
    }
    }
  
  for(d in 1:D){
    target += multinomial_lpmf(y_tilde[d, ] | theta[d, ]); 
  }
}

  
generated quantities {
  matrix[D1,P] theta_pred;
  theta_pred = pred_theta(X_pred, P, beta);
}
```

## Preparando insumos para `STAN`

  1.    Lectura y adecuación de covariables
  

```r
statelevel_predictors_df <-
  readRDS('Recursos/Día3/Sesion4/Data/predictors_satelital_dam2.rds') 
head(statelevel_predictors_df,10) %>% tba()
```

<table class="table table-striped lightable-classic" style="width: auto !important; margin-left: auto; margin-right: auto; font-family: Arial Narrow; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> dam </th>
   <th style="text-align:left;"> dam2 </th>
   <th style="text-align:right;"> luces_nocturnas </th>
   <th style="text-align:right;"> suelo_cultivo </th>
   <th style="text-align:right;"> suelo_urbano </th>
   <th style="text-align:right;"> modificacion_humana </th>
   <th style="text-align:right;"> accesibilidad_hospitales </th>
   <th style="text-align:right;"> accesibilidad_hosp_caminado </th>
   <th style="text-align:right;"> area1 </th>
   <th style="text-align:right;"> etnia2 </th>
   <th style="text-align:right;"> sexo2 </th>
   <th style="text-align:right;"> edad2 </th>
   <th style="text-align:right;"> edad3 </th>
   <th style="text-align:right;"> edad4 </th>
   <th style="text-align:right;"> edad5 </th>
   <th style="text-align:right;"> anoest2 </th>
   <th style="text-align:right;"> anoest3 </th>
   <th style="text-align:right;"> anoest4 </th>
   <th style="text-align:right;"> discapacidad1 </th>
   <th style="text-align:right;"> etnia1 </th>
   <th style="text-align:right;"> tiene_sanitario </th>
   <th style="text-align:right;"> tiene_electricidad </th>
   <th style="text-align:right;"> tiene_acueducto </th>
   <th style="text-align:right;"> tiene_gas </th>
   <th style="text-align:right;"> eliminar_basura </th>
   <th style="text-align:right;"> tiene_internet </th>
   <th style="text-align:right;"> piso_tierra </th>
   <th style="text-align:right;"> material_paredes </th>
   <th style="text-align:right;"> material_techo </th>
   <th style="text-align:right;"> rezago_escolar </th>
   <th style="text-align:right;"> alfabeta </th>
   <th style="text-align:right;"> hacinamiento </th>
   <th style="text-align:right;"> tasa_desocupacion </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01001 </td>
   <td style="text-align:right;"> 127.0742 </td>
   <td style="text-align:right;"> 105.4925 </td>
   <td style="text-align:right;"> 128.6893 </td>
   <td style="text-align:right;"> 106.7313 </td>
   <td style="text-align:right;"> 99.2730 </td>
   <td style="text-align:right;"> 99.4086 </td>
   <td style="text-align:right;"> 0.9453 </td>
   <td style="text-align:right;"> 0.0116 </td>
   <td style="text-align:right;"> 0.5180 </td>
   <td style="text-align:right;"> 0.2656 </td>
   <td style="text-align:right;"> 0.2129 </td>
   <td style="text-align:right;"> 0.1962 </td>
   <td style="text-align:right;"> 0.0671 </td>
   <td style="text-align:right;"> 0.2101 </td>
   <td style="text-align:right;"> 0.4280 </td>
   <td style="text-align:right;"> 0.2258 </td>
   <td style="text-align:right;"> 0.0574 </td>
   <td style="text-align:right;"> 0.0595 </td>
   <td style="text-align:right;"> 0.0020 </td>
   <td style="text-align:right;"> 0.3925 </td>
   <td style="text-align:right;"> 0.0303 </td>
   <td style="text-align:right;"> 0.0301 </td>
   <td style="text-align:right;"> 0.0058 </td>
   <td style="text-align:right;"> 0.2946 </td>
   <td style="text-align:right;"> 0.0022 </td>
   <td style="text-align:right;"> 0.0211 </td>
   <td style="text-align:right;"> 0.0098 </td>
   <td style="text-align:right;"> 0.3419 </td>
   <td style="text-align:right;"> 0.0381 </td>
   <td style="text-align:right;"> 0.1690 </td>
   <td style="text-align:right;"> 0.0284 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01002 </td>
   <td style="text-align:right;"> 103.2847 </td>
   <td style="text-align:right;"> 101.3865 </td>
   <td style="text-align:right;"> 101.7692 </td>
   <td style="text-align:right;"> 100.7418 </td>
   <td style="text-align:right;"> 99.2012 </td>
   <td style="text-align:right;"> 99.2972 </td>
   <td style="text-align:right;"> 0.4106 </td>
   <td style="text-align:right;"> 0.0030 </td>
   <td style="text-align:right;"> 0.5082 </td>
   <td style="text-align:right;"> 0.2690 </td>
   <td style="text-align:right;"> 0.1853 </td>
   <td style="text-align:right;"> 0.1703 </td>
   <td style="text-align:right;"> 0.0665 </td>
   <td style="text-align:right;"> 0.3188 </td>
   <td style="text-align:right;"> 0.4404 </td>
   <td style="text-align:right;"> 0.0666 </td>
   <td style="text-align:right;"> 0.0706 </td>
   <td style="text-align:right;"> 0.0318 </td>
   <td style="text-align:right;"> 0.0448 </td>
   <td style="text-align:right;"> 0.5895 </td>
   <td style="text-align:right;"> 0.4913 </td>
   <td style="text-align:right;"> 0.0650 </td>
   <td style="text-align:right;"> 0.1084 </td>
   <td style="text-align:right;"> 0.6548 </td>
   <td style="text-align:right;"> 0.0118 </td>
   <td style="text-align:right;"> 0.2598 </td>
   <td style="text-align:right;"> 0.1648 </td>
   <td style="text-align:right;"> 0.1003 </td>
   <td style="text-align:right;"> 0.0648 </td>
   <td style="text-align:right;"> 0.3137 </td>
   <td style="text-align:right;"> 0.0436 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01003 </td>
   <td style="text-align:right;"> 102.5703 </td>
   <td style="text-align:right;"> 100.2905 </td>
   <td style="text-align:right;"> 100.6374 </td>
   <td style="text-align:right;"> 101.8864 </td>
   <td style="text-align:right;"> 99.4002 </td>
   <td style="text-align:right;"> 99.4182 </td>
   <td style="text-align:right;"> 0.5802 </td>
   <td style="text-align:right;"> 0.0039 </td>
   <td style="text-align:right;"> 0.5117 </td>
   <td style="text-align:right;"> 0.2438 </td>
   <td style="text-align:right;"> 0.1828 </td>
   <td style="text-align:right;"> 0.1920 </td>
   <td style="text-align:right;"> 0.0990 </td>
   <td style="text-align:right;"> 0.3647 </td>
   <td style="text-align:right;"> 0.4001 </td>
   <td style="text-align:right;"> 0.0665 </td>
   <td style="text-align:right;"> 0.0865 </td>
   <td style="text-align:right;"> 0.0387 </td>
   <td style="text-align:right;"> 0.0116 </td>
   <td style="text-align:right;"> 1.0000 </td>
   <td style="text-align:right;"> 0.0776 </td>
   <td style="text-align:right;"> 0.0909 </td>
   <td style="text-align:right;"> 0.0035 </td>
   <td style="text-align:right;"> 0.5350 </td>
   <td style="text-align:right;"> 0.0096 </td>
   <td style="text-align:right;"> 0.1028 </td>
   <td style="text-align:right;"> 0.0070 </td>
   <td style="text-align:right;"> 0.0996 </td>
   <td style="text-align:right;"> 0.0630 </td>
   <td style="text-align:right;"> 0.2553 </td>
   <td style="text-align:right;"> 0.0647 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01004 </td>
   <td style="text-align:right;"> 99.2927 </td>
   <td style="text-align:right;"> 98.8613 </td>
   <td style="text-align:right;"> 98.8818 </td>
   <td style="text-align:right;"> 97.8499 </td>
   <td style="text-align:right;"> 99.1040 </td>
   <td style="text-align:right;"> 99.1727 </td>
   <td style="text-align:right;"> 0.5490 </td>
   <td style="text-align:right;"> 0.0042 </td>
   <td style="text-align:right;"> 0.5139 </td>
   <td style="text-align:right;"> 0.2730 </td>
   <td style="text-align:right;"> 0.2032 </td>
   <td style="text-align:right;"> 0.1587 </td>
   <td style="text-align:right;"> 0.0610 </td>
   <td style="text-align:right;"> 0.2666 </td>
   <td style="text-align:right;"> 0.4727 </td>
   <td style="text-align:right;"> 0.0785 </td>
   <td style="text-align:right;"> 0.0603 </td>
   <td style="text-align:right;"> 0.0585 </td>
   <td style="text-align:right;"> 0.0258 </td>
   <td style="text-align:right;"> 0.5185 </td>
   <td style="text-align:right;"> 0.1752 </td>
   <td style="text-align:right;"> 0.0544 </td>
   <td style="text-align:right;"> 0.0123 </td>
   <td style="text-align:right;"> 0.7144 </td>
   <td style="text-align:right;"> 0.0079 </td>
   <td style="text-align:right;"> 0.2572 </td>
   <td style="text-align:right;"> 0.0861 </td>
   <td style="text-align:right;"> 0.1261 </td>
   <td style="text-align:right;"> 0.0592 </td>
   <td style="text-align:right;"> 0.3578 </td>
   <td style="text-align:right;"> 0.0303 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01005 </td>
   <td style="text-align:right;"> 107.6633 </td>
   <td style="text-align:right;"> 100.5877 </td>
   <td style="text-align:right;"> 104.8903 </td>
   <td style="text-align:right;"> 100.5953 </td>
   <td style="text-align:right;"> 99.1894 </td>
   <td style="text-align:right;"> 99.2677 </td>
   <td style="text-align:right;"> 0.7330 </td>
   <td style="text-align:right;"> 0.0255 </td>
   <td style="text-align:right;"> 0.5014 </td>
   <td style="text-align:right;"> 0.2524 </td>
   <td style="text-align:right;"> 0.2309 </td>
   <td style="text-align:right;"> 0.1629 </td>
   <td style="text-align:right;"> 0.0569 </td>
   <td style="text-align:right;"> 0.2359 </td>
   <td style="text-align:right;"> 0.3886 </td>
   <td style="text-align:right;"> 0.1761 </td>
   <td style="text-align:right;"> 0.0511 </td>
   <td style="text-align:right;"> 0.0525 </td>
   <td style="text-align:right;"> 0.0050 </td>
   <td style="text-align:right;"> 0.9308 </td>
   <td style="text-align:right;"> 0.2182 </td>
   <td style="text-align:right;"> 0.0302 </td>
   <td style="text-align:right;"> 0.0013 </td>
   <td style="text-align:right;"> 0.3709 </td>
   <td style="text-align:right;"> 0.0039 </td>
   <td style="text-align:right;"> 0.0329 </td>
   <td style="text-align:right;"> 0.0200 </td>
   <td style="text-align:right;"> 0.2858 </td>
   <td style="text-align:right;"> 0.0538 </td>
   <td style="text-align:right;"> 0.2565 </td>
   <td style="text-align:right;"> 0.0162 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01006 </td>
   <td style="text-align:right;"> 101.2918 </td>
   <td style="text-align:right;"> 99.5395 </td>
   <td style="text-align:right;"> 99.7443 </td>
   <td style="text-align:right;"> 98.6083 </td>
   <td style="text-align:right;"> 99.0990 </td>
   <td style="text-align:right;"> 99.1562 </td>
   <td style="text-align:right;"> 0.7530 </td>
   <td style="text-align:right;"> 0.0111 </td>
   <td style="text-align:right;"> 0.5086 </td>
   <td style="text-align:right;"> 0.2595 </td>
   <td style="text-align:right;"> 0.1996 </td>
   <td style="text-align:right;"> 0.1806 </td>
   <td style="text-align:right;"> 0.0706 </td>
   <td style="text-align:right;"> 0.2497 </td>
   <td style="text-align:right;"> 0.4258 </td>
   <td style="text-align:right;"> 0.1650 </td>
   <td style="text-align:right;"> 0.0576 </td>
   <td style="text-align:right;"> 0.0210 </td>
   <td style="text-align:right;"> 0.0043 </td>
   <td style="text-align:right;"> 0.6154 </td>
   <td style="text-align:right;"> 0.0544 </td>
   <td style="text-align:right;"> 0.0303 </td>
   <td style="text-align:right;"> 0.0183 </td>
   <td style="text-align:right;"> 0.4093 </td>
   <td style="text-align:right;"> 0.0032 </td>
   <td style="text-align:right;"> 0.0464 </td>
   <td style="text-align:right;"> 0.0215 </td>
   <td style="text-align:right;"> 0.2584 </td>
   <td style="text-align:right;"> 0.0582 </td>
   <td style="text-align:right;"> 0.2585 </td>
   <td style="text-align:right;"> 0.0197 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01007 </td>
   <td style="text-align:right;"> 102.6725 </td>
   <td style="text-align:right;"> 100.9469 </td>
   <td style="text-align:right;"> 100.5439 </td>
   <td style="text-align:right;"> 99.5256 </td>
   <td style="text-align:right;"> 99.1553 </td>
   <td style="text-align:right;"> 99.2049 </td>
   <td style="text-align:right;"> 0.7223 </td>
   <td style="text-align:right;"> 0.0028 </td>
   <td style="text-align:right;"> 0.5125 </td>
   <td style="text-align:right;"> 0.2738 </td>
   <td style="text-align:right;"> 0.1898 </td>
   <td style="text-align:right;"> 0.1566 </td>
   <td style="text-align:right;"> 0.0620 </td>
   <td style="text-align:right;"> 0.2593 </td>
   <td style="text-align:right;"> 0.4439 </td>
   <td style="text-align:right;"> 0.1062 </td>
   <td style="text-align:right;"> 0.0500 </td>
   <td style="text-align:right;"> 0.0373 </td>
   <td style="text-align:right;"> 0.0107 </td>
   <td style="text-align:right;"> 0.6809 </td>
   <td style="text-align:right;"> 0.0585 </td>
   <td style="text-align:right;"> 0.0444 </td>
   <td style="text-align:right;"> 0.0432 </td>
   <td style="text-align:right;"> 0.5551 </td>
   <td style="text-align:right;"> 0.0057 </td>
   <td style="text-align:right;"> 0.1440 </td>
   <td style="text-align:right;"> 0.0729 </td>
   <td style="text-align:right;"> 0.1765 </td>
   <td style="text-align:right;"> 0.0728 </td>
   <td style="text-align:right;"> 0.3470 </td>
   <td style="text-align:right;"> 0.0192 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01008 </td>
   <td style="text-align:right;"> 99.7144 </td>
   <td style="text-align:right;"> 100.2844 </td>
   <td style="text-align:right;"> 98.6047 </td>
   <td style="text-align:right;"> 99.5866 </td>
   <td style="text-align:right;"> 99.6891 </td>
   <td style="text-align:right;"> 99.6227 </td>
   <td style="text-align:right;"> 0.4434 </td>
   <td style="text-align:right;"> 0.1588 </td>
   <td style="text-align:right;"> 0.5210 </td>
   <td style="text-align:right;"> 0.2681 </td>
   <td style="text-align:right;"> 0.1871 </td>
   <td style="text-align:right;"> 0.1591 </td>
   <td style="text-align:right;"> 0.0641 </td>
   <td style="text-align:right;"> 0.2909 </td>
   <td style="text-align:right;"> 0.4598 </td>
   <td style="text-align:right;"> 0.0736 </td>
   <td style="text-align:right;"> 0.0479 </td>
   <td style="text-align:right;"> 0.0382 </td>
   <td style="text-align:right;"> 0.0136 </td>
   <td style="text-align:right;"> 0.6316 </td>
   <td style="text-align:right;"> 0.1688 </td>
   <td style="text-align:right;"> 0.0853 </td>
   <td style="text-align:right;"> 0.0085 </td>
   <td style="text-align:right;"> 0.7140 </td>
   <td style="text-align:right;"> 0.0072 </td>
   <td style="text-align:right;"> 0.3095 </td>
   <td style="text-align:right;"> 0.0818 </td>
   <td style="text-align:right;"> 0.1224 </td>
   <td style="text-align:right;"> 0.0563 </td>
   <td style="text-align:right;"> 0.3412 </td>
   <td style="text-align:right;"> 0.0217 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01009 </td>
   <td style="text-align:right;"> 100.4092 </td>
   <td style="text-align:right;"> 99.1593 </td>
   <td style="text-align:right;"> 99.8478 </td>
   <td style="text-align:right;"> 98.6020 </td>
   <td style="text-align:right;"> 99.1182 </td>
   <td style="text-align:right;"> 99.1724 </td>
   <td style="text-align:right;"> 0.4175 </td>
   <td style="text-align:right;"> 0.0026 </td>
   <td style="text-align:right;"> 0.5112 </td>
   <td style="text-align:right;"> 0.2794 </td>
   <td style="text-align:right;"> 0.1917 </td>
   <td style="text-align:right;"> 0.1578 </td>
   <td style="text-align:right;"> 0.0689 </td>
   <td style="text-align:right;"> 0.3231 </td>
   <td style="text-align:right;"> 0.4423 </td>
   <td style="text-align:right;"> 0.0661 </td>
   <td style="text-align:right;"> 0.0544 </td>
   <td style="text-align:right;"> 0.0264 </td>
   <td style="text-align:right;"> 0.0306 </td>
   <td style="text-align:right;"> 0.7288 </td>
   <td style="text-align:right;"> 0.3110 </td>
   <td style="text-align:right;"> 0.0362 </td>
   <td style="text-align:right;"> 0.0308 </td>
   <td style="text-align:right;"> 0.5720 </td>
   <td style="text-align:right;"> 0.0101 </td>
   <td style="text-align:right;"> 0.1213 </td>
   <td style="text-align:right;"> 0.0847 </td>
   <td style="text-align:right;"> 0.1039 </td>
   <td style="text-align:right;"> 0.0731 </td>
   <td style="text-align:right;"> 0.3582 </td>
   <td style="text-align:right;"> 0.0841 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01010 </td>
   <td style="text-align:right;"> 101.4046 </td>
   <td style="text-align:right;"> 102.5622 </td>
   <td style="text-align:right;"> 99.7574 </td>
   <td style="text-align:right;"> 99.7674 </td>
   <td style="text-align:right;"> 99.1833 </td>
   <td style="text-align:right;"> 99.2439 </td>
   <td style="text-align:right;"> 0.2279 </td>
   <td style="text-align:right;"> 0.0128 </td>
   <td style="text-align:right;"> 0.5002 </td>
   <td style="text-align:right;"> 0.2671 </td>
   <td style="text-align:right;"> 0.1919 </td>
   <td style="text-align:right;"> 0.1627 </td>
   <td style="text-align:right;"> 0.0680 </td>
   <td style="text-align:right;"> 0.3292 </td>
   <td style="text-align:right;"> 0.4268 </td>
   <td style="text-align:right;"> 0.0533 </td>
   <td style="text-align:right;"> 0.0480 </td>
   <td style="text-align:right;"> 0.0353 </td>
   <td style="text-align:right;"> 0.0389 </td>
   <td style="text-align:right;"> 0.9180 </td>
   <td style="text-align:right;"> 0.1160 </td>
   <td style="text-align:right;"> 0.0563 </td>
   <td style="text-align:right;"> 0.0315 </td>
   <td style="text-align:right;"> 0.7420 </td>
   <td style="text-align:right;"> 0.0136 </td>
   <td style="text-align:right;"> 0.4060 </td>
   <td style="text-align:right;"> 0.3097 </td>
   <td style="text-align:right;"> 0.0851 </td>
   <td style="text-align:right;"> 0.0743 </td>
   <td style="text-align:right;"> 0.3758 </td>
   <td style="text-align:right;"> 0.0399 </td>
  </tr>
</tbody>
</table>
  
  2.    Seleccionar las variables del modelo y crear matriz de covariables.
  

```r
names_cov <-
  c(
    "dam2",
    "tasa_desocupacion",
    "material_paredes",
    "piso_tierra",
    "luces_nocturnas",
    "suelo_cultivo",
    "modificacion_humana"
  )
X_pred <-
  anti_join(statelevel_predictors_df %>% select(all_of(names_cov)),
            indicador_dam1 %>% select(dam2))
```

  En el bloque de código se identifican que dominios serán los predichos.  

```r
X_pred %>% select(dam2) %>% 
  saveRDS(file = "Recursos/Día3/Sesion4/Data/dam_pred.rds")
```

  Creando la matriz de covariables para los dominios no observados (`X_pred`) y los observados (`X_obs`)
  

```r
## Obteniendo la matrix 
X_pred %<>%
  data.frame() %>%
  select(-dam2)  %>%  as.matrix()

## Identificando los dominios para realizar estimación del modelo

X_obs <- inner_join(indicador_dam1 %>% select(dam2, id_orden),
                    statelevel_predictors_df %>% select(all_of(names_cov))) %>%
  arrange(id_orden) %>%
  data.frame() %>%
  select(-dam2, -id_orden)  %>%  as.matrix()
```
  
  3. Calculando el n_efectivo y el $\tilde{y}$ 
  

```r
D <- nrow(indicador_dam1)
P <- 3 # Ocupado, desocupado, inactivo.
Y_tilde <- matrix(NA, D, P)
n_tilde <- matrix(NA, D, P)
Y_hat <- matrix(NA, D, P)

# n efectivos ocupado
n_tilde[,1] <- (indicador_dam1$Ocupado*(1 - indicador_dam1$Ocupado))/indicador_dam1$Ocupado_var
Y_tilde[,1] <- n_tilde[,1]* indicador_dam1$Ocupado


# n efectivos desocupado
n_tilde[,2] <- (indicador_dam1$Desocupado*(1 - indicador_dam1$Desocupado))/indicador_dam1$Desocupado_var
Y_tilde[,2] <- n_tilde[,2]* indicador_dam1$Desocupado

# n efectivos Inactivo
n_tilde[,3] <- (indicador_dam1$Inactivo*(1 - indicador_dam1$Inactivo))/indicador_dam1$Inactivo_var
Y_tilde[,3] <- n_tilde[,3]* indicador_dam1$Inactivo
```

  Ahora, validamos la coherencia de los cálculos realizados 
  

```r
ni_hat = rowSums(Y_tilde)
Y_hat[,1] <- ni_hat* indicador_dam1$Ocupado
Y_hat[,2] <- ni_hat* indicador_dam1$Desocupado
Y_hat[,3] <- ni_hat* indicador_dam1$Inactivo
Y_hat <- round(Y_hat)

hat_p <- Y_hat/rowSums(Y_hat)
par(mfrow = c(1,3))
plot(hat_p[,1],indicador_dam1$Ocupado)
abline(a = 0,b=1,col = "red")
plot(hat_p[,2],indicador_dam1$Desocupado)
abline(a = 0,b=1,col = "red")
plot(hat_p[,3],indicador_dam1$Inactivo)
abline(a = 0,b=1,col = "red")
```
  

<img src="Recursos/Día3/Sesion4/0Recursos/theta_ajustado.png" width="800px" height="200px" style="display: block; margin: auto;" />

  4. Compilando el modelo 



```r
X1_obs <- cbind(matrix(1,nrow = D,ncol = 1),X_obs)
K = ncol(X1_obs)
D1 <- nrow(X_pred)
X1_pred <- cbind(matrix(1,nrow = D1,ncol = 1),X_pred)

sample_data <- list(D = D,
                    P = P,
                    K = K,
                    y_tilde = Y_hat,
                    X_obs = X1_obs,
                    X_pred = X1_pred,
                    D1 = D1)


library(rstan)
fit_mcmc2 <- stan(
  file = "Recursos/Día3/Sesion4/Data/modelosStan/00 Multinomial_simple_no_cor.stan",  # Stan program
  data = sample_data,    # named list of data
  verbose = TRUE,
  warmup = 1000,          # number of warmup iterations per chain
  iter = 2000,            # total number of iterations per chain
  cores = 4,              # number of cores (could use one per chain)
)

saveRDS(fit_mcmc2,
        "Recursos/Día3/Sesion4/Data/fit_multinomial_no_cor.Rds")
```


## Validación del modelo 

La validación de un modelo es esencial para evaluar su capacidad para predecir de manera precisa y confiable los resultados futuros. En el caso de un modelo de área con respuesta multinomial, la validación se enfoca en medir la precisión del modelo para predecir las diferentes categorías de respuesta. El objetivo principal de la validación es determinar si el modelo es capaz de generalizar bien a datos no vistos y proporcionar predicciones precisas. Esto implica comparar las predicciones del modelo con los datos observados y utilizar métricas de evaluación para medir el rendimiento del modelo. La validación del modelo es esencial para garantizar la calidad de las predicciones y la confiabilidad del modelo para su uso en aplicaciones futuras.


```r
infile <- paste0("Recursos/Día3/Sesion4/Data/fit_multinomial_no_cor.Rds")
fit <- readRDS(infile)

theta_dir <- indicador_dam1 %>%  
  transmute(dam2,
    n = n_desocupado + n_ocupado + n_inactivo,
        Ocupado, Desocupado, Inactivo) 

color_scheme_set("brightblue")
theme_set(theme_bw(base_size = 15))
y_pred_B <- as.array(fit, pars = "theta") %>%
  as_draws_matrix()
  
rowsrandom <- sample(nrow(y_pred_B), 100)

theta_1<-  grep(pattern = "1]",x = colnames(y_pred_B),value = TRUE)
theta_2<-  grep(pattern = "2]",x = colnames(y_pred_B),value = TRUE)
theta_3<-  grep(pattern = "3]",x = colnames(y_pred_B),value = TRUE)
y_pred1 <- y_pred_B[rowsrandom,theta_1 ]
y_pred2 <- y_pred_B[rowsrandom,theta_2 ]
y_pred3 <- y_pred_B[rowsrandom,theta_3 ]

p1 <- ppc_dens_overlay(y = as.numeric(theta_dir$Ocupado), y_pred1)/
  ppc_dens_overlay(y = as.numeric(theta_dir$Desocupado), y_pred2)/
  ppc_dens_overlay(y = as.numeric(theta_dir$Inactivo), y_pred3)

# ggsave(plot = p1,
#        filename = "Recursos/Día3/Sesion4/0Recursos/ppc.png",
#        scale = 2)
```


<img src="Recursos/Día3/Sesion4/0Recursos/ppc.png" width="800px" height="200px" style="display: block; margin: auto;" />

## Estimación de los parámetros. 

El código crea dos matrices, `theta_obs_ordenado` y `theta_pred_ordenado`, que contienen las estimaciones medias de los parámetros del modelo de respuesta multinomial con covariables para los datos de observación y predicción, respectivamente. La función `matrix()` se utiliza para dar formato a los datos con una matriz `nrow` x `ncol`, y se asignan nombres de columna apropiados a la matriz resultante utilizando `colnames()`. Luego se convierten las matrices en marcos de datos (`as.data.frame()`) y se unen mediante `full_join()` para crear una única tabla que contenga todas las estimaciones de los parámetros para los datos de observación y predicción, junto con la información del indicador de área (theta_dir). El resultado final es un marco de datos llamado estimaciones_obs.


```r
dam_pred <- readRDS("Recursos/Día3/Sesion4/Data/dam_pred.rds")
P <- 3 
D <- nrow(indicador_dam1)
D1 <- nrow(dam_pred)
## Estimación del modelo. 
theta_obs <- summary(fit, pars = "theta")$summary[, "mean"]
theta_pred <- summary(fit, pars = "theta_pred")$summary[, "mean"]

## Ordenando la matrix de theta 
theta_obs_ordenado <- matrix(theta_obs, 
                             nrow = D,
                             ncol = P,byrow = TRUE) 

colnames(theta_obs_ordenado) <- c("Ocupado_mod", "Desocupado_mod", "Inactivo_mod")
theta_obs_ordenado%<>% as.data.frame()
theta_obs_ordenado <- cbind(dam2 = indicador_dam1$dam2,
                            theta_obs_ordenado)

theta_pred_ordenado <- matrix(theta_pred, 
                             nrow = D1,
                             ncol = P,byrow = TRUE)

colnames(theta_pred_ordenado) <- c("Ocupado_mod", "Desocupado_mod", "Inactivo_mod")
theta_pred_ordenado%<>% as.data.frame()
theta_pred_ordenado <- cbind(dam2 = dam_pred$dam2, theta_pred_ordenado)
```

## Estimación de la desviación estárdar y el coeficiente de valiación 

Este bloque de código corresponde al cálculo de las desviaciones estándar (sd) y coeficientes de variación (cv) de los parámetros `theta` para los datos observados y predichos. En primer lugar, se utiliza la función `summary()` del paquete `rstan` para extraer los valores de `sd` de los parámetros `theta` observados y predichos, respectivamente, a partir del modelo (`fit`) que contiene la información de la estimación de los parámetros de la distribución Bayesiana. Luego, se organizan los valores de sd en una matriz ordenada por `dam2` y se les asignan los nombres correspondientes. Con esta matriz, se calcula otra matriz que contiene los coeficientes de variación para los parámetros `theta` observados (`theta_obs_ordenado_cv`). De manera similar, se construyen matrices ordenadas por `dam2` para los valores de sd y cv de los parámetros theta predichos (`theta_pred_ordenado_sd` y `theta_pred_ordenado_cv`, respectivamente).



```r
theta_obs_sd <- summary(fit, pars = "theta")$summary[, "sd"]
theta_pred_sd <- summary(fit, pars = "theta_pred")$summary[, "sd"]

theta_obs_ordenado_sd <- matrix(theta_obs_sd, 
                             nrow = D,
                             ncol = P,byrow = TRUE) 

colnames(theta_obs_ordenado_sd) <- c("Ocupado_mod_sd", "Desocupado_mod_sd", "Inactivo_mod_sd")
theta_obs_ordenado_sd%<>% as.data.frame()
theta_obs_ordenado_sd <- cbind(dam2 = indicador_dam1$dam2,
                            theta_obs_ordenado_sd)
theta_obs_ordenado_cv <- theta_obs_ordenado_sd[,-1]/theta_obs_ordenado[,-1]

colnames(theta_obs_ordenado_cv) <- c("Ocupado_mod_cv", "Desocupado_mod_cv", "Inactivo_mod_cv")

theta_obs_ordenado_cv <- cbind(dam2 = indicador_dam1$dam2,
                               theta_obs_ordenado_cv)

theta_pred_ordenado_sd <- matrix(theta_pred_sd, 
                              nrow = D1,
                              ncol = P,byrow = TRUE)

colnames(theta_pred_ordenado_sd) <- c("Ocupado_mod_sd", "Desocupado_mod_sd", "Inactivo_mod_sd")
theta_pred_ordenado_sd%<>% as.data.frame()
theta_pred_ordenado_sd <- cbind(dam2 = dam_pred$dam2, theta_pred_ordenado_sd)

theta_pred_ordenado_cv <- theta_pred_ordenado_sd[,-1]/theta_pred_ordenado[,-1]

colnames(theta_pred_ordenado_cv) <- c("Ocupado_mod_cv", "Desocupado_mod_cv", "Inactivo_mod_cv")

theta_pred_ordenado_cv <- cbind(dam2 = dam_pred$dam2, theta_pred_ordenado_cv)
```

El último paso es realizar la consolidación de la bases obtenidas para la estimación puntual, desviación estándar y coeficiente de variación. 


```r
theta_obs_ordenado <- full_join(theta_obs_ordenado,theta_obs_ordenado_sd) %>% 
  full_join(theta_obs_ordenado_cv)

theta_pred_ordenado <- full_join(theta_pred_ordenado,theta_pred_ordenado_sd) %>% 
  full_join(theta_pred_ordenado_cv)


estimaciones <- full_join(indicador_dam1,
                              bind_rows(theta_obs_ordenado, theta_pred_ordenado))

saveRDS(object = estimaciones, file = "Recursos/Día3/Sesion4/Data/estimaciones.rds")
tba(head(estimaciones,10))
```

<table class="table table-striped lightable-classic" style="width: auto !important; margin-left: auto; margin-right: auto; font-family: Arial Narrow; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> dam2 </th>
   <th style="text-align:right;"> n_upm </th>
   <th style="text-align:right;"> n_ocupado </th>
   <th style="text-align:right;"> n_desocupado </th>
   <th style="text-align:right;"> n_inactivo </th>
   <th style="text-align:right;"> Ocupado </th>
   <th style="text-align:right;"> Ocupado_se </th>
   <th style="text-align:right;"> Ocupado_var </th>
   <th style="text-align:right;"> Ocupado_deff </th>
   <th style="text-align:right;"> Desocupado </th>
   <th style="text-align:right;"> Desocupado_se </th>
   <th style="text-align:right;"> Desocupado_var </th>
   <th style="text-align:right;"> Desocupado_deff </th>
   <th style="text-align:right;"> Inactivo </th>
   <th style="text-align:right;"> Inactivo_se </th>
   <th style="text-align:right;"> Inactivo_var </th>
   <th style="text-align:right;"> Inactivo_deff </th>
   <th style="text-align:right;"> id_orden </th>
   <th style="text-align:right;"> Ocupado_mod </th>
   <th style="text-align:right;"> Desocupado_mod </th>
   <th style="text-align:right;"> Inactivo_mod </th>
   <th style="text-align:right;"> Ocupado_mod_sd </th>
   <th style="text-align:right;"> Desocupado_mod_sd </th>
   <th style="text-align:right;"> Inactivo_mod_sd </th>
   <th style="text-align:right;"> Ocupado_mod_cv </th>
   <th style="text-align:right;"> Desocupado_mod_cv </th>
   <th style="text-align:right;"> Inactivo_mod_cv </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 01001 </td>
   <td style="text-align:right;"> 274 </td>
   <td style="text-align:right;"> 2560 </td>
   <td style="text-align:right;"> 151 </td>
   <td style="text-align:right;"> 1609 </td>
   <td style="text-align:right;"> 0.5927 </td>
   <td style="text-align:right;"> 0.0082 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 1.2035 </td>
   <td style="text-align:right;"> 0.0361 </td>
   <td style="text-align:right;"> 0.0032 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 1.3006 </td>
   <td style="text-align:right;"> 0.3712 </td>
   <td style="text-align:right;"> 0.0079 </td>
   <td style="text-align:right;"> 0.0001 </td>
   <td style="text-align:right;"> 1.1630 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 0.5915 </td>
   <td style="text-align:right;"> 0.0362 </td>
   <td style="text-align:right;"> 0.3723 </td>
   <td style="text-align:right;"> 0.0078 </td>
   <td style="text-align:right;"> 0.0030 </td>
   <td style="text-align:right;"> 0.0079 </td>
   <td style="text-align:right;"> 0.0133 </td>
   <td style="text-align:right;"> 0.0835 </td>
   <td style="text-align:right;"> 0.0212 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01003 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 238 </td>
   <td style="text-align:right;"> 18 </td>
   <td style="text-align:right;"> 194 </td>
   <td style="text-align:right;"> 0.5399 </td>
   <td style="text-align:right;"> 0.0158 </td>
   <td style="text-align:right;"> 2e-04 </td>
   <td style="text-align:right;"> 0.4575 </td>
   <td style="text-align:right;"> 0.0362 </td>
   <td style="text-align:right;"> 0.0075 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 0.7328 </td>
   <td style="text-align:right;"> 0.4239 </td>
   <td style="text-align:right;"> 0.0138 </td>
   <td style="text-align:right;"> 0.0002 </td>
   <td style="text-align:right;"> 0.3554 </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 0.5428 </td>
   <td style="text-align:right;"> 0.0353 </td>
   <td style="text-align:right;"> 0.4219 </td>
   <td style="text-align:right;"> 0.0136 </td>
   <td style="text-align:right;"> 0.0052 </td>
   <td style="text-align:right;"> 0.0138 </td>
   <td style="text-align:right;"> 0.0251 </td>
   <td style="text-align:right;"> 0.1462 </td>
   <td style="text-align:right;"> 0.0328 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01005 </td>
   <td style="text-align:right;"> 27 </td>
   <td style="text-align:right;"> 619 </td>
   <td style="text-align:right;"> 25 </td>
   <td style="text-align:right;"> 298 </td>
   <td style="text-align:right;"> 0.6365 </td>
   <td style="text-align:right;"> 0.0182 </td>
   <td style="text-align:right;"> 3e-04 </td>
   <td style="text-align:right;"> 1.3637 </td>
   <td style="text-align:right;"> 0.0352 </td>
   <td style="text-align:right;"> 0.0077 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 1.6567 </td>
   <td style="text-align:right;"> 0.3283 </td>
   <td style="text-align:right;"> 0.0157 </td>
   <td style="text-align:right;"> 0.0002 </td>
   <td style="text-align:right;"> 1.0603 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 0.6272 </td>
   <td style="text-align:right;"> 0.0353 </td>
   <td style="text-align:right;"> 0.3375 </td>
   <td style="text-align:right;"> 0.0160 </td>
   <td style="text-align:right;"> 0.0062 </td>
   <td style="text-align:right;"> 0.0158 </td>
   <td style="text-align:right;"> 0.0255 </td>
   <td style="text-align:right;"> 0.1749 </td>
   <td style="text-align:right;"> 0.0469 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01006 </td>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:right;"> 273 </td>
   <td style="text-align:right;"> 14 </td>
   <td style="text-align:right;"> 194 </td>
   <td style="text-align:right;"> 0.5801 </td>
   <td style="text-align:right;"> 0.0200 </td>
   <td style="text-align:right;"> 4e-04 </td>
   <td style="text-align:right;"> 0.7957 </td>
   <td style="text-align:right;"> 0.0264 </td>
   <td style="text-align:right;"> 0.0056 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 0.5836 </td>
   <td style="text-align:right;"> 0.3935 </td>
   <td style="text-align:right;"> 0.0180 </td>
   <td style="text-align:right;"> 0.0003 </td>
   <td style="text-align:right;"> 0.6536 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 0.5786 </td>
   <td style="text-align:right;"> 0.0275 </td>
   <td style="text-align:right;"> 0.3939 </td>
   <td style="text-align:right;"> 0.0175 </td>
   <td style="text-align:right;"> 0.0057 </td>
   <td style="text-align:right;"> 0.0176 </td>
   <td style="text-align:right;"> 0.0302 </td>
   <td style="text-align:right;"> 0.2052 </td>
   <td style="text-align:right;"> 0.0446 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01007 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 334 </td>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:right;"> 225 </td>
   <td style="text-align:right;"> 0.6132 </td>
   <td style="text-align:right;"> 0.0312 </td>
   <td style="text-align:right;"> 1e-03 </td>
   <td style="text-align:right;"> 2.3457 </td>
   <td style="text-align:right;"> 0.0155 </td>
   <td style="text-align:right;"> 0.0059 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 1.3093 </td>
   <td style="text-align:right;"> 0.3714 </td>
   <td style="text-align:right;"> 0.0300 </td>
   <td style="text-align:right;"> 0.0009 </td>
   <td style="text-align:right;"> 2.2054 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 0.5974 </td>
   <td style="text-align:right;"> 0.0215 </td>
   <td style="text-align:right;"> 0.3812 </td>
   <td style="text-align:right;"> 0.0246 </td>
   <td style="text-align:right;"> 0.0067 </td>
   <td style="text-align:right;"> 0.0247 </td>
   <td style="text-align:right;"> 0.0412 </td>
   <td style="text-align:right;"> 0.3099 </td>
   <td style="text-align:right;"> 0.0648 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01011 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 324 </td>
   <td style="text-align:right;"> 17 </td>
   <td style="text-align:right;"> 177 </td>
   <td style="text-align:right;"> 0.6359 </td>
   <td style="text-align:right;"> 0.0290 </td>
   <td style="text-align:right;"> 8e-04 </td>
   <td style="text-align:right;"> 1.9003 </td>
   <td style="text-align:right;"> 0.0298 </td>
   <td style="text-align:right;"> 0.0074 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 0.9842 </td>
   <td style="text-align:right;"> 0.3343 </td>
   <td style="text-align:right;"> 0.0319 </td>
   <td style="text-align:right;"> 0.0010 </td>
   <td style="text-align:right;"> 2.3912 </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 0.6151 </td>
   <td style="text-align:right;"> 0.0315 </td>
   <td style="text-align:right;"> 0.3533 </td>
   <td style="text-align:right;"> 0.0256 </td>
   <td style="text-align:right;"> 0.0087 </td>
   <td style="text-align:right;"> 0.0248 </td>
   <td style="text-align:right;"> 0.0416 </td>
   <td style="text-align:right;"> 0.2769 </td>
   <td style="text-align:right;"> 0.0703 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02001 </td>
   <td style="text-align:right;"> 73 </td>
   <td style="text-align:right;"> 1359 </td>
   <td style="text-align:right;"> 55 </td>
   <td style="text-align:right;"> 979 </td>
   <td style="text-align:right;"> 0.5488 </td>
   <td style="text-align:right;"> 0.0190 </td>
   <td style="text-align:right;"> 4e-04 </td>
   <td style="text-align:right;"> 3.5128 </td>
   <td style="text-align:right;"> 0.0230 </td>
   <td style="text-align:right;"> 0.0050 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 2.6845 </td>
   <td style="text-align:right;"> 0.4282 </td>
   <td style="text-align:right;"> 0.0181 </td>
   <td style="text-align:right;"> 0.0003 </td>
   <td style="text-align:right;"> 3.2195 </td>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:right;"> 0.5553 </td>
   <td style="text-align:right;"> 0.0225 </td>
   <td style="text-align:right;"> 0.4222 </td>
   <td style="text-align:right;"> 0.0178 </td>
   <td style="text-align:right;"> 0.0051 </td>
   <td style="text-align:right;"> 0.0177 </td>
   <td style="text-align:right;"> 0.0320 </td>
   <td style="text-align:right;"> 0.2284 </td>
   <td style="text-align:right;"> 0.0419 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02002 </td>
   <td style="text-align:right;"> 141 </td>
   <td style="text-align:right;"> 2014 </td>
   <td style="text-align:right;"> 93 </td>
   <td style="text-align:right;"> 1644 </td>
   <td style="text-align:right;"> 0.5537 </td>
   <td style="text-align:right;"> 0.0113 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 1.9590 </td>
   <td style="text-align:right;"> 0.0221 </td>
   <td style="text-align:right;"> 0.0039 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 2.6821 </td>
   <td style="text-align:right;"> 0.4242 </td>
   <td style="text-align:right;"> 0.0110 </td>
   <td style="text-align:right;"> 0.0001 </td>
   <td style="text-align:right;"> 1.8694 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 0.5511 </td>
   <td style="text-align:right;"> 0.0234 </td>
   <td style="text-align:right;"> 0.4255 </td>
   <td style="text-align:right;"> 0.0112 </td>
   <td style="text-align:right;"> 0.0032 </td>
   <td style="text-align:right;"> 0.0112 </td>
   <td style="text-align:right;"> 0.0204 </td>
   <td style="text-align:right;"> 0.1388 </td>
   <td style="text-align:right;"> 0.0263 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02003 </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:right;"> 519 </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:right;"> 379 </td>
   <td style="text-align:right;"> 0.5640 </td>
   <td style="text-align:right;"> 0.0293 </td>
   <td style="text-align:right;"> 9e-04 </td>
   <td style="text-align:right;"> 3.2058 </td>
   <td style="text-align:right;"> 0.0188 </td>
   <td style="text-align:right;"> 0.0072 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 2.5963 </td>
   <td style="text-align:right;"> 0.4172 </td>
   <td style="text-align:right;"> 0.0361 </td>
   <td style="text-align:right;"> 0.0013 </td>
   <td style="text-align:right;"> 4.9275 </td>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:right;"> 0.5669 </td>
   <td style="text-align:right;"> 0.0228 </td>
   <td style="text-align:right;"> 0.4103 </td>
   <td style="text-align:right;"> 0.0261 </td>
   <td style="text-align:right;"> 0.0071 </td>
   <td style="text-align:right;"> 0.0261 </td>
   <td style="text-align:right;"> 0.0460 </td>
   <td style="text-align:right;"> 0.3097 </td>
   <td style="text-align:right;"> 0.0636 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02004 </td>
   <td style="text-align:right;"> 197 </td>
   <td style="text-align:right;"> 2077 </td>
   <td style="text-align:right;"> 116 </td>
   <td style="text-align:right;"> 1531 </td>
   <td style="text-align:right;"> 0.5577 </td>
   <td style="text-align:right;"> 0.0101 </td>
   <td style="text-align:right;"> 1e-04 </td>
   <td style="text-align:right;"> 1.5357 </td>
   <td style="text-align:right;"> 0.0327 </td>
   <td style="text-align:right;"> 0.0041 </td>
   <td style="text-align:right;"> 0e+00 </td>
   <td style="text-align:right;"> 1.9601 </td>
   <td style="text-align:right;"> 0.4096 </td>
   <td style="text-align:right;"> 0.0098 </td>
   <td style="text-align:right;"> 0.0001 </td>
   <td style="text-align:right;"> 1.4950 </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:right;"> 0.5576 </td>
   <td style="text-align:right;"> 0.0331 </td>
   <td style="text-align:right;"> 0.4093 </td>
   <td style="text-align:right;"> 0.0099 </td>
   <td style="text-align:right;"> 0.0036 </td>
   <td style="text-align:right;"> 0.0098 </td>
   <td style="text-align:right;"> 0.0177 </td>
   <td style="text-align:right;"> 0.1074 </td>
   <td style="text-align:right;"> 0.0239 </td>
  </tr>
</tbody>
</table>

## Metodología de Benchmarking 

  1. Conteos de personas agregados por dam2, personas mayores de 15 años de edad. 
  

```r
conteo_pp_dam <- readRDS("Recursos/Día3/Sesion4/Data/censo_mrp_dam2.rds") %>%
  filter(edad > 1)  %>% 
  group_by(dam , dam2) %>% 
  summarise(pp_dam2 = sum(n),.groups = "drop") %>% 
  group_by(dam) %>% 
mutate(pp_dam = sum(pp_dam2))
head(conteo_pp_dam) %>% tba()
```

<table class="table table-striped lightable-classic" style="width: auto !important; margin-left: auto; margin-right: auto; font-family: Arial Narrow; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> dam </th>
   <th style="text-align:left;"> dam2 </th>
   <th style="text-align:right;"> pp_dam2 </th>
   <th style="text-align:right;"> pp_dam </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01001 </td>
   <td style="text-align:right;"> 701329 </td>
   <td style="text-align:right;"> 1031756 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01002 </td>
   <td style="text-align:right;"> 35575 </td>
   <td style="text-align:right;"> 1031756 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01003 </td>
   <td style="text-align:right;"> 41731 </td>
   <td style="text-align:right;"> 1031756 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01004 </td>
   <td style="text-align:right;"> 11826 </td>
   <td style="text-align:right;"> 1031756 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01005 </td>
   <td style="text-align:right;"> 91311 </td>
   <td style="text-align:right;"> 1031756 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:left;"> 01006 </td>
   <td style="text-align:right;"> 33782 </td>
   <td style="text-align:right;"> 1031756 </td>
  </tr>
</tbody>
</table>

  2.    Estimación del parámetro `theta` al nivel que la encuesta sea representativa.
  

```r
indicador_agregado <-
  diseno %>% group_by_at("dam") %>% 
  filter(empleo %in% c(1:3)) %>%
  summarise(
    Ocupado = survey_ratio(numerator = (empleo == 1), 
                           denominator = 1 ),
    Desocupado = survey_ratio(numerator =( empleo == 2),denominator = 1
                             
    ),
    Inactivo = survey_ratio(numerator =  (empleo == 3), denominator = 1
                           
    )
  ) %>% select(dam,Ocupado,Desocupado, Inactivo)

tba(indicador_agregado)
```

<table class="table table-striped lightable-classic" style="width: auto !important; margin-left: auto; margin-right: auto; font-family: Arial Narrow; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> dam </th>
   <th style="text-align:right;"> Ocupado </th>
   <th style="text-align:right;"> Desocupado </th>
   <th style="text-align:right;"> Inactivo </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:right;"> 0.5974 </td>
   <td style="text-align:right;"> 0.0336 </td>
   <td style="text-align:right;"> 0.3690 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02 </td>
   <td style="text-align:right;"> 0.5552 </td>
   <td style="text-align:right;"> 0.0276 </td>
   <td style="text-align:right;"> 0.4172 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 03 </td>
   <td style="text-align:right;"> 0.5824 </td>
   <td style="text-align:right;"> 0.0297 </td>
   <td style="text-align:right;"> 0.3879 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 04 </td>
   <td style="text-align:right;"> 0.6429 </td>
   <td style="text-align:right;"> 0.0205 </td>
   <td style="text-align:right;"> 0.3365 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 05 </td>
   <td style="text-align:right;"> 0.5331 </td>
   <td style="text-align:right;"> 0.0352 </td>
   <td style="text-align:right;"> 0.4316 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 06 </td>
   <td style="text-align:right;"> 0.6115 </td>
   <td style="text-align:right;"> 0.0239 </td>
   <td style="text-align:right;"> 0.3645 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 07 </td>
   <td style="text-align:right;"> 0.6799 </td>
   <td style="text-align:right;"> 0.0158 </td>
   <td style="text-align:right;"> 0.3043 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 08 </td>
   <td style="text-align:right;"> 0.5465 </td>
   <td style="text-align:right;"> 0.0316 </td>
   <td style="text-align:right;"> 0.4219 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 09 </td>
   <td style="text-align:right;"> 0.5142 </td>
   <td style="text-align:right;"> 0.0601 </td>
   <td style="text-align:right;"> 0.4257 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 10 </td>
   <td style="text-align:right;"> 0.5668 </td>
   <td style="text-align:right;"> 0.0303 </td>
   <td style="text-align:right;"> 0.4030 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 11 </td>
   <td style="text-align:right;"> 0.5666 </td>
   <td style="text-align:right;"> 0.0334 </td>
   <td style="text-align:right;"> 0.4000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 12 </td>
   <td style="text-align:right;"> 0.6310 </td>
   <td style="text-align:right;"> 0.0195 </td>
   <td style="text-align:right;"> 0.3495 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 13 </td>
   <td style="text-align:right;"> 0.6044 </td>
   <td style="text-align:right;"> 0.0216 </td>
   <td style="text-align:right;"> 0.3740 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 14 </td>
   <td style="text-align:right;"> 0.5697 </td>
   <td style="text-align:right;"> 0.0356 </td>
   <td style="text-align:right;"> 0.3946 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 15 </td>
   <td style="text-align:right;"> 0.5290 </td>
   <td style="text-align:right;"> 0.0428 </td>
   <td style="text-align:right;"> 0.4282 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 16 </td>
   <td style="text-align:right;"> 0.6337 </td>
   <td style="text-align:right;"> 0.0185 </td>
   <td style="text-align:right;"> 0.3478 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 17 </td>
   <td style="text-align:right;"> 0.5972 </td>
   <td style="text-align:right;"> 0.0285 </td>
   <td style="text-align:right;"> 0.3743 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 18 </td>
   <td style="text-align:right;"> 0.6331 </td>
   <td style="text-align:right;"> 0.0204 </td>
   <td style="text-align:right;"> 0.3466 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 19 </td>
   <td style="text-align:right;"> 0.5429 </td>
   <td style="text-align:right;"> 0.0366 </td>
   <td style="text-align:right;"> 0.4205 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 20 </td>
   <td style="text-align:right;"> 0.6686 </td>
   <td style="text-align:right;"> 0.0130 </td>
   <td style="text-align:right;"> 0.3184 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 21 </td>
   <td style="text-align:right;"> 0.6505 </td>
   <td style="text-align:right;"> 0.0261 </td>
   <td style="text-align:right;"> 0.3234 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 22 </td>
   <td style="text-align:right;"> 0.5746 </td>
   <td style="text-align:right;"> 0.0338 </td>
   <td style="text-align:right;"> 0.3916 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 23 </td>
   <td style="text-align:right;"> 0.5785 </td>
   <td style="text-align:right;"> 0.0433 </td>
   <td style="text-align:right;"> 0.3782 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 24 </td>
   <td style="text-align:right;"> 0.5796 </td>
   <td style="text-align:right;"> 0.0272 </td>
   <td style="text-align:right;"> 0.3932 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 25 </td>
   <td style="text-align:right;"> 0.5385 </td>
   <td style="text-align:right;"> 0.0310 </td>
   <td style="text-align:right;"> 0.4305 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 26 </td>
   <td style="text-align:right;"> 0.5615 </td>
   <td style="text-align:right;"> 0.0324 </td>
   <td style="text-align:right;"> 0.4061 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 27 </td>
   <td style="text-align:right;"> 0.5990 </td>
   <td style="text-align:right;"> 0.0301 </td>
   <td style="text-align:right;"> 0.3709 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 28 </td>
   <td style="text-align:right;"> 0.5416 </td>
   <td style="text-align:right;"> 0.0295 </td>
   <td style="text-align:right;"> 0.4289 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 29 </td>
   <td style="text-align:right;"> 0.5928 </td>
   <td style="text-align:right;"> 0.0263 </td>
   <td style="text-align:right;"> 0.3809 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 30 </td>
   <td style="text-align:right;"> 0.5971 </td>
   <td style="text-align:right;"> 0.0200 </td>
   <td style="text-align:right;"> 0.3829 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 31 </td>
   <td style="text-align:right;"> 0.6536 </td>
   <td style="text-align:right;"> 0.0193 </td>
   <td style="text-align:right;"> 0.3271 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 32 </td>
   <td style="text-align:right;"> 0.5875 </td>
   <td style="text-align:right;"> 0.0132 </td>
   <td style="text-align:right;"> 0.3993 </td>
  </tr>
</tbody>
</table>

Organizando la salida como un vector. 

```r
temp <-
  gather(indicador_agregado, key = "agregado", value = "estimacion", -dam) %>%
  mutate(nombre = paste0("dam_", dam,"_", agregado))

Razon_empleo <- setNames(temp$estimacion, temp$nombre)
```
  
  3.  Definir los pesos por dominios. 
  

```r
names_cov <-  "dam"
estimaciones_mod <- estimaciones %>% transmute(
  dam = substr(dam2,1,2),
  dam2,Ocupado_mod,Desocupado_mod,Inactivo_mod) %>% 
  inner_join(conteo_pp_dam ) %>% 
  mutate(wi = pp_dam2/pp_dam)
```
  
  4. Crear variables dummys 
  

```r
estimaciones_mod %<>%
  fastDummies::dummy_cols(select_columns = names_cov,
                          remove_selected_columns = FALSE)

Xdummy <- estimaciones_mod %>% select(matches("dam_")) %>% 
  mutate_at(vars(matches("_\\d")) ,
            list(Ocupado = function(x) x*estimaciones_mod$Ocupado_mod,
                 Desocupado = function(x) x*estimaciones_mod$Desocupado_mod,
                 Inactivo = function(x) x*estimaciones_mod$Inactivo_mod)) %>% 
  select((matches("Ocupado|Desocupado|Inactivo"))) 
# head(Xdummy) %>% tba()
```
  Algunas validaciones realizadas 

```r
colnames(Xdummy) == names(Razon_empleo)
data.frame(Modelo = colSums(Xdummy*estimaciones_mod$wi),
Estimacion_encuesta = Razon_empleo)
```
  
  
  5.    Calcular el ponderador para cada nivel de la variable. 
  
#### Ocupado {-}
    

```r
library(sampling)
names_ocupado <- grep(pattern = "_O", x = colnames(Xdummy),value = TRUE)

gk_ocupado <- calib(Xs = Xdummy[,names_ocupado], 
            d =  estimaciones_mod$wi,
            total = Razon_empleo[names_ocupado],
            method="logit",max_iter = 5000,) 

checkcalibration(Xs = Xdummy[,names_ocupado], 
                 d =estimaciones_mod$wi,
                 total = Razon_empleo[names_ocupado],
                 g = gk_ocupado)
```

#### Desocupado {-} 
    

```r
names_descupados <- grep(pattern = "_D", x = colnames(Xdummy),value = TRUE)

gk_desocupado <- calib(Xs = Xdummy[,names_descupados], 
                    d =  estimaciones_mod$wi,
                    total = Razon_empleo[names_descupados],
                    method="logit",max_iter = 5000,) 

checkcalibration(Xs = Xdummy[,names_descupados], 
                 d =estimaciones_mod$wi,
                 total = Razon_empleo[names_descupados],
                 g = gk_desocupado)
```

#### Inactivo {-}


```r
names_inactivo <- grep(pattern = "_I", x = colnames(Xdummy),value = TRUE)

gk_Inactivo <- calib(Xs = Xdummy[,names_inactivo], 
                    d =  estimaciones_mod$wi,
                    total = Razon_empleo[names_inactivo],
                    method="logit",max_iter = 5000,) 

checkcalibration(Xs = Xdummy[,names_inactivo], 
                 d =estimaciones_mod$wi,
                 total = Razon_empleo[names_inactivo],
                 g = gk_Inactivo)
```
  
  6.    Validar los resultados obtenidos. 
  

```r
par(mfrow = c(1,3))
hist(gk_ocupado)
hist(gk_desocupado)
hist(gk_Inactivo)
```


<img src="Recursos/Día3/Sesion4/0Recursos/Plot_Bench_gk.jpeg" width="800px" height="200px" style="display: block; margin: auto;" />


  7.    Estimaciones ajustadas por el ponderador
  

```r
estimacionesBench <- estimaciones_mod %>%
  mutate(gk_ocupado, gk_desocupado, gk_Inactivo) %>%
  transmute(
    dam,
    dam2,
    wi,gk_ocupado, gk_desocupado, gk_Inactivo,
    Ocupado_Bench = Ocupado_mod*gk_ocupado,
    Desocupado_Bench = Desocupado_mod*gk_desocupado,
    Inactivo_Bench = Inactivo_mod*gk_Inactivo
  )
```

  8.    Validación de resultados. 
  

```r
tabla_validar <- estimacionesBench %>%
  group_by(dam) %>% 
  summarise(Ocupado_Bench = sum(wi*Ocupado_Bench),
            Desocupado_Bench = sum(wi*Desocupado_Bench),
            Inactivo_Bench = sum(wi*Inactivo_Bench)) %>% 
  inner_join(indicador_agregado) 
tabla_validar %>% tba()
```

<table class="table table-striped lightable-classic" style="width: auto !important; margin-left: auto; margin-right: auto; font-family: Arial Narrow; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> dam </th>
   <th style="text-align:right;"> Ocupado_Bench </th>
   <th style="text-align:right;"> Desocupado_Bench </th>
   <th style="text-align:right;"> Inactivo_Bench </th>
   <th style="text-align:right;"> Ocupado </th>
   <th style="text-align:right;"> Desocupado </th>
   <th style="text-align:right;"> Inactivo </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 01 </td>
   <td style="text-align:right;"> 0.5974 </td>
   <td style="text-align:right;"> 0.0336 </td>
   <td style="text-align:right;"> 0.3690 </td>
   <td style="text-align:right;"> 0.5974 </td>
   <td style="text-align:right;"> 0.0336 </td>
   <td style="text-align:right;"> 0.3690 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 02 </td>
   <td style="text-align:right;"> 0.5552 </td>
   <td style="text-align:right;"> 0.0276 </td>
   <td style="text-align:right;"> 0.4172 </td>
   <td style="text-align:right;"> 0.5552 </td>
   <td style="text-align:right;"> 0.0276 </td>
   <td style="text-align:right;"> 0.4172 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 03 </td>
   <td style="text-align:right;"> 0.5824 </td>
   <td style="text-align:right;"> 0.0297 </td>
   <td style="text-align:right;"> 0.3879 </td>
   <td style="text-align:right;"> 0.5824 </td>
   <td style="text-align:right;"> 0.0297 </td>
   <td style="text-align:right;"> 0.3879 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 04 </td>
   <td style="text-align:right;"> 0.6429 </td>
   <td style="text-align:right;"> 0.0205 </td>
   <td style="text-align:right;"> 0.3365 </td>
   <td style="text-align:right;"> 0.6429 </td>
   <td style="text-align:right;"> 0.0205 </td>
   <td style="text-align:right;"> 0.3365 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 05 </td>
   <td style="text-align:right;"> 0.5331 </td>
   <td style="text-align:right;"> 0.0352 </td>
   <td style="text-align:right;"> 0.4316 </td>
   <td style="text-align:right;"> 0.5331 </td>
   <td style="text-align:right;"> 0.0352 </td>
   <td style="text-align:right;"> 0.4316 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 06 </td>
   <td style="text-align:right;"> 0.6115 </td>
   <td style="text-align:right;"> 0.0239 </td>
   <td style="text-align:right;"> 0.3645 </td>
   <td style="text-align:right;"> 0.6115 </td>
   <td style="text-align:right;"> 0.0239 </td>
   <td style="text-align:right;"> 0.3645 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 07 </td>
   <td style="text-align:right;"> 0.6799 </td>
   <td style="text-align:right;"> 0.0158 </td>
   <td style="text-align:right;"> 0.3043 </td>
   <td style="text-align:right;"> 0.6799 </td>
   <td style="text-align:right;"> 0.0158 </td>
   <td style="text-align:right;"> 0.3043 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 08 </td>
   <td style="text-align:right;"> 0.5465 </td>
   <td style="text-align:right;"> 0.0316 </td>
   <td style="text-align:right;"> 0.4219 </td>
   <td style="text-align:right;"> 0.5465 </td>
   <td style="text-align:right;"> 0.0316 </td>
   <td style="text-align:right;"> 0.4219 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 09 </td>
   <td style="text-align:right;"> 0.5142 </td>
   <td style="text-align:right;"> 0.0601 </td>
   <td style="text-align:right;"> 0.4257 </td>
   <td style="text-align:right;"> 0.5142 </td>
   <td style="text-align:right;"> 0.0601 </td>
   <td style="text-align:right;"> 0.4257 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 10 </td>
   <td style="text-align:right;"> 0.5668 </td>
   <td style="text-align:right;"> 0.0303 </td>
   <td style="text-align:right;"> 0.4030 </td>
   <td style="text-align:right;"> 0.5668 </td>
   <td style="text-align:right;"> 0.0303 </td>
   <td style="text-align:right;"> 0.4030 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 11 </td>
   <td style="text-align:right;"> 0.5666 </td>
   <td style="text-align:right;"> 0.0334 </td>
   <td style="text-align:right;"> 0.4000 </td>
   <td style="text-align:right;"> 0.5666 </td>
   <td style="text-align:right;"> 0.0334 </td>
   <td style="text-align:right;"> 0.4000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 12 </td>
   <td style="text-align:right;"> 0.6310 </td>
   <td style="text-align:right;"> 0.0195 </td>
   <td style="text-align:right;"> 0.3495 </td>
   <td style="text-align:right;"> 0.6310 </td>
   <td style="text-align:right;"> 0.0195 </td>
   <td style="text-align:right;"> 0.3495 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 13 </td>
   <td style="text-align:right;"> 0.6044 </td>
   <td style="text-align:right;"> 0.0216 </td>
   <td style="text-align:right;"> 0.3740 </td>
   <td style="text-align:right;"> 0.6044 </td>
   <td style="text-align:right;"> 0.0216 </td>
   <td style="text-align:right;"> 0.3740 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 14 </td>
   <td style="text-align:right;"> 0.5697 </td>
   <td style="text-align:right;"> 0.0356 </td>
   <td style="text-align:right;"> 0.3946 </td>
   <td style="text-align:right;"> 0.5697 </td>
   <td style="text-align:right;"> 0.0356 </td>
   <td style="text-align:right;"> 0.3946 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 15 </td>
   <td style="text-align:right;"> 0.5290 </td>
   <td style="text-align:right;"> 0.0428 </td>
   <td style="text-align:right;"> 0.4282 </td>
   <td style="text-align:right;"> 0.5290 </td>
   <td style="text-align:right;"> 0.0428 </td>
   <td style="text-align:right;"> 0.4282 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 16 </td>
   <td style="text-align:right;"> 0.6337 </td>
   <td style="text-align:right;"> 0.0185 </td>
   <td style="text-align:right;"> 0.3478 </td>
   <td style="text-align:right;"> 0.6337 </td>
   <td style="text-align:right;"> 0.0185 </td>
   <td style="text-align:right;"> 0.3478 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 17 </td>
   <td style="text-align:right;"> 0.5972 </td>
   <td style="text-align:right;"> 0.0285 </td>
   <td style="text-align:right;"> 0.3743 </td>
   <td style="text-align:right;"> 0.5972 </td>
   <td style="text-align:right;"> 0.0285 </td>
   <td style="text-align:right;"> 0.3743 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 18 </td>
   <td style="text-align:right;"> 0.6331 </td>
   <td style="text-align:right;"> 0.0204 </td>
   <td style="text-align:right;"> 0.3466 </td>
   <td style="text-align:right;"> 0.6331 </td>
   <td style="text-align:right;"> 0.0204 </td>
   <td style="text-align:right;"> 0.3466 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 19 </td>
   <td style="text-align:right;"> 0.5429 </td>
   <td style="text-align:right;"> 0.0366 </td>
   <td style="text-align:right;"> 0.4205 </td>
   <td style="text-align:right;"> 0.5429 </td>
   <td style="text-align:right;"> 0.0366 </td>
   <td style="text-align:right;"> 0.4205 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 20 </td>
   <td style="text-align:right;"> 0.6686 </td>
   <td style="text-align:right;"> 0.0130 </td>
   <td style="text-align:right;"> 0.3184 </td>
   <td style="text-align:right;"> 0.6686 </td>
   <td style="text-align:right;"> 0.0130 </td>
   <td style="text-align:right;"> 0.3184 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 21 </td>
   <td style="text-align:right;"> 0.6505 </td>
   <td style="text-align:right;"> 0.0261 </td>
   <td style="text-align:right;"> 0.3234 </td>
   <td style="text-align:right;"> 0.6505 </td>
   <td style="text-align:right;"> 0.0261 </td>
   <td style="text-align:right;"> 0.3234 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 22 </td>
   <td style="text-align:right;"> 0.5746 </td>
   <td style="text-align:right;"> 0.0338 </td>
   <td style="text-align:right;"> 0.3916 </td>
   <td style="text-align:right;"> 0.5746 </td>
   <td style="text-align:right;"> 0.0338 </td>
   <td style="text-align:right;"> 0.3916 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 23 </td>
   <td style="text-align:right;"> 0.5785 </td>
   <td style="text-align:right;"> 0.0433 </td>
   <td style="text-align:right;"> 0.3782 </td>
   <td style="text-align:right;"> 0.5785 </td>
   <td style="text-align:right;"> 0.0433 </td>
   <td style="text-align:right;"> 0.3782 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 24 </td>
   <td style="text-align:right;"> 0.5796 </td>
   <td style="text-align:right;"> 0.0272 </td>
   <td style="text-align:right;"> 0.3932 </td>
   <td style="text-align:right;"> 0.5796 </td>
   <td style="text-align:right;"> 0.0272 </td>
   <td style="text-align:right;"> 0.3932 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 25 </td>
   <td style="text-align:right;"> 0.5385 </td>
   <td style="text-align:right;"> 0.0310 </td>
   <td style="text-align:right;"> 0.4305 </td>
   <td style="text-align:right;"> 0.5385 </td>
   <td style="text-align:right;"> 0.0310 </td>
   <td style="text-align:right;"> 0.4305 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 26 </td>
   <td style="text-align:right;"> 0.5615 </td>
   <td style="text-align:right;"> 0.0324 </td>
   <td style="text-align:right;"> 0.4061 </td>
   <td style="text-align:right;"> 0.5615 </td>
   <td style="text-align:right;"> 0.0324 </td>
   <td style="text-align:right;"> 0.4061 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 27 </td>
   <td style="text-align:right;"> 0.5990 </td>
   <td style="text-align:right;"> 0.0301 </td>
   <td style="text-align:right;"> 0.3709 </td>
   <td style="text-align:right;"> 0.5990 </td>
   <td style="text-align:right;"> 0.0301 </td>
   <td style="text-align:right;"> 0.3709 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 28 </td>
   <td style="text-align:right;"> 0.5416 </td>
   <td style="text-align:right;"> 0.0295 </td>
   <td style="text-align:right;"> 0.4289 </td>
   <td style="text-align:right;"> 0.5416 </td>
   <td style="text-align:right;"> 0.0295 </td>
   <td style="text-align:right;"> 0.4289 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 29 </td>
   <td style="text-align:right;"> 0.5928 </td>
   <td style="text-align:right;"> 0.0263 </td>
   <td style="text-align:right;"> 0.3809 </td>
   <td style="text-align:right;"> 0.5928 </td>
   <td style="text-align:right;"> 0.0263 </td>
   <td style="text-align:right;"> 0.3809 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 30 </td>
   <td style="text-align:right;"> 0.5971 </td>
   <td style="text-align:right;"> 0.0200 </td>
   <td style="text-align:right;"> 0.3829 </td>
   <td style="text-align:right;"> 0.5971 </td>
   <td style="text-align:right;"> 0.0200 </td>
   <td style="text-align:right;"> 0.3829 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 31 </td>
   <td style="text-align:right;"> 0.6536 </td>
   <td style="text-align:right;"> 0.0193 </td>
   <td style="text-align:right;"> 0.3271 </td>
   <td style="text-align:right;"> 0.6536 </td>
   <td style="text-align:right;"> 0.0193 </td>
   <td style="text-align:right;"> 0.3271 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 32 </td>
   <td style="text-align:right;"> 0.5875 </td>
   <td style="text-align:right;"> 0.0132 </td>
   <td style="text-align:right;"> 0.3993 </td>
   <td style="text-align:right;"> 0.5875 </td>
   <td style="text-align:right;"> 0.0132 </td>
   <td style="text-align:right;"> 0.3993 </td>
  </tr>
</tbody>
</table>


  9. Guardar resultados 
  

```r
estimaciones <- inner_join(estimaciones,estimacionesBench)
saveRDS(object = estimaciones, file = "Recursos/Día3/Sesion4/Data/estimaciones_Bench.rds")
```



## Mapas del mercado de trabajo.

El código carga las librerías  `sf` y `tmap`. Luego, se lee un archivo shapefile con información geográfica y se utiliza la función 'inner_join' para unirlo con las estimaciones de la encuesta previamente calculadas. Posteriormente, se definen los puntos de corte para la generación de los intervalos de clase en los mapas de cada variable de interés (ocupados, desocupados e inactivos) y se asignan a las variables 'brks_ocupado', 'brks_desocupado' y 'brks_inactivo', respectivamente.


```r
library(sf)
library(tmap)
ShapeSAE <- read_sf("Shape/MEX_dam2.shp")

P1_empleo <- tm_shape(ShapeSAE %>%
                           inner_join(estimaciones))
brks_ocupado <- seq(0.2,0.8,0.1)
brks_desocupado <- seq(0,0.2,0.05)
brks_inactivo <- seq(0.17,0.62, 0.09)
```

### Ocupado {-}

Este código está creando un mapa de la variable "Ocupado" utilizando la función `tm_fill()` de la librería `tmap.` Los valores de la variable se clasifican en diferentes categorías utilizando la función breaks, y se establece un título para la leyenda del mapa con el argumento title. Se utiliza una paleta de colores llamada "-Blues" para representar las diferentes categorías de la variable en el mapa. La función tm_layout se utiliza para establecer algunas características del diseño del mapa, como el tamaño de la leyenda, el tamaño de la fuente, y la relación de aspecto del mapa. Finalmente, el mapa se guarda en la variable Mapa_ocupado. 


```r
Mapa_ocupado <-
  P1_empleo +
  tm_fill("Ocupado_Bench",
          breaks = brks_ocupado,
          title = "Ocupado",
          palette = "-Blues") +
  tm_layout(
    legend.only = FALSE,
    legend.height = -0.3,
    legend.width = -0.2,
    asp = 1.5,
    legend.text.size = 3,
    legend.title.size = 3
  )

tmap_save(
  Mapa_ocupado,
  filename = "Recursos/Día3/Sesion4/0Recursos/Ocupados.png",
  width = 3500,
  height = 2500,
  asp = 0
)

Mapa_ocupado
```


<img src="Recursos/Día3/Sesion4/0Recursos/Ocupados.png" width="800%" style="display: block; margin: auto;" />

### Desocupado {-} 

Este código utiliza la función `tm_fill()` de la librería `tmap` para crear un mapa temático del indicador de "desocupado" a nivel de las áreas geográficas definidas en el archivo de polígonos `ShapeSAE`. La paleta de colores utilizada para representar los valores del indicador es la "YlOrRd". Se especifican los mismos parámetros de `tm_layout()` que en el mapa anterior para definir el diseño general del mapa.


```r
Mapa_desocupado <-
  P1_empleo + tm_fill(
    "Desocupado_Bench",
    breaks = brks_desocupado,
    title =  "Desocupado",
    palette = "YlOrRd"
  ) + tm_layout(
    legend.only = FALSE,
    legend.height = -0.3,
    legend.width = -0.2,
    asp = 1.5,
    legend.text.size = 3,
    legend.title.size = 3
  )


tmap_save(
  Mapa_desocupado,
  filename = "Recursos/Día3/Sesion4/0Recursos/Desocupados.png",
  width = 3500,
  height = 2500,
  asp = 0
)

Mapa_desocupado
```


<img src="Recursos/Día3/Sesion4/0Recursos/Desocupados.png" width="800%" style="display: block; margin: auto;" />


### Inactivo {-} 

Este código genera un mapa temático de la variable "Inactivo" utilizando la librería `tmap`. Primero se carga el archivo de `shapefile` y se hace una unión con las estimaciones previamente calculadas. Luego se utiliza la función `tm_fill()` para especificar que se desea utilizar el valor de la variable "Inactivo" para el relleno del mapa. Se definen los intervalos de la paleta de colores con la variable "brks_inactivo" y se especifica el título del mapa con la opción "title". Finalmente, se configura el diseño del mapa con la función `tm_layout()`, donde se ajustan parámetros como el tamaño del texto y de la leyenda, y se establece el aspecto del mapa en 1.5 para una mejor visualización.


```r
Mapa_Inactivo <-
  P1_empleo + tm_fill(
      "Inactivo_Bench",
    title =  "Inactivo",
    breaks = brks_inactivo,
    palette = "YlGn"
  ) + tm_layout(
    legend.only = FALSE,
    legend.height = -0.3,
    legend.width = -0.2,
    asp = 1.5,
    legend.text.size = 3,
    legend.title.size = 3
  )


tmap_save(
  Mapa_Inactivo,
  filename = "Recursos/Día3/Sesion4/0Recursos/Inactivo.png",
  width = 3500,
  height = 2500,
  asp = 0
)

Mapa_Inactivo
```

<img src="Recursos/Día3/Sesion4/0Recursos/Inactivo.png" width="800%" style="display: block; margin: auto;" />

    
  
