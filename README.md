# Control_de_Calidad
En esta sección aprenderemos brevemente cómo realizar el Análisis de Calidad de las Secuencias, producto del secuenciamiento.
# 1. Términos empleados
## FASTQ

Línea 1: comienza con ‘@’ que contiene información sobre el nombre del secuenciador.

Línea 2: la secuencia de nucleótidos.

Línea 3: Una línea de encabezado o una línea que comience con solo '+'.

Línea 4: representa el puntaje de calidad.


![image](https://user-images.githubusercontent.com/84040152/119056915-21005b00-b991-11eb-9e26-22217e7751dd.png)

- Existen muchos métodos diferentes para codificar los puntajes de calidad de nuestras secuencias.


## FASTA

Secuencia de nucleótidos basado en texto sin puntuación de calidad, que es solo la línea 1 y 2 de FASTQ, tiene un encabezado que comienza con “>” y la siguiente línea en la secuencia.

![image](https://user-images.githubusercontent.com/84040152/119057013-51e09000-b991-11eb-8e8f-7bee8d4c8ee3.png)

# 2. Control de calidad
La primera tarea que tenemos que hacer al recibir una data de secuenciamiento es evaluar su calidad. Para hacer esto usaremos el programa FastQC, la cual es una herramienta de control de calidad para datos NGS. 
FastQC es   util para resumir la calidad de la secuenciación y detección de problemas potenciales.
## 2.1. Instalación de FastQC
* El programa se puede descargar en http://www.bioinformatics.babraham.ac.uk/projects/fastqc/.
- Otra opción es utilizando el siguiente comando:

```
$ wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.4.zip
```
*NOTA: verificar la versión del zip, si es otro, modificar según sea necesario.*

* Una vez descargado el archivo zip, descomprimimos escribiendo:

```
$ unzip fastqc_v0.11.4.zip
```
  
* El folder generado tendrá el nombre de FastQC
  
```  
$ cd FastQC 
```
   
* Dentro de la carpeta FastQC, es útil mirar el archivo INSTALL.TXT para ver algunas instrucciones sobre la instalación y cómo utilizar el sorftware.

- Para hacer ejecutable el software se usará chmod de la siguiente manera:

```   
$ chmod 755 fastqc   
```
 
* Una vez realizado, se puede ejecutar directamente ejecutando: 
 
 ```  
 $ ./fastqc
 ```
  
* También puede colocar un enlace en /usr/local/bin para poder ejecutar el programa desde cualquier lugar.
  
``` 
$ sudo ln -s  /home/manager/FastQC/fastqc  /usr/local/bin/fastqc   
```

* Ahora podemos utilizar el programa desde cualquier lugar, escribiendo:

```
$ fastqc
```
![image](https://user-images.githubusercontent.com/84040152/119067333-6fb8ef80-b9a7-11eb-8433-1e5d695d6bd4.png)


## 2.2. Cómo correr los archivos
### 2.2.1. Correr por medio de la interfaz gráfica

Cargar los archivos en la sección "file" de la siguiente gráfica

![image](https://user-images.githubusercontent.com/84040152/119067417-a4c54200-b9a7-11eb-9ccb-ec589d2d0095.png)

### 2.2.2. Correr por medio de comandos Linux

```
$ ./fastqc good_seq.fastq bad_seq.fastq 
```
* En caso de haber copiado en /usr/local/bin, usar de la siguiente manera:

```
$ fastqc good_seq.fastq bad_seq.fastq 
```
## 2.3. Interpretación de los resultados
Antes de interpretar los resultados, tomar en consideración los siguientes símbolos: 

![image](https://user-images.githubusercontent.com/84040152/119068548-10a8aa00-b9aa-11eb-8a0d-339f471cd370.png)


* Módulos de análisis incorporados en el programa FastQC.

## 2.3.1. Estadísticas básicas

Estadísticas generales y algunos antecedentes información sobre el archivo de entrada.
En este caso, tenemos una serie de errores y advertencias que a primera vista sugieren que ha habido un problema, pero no se preocupe demasiado todavía. Repasemos a su vez.

![image](https://user-images.githubusercontent.com/84040152/119070549-d4774880-b9ad-11eb-86a1-1bc325c9d5cd.png)

## 2.3.2. Calidad por base de la secuencia

* Mide los valores de calidad de las bases en todas las lecturas del archivo FASTQ de entrada. 
* Este estadistico muestra una descripción general del rango de valores de calidad en todas las bases (en cada posición).
* Generalmente, si presenta una puntuación de calidad media superior a Q20 se considera aceptable; todo lo que está por encima de Q30 se considera "bueno".

![image](https://user-images.githubusercontent.com/84040152/120726867-c1c93d00-c49e-11eb-991a-579ee11666e1.png)

``` 
En la imagen superior; podemos observar una muestra que presenta problemas de calidad, calidad que disminuye al final de las lecturas. Es normal que la calidad de lectura empeore hacia el final de la lectura.    
```

![image](https://user-images.githubusercontent.com/84040152/120727446-2df87080-c4a0-11eb-8bd8-428b222aaa8b.png)

``` 
En la imagen superior; podemos observar una muestra que presenta una buena calidad, por encima de Q30 (recordar que una calidad por encima de Q20 es aceptable)    
```

## 2.3.3. Calidad de secuencia por mosaico

* Esta es una vista puramente teórica sobre la ejecución de secuenciación. La celda de flujo de secuenciación se divide en áreas llamadas celdas.
* El color de los mosaicos indica la calidad de la lectura.

![image](https://user-images.githubusercontent.com/84040152/120729287-61d59500-c4a4-11eb-9c57-a3a435b02423.png)

``` 
En la imagen superior; podemos observar que hay mosaicos de colores rojos, verdes, entre otros, lo cual indica una disminución de la calidad.
Lo ideal es obtener una imagen completamente azul, que es indicativo de una buena calidad por secuecnias. 
```

## 2.3.4. Valores de calidad por secuencia

* Son valores de calidad promedio por secuencia para el archivo FASTQ de entrada.

![image](https://user-images.githubusercontent.com/84040152/120729987-1328fa80-c4a6-11eb-9551-63185a65b6b5.png)

``` 
En el eje X podemos observar la calidad media de las secuencias secuencia. En general, la gráfica muestra un solo pico, lo cual indica que la mayoria de las secuencias tienen en promedio un Q30 superior.
En una muestra mala, quizás veriamos más de 1 pico en la imagen.
```
## 2.3.5. Contenido de secuencia por base

* Porcentaje de A, C, G, T en las lecturas de FASTQ.
* Para una biblioteca generada de forma completamente aleatoria con un contenido de GC del 50%, se espera que en cualquier posición dada dentro de una lectura haya un 25% de posibilidades de encontrar una base A, C, T o G.

![image](https://user-images.githubusercontent.com/84040152/120731285-ee825200-c4a8-11eb-98cc-1c3389d4ae9b.png)

``` 
En la imagen superior podemos observar que nuestra biblioteca cumple con los criterios mencionados anteriormente.
En la mayoria de casos se suele observar un sesgo  menor al comienzo de la lectura (esto puede deberse a duplicados de PCR durante la amplificación o durante la preparación de la biblioteca.
```

## 2.3.6. Contenido de GC por base 

* El contenido de GC en las lecturas de FASTQ, para cada posición de la base.

![image](https://user-images.githubusercontent.com/84040152/120733273-774ebd00-c4ac-11eb-9283-6ccc795dc9e8.png)

``` 
En la imagen superior podemos observar dos curvas, la distribución de GC teórico representado de color azul y la distribución real de GC representado en rojo. 
Lo ideal es que ambas curvas sean similares, como podemos ver en la imagen. 
```




| 2.3.7. Contenido de N por base |  2.3.8. Distribución de la longitud de la secuencia |
| ------------ | ------------- |
| Porcentaje de bases N en cada posición en las lecturas FASTQ |	Resumen de la distribución de la longitud de las lecturas FASTQ, útil después de recortar las lecturas	|
| ![image](https://user-images.githubusercontent.com/84040152/120735424-33f64d80-c4b0-11eb-8457-94c7cb2eb169.png) |	![image](https://user-images.githubusercontent.com/84040152/120735438-3bb5f200-c4b0-11eb-8c03-54cafe41d87d.png)	|


## 2.3.9. Niveles de duplicación de secuencia 

* Resumen de los recuentos de cada secuencia en el archivo FASTQ, útil para detectar problemas de enriquecimiento sesgado como la sobre amplificación por PCR


