# ProyectoModulo3-Lenguaje-De-Interfaz

Contador de Bits (Opción A)

Descripción del proyecto

Programa en C que compara el rendimiento de una función que cuenta los bits en 1 de un número de 64 bits (population count), implementada de dos formas:

C puro: revisa el número bit por bit con un ciclo while (n & 1, n >>= 1).
Ensamblador inline (asm volatile, sintaxis AT&T de GCC): se incluyen tres versiones que se eligen al compilar

Método
1 — SHR + ADC: Traducción directa del ciclo de C. SHR manda el bit menos significativo a la bandera CF y ADC $0 lo suma al contador.
Todo vive en registros y ADC suma el bit sin la operación AND aparte.

2 — Kernighan: n & (n-1) apaga el bit en 1 más bajo, así el ciclo da solo tantas vueltas como bits en 1 haya (~32 en vez de ~64).
Reduce el número de vueltas a la cantidad de bits en 1.

3 — POPCNT:	Una sola instrucción de hardware cuenta los 64 bits. El XOR previo rompe una dependencia falsa que tiene POPCNT en varios CPU Intel.
Elimina el ciclo por completo; el CPU cuenta los 64 bits en una instrucción de ~1 ciclo de reloj.

El programa genera 100 millones de números aleatorios, mide el tiempo de cada versión con clock(), verifica que ambos totales coincidan y muestra la mejora.

Instrucciones de compilación
Metodo 3 (POPCNT) - version principal
gcc -O0 -o acelerador main.c
acelerador.exe

Metodo 1 (SHR +ADC=
gcc -O0 -DMETODO=1 -o acelerador main.c
acelerador2.exe

Metodo 2 (Kernigham)
gcc -O0 -DMETODO=2 -o acelerador main.c
acelerador3.exe

<img width="592" height="175" alt="image" src="https://github.com/user-attachments/assets/7a228157-2c69-4d50-8522-bf3599d9d2db" />

Resultados:

<img width="912" height="522" alt="image" src="https://github.com/user-attachments/assets/3e4be968-61d0-424e-aa78-8feca5bcac7a" />

