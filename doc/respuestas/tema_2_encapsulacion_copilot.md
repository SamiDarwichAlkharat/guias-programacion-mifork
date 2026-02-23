<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

### Respuesta
La encapsulación en POO busca agrupar datos y operaciones dentro de una misma entidad (la clase), de manera que el uso externo se limite a una interfaz bien definida. La ocultación de información complementa este objetivo evitando que partes internas de una clase sean accesibles desde fuera. Con ello, se impide el acceso directo a los atributos internos y se controlan las modificaciones mediante métodos adecuados.
Esta estrategia reduce el acoplamiento entre distintos módulos. Cuando otros componentes sólo interactúan con la interfaz pública, la implementación interna puede cambiar sin afectar al resto del programa. Asimismo, se facilita la prevención de errores, ya que se puede evitar que valores inválidos entren directamente en los atributos internos.



## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### Respuesta
La interfaz pública de una clase es el conjunto de métodos y atributos visibles desde el exterior, es decir, aquello que los usuarios de la clase pueden invocar o consultar. Incluye los métodos constructores, métodos públicos y constantes públicas necesarias para utilizar correctamente la clase.
La relación con la ocultación de información es directa: al ofrecer únicamente una interfaz pública mínima, se restringe el acceso a la estructura interna del objeto. Así, el usuario sólo conoce qué se puede hacer, pero no cómo se implementa. Esto permite cambiar la implementación sin alterar el uso externo.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Respuesta
Diseñar con cuidado la interfaz pública es fundamental porque constituye el contrato entre la clase y sus usuarios. Una vez publicada, cualquier cambio afecta a todas las partes del programa que dependan de ella. Por ello, conviene pensar qué métodos deben ser realmente visibles y cuáles pueden quedar como detalles internos.
Modificar la interfaz pública no es sencillo. Un cambio en nombres de métodos, parámetros o comportamiento puede requerir actualizar múltiples módulos. Además, la compatibilidad con versiones anteriores se rompe fácilmente. Por eso se pretende que la interfaz pública sea estable y mínima.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Respuesta
Las invariantes de clase son condiciones que deben cumplirse siempre para que un objeto esté en un estado válido. Suelen estar relacionadas con los valores permitidos de los atributos o las relaciones entre ellos. Por ejemplo, un contador no debería tener valores negativos si esa no es su naturaleza.
La ocultación de información ayuda a mantener estas invariantes porque evita que otros componentes modifiquen directamente el estado interno. Al forzar el uso de métodos controlados, se puede verificar y garantizar que las invariantes se respeten en todo momento.

## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### Respuesta
public class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
La interfaz pública incluye el constructor y el método calcularDistanciaAOrigen. Lo marcado como public es accesible desde fuera de la clase, mientras que private restringe el acceso exclusivamente al interior de la propia clase. De este modo, las coordenadas no pueden ser modificadas directamente.

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### Respuesta
En Java estos modificadores se pueden aplicar a clases, atributos, métodos y constructores. Para clases de nivel superior, solo se admite public o el nivel package. Para miembros internos, sí pueden usarse public, private, protected o el nivel package por defecto.
Su función es controlar qué entidades pueden acceder a un miembro, permitiendo restringir la visibilidad para mejorar encapsulación y diseño.

## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Respuesta
Además de pública y privada, muchos lenguajes incorporan niveles intermedios. Java ofrece protected y el nivel de paquete (sin modificador). protected permite el acceso desde la misma clase, subclases y paquete, mientras que la visibilidad por defecto da acceso solo dentro del paquete.
Otros lenguajes pueden tener sistemas más complejos. Por ejemplo, C++ posee public, protected y private aplicables con más flexibilidad a herencias y clases anidadas. Así, cada lenguaje implementa su propio modelo de control de acceso.


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Respuesta
Los atributos privados están ocultos a otras clases, pero no a otras instancias de la misma clase. Esto significa que un objeto puede acceder a los atributos privados de otro objeto de su misma clase, porque ambos comparten el mismo contexto de acceso.
public double calcularDistanciaAPunto(Punto otro) {
    double dx = this.x - otro.x; // permitido aunque x sea private
    double dy = this.y - otro.y;
    return Math.sqrt(dx*dx + dy*dy);
}

## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Respuesta
Los getters son métodos públicos que permiten obtener el valor de un atributo privado. Los setters permiten modificarlo de manera controlada, verificando si el nuevo valor cumple las restricciones de la clase. Se emplean para mantener encapsulación sin renunciar al acceso externo.
Con estos métodos se garantiza que las invariantes de clase no se rompan, ya que la modificación se centraliza y se controla.

## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Respuesta
Cuando se afirma que la ocultación mejora la "seguridad", no se refiere a seguridad frente a ataques externos o hacking. Se refiere a la seguridad del estado interno del objeto frente a errores lógicos o modificaciones indebidas en el código.
El objetivo es evitar que partes no previstas del programa alteren los datos internos, manteniendo las invariantes y garantizando un comportamiento correcto.

## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Respuesta
Un miembro de instancia pertenece a cada objeto individual, por lo que cada instancia dispone de su propia copia. Un miembro de clase, declarado con static, pertenece a la clase en su conjunto y se comparte entre todos los objetos creados.
Los miembros de clase también pueden ser ocultados mediante private, lo que evita su uso directo desde fuera de la clase.


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta
Tiene sentido si se desea controlar completamente cómo se crean las instancias de una clase. Esto ocurre en patrones como singleton o cuando la construcción depende de métodos factoría.
Al marcar un constructor como privado se fuerza al usuario a utilizar métodos estáticos controlados para la creación de objetos.


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta
public class Punto {
    private double x;
    private double y;

    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    public static double getMaxX() { return maxX; }
    public static double getMaxY() { return maxY; }
}
Los miembros static pertenecen a la clase y se comparten entre todas las instancias.
## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta
public static Punto crearRedondeado(double x, double y) {
    return new Punto(Math.round(x), Math.round(y));
}

## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta
public static Punto crearRedondeado(double x, double y) {
    return new Punto(Math.round(x), Math.round(y));
}
La interfaz pública permanece igual, aunque la implementación interna cambia.


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta

Aunque un atributo tenga getter y setter, no conviene hacerlo público. Al hacerlo público se pierde la capacidad de controlar su modificación, lo cual puede romper invariantes y dificultar el mantenimiento.
La convención es declararlos privados. Esto se relaciona directamente con las invariantes, ya que permite validar los valores antes de asignarlos.
## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta

Una clase inmutable es aquella cuyo estado no puede cambiar después de ser creada. Un método modificador es cualquier método que altere los atributos internos. No siempre coincide con un setter; puede modificar internamente aunque no sea un método llamado "set".
Las clases inmutables reducen errores, facilitan el razonamiento y son seguras para concurrencia.
## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta
No es recomendable incluir setters por defecto. Solo deben existir si son realmente necesarios. Si un atributo no necesita cambiar, no debe permitirse su modificación.
Una clase con menos setters es más segura y estable, evitando estados inválidos.

## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta

String en Java es inmutable. Al concatenar se crea una nueva cadena, lo que puede ser costoso repetidamente. Para concatenaciones repetidas se debe usar StringBuilder.
De ese modo se evita crear múltiples objetos intermedios.
## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta
En POO puede compararse por identidad (misma referencia) o por contenido. En Java, el método equals sirve para comparar contenido. Por defecto, hereda la identidad de Object.
Las cadenas en Java deben compararse con equals, no con ==, ya que == compara referencias.

## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta
Los wrappers son clases que encapsulan tipos primitivos, como Integer o Double. En Java, este proceso puede ser automático mediante autoboxing.
Ofrecen ventajas como métodos adicionales, uso en colecciones y comportamiento como objeto. Otros lenguajes no siempre distinguen primitivos y objetos.

## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta
Un tipo enumerado define un conjunto fijo de valores. En Java, un enum es realmente una clase especial con instancias predefinidas.
Favorece la encapsulación porque permite atributos privados, métodos y constructores controlados.

## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### Respuesta
public enum Mes {
    ENERO(31,1), FEBRERO(28,2), MARZO(31,3), ABRIL(30,4),
    MAYO(31,5), JUNIO(30,6), JULIO(31,7), AGOSTO(31,8),
    SEPTIEMBRE(30,9), OCTUBRE(31,10), NOVIEMBRE(30,11), DICIEMBRE(31,12);

    private int dias;
    private int numero;

    private Mes(int dias, int numero) {
        this.dias = dias;
        this.numero = numero;
    }

    public int getDias() { return dias; }
    public int getNumero() { return numero; }
}

## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta
public boolean esDePrimavera(boolean norte) {
    return norte ? (this == MARZO || this == ABRIL || this == MAYO)
                 : (this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE);
}

public boolean esDeVerano(boolean norte) {
    return norte ? (this == JUNIO || this == JULIO || this == AGOSTO)
                 : (this == DICIEMBRE || this == ENERO || this == FEBRERO);
}

public boolean esDeOtono(boolean norte) {
    return norte ? (this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE)
                 : (this == MARZO || this == ABRIL || this == MAYO);
}

public boolean esDeInvierno(boolean norte) {
    return norte ? (this == DICIEMBRE || this == ENERO || this == FEBRERO)
                 : (this == JUNIO || this == JULIO || this == AGOSTO);
}

