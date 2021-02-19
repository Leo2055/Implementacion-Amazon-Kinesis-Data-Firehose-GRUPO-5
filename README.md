# Implementacion-Amazon-Kinesis-Data-Firehose-GRUPO5
Implementación del servicio de AWS - Amazon Kinesis Data Firehose
  
  Implementación de prueba de flujo de entrega con datos de  muestra

Se puede utilizar la Consola de administración de AWS para incorporar datos de tableros de cotizaciones simulados. La consola ejecuta un script en su navegador para colocar registros de muestra en la secuencia de entrega de Kinesis Data Firehose. Esto permite probar la configuración de la secuencia de entrega sin tener que generar nuestros propios datos de prueba. A continuación, se mostrara un ejemplo de datos simulados:

  {"TICKER_SYMBOL":"QXZ","SECTOR":"HEALTHCARE","CHANGE":-0.05,"PRICE":84.51}        

Hay que tener en cuenta que se aplicará la tarifa estándar de Amazon Kinesis Data Firehose cuando la secuencia de entrega transmita los datos, pero la generación de datos no implica cargos. Para detener este cargo, se puede detener el flujo de muestra desde la consola en cualquier momento

Requisitos Previos

Antes de comenzar, se debe crear un flujo de entrega en la sección principal de Amazon kinesis Data Firehose, para ello lo único que hacemos es buscar en la sección de servicios “Amazon Kinesis”, luego aparecerá también las características de este servicio, la cual en este caso se elegirá “Kinesis Data Firehose"

Luego nos enviara a la página principal de Amazon Kinesis Data Firehose, en donde se encuentra el botón “Create Delivery Stream” o en español “Crear flujo de entrega”, lo seleccionamos y nos enviara al proceso de configuración para crear el flujo de entrega.

Primer Paso (nombre y fuente):

1.	En el primer apartado se deberá escribir el “Nombre del flujo de entrega”, para este caso se llamara “Prueba_Entrega-KDF”. 

2.	Luego más abajo nos pedirá “Elegir una fuente” que es donde se presentan las opciones para enviar registros al flujo de entrega. Para este caso se elegirá la opción “Direct PUT u otras fuentes”, después seleccionamos el botón “próximo” para seguir con el segundo paso

Segundo Paso (Procesar registros):

1.	En este apartado trata sobre la “transformación de registros” o la “conversión de registro” antes de la entrega. En la primera opción habla sobre transformar los registros de origen con AWS Lambda. En la segunda opción trata sobre la conversión de formato de registro. En las dos opciones de este apartado se las dejara tal y como esta (deshabilitado) y luego presionamos el botón “próximo”.

Tercer Paso (elegir un destino):

1.	En esta sección se debe elegir el destino en la cual se alojaran los datos de prueba proporcionado por Kinesis Data Firehose. En este caso elegiremos Amazon S3 para efectos de prueba

2.	Más adelante nos encontraremos con el aparatado “Destino S3”, que es donde se deberá elegir un “Bucket S3” en la cual se alojaran los datos enviados. En nuestro caso el Bucket S3 ya creado se llamara “sssss-bucket-s3” (Cabe recalcar que si no se tiene un bucket ya creado, kinesis data firehose da la oportunidad de crearlo en ese momento y desde ese apartado). Luego de esto seleccionamos el botón próximo.

Cuarto Paso (configurar los ajustes):

1.	Al llegar a este apartado se debe configurar las “Condiciones del búfer S3”, en donde se debe especificar el “tamaño del buffer” (MiB) y el “Intervalo de búfer” (comprendido entre 60 y 900 segundos).

2.	Luego se debe seleccionar una opción de permisos. Se puede elegir una función de IAM ya existente o Crear una nueva con el nombre del bucket que ya se creó. Para este caso se creara una nueva y luego presionamos el botón próximo.

Quinto Paso (revisión):

1.	Para este último paso lo que se debe hacer es revisar los datos finales y si se desea se puede editar, en caso contrario podemos ya “Crear el flujo de entrega”.


Prueba con Amazon S3 como destino

1.	Seleccionar la secuencia de entrega, en este caso se denomina “Prueba_Entrega-KDF”

2.	Luego abrimos el apartado “Test with demo data” (en español – Prueba con datos de demostración) y seleccionamos “Start sending demo data” para generar datos de tableros de cotizaciones simulados.

3.	Seguir las instrucciones que aparecen en pantalla para verificar que los datos se están entregando al bucket de S3. Hay que tener en cuenta que posiblemente pasen unos minutos hasta que los objetos aparezcan en el bucket. Esto dependerá de la configuración de búfer del bucket.

4.	Una vez terminada la prueba, seleccionamos “Stop sending demo data” para detener los cargos por uso.

Verificación de Envió de datos a Amazon S3

Seleccionamos el bucket que se creó en Amazon S3, abrimos las carpetas hasta encontrar un archivo, lo abrimos y listo (en el archivo “.txt” se encuentran un conjunto de datos de tableros de cotizaciones simulados que fue generado por el servicio de Amazon Kinesis Data Firehose).
