# Registros de la JVM

Hablando un poco sobre los tipos de datos que son almacenados en la JVM y su tamaño. Es necesario también que se tenga el concepto de dónde es almacenada tal información. La JVM usa registros para almacenar varias cosas, resulta que para cada tipo de dato existe un lugar específico. Durante la ejecución de un programa existen registros que son compartidos entre toda la JVM y otros que tiene la visibilidad del `Thread` actual.

![Los registros de JVM, Method Area y Heap son compartidas por toda la JVM y Program Counter, Stack Java y Stack Nativo cada Thread tiene su juego.](chapter_3_1.png)


## Program Counter


El registro **PC**, Program Counter, es creado tan pronto un `Thread` es creado, es decir, cada `Thread` posee el suyo. Este puede almacenar dos tipos de datos: 

1. Punteros nativos
2. returnAdress

Esos datos poseen información como la instrucción que esta siendo ejecutada por el `Thread`. Si el método ejecutado fuera nativo **PC** será un puntero y no tiene un valor definido, al contrario, este tendrá la dirección de instrucción, el **returnAdress**.

![Funcionamiento de PC](chapter_3_2.png)


## Java Stack (Java Virtual Machine stack)


Así como el **PC**, este es un registro privado para cada `Thread`, este registro almacena **frames** (que se verá más adelante). Su funcionamiento es similar al de lenguajes clásicos como `C`, este sirve para almacenar variables locales y resultados parciales, invocaciones y resultados de los métodos. Este no modifica las variables directamente solamente inserta y remueve frames del registro. Tan pronto el `Thread` actual llama a un método un nuevo frame es ingresado con información de parámetros, variables locales, etc. Así que cuando el método termina de manera normal, cuando acaba el método, o por interrupción, cuando ocurre una excepción dentro del método, ese *frame* es descartado. El Java *stack* puede ser de tamaño fijo o determinado dinámicamente.


### Stack Frame


Un **frame** es una unidad de **Java stack**, este es creado tan pronto como un método es creado y es destruido cuando el método es cerrado (normalmente o interrumpido por una excepción). Cada **frame** posee una lista de las variables locales, pila de operaciones además de referencia de la clase actual y del método actual. Este frame es dividido en tres partes:

1. Stack variables
2. Stack Operand
3. Frame Data


![Stack Frame](chapter_3_3.png)



#### Stack variables


Cada **frame** contiene un vector para almacenar variables locales y parámetros y su tamaño es definido en tiempo de ejecución. En ese vector las variables `double` y `long` ocupan dos elementos del vector y son almacenados consecuentemente. Variables de tipo `int` y `returnAdress` ocupan un elemento de ese vector (`byte`, `short` y `char` son convertidos en `int`). Si el método es de instancia, no estático, el primer elemento de ese vector será ocupado por la instancia que está ejecutando ese método y enseguida los parámetros, en el orden que fueron pasados. Si el método es de clase, el método estático, no habrá referencia de la instancia que llama al método, así el primer elemento serán los parámetros.


![Las pilas de variables son compuestas por índices de 32 bits, así las variables de tipo double y long ocupan dos espacios continuos y las otras variables solo uno.](chapter_3_4.png)


#### Stack Operand


Como el nombre indica, este registro sirve para almacenar las instrucciones que ocurren dentro del método, como registro de variables locales, los valores son almacenados en un vector pero sus valores recuperados por la eliminación del último elemento del vector en vez de ser por el índice. Este es basado en la estructura de datos de la pila -stack- (el primero en entrar será el último en salir). El tamaño de las variables es de manera semejante a las variables locales.

![Pila de operación, semejante a su “hermano”, su unidad posee un tamaño de 32 bits, su paso-a-paso sigue como una pila convencional, el último en entrar será el primero en salir. En este ejemplo se utilizará la suma de dos enteros ( 10 y 20).](chapter_3_5.png)
Pila de operación, semejante a su “hermano”, su unidad posee un tamaño de 32 bits, su paso-a-paso sigue como una pila convencional, el último que entra será el primero que sale. En este ejemplo se utilizará la suma de dos enteros ( `10` y `20`).

![Como la pila de operación está compuesta por unidades de 32 bits, si fuera double o long este ocupará las dos unidades seguidas, en este ejemplo son sumados dos doubles ( 10.10 y 20.20 )](chapter_3_6.png)
Como la pila de operación está compuesta por unidades de 32 bits, si fuera `double` o `long` este ocupará las dos unidades seguidas, en este ejemplo son sumados dos doubles ( `10.10` y `20.20`)


