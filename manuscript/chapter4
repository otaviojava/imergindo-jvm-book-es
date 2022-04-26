# ByteCodes



Una vez que se tiene la noción de registros y dónde se almacena cada valor de la JVM, hablaremos un poco sobre el funcionamiento de las instrucciones, esta tiene código de operación y tamaño de 1 byte, de ahí el **bytecode**. Cada **bytecode** representa una acción o una operación. La mayoría de las operaciones de ese código operan para un tipo específico de valor, por ejemplo, `iload` (carga un `int` a la pila) y `fload` (carga un `float` a la pila) tienen operaciones similares, sin embargo, **bytecodes** diferentes. Un buen truco para saber el tipo de operador es saber la letra inicial de la operación: **i** para una operación de entero (`int`), **l** para `long`, **s** para `short`, **b** para `byte`, **c** para `char`, **f** para `float`, **d** para `double` y **a** para referencia (`address`). 


## Cargar y guardar información


Estas instrucciones realizan cambio de información entre el vector de variables locales y la pila de operaciones, en que lugar cargar, *load* (definido por `iload`, `lload`, `fload`, `dload` e `aload`) información de la pila de variables para operaciones y almacenar, *store* (definido por: istore, lstore, fstore, dstore, astore) realiza el proceso inverso.


## Operaciones aritméticas: 

Estas son realizadas con los dos primeros valores en la pila de operaciones y devuelve el resultado. Su procesamiento es subdividido en flotantes y enteros que tienen comportamientos diferentes para algunos resultados, por ejemplo, en volcado de pila y división por cero.

* **sumar**: iadd, ladd, fadd, dadd. 
* **restar**: isub, lsub, fsub, dsub. 
* **multiplicar**: imul, lmul, fmul, dmul. 
* **dividir**: idiv, ldiv, fdiv, ddiv. 
* **resto**: irem, lrem, frem, drem. 
* **negar**: ineg, lneg, fneg, dneg. 
* **mover**: ishl, sidh, iushr, lshl, lshr, lushr. 
* **"or" bit a bit**: ior, lor. 
* **"and" bit a bit**: iand, a terra. 
* **"or exclusivo" bit a bit**: ixor, lxor. 
* **incrementar variable local**: `iinc`. 
* **comparar**: `dcmpg`, `dcmpl`, `fcmpg`, `fcmpl`, `lcmp`.


## Conversión de valores (casting)

 
Las instrucciones de conversión de valores sirve para modificar el tipo de la variable (casting), esta variable puede ampliar o reducir su tipo, así: 

* **Promoción -a mayor precisión-**: de `int` a `long`, de `int` a `float`, de `int` a `double`. De `long` a `float` y de `float` a `double` (`i2l`, `i2f`, `i2d`, `l2f`, `l2d`, y `f2d`) con esta ampliación no se pierde la precisión del valor original. 
*  El **acortamiento -a menor precisión-** del tipo como: de `int` a `byte`, de `int` a `short`, de `int` a `char`, de `long` a `int`, de `long` a `float`, de `float` a `int` o a `long`, de `double` a `int`, de `double` a `long` o de `double` a `float` (`i2b`, `i2c`, `i2s`, `l2i`, `f2i`, `f2l`, `d2i`, `d2l`, y `d2f`) cabe recordar que en tales modificaciones existe la posibilidad de modificar el valor (volcado del valor).

## Creación y manipulación de objetos: 

* Instrucciones para la creación y manipulación de instancias (`new`)
* Instrucciones para creación de arrays (`newarray`, `anewarray`, `multianewarray`).
* Accesar atributos estáticos o de la instancia de una clase (`getfield`, `putfield`, `getstatic`, `putstatic`).
* Cargar (`baload`, `caload`, `saload`, `iaload`, `laload`, `faload`, `daload`, `aaload`)
* Guardar en la pila (`bastore`, `castore`, `sastore`, `iastore`, `lastore`, `fastore`, `dastore` y `aastore`) 
* Tamaño de arreglos (`arraylength`).
* Verifica la propiedad de la instancia o array (`instanceof` y `checkcast`).


## Instrucciones condicionales 

Instrucciones que retornan valores booleanos (`ifeq`, `ifne`, `iflt`, `ifle`, `ifgt`, `ifge`, `ifnull`, `ifnonnull`, `if_icmpeq`, `if_icmpne`, `if_icmplt`, `if_icmple`, `if_icmpgt` `if_icmpge`, `if_acmpeq`, `if_acmpne`, `tableswitch`, `elookupswitch`, `goto`, `goto_w`, `jsr`, `jsr_w` y `ret`).


## Llamadas de métodos y retorno de valores

Las lamadas de un método son: 

