
---

# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### Respuesta
En C, al carecer de un mecanismo nativo de excepciones, la gestión de errores se realiza habitualmente mediante el valor de retorno de la función o mediante variables globales de estado. Como el objetivo es informar al entorno llamador de que la operación matemática no es válida, se requiere un diseño explícito en la firma de la función.

Una primera opción consiste en utilizar códigos de error en el valor de retorno de la función y pasar el resultado matemático real a través de un puntero (paso por referencia). Así, la función devuelve un código entero indicando éxito o fallo.

```c
// Opción 1: Retornar código de error
int calcularRaiz(float numero, float *resultado) {
    if (numero < 0) {
        return -1; // -1 indica error
    }
    *resultado = sqrt(numero);
    return 0; // 0 indica éxito
}
```

Una segunda opción es reservar un valor de retorno especial (como un número negativo o un `NaN`, si el dominio matemático lo permite) para indicar el fallo directamente, delegando en el llamador la comprobación de ese valor anómalo.

```c
// Opción 2: Retornar un valor especial
float calcularRaizValorEspecial(float numero) {
    if (numero < 0) {
        return -1.0; // En una raíz, un resultado negativo es matemáticamente imposible, sirve como indicador de error
    }
    return sqrt(numero);
}
```

## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta
Una excepción es un evento anómalo o inesperado que ocurre durante la ejecución de un programa y que interrumpe el flujo normal de las instrucciones. Representa una situación de error que el bloque de código actual no sabe o no puede resolver por sí mismo.

Al implementar funciones, el objetivo de utilizar excepciones es separar la lógica principal del programa (el "camino feliz") de la lógica de control de errores. En lugar de plagar el código con múltiples condicionales para comprobar si cada paso tuvo éxito, simplemente se "lanza" una alerta cuando algo falla.

Al llamar a dichas funciones, el objetivo es centralizar y estructurar el manejo de esos errores en bloques específicos. Esto permite decidir en un nivel superior de la arquitectura del programa cómo reaccionar ante la anomalía (por ejemplo, reintentando la operación o abortando de forma segura), manteniendo el código de lectura mucho más limpio y mantenible.

## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### Respuesta
En Java, el manejo de errores se integra en el propio lenguaje mediante el lanzamiento y captura de objetos excepción. Si se solicita la raíz de un número negativo, se lanza una excepción explícita para abortar la operación.

El método llamador (en este caso, `main`) puede rodear la llamada con un bloque de control para interceptar específicamente ese error y tomar medidas sin que el programa completo colapse abruptamente.

```java
class Calculadora {
    public double raiz(double numero) {
        if (numero < 0) {
            throw new IllegalArgumentException("El número no puede ser negativo");
        }
        return Math.sqrt(numero);
    }
}

public class Main {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        try {
            double resultado = calc.raiz(-5.0);
            System.out.println("El resultado es: " + resultado);
        } catch (IllegalArgumentException e) {
            System.out.println("Error detectado desde fuera: " + e.getMessage());
        }
    }
}
```

## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Respuesta
"Lanzar" (`throw`) una excepción significa instanciar un objeto que representa un error y entregárselo al entorno de ejecución, deteniendo instantáneamente el flujo actual. "Controlar" o "capturar" (`catch`) consiste en interceptar esa excepción en un bloque de código preparado para manejarla, neutralizando el error para evitar el cierre del programa.

"Propagar" es el proceso automático por el cual, si una función no captura la excepción, esta se transfiere a la función que la llamó, y así sucesivamente hacia atrás en la pila de llamadas (*stack*). Durante esta propagación hacia arriba, las funciones intermedias que no controlan el error se abortan de inmediato; sus variables locales se destruyen y el flujo jamás vuelve a reanudarse en ellas.

En el ejemplo anterior, cuando `calc.raiz(-5.0)` detecta el número negativo, "lanza" la excepción. La ejecución de la función `raiz` se destruye y no calcula nada. El error se "propaga" hacia atrás y llega a `main`. Como `main` está preparado para "capturarla" con un bloque `try-catch`, el flujo de ejecución salta directamente dentro del `catch`. La función `raiz` jamás se reanuda desde donde se quedó.

## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### Respuesta
La principal ventaja de la propagación natural de excepciones frente a C es que elimina la necesidad de comprobar manualmente los códigos de error en cada nivel intermedio de la jerarquía de llamadas. En C, si una función muy profunda falla, todas las funciones intermedias deben verificar y retornar explícitamente el error paso a paso hasta llegar al punto donde se puede manejar.

Con la propagación de excepciones, el código intermedio queda completamente limpio de la gestión de errores (*boilerplate*). Las funciones intermedias simplemente se dedican a su lógica de negocio, asumiendo que todo va bien. Si algo falla más abajo, la excepción las atravesará automáticamente hasta llegar al manejador adecuado, simplificando drásticamente el código y reduciendo descuidos.

## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### Respuesta
En la programación orientada a objetos, las excepciones son, efectivamente, objetos completos instanciados a partir de clases específicas que derivan de una jerarquía base (como `Exception` en Java).

