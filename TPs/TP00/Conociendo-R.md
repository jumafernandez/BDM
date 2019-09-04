

Conociendo R
========================================================
autosize: true
width: 1200
height: 800

(Tips de Programación)

Juan Manuel Fernandez

Bases de Datos Masivas - UNLu
<br />


Sobre la Herramienta
========================================================
R es un lenguaje de programación con un enfoque al análisis estadístico.

R es software libre y es uno de los lenguajes mas utilizados en investigación por la comunidad estadística y minería de datos.

<center>
![plot of chunk unnamed-chunk-1](./images/R-logo.jpg)
</center>

Se distribuye bajo la licencia GNU GPL. Está disponible para los sistemas operativos Unix y GNU/Linux, Windows & Macintosh.
<br />
<br />
[1] https://www.r-project.org/
<br />
[2] https://www.rstudio.com/

Sobre los datos
========================================================
Un dataset consiste en una representación de un conjunto de hechos/individuos a través de un conjunto de características.

Para describir un dataset se analizan esas características (variables) y sus relaciones.

Las variables, a grandes rasgos pueden ser:
- Cualitativas/Discretas. 
- Cuantitativas/Continuas.

Es importante conocer los tipos de datos, dado que ello nos permite decidir que tipo de análisis utilizar.

Sobre el enfoque
========================================================
El análisis de datos exploratorio (EDA) tiene por objetivo identificar las principales características de un conjunto de datos mediante un número reducido de gráficos y/o valores.

Consiste en:
- Medidas cuantitativas de resumen: Métricas que explican propiedades del dataset.
- Visualización de datos: transformaciones a un formato visual que permita identificar las características y relaciones entre los elementos del dataset.

Sobre el dataset para la demostración
========================================================
<small>
Iris: 150 instancias de flores de la planta iris en sus variedades:
- Setosa,
- Versicolor,
- Virginica.

Las caracteristicas son:

```r
data(iris)
names(iris)
```

```
[1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width" 
[5] "Species"     
```
</small>

***
<center>

```r
pie(table(iris$Species))
```

![plot of chunk unnamed-chunk-3](Conociendo-R-figure/unnamed-chunk-3-1.png)
</center>
***

Empezamos: Cargando el dataset
========================================================
autosize: true
<small>
Podemos cargar el dataset de, al menos, dos maneras:
- Gráfica

<center>
![plot of chunk unnamed-chunk-4](./images/load.png)
</center>

Los datasets serán contenidos en un dato de tipo Data.Frame...

***
- Por Código

```r
library(readr)
getwd()
```

```
[1] "C:/Users/unlu/Google Drive/PC-Juan/Docencia  & Investigacion/Docencia/Bases de Datos masivas/Cursada/Trabajos Practicos/TP00 - Revision estadistica/Presentacion"
```

```r
#iris <- read_csv("C:/Users/Usuario/Google Drive/PC-Juan/Docencia  & Investigacion/Docencia/Mineria de Datos-UBA/iris.csv")
```
</small>
***

Nuestro Tipo de dato estrella: el Data.Frame
========================================================
autosize: true
<small>
El dataframe es una estructura de datos similar a la matriz, a diferencia que puede tener columnas con diferentes tipos de datos:

```r
str(iris)
```

```
'data.frame':	150 obs. of  5 variables:
 $ Sepal.Length: num  5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
 $ Sepal.Width : num  3.5 3 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 ...
 $ Petal.Length: num  1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 ...
 $ Petal.Width : num  0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 ...
 $ Species     : Factor w/ 3 levels "setosa","versicolor",..: 1 1 1 1 1 1 1 1 1 1 ...
```
Es la estructura de datos mas utilizada por su versatilidad y potencia. Podemos cargar datasets a partir de distintos tipos de archivos o podemos crearlas a partir de la conjunción de listas/arrays con la función data.frame().
</small>

el Data.Frame - Accediendo a los datos
========================================================
autosize:true
<small>
Accedemos por Atributo/Columna:

```r
iris$Sepal.Length[1:5]
```

```
[1] 5.1 4.9 4.7 4.6 5.0
```

```r
iris[1:5,1]
```

```
[1] 5.1 4.9 4.7 4.6 5.0
```
Accedemos por Instancia/Fila:

```r
iris[3,1:3]
```

```
  Sepal.Length Sepal.Width Petal.Length
3          4.7         3.2          1.3
```

```r
iris[2,-c(4,5)]
```

```
  Sepal.Length Sepal.Width Petal.Length
2          4.9           3          1.4
```
***
Seleccionamos Instancias que cumplen una condición:


```r
iris[iris$Species=="setosa" & iris$Sepal.Length>5.2,3:4]
```

```
   Petal.Length Petal.Width
6           1.7         0.4
11          1.5         0.2
15          1.2         0.2
16          1.5         0.4
17          1.3         0.4
19          1.7         0.3
21          1.7         0.2
32          1.5         0.4
34          1.4         0.2
37          1.3         0.2
49          1.5         0.2
```
</small>

Actualizando el Data.Frame (ABM)
========================================================
autosize:true
<small>
Podemos AGREGAR una instancia o un conjunto de instancias:

```r
nuevas.filas<-data.frame(Sepal.Length=5, Sepal.Width=5, Petal.Length=5, Petal.Width=5, Species="Data Mining")
iris<-rbind(iris, nuevas.filas)
```
Podemos MODIFICAR una instancia o un conjunto de instancias:


```r
iris[1,1:4]=c(4.4,4.4,4.4,4.4)
```

```r
iris[iris$Species=="setosa",1:4]=iris[iris$Species=="setosa",1:4]*5
```
Podemos ELIMINAR una instancia o un conjunto de instancias:

```r
iris<-iris[-c(1:5),]
```
</small>

Conociendo el dataset... y los datos!
========================================================
autosize: true
<small>
Deciamos que para describir un dataset se analizan sus variables y las relaciones entre ellas.
<br />
<br />
<strong>
Nos interesa la distribución de la variable, que está determinada por los valores que toma esa variable y la frecuencia con la que los toma.
A tener en cuenta: 
- Posición, 
- Dispersión,
- Forma.
</strong>
<br />
<br />
Vemos los tipos de variables y un resumen de los valores:


```r
str(iris)
```

```
'data.frame':	150 obs. of  5 variables:
 $ Sepal.Length: num  5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
 $ Sepal.Width : num  3.5 3 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 ...
 $ Petal.Length: num  1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 ...
 $ Petal.Width : num  0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 ...
 $ Species     : Factor w/ 3 levels "setosa","versicolor",..: 1 1 1 1 1 1 1 1 1 1 ...
```
</small>

Conociendo el dataset (++)
========================================================

Vemos el objeto y sus instancias:

```r
View(iris) # Instancias del dataset
```

Mas datos:

```r
summary(iris)
```

```
  Sepal.Length    Sepal.Width     Petal.Length    Petal.Width   
 Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100  
 1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300  
 Median :5.800   Median :3.000   Median :4.350   Median :1.300  
 Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199  
 3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800  
 Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
       Species  
 setosa    :50  
 versicolor:50  
 virginica :50  
                
                
                
```

Ahora vamos a estudiar el dataset...
========================================================

Decimos que nos interesa la distribución de la variable, que está determinada por los valores que toma esa variable y la frecuencia con la que los toma. Las herramientas son:
- Posición: medidas de tendencia central y gráficos (torta, barras & histogramas),
- Dispersión: medidas de dispersión (rangos, percentiles & desvío estandar) y gráficos (boxplot, scatterplot),
- y en consecuencia su forma.

También nos interesa la relación entre las variables:
- Asociación: medidas de asociación (correlación & covarianza) y gráficos (scatterplot & coordenadas paralelas)

Medidas de Posición
========================================================

Entre las medidas de posición mas conocidas se encuentran:
- Media aritmética: Valor promedio entre los valores observados.
- Moda: Valor que mas se repite entre las observaciones.
- Mediana: Valor que divide al medio a las observaciones.

<center>
![plot of chunk unnamed-chunk-20](./images/posicion.png)
</center>

Medidas de Posición -Medidas Cuantitativas-
========================================================

Media aritmética:

```r
mean(iris$Sepal.Length)
```

```
[1] 5.843333
```

Media truncada: (Elimina outliers)

```r
mean(iris$Sepal.Length, 0.05)
```

```
[1] 5.820588
```

Medidas de Posición -Medidas Cuantitativas- (++)
========================================================

Mediana y Moda:

```r
median(iris$Sepal.Length)
```

```
[1] 5.8
```

```r
library(modeest)       #Cargar la libreria
mfv(iris$Sepal.Length)  #Calcular la moda de un atributo
```

```
[1] 5
```

Medidas de Posición -Medidas Cuantitativas- (+++)
========================================================

Aplicando las medidas por especie:

```r
aggregate(Petal.Length ~ Species, data=iris, FUN=median)
```

```
     Species Petal.Length
1     setosa         1.50
2 versicolor         4.35
3  virginica         5.55
```

Medidas de Posición -Análisis Gráfico-
========================================================

Para variables discretas: 
- Gráfico de Torta

