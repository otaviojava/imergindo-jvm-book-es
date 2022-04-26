# Si quieres predecir el futuro, estudia el pasado


**JVM**, la Java Virtual Machine o máquina virtual java, tiene una historia iniciada en el año 1992. El Green Project en esa época el lenguaje era denominado Oak. Con el pasar del tiempo la maquina virtual fue evolucionando y tornándose cada vez más compleja. El lenguaje Java tiene una sintaxis similar a C++, es orientado a objetos, se convirtió popular en conjunto con la web. La JVM sirve de base de la plataforma Java siendo responsable por tratar a todas las plataformas y Sistemas Operativos de modo independiente del lenguaje. La JVM no conoce absolutamente nada del lenguaje Java, solo su **bytecode**, que viene en formato `.class`,  que son las instrucciones de la JVM (de ahi la posibilidad de llevar a otros lenguajes a la JVM, ya que esta no corre Java sino bytecode). Este `class` es el código compilado y representa una clase o interface en java. 


Desde su inicio hasta hoy, Java tuvo muchas versiones. Esas modificaciones son gestionadas por **JCP** o Java Community Process (el comité que regula los cambios de la plataforma Java con cerca de 30 empresas), a partir de JSRs (Java Specification Requests), especificaciones que proporcionan estas modificaciones y mejoras. La documentación del lenguaje queda en **Java Language Specification** -JSL- y la documentación de JVM queda en **Java Virtual Machine Specification**.


## Cronología de la JVM


Antes de hablar de los aspectos de Java, como lenguaje, plataforma y máquina virtual es interesante conocer un poco sobre la evolución que Java viene pasando. El projecto nació en 1995 y a partir de esa fecha viene adquiriendo constante evolución con ayuda de empresas y de la comunidad.


### JDK Alpha y Beta (1995) 

En las versiones alfa y beta se tuvo una máquina inestable.
1.1.2 - JDK 1.0 (23 de enero de 1996) 

Con el nombre Oak, que también fue el primer nombre del lenguaje. En la versión 1.0.2 fue lanzada la primera versión estable.


### JDK 1.1 (19 de febrero de 1997)


* Grandes mejoras y refactorizaciones en el modelo de eventos del AWT
* Se agregan las  Inner classes  al lenguaje
* JavaBeans 
* JDBC 
* RMI 
* Reflection que soportaba solo instrospección, no era posible ninguna modificación en tiempo real.



### J2SE 1.2 (8 de diciembre de 1998)

	
Con el pseudónimo **Plaground**. Esta y otras versiones fueron denominadas Java 2, J2SE Java 2 Platform, Standard Edition, hubo modificaciones significativas en esa versión triplicando el código; 1520 clases en 59 paquetes incluyendo:

* La palabra clave strictfp .
* La API de Swing fue integrada al core.
* El compilador JIT.
* El Java Plug-in.
* Java IDL, una implementación CORBA IDL para interoperabilidad.
* El framework Collections.


### J2SE 1.3 (8 de mayo de 2000)


Tuvo el pseudónimo **Kestrel**, las modificaciones más importantes fueron:

* Incluye HotSpot JVM (fue lanzado en abril de 1999 para los 1,2 J2SE JVM).
* RMI fue modificado para soportar la compatibilidad opcional con CORBA
* JavaSound
* Java Naming and Directory Interface (JNDI) incluido en bibliotecas centrales
* Java Platform Debugger Architecture (ACDP)
* Permite la creación de clases Proxy



### J2SE 1.4 (6 de febrero de 2002)
	

Con el pseudónimo **Merlin**, fue la primera versión de la plataforma desarrollada por el **JCP**, la JSR 59:


* La palabra clave assert (JSR 41)
* Expresiones regulares
* El encadenamiento de excepciones que permite que una excepción de mayor nivel encapsule una excepción de menor nivel.
* Soporte al Protocolo de internet versión 6 (IPv6)
* Nuevas llamadas I/O (llamadas NIO) nuevos Input/Output (JSR 51)
* API de loggin (JSR 47)
* API para leer y escribir imágenes en formatos como JPEG y PNG
* Integración con XML y XSLT (JAXP) en JSR 63
* Nuevas integraciones con extensiones de seguridad y cifrado (JCE, JSSE, JAAS).
* Java Web Start (JSR 56).
* API de preferencias (java.util.prefs) 



### J2SE 5.0 (30 de setiembre de 2004)


Con el pseudónimo **Tiger**, fue desarrollada en la **JSR 176**, tuvo su final de vida el 8 de abril de 2008 y el cierre de soporte el dia 3 de noviembre de 2009. **Tiger** adicionó significativas mejoras para el lenguaje:

* Generics:  (JSR14).
* Annotations: (JSR 175)
* Autoboxing/unboxing: Conversión automática entre los tipos primitivos y las clases encapsuladas (JSR 201).
* Enumerations: (JSR 201.) 
* Varargs: 
* El bucle  for each
* Correciones para Java Memory Model (Que define cómo interactúan los threads en memoria).
* import static
* Generación automática de stub para objetos RMI
* Nuevo *look and feel* para Swing llamado *synth*
* Paquete utilitario de concurrencia (java.util.concurrent)
* La clase Scanner para obtener datos del *input stream* y *buffers*


### Java SE 6 (11 de diciembre de 2006)


Con el pseudónimo **Mustangue**, en esta versión Sun sustituye el nombre “J2SE” y removió el “.0” del número de la versión. Esta versión fue desarrollada en la JSR 270.

* Soporte el lenguaje de script (JSR 223): Una API genérica para integración con lenguajes scripts y fue incorporada la integración con Mozilla JavaScript Rhino.
* Soporte a Web Service através de JAX-WS (JSR 224) 
* JDBC 4.0  (JSR 221). 
* Java Compiler API (JSR 199): una API para permitir llamar la compilación programando
* JAXB  2.0
* Mejoras en las Annotations (JSR 269)
* Mejoras en la GUI, como SwingWorker, tabla filtrada y ordenada
* Mejoras en la JVM incluyendo: sincronización e optimizaciones del compilador
* Mejoras en el algoritmo del Garbage Collector.



### Java SE 7 (28 de julio de 2011)

Con el pseudónimo **Dolphin** posee el mayor número de actualizaciones en Java. Fue lanzado el día 7 de julio y estuvo disponible al día siguiente.

* Da Vinci Machine: Soporte para lenguajes dinámicos.
* Proyecto Coin
* Strings en switch
* Automatic resource management en try-statement
* Diamond
* varargs simplificados
* Binary integer literals
* Numeric literals
* multi-try
* Nuevo paquete utilitario de concurrencia: JSR 166
* NIO2: nueva biblioteca para I/O


### Java SE 8 (18 de marzo de 2014)

 Java 8 fue liberado el día 18 de marzo de 2014 y en esta versión se incluyen algunos recursos que estaban planeados en Java 7. Los recursos presentados para esa versión fueron basados en propuestas de mejoras, los JEPS. Entre esas mejoras podemos destacar:

* JSR 223, JEP 174: **Project Nashorn**, un ejecutor runtime de JavaScript, permitiendo la ejecución del código JavaScript dentro de la aplicación. Ese proyecto tuvo como objetivo ser el sucesor de **Rhino**, usando `Invoke Dynamic` en vez de `reflection`.
* JSR 335, JEP 126: Soporte para expresiones Lambda.
* JSR 310, JEP 150: APIs Date y Time.
* JEP 122: Eliminación de Permanent generation