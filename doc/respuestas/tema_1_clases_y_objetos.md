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

¡Claro! He preparado las respuestas siguiendo tu formato. He mantenido un tono conciso para facilitar tu estudio y he utilizado **Markdown** puro para que puedas copiar y pegar el contenido directamente en tu editor, tal como se sugiere en el flujo de trabajo de la "Alternativa 1".

Aquí tienes el contenido para tu archivo:

---

# TEMA 1. Clases y objetos (Revisado con apuntes de clase)

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Respuesta

1. **Abstracción:** Consiste en ignorar los detalles irrelevantes para: a) Manejar temas complejos de forma más sencilla y b) Facilitar el mantenimiento y futuras modificaciones.
2. **Encapsulación:** Tiene dos facetas: 1) Unir la información (datos) y las funciones que actúan sobre ella en un mismo artefacto y 2) Ocultar partes del estado interno al exterior.
3. **Herencia:** Mecanismo para crear jerarquías de clases donde unas heredan de otras.
4. **Polimorfismo:** Capacidad de que una misma función tenga distintas implementaciones dependiendo del tipo de objeto que la ejecuta.

## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta

* **Java**
* **C++**
* **Python**
* **C#**

## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta

* **Antes de la estructurada (Ensamblador):** Se basaba en secuencias de instrucciones y saltos arbitrarios (difíciles de seguir).
* **Programación estructurada:** Utiliza solo tres estructuras (secuencia, bifurcación como `if`/`switch`, e iteración como `while`/`for`), eliminando los saltos arbitrarios para ganar claridad.
* **Programación modular:** Introduce conceptos como "librería", "paquete" e "interfaz" para encapsular código y permitir su reutilización en diferentes partes de un sistema.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta

1. **Identidad:** Es lo que hace único a un objeto (puedes pensarlo como su dirección única en memoria).
2. **Estado:** Definido por sus atributos o campos (el valor que tienen en un momento dado).
3. **Comportamiento:** Definido por sus métodos (las funciones que el objeto puede realizar).

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta

* **Clase:** Es el molde o plantilla que define el estado y el comportamiento. Ejemplo: La clase `Coche` (define que tiene marca y año).
* **Objeto / Instancia:** Son las realizaciones concretas en ejecución de una clase. Ejemplo: Un `Mercedes` de `2009` o un `Mazda` de `2020`. Son términos equivalentes.
* **Concepto de clase:** No todos; algunos lenguajes (como el JavaScript clásico) se basan en prototipos, no en clases.

## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**?

### Respuesta

* **Memoria:** Los objetos se suelen alojar en el **Heap**.
* **Gestión:** Varía según el lenguaje; en C++ la gestión es manual, mientras que en Java es automática.
* **Recolección de basura:** Es el proceso automático que libera la memoria ocupada por objetos que ya no están siendo utilizados por el programa.

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**?

### Respuesta

* **Método:** Son las funciones que definen el comportamiento de una clase.
* **Sobrecarga:** Es la posibilidad de crear varios métodos con el mismo nombre dentro de una clase, siempre que cambie el **tipo** y/o el **número** de sus parámetros.

## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### Respuesta

```java
class Punto {
    double x;
    double y;

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3; p.y = 4;
        System.out.println(p.calculaDistanciaAOrigen());
    }
}

```

## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta

* **Entrada:** El método `public static void main(String[] args)`.
* **`static`:** Indica que el miembro pertenece a la clase y no a las instancias. Permite usar el método o atributo sin crear un objeto.
* **Uso:** Se usa en métodos de utilidad y variables globales de clase.
* **`static final`:** Se usa para definir constantes (valores que pertenecen a la clase y no cambian).

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta

* **Comandos:** `javac Archivo.java` para compilar y `java Archivo` para ejecutar.
* **Compilación:** Java es híbrido. Se compila a un código intermedio.
* **Máquina Virtual (JVM):** Es el software que interpreta y ejecuta el código intermedio en cualquier plataforma.
* **Byte-code:** Es el código resultante de la compilación (almacenado en ficheros `.class`) que la JVM puede entender.

## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta

* **`new`:** Es el operador que solicita memoria para una nueva instancia y dispara el constructor.
* **Constructor:** Un método especial para inicializar el objeto recién creado.

```java
class Empleado {
    String dni, nombre, apellidos;
    Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}

```

## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta

* **`this`:** Es una autorreferencia al objeto actual. Se usa para diferenciar atributos de parámetros con el mismo nombre.
* **Otros lenguajes:** En Python es `self`.
* **Ejemplo:**

```java
void setCoordenadas(double x, double y) {
    this.x = x; // This.x es el atributo del objeto
    this.y = y;
}

```

## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta

```java
double distanciaA(Punto otro) {
    return Math.sqrt(Math.pow(this.x - otro.x, 2) + Math.pow(this.y - otro.y, 2));
}

```

## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función?

### Respuesta

* **Objetos (`Punto`):** Se pasa la copia de la referencia. Si modificas un atributo interno, el cambio **sí afecta** fuera.
* **Primitivos (`int`):** Se pasa por valor (copia exacta del dato). Cualquier cambio interno **no afecta** a la variable original.

## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta

* **`toString()`:** Método que define cómo se debe representar el objeto como una cadena de texto.
* **Ejemplo:**

```java
@Override
public String toString() {
    return "(" + x + "," + y + ")";
}

```

## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?

### Respuesta

Conceptualmente son parecidos (agrupan datos), pero al `struct` le falta:

1. **Comportamiento:** No puede contener métodos.
2. **Ocultación (Encapsulamiento):** No tiene `private` o `public`.
3. **Mecanismos de herencia.**

## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta

En C, tendrías que pasar el objeto (la estructura) manualmente como primer argumento:

```c
struct Punto { double x, y; };
double distancia(struct Punto *p) { ... }

```

**`this`** no es "magia", es simplemente un parámetro que los lenguajes de POO pasan de forma automática y oculta por nosotros.

---

¿Qué te parece esta versión? Si estás conforme, puedes hacer el **Commit** y el **Push** en GitHub Desktop para que estos apuntes "Premium" queden guardados. ¿Quieres que sigamos con el **Tema 2**?