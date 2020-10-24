
![Imagen](ll.jpg)
* * *
## **RESUMEN**
* * *
### **CAPITULO 1**
* * *
#### **Arquitectura ARM** 
ARM es una arquitectura RISC (Reduced Instruction Set Computer=Ordenador
con Conjunto Reducido de Instrucciones) de 32 bits, salvo la versión del core ARMv8-
A que es mixta 32/64 bits (bus de 32 bits con registros de 64 bits). Se trata de una
arquitectura licenciable, quiere decir que la empresa desarrolladora ARM Holdings
diseña la arquitectura, pero son otras compañías las que fabrican y venden los chips,
llevándose ARM Holdings un pequeño porcentaje por la licencia.
 
**Registros**


La arquitectura ARMv6 presenta un conjunto de 17 registros (16 principales más
uno de estado) de 32 bits cada uno.

**Registros Generales.** 
Su función es el almacenamiento temporal de datos. Son los
13 registros que van R0 hasta R12.

**Registros Especiales.** 
Son los últimos 3 registros principales: R13, R14 y R15.
Como son de propósito especial, tienen nombres alternativos.

- **SP/R13.** Stack Pointer ó Puntero de Pila. Sirve como puntero para almacenar variables locales y registros en llamadas a funciones.
- **LR/R14.** Link Register ó Registro de Enlace. Almacena la dirección de
retorno cuando una instrucción BL ó BLX ejecuta una llamada a una
rutina.
- **PC/R15.** Program Counter ó Contador de Programa. Es un registro que
indica la posición donde está el procesador en su secuencia de instrucciones. Se incrementa de 4 en 4 cada vez que se ejecuta una instrucción,
salvo que ésta provoque un salto.

**Registro CPSR.** Almacena las banderas condicionales y los bits de control. Los
bits de control definen la habilitación de interrupciones normales (I), interrupciones rápidas (F), modo Thumb 1
(T) y el modo de operación de la CPU.
Existen hasta 8 modos de operación, pero por ahora desde nuestra aplicación
sólo vamos a trabajar en uno de ellos, el Modo Usuario. Los demás son modos
privilegiados usados exclusivamente por el sistema operativo.
Desde el Modo Usuario sólo podemos acceder a las banderas condicionales,
que contienen información sobre el estado de la última operación realizada
por la ALU. A diferencia de otras arquitecturas en ARMv6 podemos elegir
si queremos que una instrucción actualice o no las banderas condicionales,
poniendo una “s” detrás del nemotécnico 2
. Existen 4 banderas y son las
siguientes:
- **N.** Se activa cuando el resultado es negativo.
- **Z.** Se activa cuando el resultado es cero o una comparación es cierta.
- **C.** Indica acarreo en las operaciones aritméticas.
- **V.** Desbordamiento aritmético.

**Lenguaje Ensamblador** 


El ensamblador es un lenguaje de bajo nivel que permite un control directo de
la CPU y todos los elementos asociados. Cada línea de un programa ensamblador
consta de una instrucción del procesador y la posición que ocupan los datos de esa
instrucción.
Desarrollar programas en lenguaje ensamblador es un proceso laborioso. El procedimiento es similar al de cualquier lenguaje compilado. Un conjunto de instrucciones
y/o datos forman un módulo fuente. Este módulo es la entrada del compilador, que
chequea la sintaxis y lo traduce a código máquina formando un módulo objeto. Finalmente, un enlazador (montador ó linker) traduce todas las referencias relativas a
direcciones absolutas y termina generando el ejecutable.
El ensamblador presenta una serie de ventajas e inconvenientes con respecto a
otros lenguajes de más alto nivel. Al ser un lenguaje de bajo nivel, presenta como
principal característica la flexibilidad y la posibilidad de acceso directo a nivel de
registro. En contrapartida, programar en ensamblador es laborioso puesto que los
programas contienen un número elevado de líneas y la corrección y depuración de
éstos se hace difícil.
Generalmente, y dado que crear programas un poco extensos es laborioso, el
ensamblador se utiliza como apoyo a otros lenguajes de alto nivel para 3 tipos de
situaciones:
- Operaciones que se repitan un número elevado de veces.
- Cuando se requiera una gran velocidad de proceso.
- Para utilización y aprovechamiento de dispositivos y recursos del sistema.

 **Entorno**
 
 