```r
pie(table(iris$Species))
```

![plot of chunk unnamed-chunk-25](Conociendo-R-figure/unnamed-chunk-25-1.png)
***
- Gráfico de Barras

```r
barplot(table(iris$Species)) 
```

![plot of chunk unnamed-chunk-26](Conociendo-R-figure/unnamed-chunk-26-1.png)

Medidas de Posición -Analisis Gráfico-
========================================================
<br>
Para variables continuas: Histogramas
<center>

```r
hist(iris$Sepal.Length)
```

![plot of chunk unnamed-chunk-27](Conociendo-R-figure/unnamed-chunk-27-1.png)
</center>

Medidas de Dispersión -Medidas Cuantitativas-
========================================================
Estas medidas nos dicen que tan distintas o similares tienden a ser las observaciones respecto a un valor particular (medida de tendencia central).

Rango:

```r
max(iris$Sepal.Length)-min(iris$Sepal.Length)
```

```
[1] 3.6
```

```r
range(iris$Sepal.Length)
```

```
[1] 4.3 7.9
```
***
Varianza (sumatoria de las diferencias cuadraticas con respecto a la media) y Desvio estandar (raiz cuadrada):

```r
var(iris$Sepal.Length)
```

```
[1] 0.6856935
```

```r
sd(iris$Sepal.Length)
```

```
[1] 0.8280661
```

Medidas de Dispersión -Medidas Cuantitativas- (++)
========================================================
Percentiles
<br />
El percentil k es un valor tal que el p% de las observaciones se encuentran debajo de este y el (100-k))% por encima del mismo.

Cuantil
Caso particular del concepto anterior donde:
- Q1: k=25,
- Q2: k=50,
- Q3: k=75,
- Q4: k=100.

***

<small>

```r
quantile(iris$Sepal.Length,seq(0,1,0.01))
```

```r
quantile(iris$Sepal.Length,seq(0,1,0.25))
```

```
  0%  25%  50%  75% 100% 
 4.3  5.1  5.8  6.4  7.9 
```
</small>

Medidas de Dispersión -Análisis Gráfico-
========================================================
<small>
Diagramas de Cajas: Brindan informacion sobre
- Posición y dispersión,
- Simetría de la distribución,
- Valores atípicos.
<center>
![plot of chunk unnamed-chunk-32](./images/boxplot.png)
</center>

***
<center>

```r
boxplot(iris$Sepal.Length ~ iris$Species)
```

![plot of chunk unnamed-chunk-33](Conociendo-R-figure/unnamed-chunk-33-1.png)
</center>
</small>

Medidas de Dispersión -Análisis Gráfico- (++)
========================================================
<left>
Diagramas de dispersión: Muestran la dispersión de valores observados de acuerdo
a dos variables.
</left>
<center>

```r
plot(iris$Petal.Length, iris$Petal.Width,col=iris$Species)
```

![plot of chunk unnamed-chunk-34](Conociendo-R-figure/unnamed-chunk-34-1.png)
</center>
***
<center>

```r
pairs(iris[,1:4],col=iris$Species)
```

![plot of chunk unnamed-chunk-35](Conociendo-R-figure/unnamed-chunk-35-1.png)
</center>

Medidas de Asociación -Medidas Cuantitativas-
========================================================
Estas medidas son utilizadas para verificar como varía una variable con respecto a otra.<br /><br />
Podemos calcular la covarianza (dependiente de la escala de las variables)

```r
cov(iris$Petal.Length,iris$Petal.Width)
```

```
[1] 1.295609
```
O el coeficiente de correlación de Pearson (normalizado)

```r
cor(iris$Petal.Length,iris$Petal.Width)
```

```
[1] 0.9628654
```

Medidas de Asociación -Análisis Gráfico-
========================================================
Para estudiar las relaciones entre variables, podemos utilizar:
- Scatter Plot 2d y 3d (libreria scatterplot3d),
- Gráfico de coordenadas paralelas,
- Tablas de contingencia (variables discretas).

Scatter 3D:

```r
library(scatterplot3d)
scatterplot3d(iris$Sepal.Length, iris$Sepal.Width, iris$Petal.Length)
```
***
![plot of chunk unnamed-chunk-39](Conociendo-R-figure/unnamed-chunk-39-1.png)

Medidas de Asociación -Análisis Gráfico- (++)
========================================================
Gráfico de coordenadas paralelas:
<center>

```r
library(MASS)
parcoord(iris[1:4], col=iris$Species,var.label=T)
```

![plot of chunk unnamed-chunk-40](Conociendo-R-figure/unnamed-chunk-40-1.png)
</center>
