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
La abstracción consiste en representar solo lo esencial de algo, ocultando detalles internos que no necesitas para usarlo. En Java esto se hace creando clases que exponen métodos claros mientras esconden la complejidad. Para ti, es como usar fopen() o printf() en C sin conocer la implementación interna: solo importa la interfaz. En Java, una clase puede modelar un concepto general (por ejemplo, un Sensor) sin necesidad de mostrar cómo mide, guarda o procesa los datos.
```java
class Sensor {
    public double leerValor() {
        return Math.random() * 100; // Detalles internos ocultos
    }
}

public class Main {
    public static void main(String[] args) {
        Sensor s = new Sensor();
        System.out.println(s.leerValor());
    }
}
```
El encapsulamiento protege los datos internos de un objeto obligando a acceder a ellos mediante métodos. En C puedes simularlo usando .h y .c, pero aquí el lenguaje te obliga a cumplirlo. Esto evita accesos incorrectos o modificaciones inesperadas, haciendo que el objeto controle su propio estado. Por ejemplo, si tienes una clase CuentaBancaria, nadie debería poder cambiar el saldo directamente sin pasar por reglas definidas.
```java
class CuentaBancaria {
    private double saldo;

    public CuentaBancaria(double inicial) {
        saldo = inicial;
    }

    public void ingresar(double cantidad) {
        saldo += cantidad;
    }

    public double getSaldo() {
        return saldo;
    }
}
```
La herencia permite crear clases nuevas basadas en otras ya existentes, reutilizando código y definiendo comportamientos más específicos. Si vienes de C, es similar a tener una estructura base y ampliarla, pero aquí también se heredan funciones. Por ejemplo, una clase Coche puede heredar de Vehiculo y obtener automáticamente sus métodos.
```java
class Vehiculo {
    public void arrancar() {
        System.out.println("El vehículo arranca.");
    }
}

class Coche extends Vehiculo {
    public void tocarClaxon() {
        System.out.println("Beep beep!");
    }
}
```
El polimorfismo permite que distintos objetos respondan de forma diferente al mismo método, siempre que compartan una clase base. Esto hace que puedas manejar objetos distintos de manera uniforme, algo muy útil al diseñar programas extensibles. Por ejemplo, tanto Perro como Gato pueden ser tratados como Animal, pero cada uno ejecutará su propia versión del método sonido().
```java
class Animal {
    public void sonido() {
        System.out.println("Sonido genérico");
    }
}

class Perro extends Animal {
    public void sonido() {
        System.out.println("Guau");
    }
}

class Gato extends Animal {
    public void sonido() {
        System.out.println("Miau");
    }
}
```
## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos
### Respuesta
Java, C++, Python y C#


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?
### Respuesta
La programación estructurada es un estilo de programación que organiza el código usando tres estructuras básicas: secuencia, selección (if, switch) e iteración (for, while). Su objetivo es escribir programas más claros y fáciles de seguir, evitando saltos desordenados como goto. Todo lo que haces normalmente en C —funciones bien definidas, bloques que se ejecutan en orden— forma parte de este paradigma.

La programación modular se centra en dividir un programa en módulos independientes, cada uno encargado de una parte concreta del problema. Cada módulo tiene sus propias funciones y una interfaz clara para comunicarse con otros. En C lo ves con archivos .h (interfaz) y .c (implementación). Este enfoque mejora la organización, la reutilización y el mantenimiento del código.
Mientras la programación estructurada organiza el flujo, la modular organiza el código en piezas separadas. Juntas forman la base del pensamiento que después amplía la programación orientada a objetos. Si quieres, puedo también compararlas directamente con cómo funcionan las clases en Java.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?
### Respuesta
Un objeto se define por atributos, métodos e identidad, y un ejemplo ayuda a verlos claramente. Imagina una clase sencilla llamada Coche. Los atributos representan su estado interno (por ejemplo, la velocidad), mientras que los métodos representan las acciones que puede realizar (acelerar, frenar, etc.). Cuando creas varios objetos de esta clase, cada uno tiene su identidad propia, es decir, existen como instancias distintas en memoria aunque compartan estructura.

