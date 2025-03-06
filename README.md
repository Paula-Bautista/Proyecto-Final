# Matplot ++

Matplot++ es una biblioteca grafica de C++, que genera gráficos cientificos, de manera similar a la biblioteca de Matplotlib en Python, sin necesidad de usar herramientas externas como OpenGL.
## Objetivo

Este proyecto tiene como objetivo demostrar la implementación y uso de la biblioteca Matplot++ en un entorno C++. Se presentan ejemplos de visualización de datos y gráficos matemáticos para ilustrar la funcionalidad de la librería y su aplicabilidad en proyectos científicos, asimismo se presentarán las respectivas instrucciones para su instalación y su reproducción.

### Instrucciones de la instalación

Para instalar la bilbioteca se utilizó un repositorio "https://github.com/alandefreitas/matplotplusplus/releases/" desde el cual se descargo la carpeta ```Source code (zip)``` la cual está comprimida, dicha carpeta se descarga en el computador como ```matplotplusplus-1.2.2```.

Una vez se descargaba la carpeta, usualmente se descarga en Downloads por lo que se sugiere revisar previamente o ingresar con ```cd Downloads```. Dicho esto, desde la consola ```mkdir Matplot``` o en el escritorio se puede crear una carpeta con el nombre Matplot, para después escribir en la consola ```cp matplotplusplus-1.2.2.zip Matplot``` o se copia directamente desde el escritorio, una vez adentro de la carpeta con ```cd Matplot``` en el escritorio se puede descomprimir la carpeta con click derecho, o ```unzip matplotplusplus-1.2.2.zip``` desde la consola. 
Una vez se haya descomprimido se revisa ```ls``` que haya ```cmake```luego se crea una carpeta llamada ```mkdir build``` entra a build, luego en build se escribe ``` cmake ../``` para leer la configuración, una vez se haya finalizado, al revisar el contenido de build ```ls``` entre su contenido, va a tener ```makefiles```, ahora para compilar se escribe ```make -j $(nproc)``` de manera que es mucho más rápido compilar la libreria. Para saber si funciono la instalación se debe erevisar con un ejemplo.
### Compilar
Este es el código que se va a usar para la prueba:
<p align="center">
  <img src="https://github.com/user-attachments/assets/856188ef-1194-413b-bfe4-852208974818" alt="image" width="900">
</p>

Para compilar el código se escribe en la terminal  ```g++ -I ~/Downloads/Matplot/matplotplusplus-1.2.2/source/ -L ~/Descargas/matplotplusplus-1.2.2/build/source/matplot/ -L ~/Descargas/matplotplusplus 1.2.2/build/source/3rd_party/ histogram_1.cpp -lmatplot -lnodesoup -ltiff -ljpeg -lz -lpng``` es importante que el ```-I``` y el ```-L``` tengan la ruta de donde se encuenta la carpeta ```matplotplusplus-1.2.2```        
### Ejecución y reproducción

Una vez se haya compilado el código quiere decir que se ha intalado correctamente la libreria, de forma que si se quiere ver la ejecución se puede escribir ```./a.out``` como en la ejecución de cualquier código en C++. 
<p align="center">
  <img src="https://github.com/user-attachments/assets/bb61b48e-cc13-47fc-b7fb-83e8cc6c3c67" alt="image">
</p>

Como se evidencia en la anterior imagen, el código de ejemplo compila y se ejecuta correctamente. De manera que la libreria se ha instalado correctamente. 
## Usos de la biblioteca Matplot ++
Para realizar la implementación de la biblioteca, se plantearon varios ejemplos con el fin de abarcar gran parte de las facilidades que aporta la biblioteca.
* Line_plot
* Data_distribution
Código
```cpp
#include <matplot/matplot.h>
#include <fstream>
#include <iostream>
#include <vector>

struct param_t {
   std::string IFNAME;
   double XMIN;
   double XMAX;
   int NBINS;
};

void check_args(int argc, char ** argv, param_t &p);

int main(int argc, char **argv) {
   param_t p;
   check_args(argc, argv, p);

   std::ifstream fin(p.IFNAME);
   if (!fin) {
       std::cerr << "Error al abrir el archivo." << std::endl;
       return 1;
   }

   std::vector<double> data;
   double value;

   while (fin >> value) {
       data.push_back(value);
   }

   fin.close();

   if (data.empty()) {
       std::cerr << "No se encontraron datos en el archivo." << std::endl;
       return 1;
   }

   matplot::hist(data, p.NBINS)->face_color({0.5, 0.4, 0.0, 0.4});
   matplot::xticks(matplot::linspace(p.XMIN, p.XMAX, 6));
   matplot::xtickangle(45);

   matplot::title("Histograma");
   matplot::xlim({p.XMIN, p.XMAX});
   matplot::xlabel("Valor");
   matplot::ylabel("Frecuencia");
   matplot::show();

   return 0;
}

void check_args(int argc, char **argv, param_t &p) {
   if (argc != 5) {
       std::cerr << "Error. Usage: " << argv[0] << " SAMPLES_FILE XMIN XMAX NBINS" << std::endl;
       exit(1);
   }

   p.IFNAME = std::string(argv[1]);
   p.XMIN = std::stod(argv[2]);
   p.XMAX = std::stod(argv[3]);
   p.NBINS = std::stoi(argv[4]);
} 
```
Este código es para realizar la comparación con un histograma hecho en clase, para este se usó la función ```hist()``` de matplot, en clase se creó una función que leía los datos de un archivo y sacaba los datos para un histograma y en gnuplot se grafican, en este caso, el programa usando matplot lee los datos del archivo y ya genera el histograma. Usa la misma sintaxis del código de histograma, de la línea de comandos recibe el nombre del archivo donde están los datos, el mínimo, el máximo, y en número de bins del histograma.  El código se compila con el mismo comando que el ejemplo solo que cambiando el nombre del archivo. Y para ejecutarlo, asegurarse que en la misma carpeta esté el archivo ```.txt``` de donde leerá los datos, y usar ```./a.out ifname.txt xmin xmax nbins```. En el ejemplo mostrado en clase se uso ```./a.out datar.txt -1 1 30``` en este caso en ```datar.txt```estaban los datos a los cuales se quería hacer el tratamiento de datos. 