En términos de encapsulación, esto aporta una ventaja enorme: el error deja de ser un simple número mágico opaco (como un `-1`). Ahora es una estructura de datos rica que agrupa toda la información relevante sobre el fallo. El objeto encapsula un mensaje descriptivo, el estado de las variables en el momento del error e incluso métodos para recuperar información adicional.

Por consiguiente, es totalmente posible crear excepciones personalizadas creando nuevas clases que hereden de las clases de excepción del sistema. Esto permite diseñar tipos de errores adaptados al dominio del problema (por ejemplo, `SaldoInsuficienteException` o `FicheroCorruptoException`), dotando al programa de una semántica de errores mucho más precisa.

## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Respuesta
A diferencia de C, donde un fallo suele carecer de contexto sobre dónde y por qué ocurrió exactamente, un objeto excepción en lenguajes como Java viaja cargado de metadatos automáticos provistos por la máquina virtual.

La información más esencial que lleva consigo es la **traza de la pila** (*stack trace*). Esta traza registra la secuencia exacta e histórica de llamadas a métodos (incluyendo el archivo de código fuente y el número de línea exacto) que condujeron al momento de la detonación del error. 

Además de la traza, el objeto suele contener un texto explicativo (el mensaje) y, en sistemas complejos, puede encapsular otra excepción previa (la "causa"), lo que resulta invaluable para el programador a la hora de depurar el origen real del problema desde el manejador final.

## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### Respuesta
Sí, un bloque `try` puede estar seguido por múltiples bloques `catch`. Esto permite definir diferentes estrategias o manejadores de error dependiendo del tipo específico de excepción que se haya lanzado dentro del bloque protegido (por ejemplo, actuar de una forma ante un fallo matemático y de otra ante un fallo de lectura de fichero).

Sin embargo, ante el lanzamiento de una excepción, **solo se ejecuta un único bloque `catch`**: el primero en la lista que coincida con el tipo de la excepción lanzada o con una superclase de la misma. 

Una vez que ese bloque específico termina de ejecutarse, el programa ignora el resto de los bloques `catch` de esa estructura y continúa con el flujo normal de ejecución. Por esta razón, es obligatorio colocar primero las excepciones más específicas y dejar las más genéricas (como la clase base `Exception`) en los últimos `catch`.

## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta
Para garantizar que ciertas operaciones críticas de limpieza se ejecuten invariablemente, se emplea el bloque `finally`. Este bloque se coloca al final de la estructura y su código se ejecutará siempre, haya o no haya ocurrido una excepción, sirviendo como una red de seguridad contra las fugas de recursos y la ruptura de flujo.

```java
// Ejemplo con catch y finally
try {
    // Código que abre un fichero y puede fallar
} catch (IOException e) {
    // Manejo del error
} finally {
    // Esto se ejecuta SIEMPRE, haya error o no, para cerrar el fichero
}

// Ejemplo sin catch, solo try-finally
try {
    // Código crítico que reserva memoria o bloquea un recurso
} finally {
    // Se ejecuta SIEMPRE para liberar el recurso, dejando que la excepción 
    // siga propagándose hacia arriba, ya que aquí no se capturó.
}
```

## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta
Sí, el bloque `finally` puede acompañar a un bloque `try` de manera independiente, sin necesidad de que exista un bloque `catch` intermedio. Esta estructura es idónea cuando un método no tiene la responsabilidad de solucionar un error (prefiere que se propague al llamador), pero sí tiene la obligación imperativa de dejar limpio el entorno local que manipuló.

El bloque `finally` tiene la garantía de ejecutarse prácticamente siempre. Se ejecutará si el bloque `try` finaliza con éxito y también si detona una excepción. 

Incluso si dentro del bloque `try` o del `catch` se ejecuta una instrucción `return`, `continue` o `break`, la máquina virtual suspende ese salto de flujo temporalmente, ejecuta el bloque `finally` y, solo después, consuma el retorno.

## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta
En Java, las excepciones **controladas** (*checked*) son aquellas que el compilador obliga estrictamente a capturar (con `try-catch`) o a declarar en la firma del método que van a propagarse. Por el contrario, las **no controladas** (*unchecked*) no tienen esta imposición y el compilador permite ignorarlas; todas ellas heredan de la clase especial `RuntimeException`.

Las excepciones no controladas suelen representar errores de lógica del programador o precondiciones rotas que deberían evitarse escribiendo código correcto. Las controladas representan contingencias del entorno (disco, red) de las que un programa robusto debería prever una recuperación razonable.

* **Uso de excepciones Controladas (Ej: `IOException`, `SQLException`):**
    1. Intentar abrir un archivo que el usuario borró externamente.
    2. Pérdida de conexión con la base de datos a mitad de consulta.
    3. Fallo de respuesta al intentar conectar con una API en internet.
* **Uso de excepciones No Controladas (Ej: `NullPointerException`, `IllegalArgumentException`):**
    1. Acceder a un objeto que no ha sido instanciado (es nulo).
    2. Solicitar un índice fuera de los límites de un array.
    3. Pasar un parámetro inválido a una función (como una edad negativa).

## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta
La palabra clave `throws` se utiliza en la declaración (o firma) de un método para indicar formalmente que dicho método es susceptible de lanzar determinadas excepciones hacia el exterior. Funciona como una advertencia o contrato para quien invoque la función.

Es la alternativa directa a capturar una excepción controlada porque delega la responsabilidad. Si un método de bajo nivel se encuentra con un error (ej. disco lleno), pero no tiene los conocimientos funcionales ni la interfaz de usuario para preguntar qué hacer, usa `throws` para dejar que la excepción suba por la pila de llamadas. Así el compilador queda satisfecho y el problema lo resolverá el método llamador.

## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta
```java
public void procesarConfiguracion(String ruta) throws IOException {
    FileInputStream archivo = null;
    try {
        archivo = new FileInputStream(ruta);
        // Operaciones de lectura que podrían lanzar IOException
    } finally {
        // Se garantiza el cierre del recurso, pero la posible IOException 
        // de la apertura/lectura se propagará a quien haya llamado a este método.
        if (archivo != null) {
            archivo.close();
        }
    }
}
```

## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta
Técnicamente, el lenguaje Java permite incluir excepciones no controladas (como `IllegalArgumentException` o `RuntimeException`) en la cláusula `throws` de la firma de un método, y el programa compilará sin problemas.

Sin embargo, el método llamador **no** estará obligado por el compilador a poner un bloque `try-catch` ni a redeclararlas. Las reglas de flexibilidad sobre las excepciones no controladas se mantienen intactas independientemente de si están en el `throws` o no.

En la práctica, incluir una excepción no controlada en el `throws` carece de efecto funcional, pero se utiliza frecuentemente a modo de **documentación**. Sirve para advertir claramente a los programadores que utilicen esa función de que existen ciertas precondiciones (ej. "si me pasas nulo, fallaré de esta manera concreta").

## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta
Se recomienda usar excepciones controladas cuando el error se debe a factores externos sobre los cuales el programa no tiene control total (red caída, archivo bloqueado), y se espera que la aplicación tenga una rutina de recuperación o contingencia para el usuario. Las no controladas se reservan para fallos lógicos internos o mal uso de una API por parte del desarrollador, situaciones que deberían corregirse arreglando el código fuente, no capturándolas ciegamente en tiempo de ejecución.

Esta división estricta es una peculiaridad casi exclusiva del diseño del lenguaje Java; no existe en la inmensa mayoría de los lenguajes de programación modernos.

En los lenguajes donde solo existe una opción (como C#, Python, Ruby, C++ o Kotlin), **todas las excepciones son no controladas**. La tendencia actual en ingeniería de software es evitar la verbosidad obligatoria de las excepciones controladas, dejando a criterio del programador decidir cuáles interceptar sin forzar firmas rígidas en el código.

## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta
Sí, tiene perfecto sentido lanzar excepciones desde dentro de un bloque `catch`. Esto ocurre a menudo en arquitecturas multicapa, donde una capa intermedia intercepta un error para realizar una tarea técnica, pero debe informar a la capa superior para que esta tome la decisión final de negocio.

Se puede relanzar exactamente la misma excepción capturada. Esto es habitual cuando el bloque `catch` solo quiere "espiar" la excepción para registrarla en un archivo de bitácora (*log*) o deshacer una transacción de base de datos (`rollback`), pero la gestión real del error sigue correspondiendo al llamador.

```java
// Ejemplo 1: Relanzar la misma excepción para "espiar" el error
try {
    guardarEnBaseDeDatos();
} catch (SQLException e) {
    escribirLogDeAuditoria("Fallo grave en BD: " + e.getMessage());
    throw e; // La excepción original sigue su camino intacta
}

// Ejemplo 2: Lanzar una nueva excepción diferente desde el catch
try {
    leerArchivoXML();
} catch (IOException e) {
    // Se oculta el error técnico y se lanza uno más fácil de entender por el usuario
    throw new ConfiguracionInvalidaException("No se pudo cargar la configuración.");
}
```

## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta
Que una excepción sea la "causa" de otra significa que, al lanzar una nueva excepción de alto nivel en un bloque `catch`, se introduce el objeto excepción original dentro de la nueva. Esto permite "traducir" errores muy técnicos (ej. un fallo de red) a errores lógicos de negocio (ej. fallo al realizar una compra), sin destruir ni perder la valiosa información de depuración original.

```java
try {
    conectarConServidorDePagos();
} catch (SocketTimeoutException e) {
    // La excepción 'e' de bajo nivel se pasa como argumento para que sea la causa
    throw new PagoRechazadoException("No se pudo procesar el cobro en este momento", e);
}
```

Cuando esta cadena de excepciones no se captura en niveles superiores y detona en la consola, **sí se ve**. La máquina virtual imprimirá primero el mensaje y la traza de la excepción de alto nivel y, a continuación, mostrará la frase `Caused by:` seguida del detalle y la traza de la excepción técnica original, permitiendo seguir el rastro exacto del origen del desastre.

---