<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### Respuesta

En C, al no existir un sistema automático de excepciones, el error suele indicarse mediante códigos de retorno. Una manera es hacer que la función devuelva un valor especial imposible en condiciones normales, como -1 para indicar error, dejando al código llamador la responsabilidad de comprobarlo y actuar. Este enfoque es muy habitual en funciones estándar de C, y obliga al programador a validar manualmente el retorno.
Otra opción consiste en usar un parámetro por referencia para indicar si hubo error. En este diseño, la función devuelve el resultado normalmente, pero además escribe en una variable externa un indicador de éxito o fallo. Es útil cuando el rango de retorno válido no permite elegir un valor “sentinela”.

Ejemplo 1:
#include <stdio.h>
#include <math.h>

float raiz(float x) {
    if (x < 0) return -1.0; // indicamos error
    return sqrt(x);
}

int main() {
    float r = raiz(-4);
    if (r == -1.0)
        printf("Error: número negativo.\n");
    else
        printf("Resultado: %f\n", r);
}

Ejemplo 2: 
#include <stdio.h>
#include <math.h>

float raiz(float x, int *error) {
    if (x < 0) {
        *error = 1;
        return 0.0;
    }
    *error = 0;
    return sqrt(x);
}

int main() {
    int err;
    float r = raiz(-4, &err);
    if (err)
        printf("Error: número negativo.\n");
    else
        printf("Resultado: %f\n", r);
}
## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta

Una excepción es un mecanismo de notificación automática de errores que permite que una función informe de un problema sin devolver manualmente códigos especiales. Cuando aparece una situación anómala, la ejecución se interrumpe y se envía esa señal hacia quien deba encargarse del error. Esto proporciona una forma más estructurada y clara de gestionar condiciones inesperadas.
Los programadores usan excepciones para separar la lógica normal del manejo de errores, lo que mejora la legibilidad del código. Además, permite que el error viaje hacia capas superiores sin que cada función intermedia tenga que comprobar retornos manualmente, algo que en C resulta mucho más tedioso.

## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### Respuesta

En Java, el control de errores mediante excepciones permite que el método que calcula la raíz no decida qué hacer ante un dato incorrecto, sino que el error se informe automáticamente al código que lo llame. Esto hace que la clase sea más modular: el método solo calcula, y el main decide cómo actuar.
El siguiente código muestra cómo se lanza una excepción desde el método y cómo se captura desde main usando try-catch. De esta forma, el control se hace fuera del método, igual que se pedía en el ejemplo equivalente en C pero usando un mecanismo moderno.

class Calculadora {

    public static double raiz(double x) {
        if (x < 0)
            throw new IllegalArgumentException("Número negativo");
        return Math.sqrt(x);
    }

