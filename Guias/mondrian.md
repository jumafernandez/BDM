# Guía de LABORATORIO: Definición de cubos multidimensionales con Pentaho Schema Workbench

## Introducción

Mondrian es básicamente un archivo XML que define la base de datos multidimensional que hace de capa de abstracción y nos permite hacer querys MDX a una base de datos relacional.

Schema-workbench es una herramienta visual para crear los cubos y publicarlos en el servidor de Pentaho para su uso.

Este esquema se llama ROLAP como vimos en las clases.

## Requerimientos

Para empezar con el desarrollo del cubo es necesario:

- Tener java instalado en la máquina (jdk de 64 bits, que ya viene con le jre).
- Configurar las variables de entorno JAVA_HOME y JRE_HOME.
- Descargar Mondrian.
- Instalar alguna base de datos y su correspondiente driver, en este ejemplo se va a utilizar MySQL.

## Base de datos

![texto](./imgs/sw_bd.png)

## Aplicación

Para correr el programa desde la consola, hay que ejecutar la siguiente línea

- schema-workbench.bat

----



## Creación de un cubo

Lo primero que hay que configurar es la conexión, en el caso de utilizar otra base de datos, hay que descargar
el correspondiente driver java y colocarlo en la carpeta schema-workbench/drivers

![texto](./imgs/sw_0.png)

Crear un schema desde la opción File -> New -> Schema

![texto](./imgs/sw_1.png)

Ponerle un nombre al schema

![texto](./imgs/sw_2.png)

Ahora vamos a definir una dimensión y ponerle un nombre

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


Driver MySQL

https://dev.mysql.com/downloads/connector/j/

Documentación de Mondrian

https://mondrian.pentaho.com/documentation/installation_es.php
https://mondrian.pentaho.com/documentation/workbench.php
https://help.pentaho.com/Documentation/8.1
https://help.pentaho.com/Documentation/8.1/Products/Schema_Workbench
