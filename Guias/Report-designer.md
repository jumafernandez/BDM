# Guía de LABORATORIO: Introducción a la creación de reportes con Report Designer (Pentaho)

## Introducción a Report Designer
Report Designer es la herramienta de reporting de la Suite Pentaho y es utilizada para la creación de reportes ad hoc. Dado que la definición de la estructura del reporte se realiza de forma separada de la definición de los datos del contenido, tiene la ventaja con respecto a los reportes ad hoc tradicionales que cualquier modificación en el origen de datos será reflejada en el informe de forma automática. Podemos acceder a información mas detallada de la herramienta ingresando [acá.](https://help.pentaho.com/Documentation/8.1/Products/Report_Designer)

## Creación de Reportes con Report Designer
Para ingresar a Report Designer, debemos descomprimir la carpeta descargada desde la web de [Hitachi Vantara](https://community.hitachivantara.com/docs/DOC-1009856-pentaho-reporting) y ejecutar el archivo report-designer (.sh en Ubuntu y .bat en Windows) luego de configurar la variable JAVA_HOME como se explica [aquí.](https://www.dropbox.com/s/au05tj4qn63h8xx/GL00%20-%20Gu%C3%ADa%20de%20Instalaci%C3%B3n%20Suite%20Pentaho.pdf?dl=0)

![Pantalla Report Designer](./imgs/rd-screen.png)

En la imagen se puede ver la distribución del home de la herramienta:
- A la izquierda, los diferentes componentes que podemos incorporar en nuestro reporte.
- En el centro, el paño en blanco que representa nuestro reporte y es donde vamos a incorporar los componentes y las definiciones.
- A la derecha podemos encontrar una columna con dos pestañas:
  - La primera, "Structure", donde podemos ver los componentes definidos para cada sección de nuestro reporte y definir todas las cuestiones inherentes al formato.
  - La segunda, "Data", donde vamos a definir los orígenes de datos desde los cuales vamos a consumir la información para los reportes.

__Ejemplo de la Guia:__ En esta guía vamos a graficar los conceptos desarrollando un reporte que liste y grafique (por especialidad) todos los medios de la provincia de Santa Cruz.

## Estructura de un Reporte
Los reportes en general, y en Report Designer en particular, tienen las siguientes secciones:
![Report Designer Estructura](./imgs/rd-structure.png)

Las secciones se explican a continuación:
- __Page Header & Footer:__ Estas dos secciones representan los típicos encabezados y pies de páginas y suelen no modificarse a lo largo de un informe. En general, se utilizan para incorporar los logos institucionales, nombres de las áreas, números de páginas, fecha, etc.
- __Report Header, Details & Footer:__ Estas tres secciones son utilizadas para organizar los elementos de cada reporte. En general, el encabezado es utilizado para explicar la misión del reporte con un título y una breve explicación, mientras que en details puede observarse información desagregada, generalmente a partir de una tabla o detalle a la vez que en el pie del reporte generalmente se presenta algún gráfico que pueda sintetizar esa información o complementarla.

## Paso 1: Configurando los datasources de nuestro Reporte
Para configurar los datasources que serán consumidos para armar el reporte, debemos presionar el botón derecho sobre el ícono "Data Sets" de la pestaña Data (derecha de la pantalla).
![Report Designer Data](./imgs/rd-data.png)

Luego, si por ejemplo deseamos conectarnos a una Base de datos relacional, el proceso será similar al que realizamos en CDE.
![Report Designer Datasource](./imgs/rd-datasource.png)

A continuación, vemos el editor del query SQL donde escribimos el query que recuperará la información que volcaremos en nuestro reporte; es importante hacer notar que cada componente espera la información de una manera distinta. 
Por un lado, para el listado de medios, vamos a seleccionar un conjunto de atributos de cada uno de los medios de la provincia de Santa Cruz:
![Report Designer query1](./imgs/rd-query1.png)

Por el otro, en el caso del gráfico de torta, que es el ejemplo que vamos a trabajar, el componente espera que le enviemos la información con una lista de etiquetas (leyenda de la barra) y un valor cuantitativo para cada etiqueta (alto de la barra).
![Report Designer query2](./imgs/rd-query2.png)