* **invokevirtual**: Llama un método de una instancia
* **invokeinterface**: Llama un método de una interface
* **invokespecial**: Llamadas de un método privado o de la superclase
* **invokestatic**: Realiza la llamada de un método estático
* **invokedynamic**: método que construye un objeto 

El retorno de una instrucción puede ser definido (`ireturn`, `lreturn`, `freturn`, `dreturn` y `areturn`). Durante la ejecución del método en caso sea interrumpida de manera inesperada con una excepción se realiza la llamada a throw. Los métodos síncronos son posibles gracias a la presencia de un simple encapsulado llamado de monitor, esos tipos de métodos son definidos por el flag `ACC_SYNCHRONIZED` en su *constast pool*, que cuando tiene tal flag el método entra en el monitor(`monitorenter`) y es ejecutado, y ningun otro *Thread* puede accesarlo, y sale (`monitorexit`) cuando su método es cerrado (de un modo normal o por interrupción).


## Clases después de la compilación


Al hablar de **bytecodes** es interesante “tirar el gancho” y hablar del cómo queda una clase después de su compilación. Como ya se dijo, después de la compilación es generado un **bytecode**, cuyo archivo tiene una extensión .class, y cada archivo representa solo una clase. Cada archivo tiene las siguientes características:

 
* Un número mágico en hexadecimal que define que esa clase es un .class el valor es **0xCAFEBABE**

* El mayor y menor número de la versión del archivo class que juntos definen la versión del archivo, o sea, la JVM antes de correrla necesita verificar si la versión V que esta puede ejecutar está entre: Versión menor < V < Versión mayor.

* **access_flags**: Este flag indica el tipo de encapsulamiento de la clase, métodos y sus propiedades. Los flags pueden ser:


* **ACC_PUBLIC**: flag método, atributos públicos
* **ACC_PRIVATE**: flag para privados
* **ACC_PROTECTED**: protected
* **ACC_STATIC**: estático
* **ACC_FINAL**: final
* **ACC_SYNCHRONIZED**: indica un método sincronizado
* **ACC_BRIDGE**: indica que el método fue generado por el compilador
* **ACC_VARARGS**: indica que es varags 
* **ACC_NATIVE**: nativo
* **ACC_ABSTRACT**: abstracto
* **ACC_STRICT**: indica que el método es strict
* **ACC_SYNTHETIC**: indica que el método no es “original”


. 
* **this_class**: el valor de la clase actual debe tener un índice válido en la *constant pool*
 
* **super_class**: la información de la superclase debe estar dentro y puede ocupar el índice cero o no, si ocupa el índice cero esa clase es java.lang.Object, la única clase que no tiene padre, de otra manera tendrá que ser un índice válido y tener informaciones que apuntan para la clase padre. Las informaciones de la clase es definida por su nombre con su ruta, por ejemplo, el nombre de String seria java/lang/String.

* **constant pool**: El constant pool es una estructura de tabla que contiene el nombre de las clases, interfaces, métodos, atributos y otras informaciones de las clases. Para guardar esas informaciones existen dos registos para cada información importante: El vector con información de la clase, método, o atributos y su contador o índice que funciona como limitador del vector. Este es el caso de las interfaces que la clase implementa, atributos, métodos que tienen sus respectivos vector e índices.

