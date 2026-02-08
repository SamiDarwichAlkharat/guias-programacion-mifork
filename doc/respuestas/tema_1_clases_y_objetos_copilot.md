<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Respuesta 
La abstracción consiste en centrarse solo en los aspectos esenciales de un elemento, ocultando los detalles irrelevantes. En POO se expresa mediante clases que representan conceptos del mundo real de forma simplificada. Gracias a ella es posible trabajar con ideas complejas sin necesidad de conocer su funcionamiento interno.
La encapsulación implica proteger el estado interno de un objeto, permitiendo acceder solo mediante métodos controlados. Esto evita modificaciones no deseadas y mantiene la integridad de los datos. En Java se apoya en modificadores de acceso como private o public.
La herencia permite crear nuevas clases basadas en otras ya existentes, reutilizando su comportamiento y ampliándolo. Esto reduce duplicación de código y facilita la organización jerárquica de conceptos. Java aplica herencia simple, lo que significa que una clase solo puede tener una clase padre directa.
El polimorfismo permite que distintas clases respondan de manera diferente ante un mismo mensaje o método. Este mecanismo hace posible tratar objetos de distintos tipos mediante una interfaz común, facilitando la extensibilidad del código y la reutilización de algoritmos.


## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta
Java es uno de los lenguajes más representativos del paradigma orientado a objetos, con un modelo centrado en clases y objetos desde su diseño inicial. Permite aplicar todos los conceptos fundamentales de la POO de forma estricta.
C++, aunque no es puramente orientado a objetos, incorpora clases, herencia, polimorfismo y otros mecanismos propios del paradigma. Es muy utilizado cuando se requiere eficiencia combinada con modelado basado en objetos. Además, Python y C# también son lenguajes muy populares que soportan POO de manera completa y flexible.


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta 
La programación estructurada se basa en dividir el programa en secuencias, decisiones y bucles, evitando el uso de saltos incontrolados como goto. Este enfoque conduce a programas más claros, previsibles y fáciles de mantener. Lenguajes como C la promovieron ampliamente.
La programación modular supone un paso más allá, separando el programa en módulos independientes que agrupan funciones relacionadas. Cada módulo tiene responsabilidad propia y puede desarrollarse, probarse y entenderse de forma aislada. Este enfoque facilita la reutilización del código y mejora la organización del proyecto, aunque no llega a representar entidades del mundo real como lo hace la POO.


## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta
Un objeto se define principalmente por sus atributos, que representan su información o estado interno. Cada objeto mantiene sus propios valores, lo que permite que existan múltiples instancias con estados distintos dentro de un programa.
Además, un objeto posee métodos, que describen su comportamiento o las acciones que puede realizar. Estos métodos son funciones asociadas directamente al objeto y suelen permitir modificar o consultar el estado.
Finalmente, un objeto tiene una identidad propia, que lo diferencia de otros objetos incluso si tienen los mismos valores. Esta identidad es fundamental para la referencia a objetos concretos en memoria y para entender sus interacciones.


## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta
Una clase es una plantilla o modelo que define qué atributos y métodos tendrá un objeto. Actúa como un plano que describe cómo se comportarán y qué información almacenarán las futuras instancias creadas a partir de ella. La clase en sí no ocupa memoria para datos concretos, solo define la estructura.
Un objeto no es lo mismo que una clase: es una entidad real creada a partir de la clase. Cuando se crea un objeto, se habla de una instancia de esa clase, ya que la clase sirve como molde para generar múltiples objetos independientes.
No todos los lenguajes orientados a objetos requieren clases para funcionar. Algunos, como JavaScript, permiten crear objetos sin necesidad de definir previamente una clase clásica; emplean prototipos para organizar el comportamiento. Sin embargo, en Java el concepto de clase es esencial y obligatorio.


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Respuesta
En Java, los objetos se almacenan en una zona de memoria llamada heap, gestionada automáticamente por la máquina virtual. Las variables que contienen referencias a objetos suelen estar en la pila (stack), pero apuntan a datos situados en el heap. Esto facilita la gestión dinámica de memoria sin intervención directa del programador.
En C++, en cambio, la ubicación depende de cómo se cree el objeto: en la pila si se instancian directamente, o en el heap si se usa new. La gestión de memoria es manual, lo que implica liberar recursos explícitamente utilizando delete. Cada lenguaje adopta su propio modelo, así que no existe un mecanismo universal.
La recolección de basura, o garbage collection, es un sistema automático que elimina objetos que ya no están siendo utilizados por el programa. Esto evita fugas de memoria y simplifica el desarrollo, ya que el programador no necesita liberar memoria manualmente.

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Respuesta
Un método es una función asociada a una clase u objeto que define un comportamiento concreto. A diferencia de las funciones libres en C, los métodos operan directamente sobre el estado del objeto, accediendo a sus atributos o interactuando con otros métodos. En Java, los métodos se declaran dentro de una clase y determinan cómo se manipula la información del objeto.
La sobrecarga de métodos consiste en definir varios métodos con el mismo nombre pero con diferentes parámetros. Cada versión se selecciona en función del número o tipo de argumentos proporcionados. Esto permite expresar acciones similares de forma más intuitiva, adaptándose a distintas necesidades sin cambiar el nombre del método.

## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### Respuesta
class Punto {
    float x;
    float y;

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}

public class Principal {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3;
        p.y = 4;
        System.out.println(p.calculaDistanciaAOrigen()); // imprime 5.0
    }
}


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta
En Java, el punto de entrada de cualquier programa ejecutable es el método main, cuyo encabezado debe ser exactamente public static void main(String[] args). Este método es invocado automáticamente por la JVM al iniciar el programa y actúa como la puerta de acceso al código del proyecto.
La palabra clave static indica que un método o atributo pertenece a la clase y no a los objetos individuales. Así, puede ejecutarse sin necesidad de crear una instancia. Aunque se usa en main, no es exclusivo de este: se usa también para atributos compartidos, funciones auxiliares y constantes globales.
Cuando static se combina con final, se obtiene una constante de clase, un valor que no puede modificarse una vez asignado. Esto es útil para valores universales, como constantes matemáticas, límites o configuraciones que no deben alterarse durante la ejecución.


## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta
Para compilar un archivo Java llamado Principal.java, se utiliza el comando javac Principal.java. Este comando genera un archivo .class que contiene el bytecode. Para ejecutarlo, se usa java Principal, sin añadir la extensión. Todo se realiza desde la línea de comandos y puede hacerse en cualquier sistema donde esté instalado el JDK.
Java se considera un lenguaje compilado e interpretado a la vez. Se compila primero a bytecode mediante javac, pero este código no es nativo: debe ser interpretado o ejecutado por la Java Virtual Machine. Esa combinación proporciona portabilidad entre plataformas.
La máquina virtual Java (JVM) es el entorno que interpreta el bytecode y lo ejecuta en la plataforma donde se esté corriendo el programa. Gracias a ello, un mismo .class puede funcionar en Windows, Linux o macOS sin recompilación. Los archivos .class contienen el bytecode generado durante la compilación y son la unidad básica de ejecución para la JVM.

## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta
La palabra clave new en Java sirve para crear objetos en tiempo de ejecución. Cuando se usa, se reserva memoria en el heap para un nuevo objeto y se devuelve una referencia que permite manipularlo. Toda creación de objetos pasa necesariamente por este mecanismo.
Un constructor es un método especial que se ejecuta justo en el momento de crear la instancia. Su finalidad es inicializar correctamente el objeto, asignando valores iniciales a los atributos o realizando configuraciones necesarias. No tiene tipo de retorno y su nombre coincide con el de la clase.

class Empleado {
    String dni;
    String nombre;
    String apellidos;

    Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta
La referencia this identifica al objeto actual dentro de su propio código. Permite distinguir entre atributos del objeto y parámetros del método cuando tienen el mismo nombre, y señala explícitamente que se está accediendo al estado del objeto en curso. Es una herramienta fundamental en programación orientada a objetos.
No todos los lenguajes usan el mismo nombre: en C++ se usa también this, mientras que en Python se emplea self. Sin embargo, todos cumplen la misma función: señalar la instancia que está ejecutando un método.

double distanciaA(Punto otro) {
    return Math.sqrt(
        (this.x - otro.x) * (this.x - otro.x) +
        (this.y - otro.y) * (this.y - otro.y)
    );
}


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta
double distanciaA(Punto p) {
    return Math.sqrt(
        (this.x - p.x) * (this.x - p.x) +
        (this.y - p.y) * (this.y - p.y)
    );
}


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### Respuesta
En Java, todas las variables se pasan por valor, pero cuando se trata de objetos, lo que se pasa por valor es la referencia. Esto implica que, si dentro del método se modifican los atributos del objeto recibido, los cambios afectan a la instancia original. No se copia el objeto, solo la referencia que apunta a él.
En cambio, los tipos primitivos como int, float o boolean sí se copian completamente. Si un método recibe un entero y lo modifica, el parámetro externo permanecerá igual porque se trabaja sobre una copia independiente. Este comportamiento permite distinguir claramente entre objetos y valores simples.


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta
toString() es un método heredado de la clase base Object en Java y sirve para obtener una representación en texto del objeto. Se ejecuta automáticamente cuando se concatena un objeto con una cadena o cuando se imprime mediante System.out.println(). Su propósito es facilitar la depuración y la lectura del estado del objeto.
Este método puede sobrescribirse para personalizar la salida. Su implementación suele devolver una cadena con los valores internos del objeto de forma legible. Otros lenguajes, como Python o C#, también ofrecen mecanismos similares para representar objetos en texto.

@Override
public String toString() {
    return "Punto(" + x + ", " + y + ")";
}

## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Respuesta
Un struct en C se parece a una clase en la medida en que ambos agrupan datos bajo un mismo tipo. Permiten organizar información de forma coherente, especialmente cuando varios valores están relacionados. Sin embargo, hasta ahí llega la similitud.
A un struct le falta la capacidad de contener métodos, mecanismos de encapsulación, constructores, herencia y polimorfismo. En otras palabras, solo representa datos, no comportamiento. Las clases, en cambio, integran tanto datos como operaciones, lo que permite modelar entidades completas y sus acciones.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta
struct Punto {
    float x;
    float y;
};

double distanciaAOrigen(struct Punto* p) {
    return sqrt(p->x * p->x + p->y * p->y);
}