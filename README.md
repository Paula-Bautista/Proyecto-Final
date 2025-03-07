# Matplot ++

Matplot++ es una biblioteca gráfica de C++ que genera gráficos científicos, de manera similar a la biblioteca de Matplotlib en Python, sin necesidad de usar herramientas externas como OpenGL.

## Objetivo

Este proyecto tiene como objetivo demostrar la implementación y el uso de la biblioteca Matplot++ en un entorno C++. Se presentan ejemplos de visualización de datos y gráficos matemáticos para ilustrar la funcionalidad de la librería y su aplicabilidad en proyectos científicos; asimismo, se presentarán las respectivas instrucciones para su instalación y su reproducción.

### Instrucciones de la instalación

Para instalar la biblioteca se utilizó un repositorio "https://github.com/alandefreitas/matplotplusplus/releases/" desde el cual se descargó la carpeta, ```Source code (zip)``` la cual está comprimida; dicha carpeta se descarga en el computador como ```matplotplusplus-1.2.2```.

Una vez que se descargaba la carpeta, usualmente se descarga en Downloads, por lo que se sugiere revisar previamente o ingresar con ```cd Downloads```. Dicho esto, desde la consola ```mkdir Matplot``` o en el escritorio se puede crear una carpeta con el nombre Matplot, para después escribir en la consola, ```cp matplotplusplus-1.2.2.zip Matplot``` o se copia directamente desde el escritorio. Una vez adentro de la carpeta, con ```cd Matplot``` en el escritorio se puede descomprimir la carpeta con click derecho o ```unzip matplotplusplus-1.2.2.zip``` desde la consola. 

Una vez se haya descomprimido, se revisa ```ls``` que haya ```cmake``` luego se crea una carpeta llamada ```mkdir build``` entra a build, luego en build se escribe ``` cmake ../``` para leer la configuración, una vez se haya finalizado, al revisar el contenido de build ```ls``` entre su contenido, va a tener ```makefiles```Ahora, para compilar, se escribe ```make -j $(nproc)``` de manera que es mucho más rápido compilar la librería. Para saber si funcionó la instalación, se debe revisar con un ejemplo.
### Compilar
Este es el código que se va a usar para la prueba:
<p align="center">
  <img src="https://github.com/user-attachments/assets/856188ef-1194-413b-bfe4-852208974818" alt="image" width="900">
</p>

Para compilar el código se escribe en la terminal  ```g++ -I ~/Downloads/Matplot/matplotplusplus-1.2.2/source/ -L ~/Descargas/matplotplusplus-1.2.2/build/source/matplot/ -L ~/Descargas/matplotplusplus 1.2.2/build/source/3rd_party/ histogram_1.cpp -lmatplot -lnodesoup -ltiff -ljpeg -lz -lpng``` es importante que el ```-I``` y el ```-L``` tengan la ruta de donde se encuenta la carpeta ```matplotplusplus-1.2.2```        

## Ejecución y reproducción

Una vez se haya compilado el código quiere decir que se ha intalado correctamente la libreria, de forma que si se quiere ver la ejecución se puede escribir ```./a.out``` como en la ejecución de cualquier código en C++. 
<p align="center">
  <img src="https://github.com/user-attachments/assets/bb61b48e-cc13-47fc-b7fb-83e8cc6c3c67" alt="image">
</p>

Como se evidencia en la anterior imagen, el código de ejemplo compila y se ejecuta correctamente. De manera que la libreria se ha instalado correctamente. 
## Uso de funciones
* `std::exp(double x)`

La función `exp(x)` calcula la exponencial de `x`, es decir, \(e^x\). Permite, modelar crecimientos exponenciales, y el cálculo de funciones matemáticas.

* `matplot::plot(std::vector<double>, std::vector<double>)`

La función `plot()` en Matplot++ grafica datos en 2D, se usa para la visualización de funciones matemáticas y la representación de datos en gráficos.

* `matplot::linspace(double a, double b, int n)`
Genera un conjunto de `n ` etiquetas `a` y `b`, sirve para definir un rango de valores para graficación o cálculo.

* `matplot::hist(string, int n)->face_color({double a, double R, double G, double B})`
Esta función crea un histograma con `n` columnas en el histograma,  `string` Es el nombre del vector en donde estan guardados los datos. `face_color` es para el color de las columnas a, R, G, B son valores entre 0.0 y 1.0, `a` representa la opacidad y  `R`, `G`, `B` representa la escala de Red, Green, Blue. 

* `matplot::xtickangle(double r)` es de diseño `r` define el ángulo de inclinación de las etiquetas en grados, en este caso del eje x, pero se puede hacer para y con `matplot::ytickangle(double r)` 

________________________________________________________________________________________________________________________________________________________________________
* `matplot::meshgrid(std::vector<double>, std::vector<double>)`  
  La función `meshgrid()` en Matplot++ genera dos matrices a partir de dos vectores de coordenadas, permitiendo crear mallas rectangulares para la visualización de superficies en gráficos 3D.

* `matplot::linspace(double a, double b, int n)`  
  La función `linspace()` en Matplot++ genera un conjunto de `n` valores equiespaciados entre `a` y `b`. Se usa para definir rangos de valores en gráficos.

* `matplot::iota(std::vector<double>& v, double start, double step)`  
  La función `iota()` en Matplot++ llena un vector con valores en un rango dado, comenzando desde `start` y aumentando en `step`. Se usa para generar secuencias numéricas de manera eficiente.

* `matplot::quiver(std::vector<double>, std::vector<double>, std::vector<double>, std::vector<double>)`  
  La función `quiver()` en Matplot++ dibuja campos de vectores en 2D, útil para representar direcciones y magnitudes en diagramas vectoriales.

* `matplot::gradient(std::vector<double>)`  
  La función `gradient()` en Matplot++ calcula la derivada aproximada de un conjunto de datos, útil para analizar cambios en funciones discretas o aproximar pendientes.

* `matplot::transform(std::vector<double>, std::function<double(double)>)`  
  La función `transform()` en Matplot++ aplica una transformación a cada elemento de un vector, permitiendo modificaciones como normalización, escalado o cualquier función personalizada.

* `matplot::subplot(int filas, int columnas, int índice)`  
  La función `subplot()` en Matplot++ divide una figura en varias subgráficas, permitiendo organizar múltiples gráficos dentro de un mismo espacio.

* `matplot::figure()`  
  La función `figure()` en Matplot++ crea una nueva ventana de gráfico, permitiendo visualizar diferentes gráficas en ventanas separadas o superpuestas.


## Referencias

* [Github](https://github.com/alandefreitas/matplotplusplus/releases/) - para la instalación

## Autores

* Juan Esteban Cabrera Peralta
* Juan Camilo Villamil Mateus
* Manuel Alejandro Carrasco Becerra  
* Paula Alejandra Bautista Vargas