En este ejemplo, cada coche tiene su propio estado (sus atributos), puede realizar acciones (sus métodos) y existe como un objeto distinto aunque ambos provengan de la misma clase.
```java
class Coche {
    // Atributo: estado del objeto
    private int velocidad = 0;

    // Método: comportamiento del objeto
    public void acelerar() {
        velocidad += 10;
    }

    public int getVelocidad() {
        return velocidad;
    }
}

public class Main {
    public static void main(String[] args) {
        Coche c1 = new Coche(); // Identidad 1
        Coche c2 = new Coche(); // Identidad 2

        c1.acelerar();
        System.out.println(c1.getVelocidad()); // 10
        System.out.println(c2.getVelocidad()); // 0 → distinto objeto, distinto estado
    }
}
```
## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?
### Respuesta
Una clase es un molde o plantilla que describe cómo serán los objetos que se creen a partir de ella. Dentro de una clase se definen los atributos (datos) y métodos (acciones) que caracterizan a ese tipo de entidad. Si vienes de C, puedes imaginarlo como una mezcla entre un struct (por los datos) y todas las funciones que trabajan sobre ese struct, pero agrupado en un único bloque lógico. Una clase no ocupa memoria por sí misma para representar “cosas reales”; solo describe cómo deben ser esas cosas.

Un objeto, en cambio, es una instancia real y concreta de esa clase. Es decir, es un ejemplar que sí existe en memoria, con sus propios valores internos, incluso si procede de la misma plantilla. Una instancia no es más que el nombre formal que recibe un objeto creado a partir de una clase. Si una clase es como el plano de una casa, cada objeto es una casa construida usando ese plano: pueden ser iguales por diseño, pero son casas distintas.

