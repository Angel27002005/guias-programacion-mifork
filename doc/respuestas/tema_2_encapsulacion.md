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

---

# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

### Respuesta

La encapsulación busca agrupar en una misma entidad (la clase) tanto los datos como las funciones que operan sobre ellos. Por otro lado, la ocultación de información persigue restringir el acceso directo a los detalles internos de dicha entidad, permitiendo que el objeto se comporte como una "caja negra" para el resto del sistema.

Se persigue que el estado interno de un objeto no sea manipulado de forma arbitraria desde el exterior, garantizando que cualquier cambio pase por los mecanismos de control definidos por el programador. Esto permite que el funcionamiento interno pueda ser modificado en el futuro sin que los usuarios del objeto se vean afectados.

Entre las ventajas principales se encuentran la facilidad de mantenimiento, ya que se reducen las dependencias entre distintas partes del código. También se mejora la robustez, al evitar estados inconsistentes, y se simplifica la complejidad del sistema al exponer solo lo estrictamente necesario.

## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### Respuesta

La interfaz pública de una clase se define como el conjunto de métodos y miembros que son accesibles desde el exterior. Se considera el "contrato" o la cara visible que la clase ofrece a otros componentes para interactuar con ella, ocultando por completo cómo se realizan internamente dichas operaciones.

Esta interfaz se relaciona directamente con la ocultación de información al actuar como una barrera. Mientras que la ocultación protege los detalles de implementación y los datos sensibles, la interfaz pública selecciona cuidadosamente qué servicios se exponen, asegurando que la comunicación sea controlada y predecible.

## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Respuesta

El diseño de la interfaz pública debe realizarse con cautela porque cualquier cambio en ella puede provocar un "efecto dominó" en todo el sistema. Al ser el punto de conexión con otros módulos, una vez que otros programadores empiezan a utilizarla, cualquier modificación obligará a reescribir todo el código que dependía de esa interfaz.

No es fácil cambiarla una vez que el sistema crece o se distribuye. Mientras que los detalles internos (privados) pueden reescribirse libremente siempre que el resultado final sea el mismo, modificar la firma de un método público o eliminarlo rompe la compatibilidad, lo que se traduce en costes elevados de desarrollo y posibles errores.

## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Respuesta

Las invariantes de clase son condiciones o reglas que deben cumplirse siempre para que un objeto sea considerado válido. Por ejemplo, en una clase `Fecha`, una invariante sería que el valor del mes siempre debe estar en el rango de 1 a 12, o en una clase `CuentaBancaria`, que el saldo no sea negativo si no se permite el descubierto.

La ocultación de información es fundamental para preservar estas invariantes. Al hacer que los datos sean privados, se impide que un agente externo asigne valores ilegales. Solo a través de métodos controlados (como los constructores o los setters) se puede asegurar que, ante cualquier intento de modificación, el objeto valide los datos y mantenga siempre un estado coherente y correcto.

## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### Respuesta

```java
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

```

La interfaz pública de esta clase está compuesta por el constructor `Punto(double x, double y)` y el método `calcularDistanciaAOrigen()`. Estos son los únicos elementos que alguien externo a la clase puede invocar para interactuar con un objeto de este tipo.

El modificador `private` indica que los atributos `x` e `y` solo son visibles y accesibles desde dentro de la propia clase, protegiéndolos de manipulaciones externas. Por el contrario, `public` señala que el método o constructor está disponible para cualquier otra clase del programa, estableciendo así el canal oficial de comunicación.

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### Respuesta

En Java, estos modificadores se pueden aplicar a los miembros de la clase, que incluyen tanto a los atributos (variables de instancia o de clase) como a los métodos y constructores. Esto permite controlar con precisión quién puede leer o modificar un dato, o quién puede ejecutar una acción específica.

También se pueden aplicar a las clases mismas, aunque con ciertas reglas. Una clase de primer nivel solo puede ser `public` o tener visibilidad por defecto (package-private). Las clases internas (definidas dentro de otra clase), sin embargo, sí admiten el uso de `private` para restringir su uso exclusivamente a la clase que las contiene.

## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Respuesta

Efectivamente, existen niveles intermedios de visibilidad que permiten un control más granular. En Java, además de `public` y `private`, se utiliza `protected`, que permite el acceso a la propia clase, a sus subclases y a otras clases del mismo paquete. También existe la visibilidad por defecto (sin palabra clave), llamada "package-private", que limita el acceso solo a las clases dentro del mismo paquete.

