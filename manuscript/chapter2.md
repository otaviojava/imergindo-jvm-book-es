# Funcionamento básico de la JVM


Este capítulo hablará un poco sobre el funcionamiento básico de la JVM, que es el corazón del lenguaje Java. Es la responsable por la independencia entre las plataformas y corre básicamente dos tipos de procesos: 

* Los escritos en Java que son **bytecodes** generados.
* Los nativos que son escritos en lenguajes como C/C++ y *enlazados* dinámicamente para una plataforma específica.

Los métodos nativos son muy interesantes para obtener información del SO donde la JVM está en ejecución, además de utilizar recursos de este. Y es en función de eso que a pesar de ser un lenguaje **RunAnyWhere** la JVM no lo es, es decir, para cada plataforma existe una máquina virtual específica. Esto sucede, por ejemplo, para usar recursos específicos de la plataforma donde, por ejemplo, existen llamadas distintas para trabajar con directorios y archivos.


![La JVM necesita ser compilada para una plataforma específica.](chapter_2_1.png)



El único y principal motivo de la JVM es correr el aplicativo. Cuando se inicia una ejecución la JVM nace y cuando la aplicación termina esta muere. Para cada aplicación se crea una JVM, o sea, si se ejecuta tres veces el mismo código en una misma máquina serán iniciadas 3 JVMs. Para correr una aplicación es suficiente que su clase tenga un método público y estático con el nombre main y tenga como parámetro un array de `String`.


Al iniciar una JVM existen algunos procesos que corren en paralelo y en segundo plano y ejecutan diversas operaciones y procesos para mantener a la JVM siempre disponible: 


* Los Timers que son responsables por los eventos que suceden periódicamente, por ejemplo, interrupciones, estos son usados para organizar los procesos que ocurren continuamente. 
* Los procesos *Garbage Collector* que son responsables de ejecutar las actividades del Garbage Collector de la JVM.
* Compiladores que son responsables por transformar bytecode en código nativo.
* Los *listeners*, que reciben señales (información) y tiene como principal objetivo enviar esa información al proceso correcto dentro de la JVM.
 

Hablando un poco más sobre esos procesos paralelos o `Threads`, la JVM permite que múltiples procesos se ejecuten concurrentemente, esta rutina en Java está directamente relacionada con un `Thread` nativo. Tan pronto un proceso paralelo en Java nace, sus primeros pasos son:

* Asignación de memoria
* Sincronización de los objetos
* Creación de los registros específicos para estos y la asignación del `Thread` nativo.
 
Cuando esta rutina genera una excepción la parte nativa envía esa información a la JVM que la cierra. Cuando un `Thread` termina todos los recursos específicos, tanto para Java como para la parte nativa, son entregados a la JVM.

Como en el lenguaje, la JVM opera con dos tipos de datos: 

1. Los primitivos
2. Los valores de referencia. 


La JVM espera que toda la verificación como tipo haya sido realizado en tiempo de ejecución, siendo que los tipos primitivos no necesitan de tal verificación o inspección ya que ellos operan con un tipo específico de instrucción (por ejemplo: iadd, ladd, fadd, y dadd para entero, long, float y double respectivamente).

La JVM tiene soporte para objetos que son instancia de una clase asignada dinámicamente o un array, esos valores son de tipo **reference** y su funcionamiento es semejante a los lenguajes como  C/C++.

Los tipos primitivos existentes en JVM son: 

* Numérico
* Booleano 
* returnAdress

Los tipo numérico son los valores enteros y flotantes.

|Nombre|Tamaño|variación|Valor default|Tipo|
| -- | -- | -- | -- | -- |
|byte|8-bit|-2⁷  hasta 2⁷|0|entero|
| -- | -- | -- | -- | -- |
|short|16-bits|-2¹⁵ hasta  2¹⁵|0|entero|
| -- | -- | -- | -- | -- |
|integer|32-bits|-2³² hasta 2³¹|0|entero|
| -- | -- | -- | -- | -- |
|long|64-bits|-2⁶³ hasta 2⁶³|0|entero|
| -- | -- | -- | -- | -- |
|char|16-bits|UFT-8|'\u0000'|entero|
| -- | -- | -- | -- | -- |
|float|32-bits||0|flotante|
| -- | -- | -- | -- | -- |
|double|64-bits||0|flotante|
| -- | -- | -- | -- | -- |
|boolean|entero||false|booleano|
| -- | -- | -- | -- | -- |
|returnAddress|||null|puntero|

Los formatos de punto flotante son `float`, con precisión simple, y `double`, con doble precisión. Tanto los valores como las operaciones siguen lo especificado en el estándar IEEE para aritmética de punto flotante binario (ANSI/ IEEE. 754-1985, New York). Este estándar no incluye solo valores positivos y negativos, más cero, infinito positivo y negativo y un no numérico -Not A Number- (abreviado como **Nan** es utilizado para representar valores no válidos como el resultado de la división por cero). Por estándar, las JVM soportan ese formato, pero tambien pueden soportar versiones extendidas como `double` y `float`.

El **returnAdress** es usado solo por la JVM, no tiene representación en el lenguaje, tiene su funcionamento similar a los punteros y diferente de los tipos primitivos no podrán ser modificados en tiempo de ejecución.

En la JVM el tipo booleano tiene un soporte bien limitado, no existen instrucciones para booleano, la verdad ellos son compilados para usar los tipos de instrucciones de `int` y de array de booleano son manipulados como `array` de `byte`. Los valores son representados con `1` para verdadero y `0` para falso.

Existen tres tipos de referencia: 

1. class
2. array
3. interface


El valor de referencia es iniciado como `null`, nulo no es un tipo definido, pero se puede hacer *cast* para cualquier tipo de referencia.
	
Resumiendo, existen basicamente dos tipos de datos:

* Primitivos y referencias.
 * Las referencias tienen tres subtipos: class, interface y array.
 * Los primitivos tienen returnAdress, booleano, flotantes (float y double; de simple y doble precisión respectivamente), enteros (short, byte, int, long, char).