Respecto a si todos los lenguajes orientados a objetos manejan el concepto de clase, la respuesta es no. La mayoría sí lo hacen (Java, C++, C#, Swift…), pero existen lenguajes orientados a objetos que no usan clases en el sentido tradicional. Por ejemplo, JavaScript originalmente se basaba en objetos y prototipos, sin clases formales; las clases que tiene hoy son solo “azúcar sintáctico” sobre ese sistema de prototipos. Otros lenguajes como Self también son orientados a objetos sin usar clases.

## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 
### Respuesta
Los objetos, en lenguajes como Java, suelen almacenarse en una zona de memoria llamada heap. Cuando creas un objeto con new, el sistema reserva espacio en ese heap y devuelve una referencia para manejarlo. Esta idea difiere de C/C++, donde decides explícitamente si algo va en la pila (stack) o en el heap usando malloc o declarando variables locales. En Java, en cambio, los objetos siempre viven en el heap, mientras que las referencias que los apuntan viven en la pila.

No todos los lenguajes orientados a objetos gestionan la memoria igual. En C++, por ejemplo, puedes crear objetos tanto en el stack como en el heap, dependiendo de cómo los declares; incluso puedes omitir la liberación manual… o causar fugas si se te olvida. En Python y Java, todos los objetos se almacenan en el heap y el lenguaje se encarga de liberar la memoria automáticamente. Otros lenguajes como Rust usan un sistema distinto basado en ownership, sin recolección de basura.

La recolección de basura (garbage collection) es un mecanismo automático que libera la memoria ocupada por objetos que ya no están siendo usados por el programa. En lugar de que el programador tenga que llamar a free() como en C, el lenguaje detecta cuándo un objeto ya no es accesible desde ninguna parte y lo elimina. Esto reduce errores comunes como fugas o accesos a memoria liberada, aunque a cambio introduce cierto coste de rendimiento que el sistema intenta minimizar.

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 
### Respuesta
Un método es una función definida dentro de una clase y representa el comportamiento de los objetos creados a partir de ella. A diferencia de C/C++, donde las funciones están separadas de las estructuras, en Java los métodos viven dentro de la clase y operan directamente sobre sus atributos. Esto permite que cada objeto pueda realizar acciones que afectan a su propio estado, como cambiar valores, hacer cálculos o comunicarse con otros objetos.

La sobrecarga de métodos (method overloading) consiste en tener varios métodos con el mismo nombre, pero con diferentes parámetros (tipo, número o ambos). El objetivo es ofrecer varias formas de realizar una misma acción dependiendo de la información disponible. Esto no existe de la misma forma en C, pero sí se parece a tener varias funciones relacionadas, solo que aquí comparten nombre para que el código sea más natural y fácil de leer.
```java
class Calculadora {
    // Método 1: suma de enteros
    public int sumar(int a, int b) {
        return a + b;
    }

    // Método 2: suma de doubles (sobrecarga)
    public double sumar(double a, double b) {
        return a + b;
    }
}
```
## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método
### Respuesta
clase Punto en Java con dos atributos x e y (con visibilidad por defecto, es decir, package‑private) y un método calculaDistanciaAOrigen() que devuelve la distancia al origen (0,0). He añadido también un ejemplo de uso creando una instancia y llamando al método. Para calcular la distancia uso Math.sqrt(x*x + y*y).

Fíjate en que Punto no tiene modificador de acceso (no es public), cumpliendo así la visibilidad por defecto para los atributos x e y. En el main creamos un Punto, asignamos coordenadas y mostramos la distancia. Este patrón te resultará familiar viniendo de C/C++: piensa en Punto como un struct con funciones asociadas dentro de la propia clase.
```java
// Clase con visibilidad por defecto (sin 'public') y atributos con visibilidad por defecto
class Punto {
    int x; // visibilidad por defecto (package-private)
    int y; // visibilidad por defecto (package-private)

    // Método que calcula la distancia al origen (0,0)
    public double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}


public class Main {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3;  // acceso permitido: visibilidad por defecto dentro del mismo paquete
        p.y = 4;

        double d = p.calculaDistanciaAOrigen();
        System.out.println("Distancia al origen: " + d); // 5.0
    }
}
```

## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?
### Respuesta
El punto de entrada de un programa en Java es el método main, cuya firma exacta debe ser:
public static void main(String[] args). Cuando ejecutas un programa, la JVM busca ese método y empieza a correr desde ahí, igual que en C/C++ busca la función main(). La diferencia es que, en Java, siempre está dentro de una clase, porque el lenguaje no permite código fuera de ellas. Es decir, el main no representa a una clase ni a un objeto, solo es el punto inicial donde la JVM comienza la ejecución.

La palabra static significa que ese método pertenece a la clase, no a un objeto concreto. Por eso no necesitas crear una instancia para ejecutarlo. En tu experiencia en C, puedes imaginarlo como una función global dentro de un archivo, accesible sin necesitar un struct. Esto explica por qué el main debe ser estático: la JVM debe poder llamarlo sin crear ningún objeto previamente. Pero static no se usa solo para el main. También se emplea para crear métodos de utilidad (como Math.sqrt()) o variables compartidas por todas las instancias de la clase.
Cuando se combina static con final, normalmente se busca crear constantes. En Java, una constante típica se declara como public static final, lo que significa:

static: pertenece a la clase, no a cada objeto; solo existe una copia.
final: su valor no puede cambiar una vez asignado.
Esto se usa para valores como PI, MAX_VALUE, o configuraciones que no varían durante la ejecución.

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?
### Respuesta
Para compilar y ejecutar un programa Java desde la línea de comandos, se usan dos herramientas: javac (el compilador) y java (el ejecutor de la JVM). Si tienes un fichero llamado Main.java, primero lo compilas con javac Main.java, lo cual genera un archivo Main.class que contiene bytecode. Luego lo ejecutas con java Main (sin .class y sin ruta al fichero). Este proceso es distinto a C/C++, donde el compilador genera directamente un binario ejecutable; en Java, primero se compila a bytecode y luego lo interpreta/ejecuta la máquina virtual.

Java se considera un lenguaje compilado e interpretado a la vez: es compilado porque javac transforma tu código fuente en bytecode; y es interpretado/ejecutado porque ese bytecode no corre directamente en tu CPU, sino dentro de la máquina virtual Java (JVM). La JVM actúa como un intérprete especializado que entiende ese bytecode y lo convierte dinámicamente a instrucciones de máquina reales. Gracias a esto, un mismo .class funciona en Windows, Linux o macOS sin recompilar, porque lo que cambia es la JVM, no tu programa.

El bytecode es un lenguaje intermedio, más bajo nivel que Java pero independiente del hardware. Este bytecode se guarda en los ficheros .class generados por javac. Cada clase pública produce su propio fichero .class. La máquina virtual Java (JVM) es el software encargado de leer estos archivos .class, verificar el bytecode, optimizar su ejecución (con técnicas como Just‑In‑Time compilation) y manejar recursos como memoria, hilos o el garbage collector. En resumen: Java no se ejecuta directamente sobre el hardware, sino sobre esta capa intermedia llamada JVM

```java
//codigo a ejecutar
// Main.java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hola desde Java");
        System.out.println("Argumentos: " + java.util.Arrays.toString(args));
    }
}
```
 línea de comandos (Linux/macOS/Windows PowerShell o CMD) compila y ejecuta así. Observa que al ejecutar no se pone la extensión .class, solo el nombre de la clase (y si hubiese paquetes, el nombre cualificado).

 # 1) Compilar: genera Main.class (bytecode)
javac Main.java

# 2) Ejecutar: la JVM carga Main.class y lo corre
java Main

# 3) Pasar argumentos (opcional)
java Main uno dos tres
*/
Notas útiles: si tuvieras paquetes (por ejemplo package demo;), la ruta de carpetas debe coincidir (demo/Main.java), compilas desde el directorio raíz del proyecto (javac demo/Main.java) y ejecutas con el nombre cualificado: java demo.Main. Para compilar varios ficheros a la vez, puedes usar javac *.java, y para elegir una carpeta de salida: javac -d out src/*.java y luego java -cp out Main. Si el comando javac/java no aparece, verifica que tienes instalado el JDK y que el PATH está correctamente configurado.

## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos
### Respuesta
En Java, new es el operador que reserva memoria en el heap y crea un objeto de una clase, devolviendo una referencia a ese objeto. Desde tu experiencia en C/C++, piensa en new como un “malloc + construcción” en una sola operación, pero sin necesidad de free porque la liberación la gestiona el garbage collector. Cuando haces Punto p = new Punto();, estás pidiendo espacio para un Punto y llamando a su constructor para inicializarlo.

Un constructor es un método especial de la clase que tiene el mismo nombre que la clase, no tiene tipo de retorno (ni siquiera void) y se usa para inicializar el estado del objeto. Puede haber varios constructores (sobrecarga) con distintas listas de parámetros. Si no defines ninguno, Java crea un constructor por defecto sin parámetros que no hace nada adicional más allá de la inicialización por defecto de los atributos (cero, false, null, etc.). Definir constructores propios te permite exigir datos mínimos o aplicar validaciones al crear la instancia.
```java
class Empleado {
    // Atributos (por sencillez, visibilidad por defecto)
    String dni;
    String nombre;
    String apellidos;

    // Constructor completo (inicializa todos los campos)
    public Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }

    // Constructor por defecto (opcional)
    public Empleado() {
        // podrías asignar valores por defecto si quieres
        this.dni = "DESCONOCIDO";
        this.nombre = "";
        this.apellidos = "";
    }
}

public class Main {
    public static void main(String[] args) {
        // Usa el constructor completo
        Empleado e1 = new Empleado("12345678A", "Ana", "Pérez López");

        // Usa el constructor por defecto y luego asigna
        Empleado e2 = new Empleado();
        e2.dni = "87654321B";
        e2.nombre = "Luis";
        e2.apellidos = "García Ruiz";
    }
}
```

## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`
### Respuesta
La referencia this en Java apunta al objeto actual dentro de sus métodos o constructores. Se usa para acceder a los atributos y métodos del propio objeto, y resulta especialmente útil para desambiguar entre parámetros y campos con el mismo nombre (por ejemplo, this.x = x). Además, sirve para encadenar constructores (llamando a this(...)) y para pasar la referencia del objeto actual a otros métodos. En C++ y JavaScript también se llama this; en Python el concepto equivalente es el primer parámetro convencional llamado self; y en Rust es self (o &self/&mut self), por si te cruzas con otros lenguajes.

Aplicado a tu clase Punto, this te permite inicializar claramente los campos y, si quieres, diferenciar entre el uso de variables locales y los atributos del objeto. Aunque dentro de un método puedes escribir x en lugar de this.x (porque el acceso al campo es implícito), usar this mejora la legibilidad y evita sombras de nombres.
```java
class Punto {
    int x;  // visibilidad por defecto
    int y;  // visibilidad por defecto

    // Constructor: desambigua parámetros y atributos con 'this'
    public Punto(int x, int y) {
        this.x = x; // 'this.x' es el campo; 'x' es el parámetro
        this.y = y;
    }

    // Método de instancia: 'this' es el objeto actual
    public double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
        // Podrías escribir x*x + y*y; 'this' aquí es opcional
    }

    // Ejemplo adicional: mover el punto y devolver el propio objeto (fluent)
    public Punto mover(int dx, int dy) {
        this.x += dx;
        this.y += dy;
        return this; // devuelve la referencia al objeto actual
    }
}

public class Main {
    public static void main(String[] args) {
        Punto p = new Punto(3, 4);
        System.out.println(p.calculaDistanciaAOrigen()); // 5.0
        p.mover(1, -2);
        System.out.println(p.x + ", " + p.y); // 4, 2
    }
}
```
## 13. Añade ahora otro nuevo método que se llame `distancia`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado
### Respuesta
La idea es calcular la distancia Euclídea entre dos puntos: si this es (x1, y1) y el punto parámetro es (x2, y2), entonces la distancia es sqrt((x1 - x2)^2 + (y1 - y2)^2). En Java, lo natural es recibir un objeto Punto y acceder a sus campos. Desde tu base en C/C++, piensa que es como pasar un struct Punto a una función que opera con ambos, solo que aquí el método vive dentro de la clase y this representa al objeto actual.

Añado el método distanciaA(Punto otro) a la clase Punto, y un pequeño ejemplo de uso. Mantengo los atributos con visibilidad por defecto tal y como pediste antes. Fíjate en cómo this.x y this.y hacen referencia al objeto actual, y otro.x, otro.y al parámetro recibido.
```java
class Punto {
    int x;  // visibilidad por defecto
    int y;  // visibilidad por defecto

    // Constructor: desambigua parámetros y atributos con 'this'
    public Punto(int x, int y) {
        this.x = x; // 'this.x' es el campo; 'x' es el parámetro
        this.y = y;
    }

    // Método de instancia: 'this' es el objeto actual
    public double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
        // Podrías escribir x*x + y*y; 'this' aquí es opcional
    }

    // Ejemplo adicional: mover el punto y devolver el propio objeto (fluent)
    public Punto mover(int dx, int dy) {
        this.x += dx;
        this.y += dy;
        return this; // devuelve la referencia al objeto actual
    }
}

public class Main {
    public static void main(String[] args) {
        Punto p = new Punto(3, 4);
        System.out.println(p.calculaDistanciaAOrigen()); // 5.0
        p.mover(1, -2);
        System.out.println(p.x + ", " + p.y); // 4, 2
    }
}
```
## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 
### Respuesta
En Java todo es paso por valor. Cuando pasas un Punto a un método, lo que se copia es el valor de la referencia (un “puntero” seguro) hacia el mismo objeto en el heap. Por eso, si dentro del método modificas los atributos del Punto (por ejemplo, p.x = 10;), esos cambios sí afectan al mismo objeto que ves fuera del método. En cambio, si reasignas el parámetro (p = new Punto(...)), solo cambias la copia local de la referencia: fuera del método se seguirá apuntando al objeto original.

Con los tipos primitivos (como int), también se pasa por valor, pero aquí el valor es el dato en sí. Si un método recibe un int y lo modifica (n = 99;), el cambio no afecta a la variable del llamador, porque se trabajó sobre una copia del número. Esta diferencia práctica suele resumirse así: objetos → puedes cambiar su estado interno; primitivos → no puedes cambiar el valor del llamador (y con objetos, tampoco puedes cambiar qué objeto referencia el llamador, solo su contenido).
```java
// Caso objeto: cambia el estado y se ve fuera
void ajustar(Punto p) { 
    p.x += 5;           // afecta fuera
    p = new Punto(0,0); // NO afecta fuera (reasignación local)
}

// Caso primitivo: no afecta fuera
void ponerANoventaYNueve(int n) {
    n = 99;             // cambio local, fuera sigue igual
}
```
## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java
### Respuesta
toString() es un método de instancia definido en java.lang.Object que devuelve una representación textual del objeto. Al sobrescribirlo en tus clases, controlas cómo se “imprime” ese objeto (por ejemplo, en System.out.println(obj) o al concatenarlo con cadenas). Por defecto, Object.toString() muestra el nombre de la clase y un hash en hex, así que casi siempre conviene sobrescribirlo para algo legible y útil (p. ej., valores de sus atributos).

Este concepto existe en otros lenguajes, aunque con nombres distintos: en C# también es ToString(), en Python es __str__ (y __repr__ para una representación más técnica), y en C++ se suele lograr con la sobrecarga de operator<< para std::ostream. La idea común es la misma: ofrecer una forma coherente de convertir un objeto a texto para depuración, logs o interfaces de usuario.
```java
class Punto {
    int x;  // visibilidad por defecto
    int y;  // visibilidad por defecto

    public Punto(int x, int y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public String toString() {
        return "(" + x + ", " + y + ")";
    }
}

public class Main {
    public static void main(String[] args) {
        Punto p = new Punto(3, 4);
        System.out.println(p);                   // usa toString(): (3, 4)
        System.out.println("Punto = " + p);      // concatena: (3, 4)
    }
}
```

## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?
### Respuesta
Una clase se parece a un struct de C en el sentido de que ambos permiten agrupar datos bajo un mismo tipo. Pero una clase va mucho más allá, porque además de atributos también incluye métodos, control de acceso, constructores, encapsulamiento y reglas de comportamiento. En cambio, un struct de C solo contiene datos, sin funciones internas ni mecanismos propios del paradigma orientado a objetos. Por eso, aunque conceptualmente son parecidos como “contenedores de datos”, su papel en el lenguaje es totalmente distinto.

A un struct de C le faltan varias características para ser equivalente a una clase. La principal es que no puede contener métodos asociados, es decir, no puede encapsular comportamiento junto al estado. Tampoco tiene constructores, destructores automáticos, visibilidad (public, private), herencia, ni polimorfismo. Además, las variables de tipo struct en C no son “instancias” en el sentido orientado a objetos: simplemente son bloques de memoria con la forma definida por el struct, pero no tienen identidad de objeto, ni se accede a ellas a través de referencias gestionadas por una máquina virtual como en Java.

Dicho de otro modo: para que un struct fuera como una clase, debería poder combinar datos y funciones, permitir crear instancias mediante constructores, y ser capaz de tener comportamiento propio. Todo esto es justo lo que aporta la definición de clase en lenguajes como Java o C++. Por eso, la orientación a objetos no es solo “una struct con funciones”: es una forma completa de organizar el software alrededor de entidades con estado, comportamiento e identidad. Si quieres, puedo mostrarte una comparación directa de un struct en C y una clase en Java con el mismo propósito.
Proporcione sus comentarios sobre BizChat

## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?
### Respuesta
Sí, puedes emular una clase como Punto en C usando un struct para los datos y funciones externas que operen sobre él. La diferencia clave es que en C no hay métodos dentro del struct, ni constructores, ni control de acceso: tú te encargas de inicializar y pasar el struct a las funciones. Para simular el “método” que calcula la distancia al origen, defines una función que reciba un puntero a struct Punto. Así evitas copias innecesarias y puedes acceder/modificar sus campos si lo necesitas.

Respecto a this: en Java es una referencia implícita al objeto actual dentro de sus métodos. En C no existe this; lo emulas pasando explícitamente un parámetro (normalmente un puntero) al struct sobre el que quieres operar. Es decir, el parámetro Punto* p en C cumple el papel de this en Java. También es habitual “namespear” las funciones con un prefijo (por ejemplo, punto_) para que quede claro a qué “tipo” pertenecen.
Codigo en C:
```c
// punto.c (o en un único .c para algo mínimo)
#include <stdio.h>
#include <math.h>

typedef struct {
    int x;  // no hay encapsulamiento: es público por defecto
    int y;
} Punto;

// "Constructor" manual: una función fábrica
Punto punto_crear(int x, int y) {
    Punto p;
    p.x = x;
    p.y = y;
    return p; // devuelve por valor (copia pequeña, OK)
}

// "Método" que calcula la distancia al origen: recibe el "this" explícito
double punto_distancia_origen(const Punto* p) {
    return sqrt((double)p->x * p->x + (double)p->y * p->y);
}

// (Opcional) distancia entre dos puntos
double punto_distancia(const Punto* a, const Punto* b) {
    int dx = a->x - b->x;
    int dy = a->y - b->y;
    return sqrt((double)dx * dx + (double)dy * dy);
}

int main(void) {
    Punto p = punto_crear(3, 4);
    printf("Distancia al origen: %.1f\n", punto_distancia_origen(&p)); // 5.0

    Punto q = punto_crear(6, -2);
    printf("Distancia p–q: %.3f\n", punto_distancia(&p, &q));
    return 0;
}
```
En resumen: con struct + funciones externas puedes modelar estado y operaciones, pero no hay encapsulamiento, no hay métodos ni this implícito, no hay constructores (los sustituyes por funciones de inicialización) y no hay polimorfismo/herencia. Aun así, esta técnica es la base de la programación estructurada/modular en C y te permite aproximarte al estilo de “clase ligera” de forma ordenada.

Fuentes utilizadas
Microsoft. (2026). M365 Copilot (versión GPT‑5 Chat) 
https://m365.cloud.microsoft/chat/