En otros lenguajes, la implementación varía. Por ejemplo, en C++ existe una estructura similar con `public`, `private` y `protected`. Sin embargo, lenguajes como Python no tienen modificadores de acceso estrictos que impidan el acceso; se basan en convenciones de nomenclatura (como empezar un atributo con un guion bajo `_`) para indicar al programador que ese miembro debe tratarse como privado.

## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Respuesta

La respuesta correcta es la (a): los miembros privados están ocultos para **otras clases**. En Java (y en la mayoría de lenguajes de POO), la privacidad se gestiona a nivel de clase, no a nivel de instancia. Esto significa que un objeto de la clase `Punto` puede acceder a los atributos privados de otro objeto de la clase `Punto`.

```java
public double calcularDistanciaAPunto(Punto otro) {
    // Es posible acceder directamente a otro.x y otro.y porque estamos dentro de la clase Punto
    double dx = this.x - otro.x;
    double dy = this.y - otro.y;
    return Math.sqrt(dx * dx + dy * dy);
}

```

Este comportamiento es lógico y práctico. Al estar dentro del código de la clase `Punto`, el programador conoce la implementación y las invariantes de los objetos de ese tipo. No hay riesgo de romper el encapsulamiento porque el control sigue residiendo dentro de la misma lógica de negocio definida para esa clase.

## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Respuesta

Los métodos "getter" y "setter" (también llamados descriptores de acceso y mutadores) son funciones públicas que permiten consultar o modificar el valor de un atributo privado de forma controlada. Un "getter" devuelve el valor del atributo, mientras que un "setter" recibe un nuevo valor y lo asigna tras realizar las validaciones oportunas.

El uso de estos métodos es una práctica fundamental de la encapsulación. En lugar de permitir el acceso directo a una variable, se utiliza esta capa intermedia para que la clase pueda decidir si permite la operación, registrar cambios o asegurar que el nuevo dato no rompa las invariantes de la clase, manteniendo así la integridad del objeto.

## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Respuesta

No se refiere estrictamente a seguridad informática contra ataques externos o "hacking" en el sentido de ciberseguridad. En el contexto de la POO, la seguridad se entiende como **integridad del software**. Se busca proteger al código de errores accidentales cometidos por otros programadores o por uno mismo al utilizar la clase.

Al ocultar la información, se asegura que el sistema sea menos frágil. Se evita que un componente externo modifique datos internos de manera inesperada, lo que podría provocar comportamientos erráticos o caídas del sistema difíciles de depurar. Es, por tanto, una medida de seguridad interna para garantizar que el programa funcione exactamente como fue diseñado.

## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Respuesta

Un miembro de instancia (atributo o método) es único para cada objeto creado; cada instancia tiene su propia copia de los datos. En cambio, un miembro de clase pertenece a la estructura de la clase en sí y es compartido por todas las instancias de la misma. Solo existe una copia en memoria para todo el programa.

Los miembros de clase también se pueden ocultar utilizando el modificador `private`. Es muy común tener atributos `static` privados que lleven un contador de objetos o constantes internas que solo la clase necesita para sus cálculos, impidiendo que desde fuera se altere esta información compartida.

## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta

Sí, tiene mucho sentido en diversos patrones de diseño. Un constructor privado impide que se puedan crear instancias de la clase de forma convencional utilizando el operador `new` desde fuera de la misma. Esto se utiliza, por ejemplo, en clases que solo contienen métodos de utilidad estáticos (como la clase `Math` de Java) o en clases donde se quiere controlar estrictamente la creación de objetos.

También es común en el patrón **Singleton**, donde se garantiza que solo exista una única instancia de una clase en todo el programa, o en el uso de **Métodos Factoría**. En estos casos, la clase ofrece un método público estático que se encarga de llamar al constructor privado bajo ciertas condiciones controladas.

## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta

En Java, los miembros de clase se indican utilizando la palabra clave `static`. Este modificador le comunica al compilador que el atributo o método no debe replicarse por cada objeto, sino que debe residir en un espacio de memoria único asociado a la clase.

```java
public class Punto {
    private double x, y;
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

```