    public static void main(String[] args) {
        try {
            double r = raiz(-4);
            System.out.println("Resultado: " + r);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}

## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Respuesta
Lanzar una excepción significa ejecutar explícitamente la instrucción throw, o que Java genere automáticamente una al detectar una situación irregular. Esto detiene la ejecución normal de la función y salta hacia el primer bloque catch adecuado. En ese sentido, lanzar equivale a decir: “ha ocurrido un problema y esta función no quiere o no puede manejarlo”.
Capturar una excepción consiste en usar un bloque try-catch que intercepte ese error. Si una función no captura la excepción, esta se propaga hacia su llamador. La propagación recorre la pila de llamadas: cada función se va abandonando sin continuar la ejecución después del punto donde ocurrió el fallo. Importante: las funciones que no capturan la excepción no reanudan la ejecución.
Aplicado al ejemplo de la raíz, si raiz(-4) lanza una excepción, la función abandona su ejecución y sube al main. Si el main tiene un catch, la controla; si no, la excepción continúa subiendo hasta llegar al sistema, terminando el programa.


## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### Respuesta

En C, cada función debe comprobar manualmente los posibles errores de las funciones que llama, encadenando comprobaciones que ensucian el código y aumentan la probabilidad de errores. Esto obliga a que cada nivel de la pila participe en el manejo del problema, incluso aunque no tenga nada inteligible que hacer con él.
En Java, la propagación automática permite omitir controles repetitivos. Las funciones intermedias pueden ignorar completamente la gestión del error si no les corresponde, y la excepción viajará hasta el punto donde realmente tenga sentido manejarla. Esto produce código más limpio, modular y fácil de mantener.

## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### Respuesta

En orientación a objetos, una excepción es un objeto derivado de la clase Throwable. Esto permite encapsular dentro del objeto detalles del error, como el mensaje descriptivo, la causa interna u otros datos relevantes. La excepción no es solo una señal, sino un contenedor estructurado de información.
Al ser objetos, es posible definir excepciones personalizadas, extendiendo clases como Exception o RuntimeException. Esto permite representar errores específicos del dominio del problema, mejorando la claridad y precisión del manejo de errores.

## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Respuesta

Una excepción incluye siempre un mensaje textual que describe la causa del error. Este mensaje es fundamental para comprender la situación al llegar a un catch, algo que en C suele requerir cadenas manuales o códigos numéricos difíciles de interpretar. Además, el objeto contiene la traza de pila, que indica dónde se originó el fallo.
Esta información resulta invaluable cuando el error se analiza desde un punto lejano en el flujo de llamadas. Mientras que en C la depuración depende totalmente del programador, en Java la excepción ya transporta automáticamente datos diagnósticos que facilitan el análisis de problemas.

## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### Respuesta

En Java se pueden tener varios bloques catch tras un único try. Esto permite capturar distintos tipos de excepciones de forma diferenciada, lo que garantiza que cada error se maneje de la manera más adecuada según su naturaleza. Cada catch especifica el tipo de excepción que está preparado para interceptar.
Pese a tener varios, solo se ejecuta uno: el primero cuyo tipo sea compatible con la excepción lanzada. Esto evita ambigüedades y garantiza un flujo de control determinista.

## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta

El bloque finally permite ejecutar código que debe ejecutarse siempre, ocurra o no una excepción. Es útil para liberar recursos como ficheros abiertos, conexiones o buffers. Aunque el try termine de forma anómala, el finally se ejecuta garantizando que el programa deje el estado correcto antes de continuar propagando el error.
El finally puede coexistir con catch, pero también puede usarse sin él. Su comportamiento no depende de que haya habido o no error.

Con catch: 
try {
    abrirFichero();
} catch (IOException e) {
    System.out.println("Error abriendo fichero");
} finally {
    cerrarFichero();
}

Sin catch: 
try {
    abrirFichero();
} finally {
    cerrarFichero();
}
``

## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta
Sí, el bloque finally puede aparecer sin catch. En ese caso, el try puede lanzar la excepción y no capturarse, pero aun así se ejecutará el finally. De esta forma, se asegura que el código de limpieza siempre corra incluso si no se está manejando directamente la excepción.
El finally se ejecuta incluso si dentro del try hay un return. Antes de devolver el valor, el programa entra en el bloque finally, ejecuta su contenido y solo después vuelve al flujo normal o continúa propagando la excepción si la hubiera.

## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta

Las excepciones controladas son aquellas que el compilador exige declarar (throws) o capturar (try-catch). Representan errores previsibles del entorno, como fallos de E/S. En cambio, las no controladas derivan de RuntimeException y no obligan a usar ni try-catch ni throws, ya que suelen indicar errores de programación.
RuntimeException es la clase base de las no controladas. Su presencia indica errores que deberían corregirse en el código, no en tiempo de ejecución mediante capturas.
Situaciones típicas para excepciones controladas

Archivo no encontrado (IOException).
Problemas de red (SocketException).
Error al leer de un buffer.
Base de datos inaccesible.

Situaciones típicas para excepciones no controladas

Índice fuera de rango (IndexOutOfBoundsException).
Argumento inválido (IllegalArgumentException).
División entre cero (ArithmeticException).
Error lógico del programador.



## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta
La palabra clave throws indica que un método puede producir una excepción controlada y que no desea manejarla internamente. En este caso, el método delega la responsabilidad al llamador. Esto permite que el control de errores se realice en un nivel más adecuado del programa.
Es una alternativa a capturar la excepción localmente. Si un método no tiene suficiente contexto para gestionar un error, es preferible que lo propague mediante throws en lugar de incluir un try-catch vacío o poco útil.

## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta
Aquí se muestra un método que abre un archivo pero no gestiona internamente la excepción IOException. El finally asegura que el recurso se cierre.

import java.io.*;

public class Gestor {

    public static void abrir() throws IOException {
        BufferedReader br = null;
        try {
            br = new BufferedReader(new FileReader("datos.txt"));
        } finally {
            if (br != null) br.close();
        }
    }
}

## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta
Es técnicamente posible declarar excepciones no controladas (RuntimeException) en throws, pero no se considera práctico. Dado que no obligan al llamador a capturarlas, añadirlas en la firma del método no añade seguridad real ni requisitos de compilación.
El método llamador no estaría obligado a poner un try-catch. Declararlas en throws solo sirve como documentación, no como mecanismo de control. Se usa ocasionalmente para indicar que una función puede fallar por razones lógicas, pero no se espera que se manejen en ese punto.

## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta

Las excepciones controladas se recomiendan cuando el error es parte normal del funcionamiento del programa, como que un archivo pueda no existir. Estas situaciones no representan fallos de programación sino condiciones externas esperables.
Las excepciones no controladas se usan cuando el error constituye un problema lógico interno, como parámetros inválidos o estados inconsistentes. No tiene sentido obligar al programador a capturar constantemente errores que debería prevenir.
En lenguajes donde solo existe un tipo, normalmente se comportan como no controladas. Java es uno de los pocos que diferencia ambas de forma estricta.
## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta
Dentro de un bloque catch puede lanzarse una nueva excepción distinta. Esto tiene sentido cuando se desea transformar un error bajo nivel en uno de mayor nivel semántico, más adecuado para la capa superior del programa.
También es posible relanzar la misma excepción capturada. Esto se emplea cuando el método actual necesita realizar limpieza o registrar el error pero no quiere absorberlo. Una vez cumplida su función, la relanza para que otro nivel lo maneje.

Lanzar otra excepción
catch (IOException e) {
    throw new IllegalStateException("Fallo en la lectura", e);
}

Reenlazar la misma:
catch (IOException e) {
    logError(e);
    throw e;
}
## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta

Una excepción puede envolver otra como su causa, usando el constructor que recibe una excepción interna. Esto permite preservar la información del error original mientras se transforma en otra más significativa para niveles superiores. El encadenamiento facilita el diagnóstico completo.
Cuando se imprime la excepción resultante, la traza incluye también la causa interna. De esta forma, el análisis puede rastrear la cadena completa del fallo.

Ejemplo: 
try {
    leerArchivo();
} catch (IOException e) {
    throw new MiExcepcion("Error en capa de negocio", e);
}

Si esta excepción se muestra en consola, Java imprime tanto la pila de MiExcepcion como la pila completa de la excepción original (IOException).s
