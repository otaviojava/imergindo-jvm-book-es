# Garbage Collector


Diferente de algunos lenguajes Java tiene una gestión de memoria automática, eso permite que la memoria de un objeto no mas utilizado sea retomada, eso ciertamente es una de las grandes ventajas de la plataforma en relación a `C`. El primer desafio de la JVM es identificar cuales objetos son dispensables, y asi retomar la memoria con eso fue realizada varias técnicas para asi hacerlo.



![Estilo mark and sweep, en que los objetos utilizados son marcados, los no utilizados son marcados, despues de esos dos pasos el proximo paso será desfragmentar la memoria principal.](chapter_6_1.png)


El mas conocido es el **Mark and Sweep**, basicamente dos procesos que marca los objetos utilizados y en el final los objetos no marcados son dispensables para retomar la memoria, el mayor problema es que todos los procesos son parados para ejecutar tal procedimento inviabilizando llamarlo constantemente. En función de ese problema citado anteriormente hablaremos del segundo algoritmo, que lleva en consideración que muchos objetos no tiene una larga vida, no obstante, algunos llevan bastante tempo en la memoria, asi los algoritmos se basa en generaciones que divide la memoria en tres partes (joven, efectiva y permanente).

Para mejor gestionar el colector de basura la memoria heap es dividida basicamente en algunas partes:


* **Young Generation**: Es donde contienen los objetos recien creados, la grande mayoria de los objetos mueren dentro de esa area. Esta es subdividida en dos partes: **Eden** (lugar donde los objetos nacen) y **Survivers(N)** lugares donde los objetos van pasando hasta salir de Young Generation. Su funcionamento es de manera simple: Los objetos nacen en **Eden**, despues de un tiempo, los objetos son copiados “vivos” para los **Survivers**, los objetos que no fueron copiados no son borrados, pero en el futuro, otros objetos ocuparan su espacio. 
* Con el pasar de las colecciones los objetos existentes salen de la **Young** y van para **Tenured generation**, en ese espacio la gestión de objetos es realizado de forma diferente, asi no hay copia, existen algoritmos derivados de **Swep and Mark**, con los objetos borrados la próxima preocupación será en relación a la fragmentación del registrador, asi habrá el proceso de compactación de los datos.


![División de la memória por generación](chapter_6_2.png)
 
Comentando un poco sobre los procesos de **menor colector** (procedimiento de generation que copia objetos para registradores sobreviventes) y el **mayor colector** (procedimiento cuyo algoritmos son derivados de **Mark and Swep** que borra los objetos no utilizados y cuando está fragmentada la memoria sucederá el procedimiento de compactación, cabe recordar que para tal procedimiento la JVM es para todos sus procesos). El objetivo ahora será hablar sobre el estilo o el modo de los Garbage Collector.


## Implementación Serial


Este estilo es muy indicado para pequeñas aplicaciones o hardware de pequeño poder computacional y solo un processador, monocore, este se basa en la ejecución de los procesos, mayor y menor colector, utilizando solo un `Thread`, de ese modo puede economizar recursos, pero si hay un gran número de memoria habrá un gran delay. 

![Serial](chapter_6_3.png)


## Implementación Paralelo



Trabaja de forma semejante de serial, no obstante, será utilizado dos o mas `Threads` por colección, asi el proceso tiende a realizarse en un tiempo menor, asi utiliza mas recursos de maquina.

![Implementación Paralelo](chapter_6_4.png)


## Implementación Concurrente


Este tambien ejecuta procesos en paralelo, no obstante, su objetivo es disminuir el tiempo de mayor colector, incluso si lo ejecuta varias veces. Conveniente para muchos objetos que duran mucho tiempo, asi estos quedan en **Turnered**. Resumiendo sus divisiones de proceso realizan marcación en que todas las `Thread` estan paradas y marcaciones concurrentes, pero la eliminación de los objetos ocurren sin detener ningun proceso, el único problema de ese estilo es el hecho que no hay compactación de datos periodico, solo cuando se vuelva crítico (usando **SerialOdl**).


![Implementación concurrente](chapter_6_5.png)


## Implementación Incremental Concurrent


Tambien es concurrente, pero es realizado de forma incremental (realizado a pocos y agendado entre los menor-colector) su funcionamiento es bien semejante al anterior, pero adiciona un proceso que es redimensionar y preparar los datos para una proxima colección o ciclo que controla el tiempo que el colector queda en el procesador. En caso tenga problemas de fragmentación, este tambien accionará el serialOdl (que ademas de remover los datos tambien compactará los objetos sobreviventes).

![Incremental concurrent](chapter_6_6.png)


## Implementación Garbage First
	


Lanzado en la versión 7 de Java, el **Garbage first**, es colector paralelo diseñado para tener un gran throughput, este fue diseñado para sistemas con una alta cantidad de memoria y de procesadores. Para alcanzar su objetivo este divide igualmente el tamaño del **Heap**. Asi como los dos ultimos concurrentes, este tiene una fase en que realiza la marcación concurrente, y realiza el calculo de objetos alcanzables de cada región, por lo que de vez en cuando, todos los procesos son parados los objetos vivos son copiados para otra región, haciendo que la región en cuestión sea totalmente tomada. Tendran mayor prioridad las regiones con mayor numero de objetos “muertos” (asi se tendrá menos trabajo en realizar la copia para otra area). El **G1** vino para sustituir los tipos concurrente de colección (`CMS` y `I-CMS`) debido a la brecha que ambos dejaban.

No tiene un tiempo determinado para dejar el procesador y la compactación del heap (muy critica la llamada serialOdl). El **G1** toma como estrategia el hecho de ser mas facil controlar pequeñas regiones de que una generación, otro aspecto es que tan pronto las memorias existentes haya sido copiado para una nueva area, la anterior es considerada una area limpia.


![G1](chapter_6_7.png)