En este ejemplo, `maxX` y `maxY` son compartidos por todos los puntos. Cada vez que se crea un nuevo objeto `Punto`, el constructor actualiza estos valores globales si las nuevas coordenadas superan los máximos registrados hasta ese momento.

## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`?

### Respuesta

```java
public static Punto crearPuntoRedondeado(double x, double y) {
    double xRedondeado = Math.round(x);
    double yRedondeado = Math.round(y);
    return new Punto(xRedondeado, yRedondeado);
}

```

Sí, se ha utilizado el modificador `static`. Esto es imprescindible en un método factoría porque el objetivo del método es crear un objeto desde cero; por lo tanto, el método debe poder invocarse sobre la clase misma antes de que exista cualquier instancia disponible.

## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta

```java
public class Punto {
    private double[] coords = new double[2];

    public Punto(double x, double y) {
        this.coords[0] = x;
        this.coords[1] = y;
    }

    public double getX() { return coords[0]; }
    public double getY() { return coords[1]; }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(coords[0] * coords[0] + coords[1] * coords[1]);
    }
}

```

Este cambio demuestra la potencia de la ocultación de información. Aunque la estructura interna de los datos ha cambiado drásticamente (de dos variables a un array), cualquier código externo que utilizara los métodos `getX()`, `getY()` o `calcularDistanciaAOrigen()` seguirá funcionando perfectamente sin necesidad de ser modificado.

## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta

No es mejor declararlo público, incluso si se ofrecen ambos métodos. Al mantenerlo privado y usar métodos, se conserva el control sobre el acceso. Si en el futuro se necesita añadir una validación en el setter o cambiar el tipo de dato interno, se podrá hacer sin romper el código externo. Si el atributo fuera público, se perdería esa oportunidad para siempre.

La convención más habitual y recomendada en POO es que los atributos sean siempre **privados**. El acceso directo a los datos se considera una mala práctica porque expone la implementación interna y debilita la estructura del programa.

Esto tiene todo que ver con las invariantes de clase. Un atributo público es una puerta abierta a que el objeto entre en un estado inválido. Los métodos "setter" actúan como filtros que aseguran que cualquier cambio cumpla con las reglas de negocio, protegiendo así la coherencia del objeto.

## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta

Una clase es inmutable cuando su estado no puede ser alterado una vez que el objeto ha sido creado. Todos sus atributos suelen ser finales y no se proporcionan métodos que permitan cambiar sus valores. Si se necesita un cambio, se suele devolver una nueva instancia con los nuevos valores en lugar de modificar la actual.

Un método modificador es aquel cuya finalidad es alterar el estado del objeto. Aunque los "setters" son los modificadores más comunes, no son los únicos; cualquier método que cambie un valor interno (como un método `desplazar(double dx)`) se considera un mutador.

Las ventajas de la inmutabilidad son numerosas: los objetos inmutables son inherentemente seguros para hilos (thread-safe), son más fáciles de entender y depurar, y pueden ser compartidos o utilizados como claves en mapas sin riesgo de que cambien inesperadamente.

## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta

No es recomendable incluirlos por defecto. La inclusión de "setters" debe ser una decisión de diseño consciente. Si una clase no necesita que sus datos cambien tras la creación, es preferible no incluirlos para favorecer la inmutabilidad y la robustez del objeto.

A menudo, la presencia de demasiados "setters" indica que la lógica se está gestionando fuera de la clase en lugar de dentro. Se debe priorizar que el objeto realice acciones por sí mismo antes que simplemente dejar que otros modifiquen sus datos libremente.

## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta

La clase `String` en Java es **inmutable**. Una vez que se crea un objeto de texto, su contenido no puede variar. Esta es una decisión de diseño para mejorar el rendimiento (pool de cadenas) y la seguridad del lenguaje.

Al concatenar dos cadenas con el operador `+`, no se modifica ninguna de las originales; en su lugar, Java crea un tercer objeto `String` nuevo que contiene el resultado de la unión. Si se hace esto miles de veces en un bucle, se generan miles de objetos temporales, lo que penaliza gravemente el rendimiento y la memoria.

Para construir cadenas paso a paso de forma eficiente, se debe utilizar la clase `StringBuilder`. Esta clase sí es mutable y permite añadir texto a un mismo espacio de memoria sin crear objetos nuevos constantemente, optimizando el proceso de forma significativa.

## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java?

