# TesisComparador
Archivos de la tesis de comparativa de Stack Overflow

# *IMPORTANTE*
Para replicar el comparador primero debemos empezar por el Traductor, para ello vamos a ejecutar en un entorno que soporte el lenguaje phyton (p. ej: el entorno de google colab, que fue donde se realizó el proyecto), tener en cuenta que debe ser realizado secuencialmente la corrida de los comandos en el colab.
El traductor es para traducir oraciones de español a su versión en inglés
Otra cosa a tener en cuenta es que al usar google colab se recomienda tener espacio en el drive, así como una suscripción al colab debido a que consume mas recursos de la cantidad que ofrece de manera gratuita

# *--------------------------TRANSFORMER---------------------------------*

## *LIBRERIAS*

Empezamos cargando las librerias del traductor 
![image](https://user-images.githubusercontent.com/107890153/225494549-cfd0d521-14a1-40c2-9a7b-7ada8cb68722.png)

## *HIPERPARAMETROS*

Luego de eso, ajustamos los hiperparametros de nuestro modelo en base a como querremos que estén configurados, los parametros a tomarse en cuenta son:

![image](https://user-images.githubusercontent.com/107890153/225496030-f7d5334c-b0db-4505-8269-285a27a6fe69.png)


NUM_SAMPLES -> que indica el número de muestras que tendrá nuestro dataset con el que vamos a entrenar 

MAX_VOCAB_SIZE -> indica el número maximo de vocabulario que habrá (aquí se utilizó la formula de potenciación ** , de igual forma se puede establecer un número si se lo desea)

BATCH_SIZE -> indica el tamaño de lotes para el entrenamiento

EPOCHS -> indica el número de epocas por la cual se va a entrenar nuestro modelo transformer (en este caso se dejó como 1 debido a que ya se entrenó previamente y los checkpoints ya se encuentran generados por lo que solo se cargaría) 

MAX_LENGTH -> indica el número máximo de caracteres que tendrá las palabras de nuestro vocabulario

## *PARAMETROS GLOBALES*

Ajustamos los parametros globales que serán donde guardaremos checkpoints y la data 

![image](https://user-images.githubusercontent.com/107890153/225497047-15103b08-0430-4ebb-97fc-d39c562da9fb.png)

## *PROCESAMIENTO DE TEXTOS Y DATASET*

Luego de realizar el ajuste de parametros se procede a ejecutar el procesamiento de texto

![image](https://user-images.githubusercontent.com/107890153/225498383-f6e97d38-1499-4c8f-b1af-2388890008d4.png)

Y luego se ejecuta la celda de cargar el dataset desde nuestro drive (al ejecutarlo nos pedirá que ingresemos a una cuenta)

![image](https://user-images.githubusercontent.com/107890153/225498680-60ce96ac-1840-421c-90f8-a5e12366aa04.png)

## *TOKENS, TRANSFORMER Y DECODER*

Continuamos ejecutando los bloques durante todas las secuencias de tokenizar la data y para preparar el transformer previo al entrenamiento

![image](https://user-images.githubusercontent.com/107890153/225499071-cc37bac9-120d-4db4-b6e6-1f31ae7f113e.png)

![image](https://user-images.githubusercontent.com/107890153/225500584-75b42042-7a54-4df7-92cf-4cf10bc8329b.png)

![image](https://user-images.githubusercontent.com/107890153/225500808-13df88ae-aa3b-462f-be1e-1a68231de021.png)

![image](https://user-images.githubusercontent.com/107890153/225500934-3d6ccc8f-7cc9-4288-8e97-e9919dc9804b.png)

## *CHECKPOINTS Y ENTRENAMIENTO*

Al ejecutar la celda de entrenamiento, si hay puntos de control (checkpoints) previamente guardados, los restaurará para que se continue con el entrenamiento, caso contrario, empezará el entrenamiento desde 0

![image](https://user-images.githubusercontent.com/107890153/225501604-49d419ab-235f-469f-86cd-f78208bd1552.png)

El entrenamiento se hará en base al número de epocas indicado al inicio, tener en cuenta que en base a dichas epocas se tomará su tiempo determinado

![image](https://user-images.githubusercontent.com/107890153/225503158-d96e87c3-0af5-4657-a840-7a8980def627.png)

## *RESULTADOS DEL ENTRENAMIENTO*

Una vez que se realizó el entrenamiento, la siguiente celda de comandos mostrará los resultados de la precisión y de la perdida de precisión

![image](https://user-images.githubusercontent.com/107890153/225503451-b9f96fb5-b12e-4c0d-a6ad-47c64504c861.png)

## *TRADUCCIONES*

Se procede a ejecutar las 2 siguientes celdas de comando que servirán para realizar la traducción

![image](https://user-images.githubusercontent.com/107890153/225504581-55214b1f-9b4f-4328-8613-e5e7c35cc35d.png)

![image](https://user-images.githubusercontent.com/107890153/225504133-04060777-f283-47b2-9697-080d912c9ee7.png)

Una vez ejecutadas se puede ingresar un query en las oraciones de prueba para verificar la precisión de nuestro entrenamiento 

![image](https://user-images.githubusercontent.com/107890153/225504888-b642af2e-01d3-4693-94fa-5b6d7f5a3150.png)

# *--------------------------COMPARADOR---------------------------------*

## *Instalación de flair*

Previo a la importación de librerias, debemos instalar los siguientes paquetes de flair, así como una pequeña actualización de la libreria de pandas

![image](https://user-images.githubusercontent.com/107890153/225508552-29fb4270-d6c7-420b-834e-4ace20a2d779.png)

## *IMPORTACIÓN DE LIBRERIAS Y DATASET*

Se procede a importar las librerias que se van a utilizar para el comparador

![image](https://user-images.githubusercontent.com/107890153/225509480-303a45ef-7a8d-46e9-8bc7-1ab06bfbcd48.png)

Así como un dataset para que se realice la comparación

![image](https://user-images.githubusercontent.com/107890153/225509745-5986dbf9-5c91-4859-b77e-531ec741c892.png)

## *IMPORTACIÓN DEL TRADUCTOR*

Con el traductor previamente entrenado, procederemos a ingresar un query con la oración que queremos buscar y ejecutamos el traductor

![image](https://user-images.githubusercontent.com/107890153/225510081-492eee9f-35cd-4028-9b08-4ca833002ed0.png)

## *COMPARADOR*

Se procede a ejecutar el comparador el cual nos dará los resultados basandonos en 2 modelos: Word2vec (específicamente Glove) y Bert

![image](https://user-images.githubusercontent.com/107890153/225513039-d66b8f4c-7ce8-4c54-ae56-ec81fbce934f.png)

![image](https://user-images.githubusercontent.com/107890153/225510688-b92042ac-1df5-4ee1-9b9c-18117d61c888.png)


## *TREESHOLD Y CURVA DE ROC*

Ejecutamos nuestra celda de código para realizar el treeshold a nuestro dataset, es decir, para clasificar los datos según lo establecido y luego se presentan estos datos en nuestra curva de ROC

![image](https://user-images.githubusercontent.com/107890153/225510852-316810d9-4df0-413d-91a8-99c6eb7f1891.png)

![image](https://user-images.githubusercontent.com/107890153/225511082-086c2086-3040-4242-8d92-1ecb60f95ee6.png)

![image](https://user-images.githubusercontent.com/107890153/225511165-3a1aa829-f660-4cdd-abb2-a575d805ef62.png)

![image](https://user-images.githubusercontent.com/107890153/225511231-3ed884f5-c271-4a4b-b423-fc3ce8079c8e.png)

## *COMPARATIVA*

Una vez hecha la ejecución de la curva de ROC, se ejecuta la celda para verificar los resultados de nuestro comparador

![image](https://user-images.githubusercontent.com/107890153/225511453-8cd04954-73b9-465a-a01d-145d71ccb019.png)

![image](https://user-images.githubusercontent.com/107890153/225511556-9b6e0edd-750c-443a-94c1-420c57d08075.png)

## *MATRIZ DE CONFUSIÓN*

Se ejecuta las celdas para obtener la matriz de confusión y obtener los valores de "Verdadero positivo" (VP), "Falso positivo" (FP), "Verdadero negativo" (VN) y "Falso negativo" (FN)

![image](https://user-images.githubusercontent.com/107890153/225511711-a0138d31-2a11-4947-ab7c-42d0a484728f.png)

![image](https://user-images.githubusercontent.com/107890153/225513585-de0d0d10-89ef-4774-9103-2f2243541114.png)

