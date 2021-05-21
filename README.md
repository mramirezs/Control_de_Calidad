# Control_de_Calidad
En esta sección aprenderemos brevemente cómo realizar el Análisis de Calidad de las Secuencias, producto del secuenciamiento.
# 1. Términos empleados
## FASTQ

Línea 1: comienza con ‘@’ que contiene información sobre el nombre del secuenciador.

Línea 2: la secuencia de nucleótidos.

Línea 3: Una línea de encabezado o una línea que comience con solo '+'.

Línea 4: representa el puntaje de calidad.


![image](https://user-images.githubusercontent.com/84040152/119056915-21005b00-b991-11eb-9e26-22217e7751dd.png)

## FASTA

Secuencia de nucleótidos basado en texto sin puntuación de calidad, que es solo la línea 1 y 2 de FASTQ, tiene un encabezado que comienza con “>” y la siguiente línea en la secuencia.

![image](https://user-images.githubusercontent.com/84040152/119057013-51e09000-b991-11eb-8e8f-7bee8d4c8ee3.png)

# 2. Control de calidad
La primera tarea que tenemos que hacer al recibir una data de secuenciamiento es evaluar su calidad. Para hacer esto usaremos el programa FastQC, la cual es una herramienta de control de calidad para datos NGS. 
FastQC es   util para resumir la calidad de la secuenciación y detección de problemas potenciales.
## 2.1. Instalación de FastQc
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

## Estadísticas básicas

Estadísticas generales y algunos antecedentes información sobre el archivo de entrada.
En este caso, tenemos una serie de errores y advertencias que a primera vista sugieren que ha habido un problema, pero no se preocupe demasiado todavía. Repasemos a su vez.

![image](https://user-images.githubusercontent.com/84040152/119070549-d4774880-b9ad-11eb-86a1-1bc325c9d5cd.png)