* Polar line - Function plot
```cpp
#include <matplot/matplot.h> 
#include <cmath>
#include <valarray>
#include <vector>

using state_t = std::valarray<double>;

// Funciones
void deriv(double t, const state_t &s, state_t &dsdt);
void RK4(double t, state_t &s);
void initialize(state_t &s, std::vector<double> &r_vals, std::vector<double> &theta_vals);
void compute_trajectory(state_t &s, std::vector<double> &r_vals, std::vector<double> &theta_vals);
void plot_results(const std::vector<double> &r_vals, const std::vector<double> &theta_vals);

const double T0 = 0.0;
const double TF = 10.0;
const double DT = 0.1;
const double b = 2;
const double c = 1;
const double w = 1;

int main() {
    state_t s(2);
    std::vector<double> r_vals, theta_vals;

    initialize(s, r_vals, theta_vals);
    compute_trajectory(s, r_vals, theta_vals);
    plot_results(r_vals, theta_vals);

    return 0;
}

// Función para inicializar las variables
void initialize(state_t &s, std::vector<double> &r_vals, std::vector<double> &theta_vals) {

    s[0] = b + c;  // r inicial
    s[1] = 0.0;    // theta inicial

    r_vals.clear();
    theta_vals.clear();
}

// Función para calcular la trayectoria usando RK4
void compute_trajectory(state_t &s, std::vector<double> &r_vals, std::vector<double> &theta_vals) {

    for (double t = T0; t <= 2 * M_PI / w; t += DT) {
        RK4(t, s);
        r_vals.push_back(s[0]);
        theta_vals.push_back(s[1]);
    }
}

// Función para graficar los resultados
void plot_results(const std::vector<double> &r_vals, const std::vector<double> &theta_vals) {

    matplot::sgtitle("Caracol de Pascal");

    // Gráfica en coordenadas polares
    matplot::subplot(1, 2, 0);
    matplot::polarplot(theta_vals, r_vals, "m-");
    matplot::rlim({0, 4});
    matplot::title("Caracol de Pascal en polares");

    // Gráfica en coordenadas cartesianas
    matplot::subplot(1, 2, 1);
    matplot::fplot("1+2*cos(x)", "g-");
    matplot::xlim({0,2*M_PI});
    matplot::title("Caracol de Pascal en coordenadas cartesianas");
    matplot::xlabel("X");
    matplot::ylabel("Y");
    matplot::textbox(2,2.5,3,0.25,"y=1+2*cos(x)");

    matplot::gcf()->size(1000, 600); // Ajustar tamaño de imagen
    matplot::save("Pascal.png");
    matplot::show();
}

// Función de derivadas
void deriv(double t, const state_t &s, state_t &dsdt) {
    dsdt[0] = -b * std::sin(s[1]) * w;
    dsdt[1] = w;
}

// Método de integración RK4
void RK4(double t, state_t &s) {
    state_t K1(s.size()), K2(s.size()), K3(s.size()), K4(s.size());

    deriv(t, s, K1);
    deriv(t + DT / 2, s + DT * K1 / 2, K2);
    deriv(t + DT / 2, s + DT * K2 / 2, K3);
    deriv(t + DT, s + DT * K3, K4);

    s += (DT / 6.0) * (K1 + 2 * K2 + 2 * K3 + K4);
}
```
Este código en C++ utiliza la librería Matplot++ para graficar la curva conocida como Caracol de Pascal en coordenadas polares y cartesianas.
Primero se definen parámetros como el intervalo de tiempo T0, TF, el paso DT, y los coeficientes b, c, y w que afectan la forma del caracol.  initialize(): Inicializa los valores iniciales de r y theta, y limpia los vectores de almacenamiento. compute_trajectory(): Usa el método de Runge-Kutta de orden 4 (RK4) para resolver la ecuación diferencial que gobierna la evolución de r y theta, almacenando los resultados en vectores. plot_results(): Dibuja los resultados usando Matplot++: se grafica la curva en coordenadas polares con polarplot(), tambien se grafica la función teórica 1+2*cos(x) en coordenadas cartesianas con fplot(). y ademas se añade una caja de texto y se guarda la imagen como "Pascal.png". Método de integración RK4: es el metodo numerico que vimos durante las clases. Este código simula y visualiza la evolución del Caracol de Pascal mediante integración numérica (RK4) y gráficos en dos sistemas de coordenadas.

## Referencias

* [Github](https://github.com/alandefreitas/matplotplusplus/releases/) - para la instalación

## Autores

* Juan Esteban Cabrera Peralta
* Juan Camilo Villamil Mateus
* Manuel Alejandro Carrasco Becerra  
* Paula Alejandra Bautista Vargas