Los pasos habituales para hacer un programa (en cualquier lenguaje) son los
siguientes: lo primero es escribir el programa en el lenguaje fuente mediante un editor de programas. El resultado es un fichero en un lenguaje que puede entender el
usuario, pero no la máquina. Para traducirlo a lenguaje máquina hay que utilizar
un programa traductor. Éste genera un fichero con la traducción de dicho programa,
pero todavía no es un programa ejecutable. Un fichero ejecutable contiene el programa traducido más una serie de códigos que debe tener todo programa que vaya a ser
ejecutado en una máquina determinada. Entre estos códigos comunes se encuentran
las librerías del lenguaje. El encargado de unir el código del programa con el código
de estas librerías es un programa llamado montador (linker) que genera el programa
ejecutable.


[Imagen](https://fulldevelopersite.files.wordpress.com/2015/10/sin-tc3adtulo.png)

 **Caracteristicas**
 
 
La principal característica de un módulo fuente en ensamblador es que existe
una clara separación entre las instrucciones y los datos. La estructura más general
de un módulo fuente es:

- **Sección de datos.** Viene identificada por la directiva .data. En esta zona se
definen todas las variables que utiliza el programa con el objeto de reservar
memoria para contener los valores asignados. Hay que tener especial cuidado
para que los datos estén alineados en palabras de 4 bytes, sobre todo después
de las cadenas. Alinear significa rellenar con ceros el final de un dato para que
el siguiente dato comience en una dirección múltiplo de 4 (con los dos bits
menos significativos a cero). Los datos son modificables.

- **Sección de código.** Se indica con la directiva .text, y sólo puede contener código
o datos no modificables. Como todas las instrucciones son de 32 bits no hay
que tener especial cuidado en que estén alineadas. Si tratamos de escribir en
esta zona el ensamblador nos mostrará un mensaje de error.


De estas dos secciones la única que obligatoriamente debe existir es la sección
.text (o sección de código). 
Un módulo fuente, como el del ejemplo, está formado por instrucciones, datos,
símbolos y directivas. Las instrucciones son representaciones nemotécnicas del juego
de instrucciones del procesador. Un dato es una entidad que aporta un valor numérico, que puede expresarse en distintas bases o incluso a través de una cadena.
Los símbolos son representaciones abstractas que el ensamblador maneja en tiempo
de ensamblado pero que en el código binario resultante tendrá un valor numérico
concreto. Hay tres tipos de símbolos: las etiquetas, las macros y las constantes simbólicas. Por último tenemos las directivas, que sirven para indicarle ciertas cosas
al ensamblador, como delimitar secciones, insertar datos, crear macros, constantes
simbólicas, etc... Las instrucciones se aplican en tiempo de ejecución mientras que
las directivas se aplican en tiempo de ensamblado.


**Datos**


Los datos se pueden representar de distintas maneras. Para representar números
tenemos 4 bases. La más habitual es en su forma decimal, la cual no lleva ningún
delimitador especial. Luego tenemos otra muy útil que es la representación hexadecimal, que indicaremos con el prefijo 0x. Otra interesante es la binaria, que emplea
el prefijo 0b antes del número en binario. La cuarta y última base es la octal, que
usaremos en raras ocasiones y se especifica con el prefijo 0. Sí, un cero a la izquierda
de cualquier valor convierte en octal dicho número. Por ejemplo 015 equivale a 13 en
decimal. Todas estas bases pueden ir con un signo menos delante, codificando el valor
negativo en complemento a dos. Para representar carácteres y cadenas emplearemos
las comillas simples y las comillas dobles respectivamente.


**Símbolos**


Como las etiquetas se pueden ubicar tanto en la sección de datos como en la de
código, la versatilidad que nos dan las mismas es enorme. En la zona de datos, las
etiquetas pueden representar variables, constantes y cadenas. En la zona de código
podemos usar etiquetas de salto, funciones y punteros a zona de datos.
Las macros y las constantes simbólicas son símbolos cuyo ámbito pertenece al
preprocesador, a diferencia de las etiquetas que pertenecen al del ensamblador. Se
especifican con las directivas .macro y .equ respectivamente y permiten que el código
sea más legible y menos repetitivo.


**Instrucciones**

- Instrucciones de transferencia de datos Mueven información entre registros
y posiciones de memoria. En la arquitectura ARMv6 no existen puertos ya
que la E/S está mapeada en memoria. Pertenecen a este grupo las siguientes
instrucciones: mov, ldr, str, ldm, stm, push, pop.
- Instrucciones aritméticas. Realizan operaciones aritméticas sobre números binarios o BCD. Son instrucciones de este grupo add, cmp, adc, sbc, mul.
- Instrucciones de manejo de bits. Realizan operaciones de desplazamiento, rotación y lógicas sobre registros o posiciones de memoria. Están en este grupo
las instrucciones: and, tst, eor, orr, LSL, LSR, ASR, ROR, RRX.
- Instrucciones de transferencia de control. Se utilizan para controlar el flujo de
ejecución de las instrucciones del programa. Tales como b, bl, bx, blx y sus
variantes condicionales.

**Directivas**


Las directivas son expresiones que aparecen en el módulo fuente e indican al
compilador que realice determinadas tareas en el proceso de compilación. Son fácilmente distinguibles de las instrucciones porque siempre comienzan con un punto.
El uso de directivas es aplicable sólo al entorno del compilador, por tanto varían
de un compilador a otro y para diferentes versiones de un mismo compilador. Las
directivas más frecuentes en el as son:

- **Directivas de asignación:** Se utilizan para dar valores a las constantes o reservar
posiciones de memoria para las variables (con un posible valor inicial). .byte,
.hword, .word, .ascii, .asciz, .zero y .space son directivas que indican
al compilador que reserve memoria para las variables del tipo indicado.

- **Directivas de control:** .text y .data sirven para delimitar las distintas secciones de nuestro módulo. .align alineamiento es para alinear el siguiente dato,
rellenando con ceros, de tal forma que comience en una dirección múltiplos
del número que especifiquemos en alineamiento, normalmente potencia de 2.
Si no especificamos alineamiento por defecto toma el valor de 4 (alineamiento a palabra) .include para incluir un archivo fuente dentro del actual. .global hace visible
al enlazador el símbolo que hemos definido con la etiqueta del mismo nombre.

- **Directivas de operando:** Se aplican a los datos en tiempo de compilación. En
general, incluyen las operaciones lógicas &, |, ∼, aritméticas +, -, *, /, % y de
desplazamiento <, >, <<, >>.

- **Directivas de Macros:** Una .macro es un conjunto de sentencias en ensamblador
(directivas e instrucciones) que pueden aparecer varias veces repetidas en un programa con algunas modificaciones (opcionales). Por ejemplo, supongamos
que a lo largo de un programa realizamos varias veces la operación n
2+1 donde n y el resultado son registros.

* * *
### **CAPITULO 2**
* * *

### **Modos de direccionamiento del ARM**


En la arquitectura ARM los accesos a memoria se hacen mediante instrucciones
específicas ldr y str (luego veremos las variantes ldm, stm y las preprocesadas push y pop). El resto de instrucciones toman operandos desde registros o valores inmediatos, sin excepciones. En este caso la arquitectura nos fuerza a que trabajemos de
un modo determinado: primero cargamos los registros desde memoria, luego procesamos el valor de estos registros con el amplio abanico de instrucciones del ARM,
para finalmente volcar los resultados desde registros a memoria. Existen otras arquitecturas como la Intel x86, donde las instrucciones de procesado nos permiten
leer o escribir directamente de memoria. Ningún método es mejor que otro, todo
es cuestión de diseño. Normalmente se opta por direccionamiento a memoria en
instrucciones de procesado en arquitecturas con un número reducido de registros,
donde se emplea la memoria como almacén temporal. En nuestro caso disponemos
de suficientes registros, por lo que podemos hacer el procesamiento sin necesidad de
interactuar con la memoria, lo que por otro lado también es más rápido.

- **Direccionamiento inmediato.** El operando fuente es una constante, formando
parte de la instrucción.

- **Direccionamiento inmediato con desplazamiento o rotación.** Es una variante del anterior en la cual se permiten operaciones intermedias sobre los registros.

- **Direccionamiento a memoria, sin actualizar registro puntero.** Es la forma
más sencilla y admite 4 variantes. Después del acceso a memoria ningún registro implicado en el cálculo de la dirección se modifica.Simplemente añade (o sustrae) un valor inmediato al registro dado para
calcular la dirección. Es muy útil para acceder a elementos fijos de un
array, ya que el desplazamiento es constante.

- **Direccionamiento a memoria, actualizando registro puntero.** En este modo
de direccionamiento, el registro que genera la dirección se actualiza con la propia dirección. De esta forma podemos recorrer un array con un sólo registro
sin necesidad de hacer el incremento del puntero en una instrucción aparte.
Hay dos métodos de actualizar dicho registro, antes de ejecutar la instrucción
(preindexado) o después de la misma (postindexado).


**Tipos de Datos**


**Tipos de datos básicos.** En la siguiente tabla se recogen los diferentes tipos de datos básicos que podrán aparecer en los ejemplos, así como su
tamaño y rango de representación.


[Imagen](https://i1.wp.com/rduinostar.com/wp-content/uploads/2012/10/Tipos-de-Variables-Arduino.jpg)


**Punteros.** Un puntero siempre ocupa 32 bits y contiene una dirección de memoria.
En ensamblador no tienen tanta utilidad como en C, ya que disponemos de registros
de sobra y es más costoso acceder a las variables a través de los punteros que directamente. 

**Vectores.** Todos los elementos de un vector se almacenan en un único bloque de
memoria a partir de una dirección determinada. Los diferentes elementos se almacenan en posiciones consecutivas, de manera que el elemento i está entre los i-1 e
i+1.  Los vectores están definidos siempre a partir de la posición 0. El
propio índice indica cuántos elementos hemos de desplazarnos respecto del comienzo
del primer elemento (para acceder al elemento cero hemos de saltarnos 0 elementos,
para acceder al elemento 1 hemos de saltarnos un elemento, etc...; En general, para
acceder al elemento con índice i hemos de saltarnos los i elementos anteriores).

**Matrices bidimensionales.** Una matriz bidimensional de N×M elementos se almacena en un único bloque de memoria. Interpretaremos una matriz de N×M como
una matriz con N filas de M elementos cada una. Si cada elemento de la matriz
ocupa B bytes, la matriz ocupará un bloque de M ×N ×B bytes.


**Instrucciones de salto.** 


Las instrucciones de salto pueden producir saltos incondicionales (b y bx) o
saltos condicionales. Cuando saltamos a una etiqueta empleamos b, mientras que
si queremos saltar a un registro lo hacemos con bx. La variante de registro bx la
solemos usar como instrucción de retorno de subrutina, raramente tiene otros usos.
En los saltos condicionales añadimos dos o tres letras a la (b/bx), mediante las
cuales condicionamos si se salta o no dependiendo del estado de los flags. Estas
condiciones se pueden añadir a cualquier otra instrucción, aunque la mayoría de las
veces lo que nos interesa es controlar el flujo del programa y así ejecutar o no un
grupo de instrucciones dependiendo del resultado de una operación (reflejado en los flags).
Las instrucciones de salto en la arquitectura ARM abarcan una zona muy extensa, hasta 64 Mb (32 Mb hacia adelante y otros 32 Mb hacia atrás). Estos límites
podemos justificarlos atendiendo al formato de instrucción que podemos ver en el
apéndice A. El código de operación ocupa 8 de los 32 bits, dejándonos 24 bits para
codificar el destino del salto.


**Estructuras de control de alto nivel**


En este punto veremos cómo se traducen a ensamblador las estructuras de control
de alto nivel que definen un bucle (for, while, . . . ), así como las condicionales
(if-else).
Las estructuras for y while se pueden ejecutar un mínimo de 0 iteraciones (si
la primera vez no se cumple la condición). La traducción de las estructuras for y
while se puede ver en los listados **2.1 y 2.2.**
Para programar en ensamblador estas estructuras se utilizan instrucciones de
salto condicional. Previo a la instrucción de salto es necesario evaluar la condición
del bucle o de la sentencia if, mediante instrucciones aritméticas o lógicas, con el
fin de actualizar los flags de estado. 


**Compilación a ensamblador** 


Para acabar la teoría veamos cómo trabaja un compilador de C real. Normalmente los compiladores crean código compilado (archivos .o) en un único paso. En
el caso de gcc este proceso se hace en dos fases: en una primera se pasa de C a
ensamblador, y en una segunda de ensambladador a código compilado (código máquina). Lo interesante es que podemos interrumpir justo después de la compilación
y ver con un editor el aspecto que tiene el código ensamblador generado a partir del
código fuente en C.


* * *