* Las descripciones de los atributos o de los parámetros en un método como su tipo es definido a continuación:

  * B byte signed byte 
  * C char 
  * D double 
  * F float 
  * I int 
  * J long 
  * L Classname; referencia 
  * S short
  * Z boolean 
  * [ referencia de un vector 
  * [[ referencia de una matriz 


Asi, por ejemplo: `double dobro(double d)` es igual  `(D)D` y `Double dobro(Double d)` es `(Ljava/lang/Double;)Ljava/lang/Double`.

Dentro del *constant pool* cada información tiene su primer byte que indica su tipo de información:


  * CONSTANT_Class 7 
  * CONSTANT_Fieldref 9 
  * CONSTANT_Methodref 10 
  * CONSTANT_InterfaceMethodref 11 
  * CONSTANT_String 8 
  * CONSTANT_Integer 3 
  * CONSTANT_Float 4 
  * CONSTANT_Long 5 
  * CONSTANT_Double 6 
  * CONSTANT_NameAndType 12 
  * CONSTANT_Utf8 1 
  * CONSTANT_MethodHandle 15 
  * CONSTANT_MethodType 16 
  * CONSTANT_InvokeDynamic 18 




**StackMapTable**: es compuesto de stackmapframe y tiene el objetivo de verificaciones para el bytecode.

Para ayudar en la depuración en el lenguaje Java existen información para depurar el código esas variables son: LocalVariableTable y LocalVariableTypeTable que define las información de variables locales para el debug y LineNumberTable define la parte de bytecode y su correspondiente linea de código.
Para las anotaciones existen: `RuntimeVisibleAnnotations`, `RuntimeInvisibleAnnotations`, `RuntimeVisibleParameterAnnotations`, `RuntimeInvisibleParameterAnnotations` que contienen información de las anotaciones como su visibilidad en tiempo de ejecución a los atributos y métodos o no, existen esas mismas informaciones para los parámetros como sus visibilidades. `AnnotationDefault` define las informaciones dentro de las anotaciones.


El contador de *constant pool* posee 16 bits, o sea, este solo puede contener 2¹⁶=65535 elementos, ese mismo número vale para el número de métodos, atributos, interfaces implementadas, variables locales, pila de operaciones (en que lugar para esos dos últimos `long` y `double` ocupan dos espacios), el nombre del método o atributo. El número de dimensiones de una matriz es 255 el mismo número vale para la cantidad de parámetros, en caso no sea un método estático se debe incluir la instancia.
	
Con el objetivo de poner en práctica y visualizar esos **bytescodes**, será muestra un código simple y su respectivo bytecode.


```java 
public class PrimerTest{ 

public Double sumarIntancias(Double a, Double b) { 

	Double resultado = a + b; 
	return resultado; 
} 

public double sumarDouble(double a, double b) { 
        return a + b; 
} 
public int sumarEnteros(int a, int b) { 
        return a + b; 
} 

public short sumarShort(short a, byte b) { 
        return (short) (a + b); 
} 

public static int sumarStatic(int a, int b) { 
        return a + b; 
} 

}
```


Creado el archivo PrimerTest.java e insertado el código 1 en ese archivo, los próximos pasos serán entrar por el terminal en la ruta que se encuentra el archivo PrimerTest.java, compilar y analizar su respectivo bytecode con los siguientes comandos.

* `javac PrimerTest.java`
* `javap -verbose PrimerTest`

El resultado:

```bytecode

  minor version: 0 
  major version: 51 
  flags: ACC_PUBLIC, ACC_SUPER 
Constant pool: 
   #1 = Methodref          #5.#21         //  java/lang/Object."<init>":()V 
   #2 = Methodref          #22.#23        //  java/lang/Double.doubleValue:()D 
   #3 = Methodref          #22.#24        //  java/lang/Double.valueOf:(D)Ljava/lang/Double; 
   #4 = Class              #25            //  PrimerTest 
   #5 = Class              #26            //  java/lang/Object 
   #6 = Utf8               <init> 
   #7 = Utf8               ()V 
   #8 = Utf8               Code 
   #9 = Utf8               LineNumberTable 
  #10 = Utf8               sumarIntancias 
  #11 = Utf8               (Ljava/lang/Double;Ljava/lang/Double;)Ljava/lang/Double; 
  #12 = Utf8               sumarDouble 
  #13 = Utf8               (DD)D 
  #14 = Utf8               sumarEnteros 
  #15 = Utf8               (II)I 
  #16 = Utf8               sumarShort 
  #17 = Utf8               (SB)S 
  #18 = Utf8               sumarStatic 
  #19 = Utf8               SourceFile 
  #20 = Utf8               PrimerTest.java 
  #21 = NameAndType        #6:#7          //  "<init>":()V 
  #22 = Class              #27            //  java/lang/Double 
  #23 = NameAndType        #28:#29        //  doubleValue:()D 
  #24 = NameAndType        #30:#31        //  valueOf:(D)Ljava/lang/Double; 
  #25 = Utf8               PrimerTest 
  #26 = Utf8               java/lang/Object 
  #27 = Utf8               java/lang/Double 
  #28 = Utf8               doubleValue 
  #29 = Utf8               ()D 
  #30 = Utf8               valueOf 
  #31 = Utf8               (D)Ljava/lang/Double; 
  
 ```


En ese primer resultado podemos visualizar el constant pool y la menor y la mayor versión del class. El Constant Pool contiene las informaciones de la respectiva clase, ya que toda clase tiene esa información, inclusive los InnerClass, y estos son almacenados en un vector.



```bytecode

public PrimerTest(); 
    flags: ACC_PUBLIC 
    Code: 
      stack=1, locals=1, args_size=1 
         0: aload_0       
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V 
         4: return        
      LineNumberTable: 
        line 1: 0 
      LocalVariableTable: 
        Start  Length  Slot  Name   Signature 
               0       5     0  this   LPrimerTest; 

  public java.lang.Double sumarIntancias(java.lang.Double, java.lang.Double); 
    flags: ACC_PUBLIC 
    Code: 
      stack=4, locals=4, args_size=3 
         0: aload_1       
         1: invokevirtual #2                  // Method java/lang/Double.doubleValue:()D 
         4: aload_2       
         5: invokevirtual #2                  // Method java/lang/Double.doubleValue:()D 
         8: dadd          
         9: invokestatic  #3                  // Method java/lang/Double.valueOf:(D)Ljava/lang/Double; 
        12: astore_3      
        13: aload_3       
        14: areturn       
      LineNumberTable: 
        line 5: 0 
        line 6: 13 
      LocalVariableTable: 
        Start  Length  Slot  Name   Signature 
               0      15     0  this   LPrimerTest; 
               0      15     1     a   Ljava/lang/Double; 
               0      15     2     b   Ljava/lang/Double; 
              13       2     3 resultado   Ljava/lang/Double; 

  public double sumarDouble(double, double); 
    flags: ACC_PUBLIC 
    Code: 
      stack=4, locals=5, args_size=3 
         0: dload_1       
         1: dload_3       
         2: dadd          
         3: dreturn       
      LineNumberTable: 
        line 10: 0 
      LocalVariableTable: 
        Start  Length  Slot  Name   Signature 
               0       4     0  this   LPrimerTest; 
               0       4     1     a   D 
               0       4     3     b   D 

  public int sumarEnteros(int, int); 
    flags: ACC_PUBLIC 
    Code: 
      stack=2, locals=3, args_size=3 
         0: iload_1       
         1: iload_2       
         2: iadd          
         3: ireturn       
      LineNumberTable: 
        line 13: 0 
      LocalVariableTable: 
        Start  Length  Slot  Name   Signature 
               0       4     0  this   LPrimerTest; 
               0       4     1     a   I 
               0       4     2     b   I 

  public short sumarShort(short, byte); 
    flags: ACC_PUBLIC 
    Code: 
      stack=2, locals=3, args_size=3 
         0: iload_1       
         1: iload_2       
         2: iadd          
         3: i2s           
         4: ireturn       
      LineNumberTable: 
        line 17: 0 
      LocalVariableTable: 
        Start  Length  Slot  Name   Signature 
               0       5     0  this   LPrimerTest; 
               0       5     1     a   S 
               0       5     2     b   B 

  public static int sumarStatic(int, int); 
    flags: ACC_PUBLIC, ACC_STATIC 
    Code: 
      stack=2, locals=2, args_size=2 
         0: iload_0       
         1: iload_1       
         2: iadd          
         3: ireturn       
      LineNumberTable: 
        line 21: 0 
      LocalVariableTable: 
        Start  Length  Slot  Name   Signature 
               0       4     0     a   I 
               0       4     1     b   I 
               
```


Cuando vemos los metodos podemos percibir que todos los métodos tienen el tamaño de la pila de operación y de variables además del tamaño de las variables implicadas en un determinado método. 

En el primero que es el método constructor, ese método es construido automáticamente en caso no se haya hecho por el usuario, este tiene tamaño 1 de operación, ya que se trata de la creación de un objeto del tipo referencia y este ocupa un espacio en el vector de operación, 1 en el tamaño de variable, ya que este es un método no estático y esa información pertenece a la interface que la está llamando y el número de variables utilizadas es de uno ya que nos estamos refiriendo a la instancia creada. 
En el segundo método, la suma de las instancias y retorna una tercera instancia, `(Ljava/lang/Double;Ljava/lang/Double;)Ljava/lang/Double`, este tiene el tamaño de tres en la pila de variables, una para las dos variables de referencia y una para método y de las instancias, cuatro en el tamaño de pila de operaciones, ya que en el proceso los Doubles serán transformados en double primitivo, así cada uno ocupará dos unidades en el vector. El campo `LineNumberTable` es para ayudar a debuggear el código en un determinado método, `LineNumberTable` 5: 0, dice que la línea de número cinco del código Java equivale a la instrucción del comienzo, linea cero del **bytecode** y linea 6: 13, la línea seis del código Java comienza en la instrucción del **bytecode** número 13. El campo `LocalVariableTable` tambien sirve para debuggear y define el nombre del campo, tipo, linea en la que nace y que muere. Eso demuestra cómo es diferente el código Java y el **byteCode** generado.


En este capítulo hablamos un poco sobre **bytecode** y el truco para entenderlo, mirando por los inicios en comando, cabe recordar que durante la ejecución los booleanos, byte, shorts son transformados en enteros. Se demostró cuan diferente es el código Java del bytecode generado y en función de eso se creó tablas y variables, por ejemplo, LocalVariable y LineNumberTable para auxiliar a la hora de debuggear, esas variables son utilizadas por el modo debug de las IDEs modernas.