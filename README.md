# Matplot ++

Matplot++ es una biblioteca grafica de C++, que genera gráficos cientificos, de manera similar a la biblioteca de Matplotlib en Python, sin necesidad de usar herramientas externas como OpenGL.
## Objetivo

Este proyecto tiene como objetivo demostrar la implementación y uso de la biblioteca Matplot++ en un entorno C++. Se presentan ejemplos de visualización de datos y gráficos matemáticos para ilustrar la funcionalidad de la librería y su aplicabilidad en proyectos científicos, asimismo se presentarán las respectivas instrucciones para su instalación y su reproducción.

### Instrucciones de la instalación

Para instalar la bilbioteca se utilizó un repositorio "https://github.com/alandefreitas/matplotplusplus/releases/" desde el cual se descargo la carpeta ```Source code (zip)``` la cual está comprimida, dicha carpeta se descarga en el computador como ```matplotplusplus-1.2.2```.

Una vez se descargaba la carpeta, usualmente se descarga en Downloads por lo que se sugiere revisar previamente o ingresar con ```cd Downloads```. Dicho esto, desde la consola ```mkdir Matplot``` o en el escritorio se puede crear una carpeta con el nombre Matplot, para después escribir en la consola ```cp matplotplusplus-1.2.2.zip Matplot``` o se copia directamente desde el escritorio, una vez adentro de la carpeta con ```cd Matplot``` en el escritorio se puede descomprimir la carpeta con click derecho, o ```unzip matplotplusplus-1.2.2.zip``` desde la consola. 
Una vez se haya descomprimido se revisa ```ls``` que haya ```cmake```luego se crea una carpeta llamada ```mkdir build``` entra a build, luego en build se escribe ``` cmake ../``` para leer la configuración, una vez se haya finalizado, al revisar el contenido de build ```ls``` entre su contenido, va a tener ```makefiles```, ahora para compilar se escribe ```make -j $(nproc)``` de manera que es mucho más rápido compilar la libreria. Para saber si funciono la instalación se debe erevisar con un ejemplo.
### Compilar

```
Foto de un ejemplo x y su compilacion
```

Bandera para graficar g++ -I ~/Matplotlib/matplotplusplus-1.2.2/source/ -L ~/Matplotlib/matplotplusplus-1.2.2/build/source/3rd_party/ -L ~/Matplotlib/matplotplusplus-1.2.2/build/source/matplot/plot_2.cpp -lmatplot -lnodesoup -ltiff -ljpeg -lz -lpng
### Ejecución y reproducción

```
Foto de un ejemplo x y una grafica o algo
```

## Referencias

* [Github](https://github.com/alandefreitas/matplotplusplus/releases/) - para la instalación

## Autores

* Juan Esteban Cabrera Peralta
* Juan Camilo Villamil Mateus
* Manuel Alejandro Carrasco Becerra  
* Paula Alejandra Bautista Vargas