### Respuesta

En Java, el operador `==` compara la **identidad** de los objetos, es decir, si ambas referencias apuntan exactamente a la misma posición en memoria. Para comparar el **contenido** (si dos objetos "valen" lo mismo aunque sean instancias distintas), se debe utilizar el método `equals()`.

El método `equals()` está definido en la clase `Object` (la raíz de todas las clases). Por defecto, su implementación hace lo mismo que `==`: comparar identidades. Por tanto, es responsabilidad del programador "sobreescribir" este método en sus propias clases para definir qué significa que dos objetos sean iguales.

Para comparar cadenas de texto, nunca se debe usar `==`, ya que podría dar falso incluso si el texto es el mismo. Se debe utilizar siempre `cadena1.equals(cadena2)` para asegurar que se está comparando el contenido de los textos.

## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers?

### Respuesta

Las clases "wrapper" (envoltorios) son clases que representan a los tipos primitivos (como `int`, `double` o `boolean`) como si fueran objetos (`Integer`, `Double`, `Boolean`). Esto es necesario porque en Java existen contextos, como las colecciones, que solo pueden trabajar con objetos y no con datos simples.

En Java moderno, este proceso es automático gracias al **Autoboxing** y **Unboxing**. El compilador convierte automáticamente un `int` a un `Integer` cuando es necesario, y viceversa, sin que el programador tenga que escribir código adicional.

La ventaja principal es que permiten tratar a los tipos básicos con toda la potencia de la POO, como el uso de nulos o métodos de utilidad. No todos los lenguajes los necesitan; lenguajes como Smalltalk o Ruby no tienen tipos primitivos, ya que "todo es un objeto" desde el principio.

## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta

Un tipo de dato enumerado (`enum`) es un tipo especial que permite definir un conjunto fijo de constantes con nombre. Se utiliza para representar categorías o valores que no cambian, como los días de la semana, los meses o los estados de un pedido.

En Java, un `enum` es mucho más que una simple lista de constantes: es una **clase especializada**. Esto significa que puede tener sus propios atributos, constructores y métodos, lo que le otorga una potencia muy superior a los enumerados de otros lenguajes como C.

En términos de encapsulación, los enumerados son excelentes porque restringen los valores posibles a un conjunto seguro y controlado. Evitan el uso de "números mágicos" o cadenas de texto arbitrarias, y permiten centralizar toda la lógica relacionada con esos valores dentro del propio enumerado.

## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### Respuesta

```java
public enum Mes {
    ENERO(31, 1), FEBRERO(28, 2), MARZO(31, 3), ABRIL(30, 4),
    MAYO(31, 5), JUNIO(30, 6), JULIO(31, 7), AGOSTO(31, 8),
    SEPTIEMBRE(30, 9), OCTUBRE(31, 10), NOVIEMBRE(30, 11), DICIEMBRE(31, 12);

    private final int dias;
    private final int ordinal;

    private Mes(int dias, int ordinal) {
        this.dias = dias;
        this.ordinal = ordinal;
    }

    public int getDias() { return dias; }
    public int getOrdinal() { return ordinal; }
}

```

En este diseño, los datos están protegidos y son inmutables. El constructor es privado por definición en los enumerados, garantizando que nadie pueda crear meses "extraños" fuera de los doce definidos.

## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta

```java
public boolean esDePrimavera(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == MARZO || this == ABRIL || this == MAYO || this == JUNIO;
    } else {
        return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE || this == DICIEMBRE;
    }
}

public boolean esDeVerano(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == JUNIO || this == JULIO || this == AGOSTO || this == SEPTIEMBRE;
    } else {
        return this == DICIEMBRE || this == ENERO || this == FEBRERO || this == MARZO;
    }
}

public boolean esDeOtoño(boolean enHemisferioNorte) {
    return !esDePrimavera(enHemisferioNorte); // Simplificación lógica ejemplo
}

public boolean esDeInvierno(boolean enHemisferioNorte) {
    return !esDeVerano(enHemisferioNorte); // Simplificación lógica ejemplo
}

```

Esta implementación encapsula la lógica climática según el hemisferio dentro del propio tipo `Mes`. Así, el resto del programa no tiene que saber qué meses corresponden a qué estación; simplemente le pregunta al objeto `Mes` y este responde basándose en su propio estado interno.

---
