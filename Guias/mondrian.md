# Guía de LABORATORIO: Definición de cubos multidimensionales con Pentaho Schema Workbench (Mondrian)

## Introducción

### Conceptos iniciales

Mondrian Schema Workbench es una herramienta con una interfaz visual para crear cubos OLAP para luego procesar, a través del motor Mondrian, las solicitudes MDX contra esquemas ROLAP (Relacional OLAP, como vimos en clase). 
La herramienta genera estos esquemas a través de la denifición de modelos sobre los metadatos del esquema ROLAP en un archivo XML que consta de una estructura específica. Estos modelos XML pueden considerarse estructuras en forma de cubo que utilizan las tablas de hechos y dimensiones que se encuentran en el Sistema Gestor de Base de Datos Relacional utilizado (en el ejemplo que sigue será  MySQL). 
Como abordamos de forma teórica, los esquemas ROLAP no requieren que se construya o mantenga un cubo físico real; solo se crea el modelo de metadatos, que hace las veces de "cubo lógico".

### Requerimientos de Mondrian

Para empezar con el desarrollo del cubo es necesario:
- Tener Java instalado en la máquina (jdk de 64 bits, que ya viene con JRE).
- Configurar las variables de entorno JAVA_HOME (JDK) y JRE_HOME (JRE) (![Anexo I: Guía de Instalación Pentaho](https://github.com/jumafernandez/BDM/blob/master/Guias/Gu%C3%ADa%20de%20Instalaci%C3%B3n%20Suite%20Pentaho.pdf)).
- Descargar Mondrian Schema Workbench.
- Instalar un SGBD relacional y descargar su correspondiente driver (en este ejemplo vamos a utilizar MySQL).

### Ejecución de Schema Workbench

Para correr la aplicación, hay que ejecutar la siguiente línea:
- workbench.sh (Ambientes Unix),
- workbench.bat (Ambientes Windows).

----

## Creación y Navegación de Cubos OLAP a través de Mondrian y Saiku (Suite Pentaho) 

El objetivo de esta guía es abordar los siguientes temas paso a paso:
1. Definir un cubo a partir de Schema Workbench (Modelo ROLAP),
2. Navegar el cubo con un Explorador OLAP (Saiku).

Para el abordaje de los temas anteriores, vamos a trabajar a partir de un _esquema de estrella_ para un cubo que permitir realizar análisis respecto de algunas características de los Estudiantes de la UNLu. Como vamos a trabajar sobre un Modelo ROLAP, asumiremos que partimos de una Base de Datos Relacional de MySQL con la siguiente estructura:

![texto](./imgs/sw_bd.png)


### Paso 1: Creación del cubo mediante Mondrian

1. Lo primero que debemos hacer es configurar es la conexión a la base de datos donde se encuentra nuestro modelo físico de la Base de Datos. En este caso, trabajaremos con MySQL, en el caso de utilizar otra base de datos debemos descargar el correspondiente driver Java y colocarlo en la carpeta __schema-workbench/drivers__. Accedemos a la configuración de la conexión de la Base de Datos a partir de la opción _Options > Connection..._ e ingresamos los datos correspondientes al acceso a la Base de Datos:

![texto](./imgs/sw_0.png)

2. Una vez realizada la conexión, debemos crear el Esquema, para ello ingresamos desde la opción _File -> New -> Schema_. Aquí es importante hacer notar que un Schema es el ambiente del Data Warehouse y, como vimos en la clse teórica, un DW puede estar compuesto de múltiples cubos.

![texto](./imgs/sw_1.png)

3. Luego, definimos el nombre que va a identificar a nuestro esquema (DW):

![texto](./imgs/sw_2.png)

4. A continuación, vamos a comenzar por definir cada una de las dimensiones de nuestro Esquema. 

__Muy importante: El caso que vamos a abordar consta de un Data Warehouse MUY simple que consta de un solo Cubo. En general, los DW se enfocan en múltiples aspectos de la organización y poseen mas de un Cubo. Para esos casos, iremos creando cubos que dependan del esquema a partir de la opción "Add cube" que aparece cuando presionamos click derecho sobre el Schema.__

5. Realizada la salvedad anterior, vamos a trabajar, __en este caso__, directamente sobre el Schema definiendo las métricas y dimensiones del cubo. Iniciamos la definición a partir de las dimensiones:

![texto](./imgs/sw_3.png)

Por defecto crea una jerarquía, dejarla sin nombre

![texto](./imgs/sw_4.png)

Vamos a agregar la tabla que corresponde a esta dimensión

![texto](./imgs/sw_5.png)

Si la conexión es correcta, nos despliega las tablas de la base de datos

![texto](./imgs/sw_6.png)

Ahora hay que agregar un nivel

![texto](./imgs/sw_7.png)

Acá vamos a relacionar la tabla de la dimensión, en el campo column va el identificador y el nameColumn el campo descripción de la tabla

![texto](./imgs/sw_8.png)

Esto lo hacemos con todas las dimensiones.

En este ejemplo, las dimensiones se agregan fuera del cubo que vamos a agregar porque en esquemas más complejos en los que necesitamos más de un cubo, es probable que necesitemos compartir las dimensiones, las que se definen dentro de los cubos son solamente para el cubo en cuestión

Una vez que terminamos, vamos a agregar el cubo con la tabla de hechos y sus relaciones.

Creamos un cubo y le ponemos el nombre de la tabla de hechos

![texto](./imgs/sw_9.png)

Creamos una tabla y seleccionamos la tabla de hechos

![texto](./imgs/sw_10.png)

Ahora vamos a relacionar las dimensiones que creamos anteriormente

Seleccionamos la opcion dimension usage en vez de crear una normal, esto nos permite seleccionar las dimensiones que tenemos disponibles en el esquema

![texto](./imgs/sw_11.png)

Le ponemos le nombre, seleccionamos la foreign key de la tabla de hechos que apunta a la tabla de la dimensión y en source, seleccionamos la dimensión que creamos anteriormente

![texto](./imgs/sw_12.png)

Hacemos esto con todas las dimensiones que creamos en el esquema

Lo que falta es definir las medidas que va a tener el cubo, vamos a agregar una que cuente la cantidad de alumnos.

Agregamos una medida

![texto](./imgs/sw_13.png)

En el campo agregator, seleccionamos la función que se va a calcular para este campo

![texto](./imgs/sw_14.png)

En el campo column, seleccionamos el campo con el que se va a realizar el cálculo, en este caso como sólo es contar, podría seleccionar cualquiera

![texto](./imgs/sw_15.png)

Ya tenemos el cubo listo para publicar

![texto](./imgs/sw_16.png)

Vamos a publicar el cubo

![texto](./imgs/sw_17.png)

Completamos los datos que apuntan al servidor de Pentaho y publicamos

![texto](./imgs/sw_18.png)

En Pentaho, aparece el cubo que acabamos de publicar para poder realizar en un análisis

![texto](./imgs/sw_19.png)

Con la herramienta Saiku, podemos mezclar las dimensiones y ver como se calcula la medida

![texto](./imgs/sw_20.png)

Incluso podemos hacer gráficos con el mismo cruce de los datos

![texto](./imgs/sw_21.png)

## Links

Driver MySQL

https://dev.mysql.com/downloads/connector/j/

Java JDK

https://www.oracle.com/java/technologies/jdk8-downloads.html

Mondrian

https://mondrian.pentaho.com/documentation/installation_es.php

https://mondrian.pentaho.com/documentation/workbench.php

https://help.pentaho.com/Documentation/8.1/Products/Schema_Workbench

Pentaho

https://www.hitachivantara.com/go/pentaho.html

https://help.pentaho.com/Documentation/8.1

Saiku

https://saiku-documentation.readthedocs.io/en/latest/