#### Frame Data


Este pequeño registro tiene el *link* del *pool* de constantes de la clase que lo tiene y el método que está siendo ejecutado.


## Native Method Stack


Tiene la finalidad de almacenar variables y valores nativos (métodos escritos en otros lenguajes), es creado tan pronto un `Thread` es iniciado y todos los `Threads` poseen su registro.


![Pila nativa](chapter_3_7.png)


## Method Area


Este registro tiene la finalidad de almacenar lógicamente el *stream* de clases, esa área es compartida entre todos los `Threads`. Logicamente forma parte del *Heap Space*. Por ser parte tiene la labor de reunir la memoria automática, *Garbage Collector*. Las clases contienen la siguiente información:


* El **qualified** de la clase (El *qualifed* es la dirección de su clase que es definido por el paquete más `.` y el nombre de la clase, por ejemplo, `java.lang.Object` o `java.util.Date`).
* El **qualified** de la clase padre (menos para las Interfaces es `java.lang.Object`).
* Información de si es una clase o una interface.
* Los modificadores.
* La lista con los **qualifieds** de las interfaces.


Para cada clase cargada en Java es cargada un **constant pool**, que contiene la siguiente información:


* El **constant pool** de tipo (Para cada clase cargada es creada un *constant pool*, este contiene el link simbólico para los métodos y para los atributos, además de las constantes existentes en el tipo).
* Información de los atributos (el nombre del atributo, el tipo y su modificador).
* Información de los métodos (el nombre del método, su retorno, el número y tipo de los parámetros en orden y el tipo y su modificador).
* Referencia para `ClassLoader` (clase responsable de cargar la clase)
* Variables de la clase (variables compartidas entre todas las clases, eso incluye las constantes).
* Referencia de la clase (una instancia de `java.lang.Class` para toda clase cargada).

### Heap Space

Tan pronto se crea una instancia, la información de su objeto queda almacenada aquí, ese espacio de memoria también es compartido entre los `Threads`. El **heap** tiene un mecanismo de reclamar memoria en tiempo de ejecución además de mover objetos evitando la fragmentación del espacio.


![Representación de una variable de tipo de referencia dentro del Heap](chapter_3_8.png)


Representación de una variable de tipo de referencia dentro del **Heap** es diferente de los tipos primitivos, este tiene su mecanismo muy semejante a los punteros de `C/C++` ya que este no tiene la información, solo apunta hacia el lugar donde está. El objeto de referencia es constituido de dos punteros menores:

* Uno apuntará al pool de objetos, lugar donde está la información.
* El segundo apuntará a su *constant pool* (que tiene la información de la clase como los atributos, métodos, encapsulamientos, etc.) que queda localizado en el **method Area**.


La representación de los vectores se comporta de forma semejante a las variables de referencia, pero estos tienen dos campos más: 

1. **size**, que define el tamaño del vector
2. **lista de referencia** que apunta a los objetos que están dentro de ese vector. 


![Representación de un vector dentro del Heap](chapter_3_9.png)


## Cache de código


Este registro es usado para compilación y almacenamiento de los métodos que fueron compilados en modo nativo por el **JIT**, este registro es compartido por todos los `Threads`.


### Just In Time (JIT) Compilation


Los **bytecode** Java interpretados no son tan rápidos como el código nativo, para cubrir este problema de performance, la JVM verifica métodos críticos (regiones que se ejecutan repetidamente, por ejemplo) y compila para él código nativo. Este código nativo será almacenado dentro de **cache de código** en una región fuera del *heap*. La JVM intenta escoger las regiones más críticas para que incluso con el gasto de memoria y poder computacional de compilar el código para nativo, sea una decisión ventajosa.


## Resumen


Con eso se describió todo sobre los registros que tiene la JVM, vale recordar que algunas son exclusivas por `Threads`y otras no. La **pila nativa** es importante para obtener recursos de la máquina, no obstante, sus valores son indefinidos, y las **pilas Java** son creadas tan pronto un método es iniciado, este es subdividido en **frames**, ambas pilas son particulares por cada `Thread`. El registro **PC** no tiene información, solo apunta para la instrucción que está siendo ejecutada y tiene una por `Thread`. El **Heap** y el **method Area** son compartidas por la JVM, todas las `Threads`, y tiene la responsabilidad de almacenar la instancia de los objetos y los *streams* y la información de la clase, respectivamente.