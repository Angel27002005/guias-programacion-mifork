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

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Respuesta

1. **Abstracción:** Capacidad de ignorar los detalles irrelevantes y centrarse en las características esenciales de un objeto.
2. **Encapsulamiento:** Agrupación de datos y métodos en una sola unidad, protegiendo el estado interno del objeto del acceso directo exterior.
3. **Herencia:** Mecanismo que permite crear nuevas clases basadas en clases existentes, reutilizando código y estableciendo jerarquías.
4. **Polimorfismo:** Capacidad de que diferentes objetos respondan de forma distinta al mismo mensaje o llamada a un método.

## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta

* **Java**
* **C++**
* **Python**
* **C#**

## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta

* **Programación estructurada:** Se basa en dividir el programa en estructuras de control (secuencias, selecciones e iteraciones) y funciones, buscando mejorar la claridad y el flujo lógico.
* **Programación modular:** Consiste en dividir un programa en partes independientes llamadas módulos, cada uno con una funcionalidad específica, lo que facilita el mantenimiento y la reutilización.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta

1. **Estado:** Representado por sus atributos o datos.
2. **Comportamiento:** Representado por sus métodos o funciones.
3. **Identidad:** Lo que diferencia a un objeto de otro, independientemente de su estado (su dirección única en memoria).

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta

* **Clase:** Es el "molde" o plantilla que define los atributos y métodos comunes a un tipo de objeto.
* **Diferencia:** No es lo mismo; la clase es el diseño y el **objeto** es la entidad física creada a partir de ese diseño.
* **Instancia:** Es sinónimo de objeto; el proceso de crear un objeto se llama "instanciar".
* **Lenguajes:** No todos. Algunos lenguajes (como JavaScript en sus versiones originales) usan **prototipos** en lugar de clases.

## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**?

### Respuesta

* **Almacenamiento:** Generalmente en el **Heap** (montículo), mientras que las referencias a ellos suelen ir al **Stack** (pila).
* **Diferencia entre lenguajes:** El concepto es similar, pero la gestión varía (C++ requiere liberación manual, Java es automática).
* **Recolección de basura (Garbage Collection):** Es un proceso automático que identifica y elimina objetos que ya no tienen referencias activas para liberar memoria.

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**?

### Respuesta

* **Método:** Es una función definida dentro de una clase que representa una acción o comportamiento del objeto.
* **Sobrecarga de métodos:** Capacidad de definir varios métodos con el mismo nombre en la misma clase, pero con diferentes parámetros (distinto número o tipo).

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

// Ejemplo de uso
public class Main {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3;
        p.y = 4;
        System.out.println("Distancia: " + p.calculaDistanciaAOrigen());
    }
}

```

## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta

* **Punto de entrada:** El método `public static void main(String[] args)`.
* **`static`:** Indica que el miembro pertenece a la clase y no a una instancia específica. Se puede llamar sin crear un objeto.
* **Uso:** Se usa también para métodos de utilidad (como `Math.sqrt`) o variables compartidas.
* **Combinación con `final`:** Se usa para definir **constantes** de clase (ej. `static final double PI = 3.1415;`).

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta

* **Comandos:** `javac Archivo.java` (compila) y `java Archivo` (ejecuta).
* **¿Compilado?:** Es un híbrido; se compila a un código intermedio y luego se interpreta o compila en tiempo de ejecución (JIT).
* **Máquina Virtual (JVM):** Entorno que ejecuta el código Java en cualquier sistema operativo.
* **Byte-code:** El código intermedio generado por el compilador.
* **Ficheros `.class`:** Archivos que contienen el byte-code resultante de la compilación.

## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta

* **`new`:** Operador que reserva memoria para un nuevo objeto y llama al constructor.
* **Constructor:** Método especial que se ejecuta al crear un objeto para inicializar sus atributos.

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

* **`this`:** Referencia al objeto actual dentro de uno de sus métodos o constructores.
* **Otros lenguajes:** En Python se llama `self`, en PHP se usa `$this`.
* **Ejemplo:**

```java
void setUbicacion(double x, double y) {
    this.x = x; // 'this.x' es el atributo, 'x' es el parámetro
    this.y = y;
}

```

## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta

```java
double distanciaA(Punto otro) {
    double dx = this.x - otro.x;
    double dy = this.y - otro.y;
    return Math.sqrt(dx * dx + dy * dy);
}

```

## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función?

### Respuesta

* **Punto:** En Java se pasa la **copia de la referencia**. Si modificas un atributo (`punto.x = 10`), el cambio **sí afecta** fuera del método.
* **Entero (`int`):** Se pasa **por valor** (copia del dato). Si modificas el entero dentro de la función, el cambio **no afecta** a la variable original fuera.

## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta

* **`toString()`:** Método que devuelve una representación en cadena (texto) del objeto.
* **Otros lenguajes:** Python tiene `__str__` o `__repr__`.
* **Ejemplo:**

```java
@Override
public String toString() {
    return "Punto(x=" + x + ", y=" + y + ")";
}

```

## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?

### Respuesta

Una clase es conceptualmente similar a un `struct`, pero al `struct` le falta:

1. **Métodos:** No puede contener lógica asociada directamente a los datos.
2. **Control de acceso:** No tiene modificadores como `private` o `protected`.
3. **Herencia y Polimorfismo:** No soporta jerarquías de tipos de forma nativa.

## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta

En C se pasaría el puntero de la estructura manualmente a una función:

```c
struct Punto { double x, y; };

double calculaDistanciaAOrigen(struct Punto* p) {
    return sqrt(p->x * p->x + p->y * p->y);
}

```

**¿Qué pasó con `this`?** El puntero `p` que pasamos explícitamente es el equivalente funcional a `this`. En POO, ese paso de parámetro es automático y oculto.

---

¿Te gustaría que profundizara en algún concepto de estos o que pasemos al siguiente tema de tu guía?