# 2.1. Lectura y ejercicios de ARM32 del ebook OpenSource
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
 
##### **Registros**
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


