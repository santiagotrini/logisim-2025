¡Claro! Un excelente ejercicio de un tipo diferente, que se centra en el **impacto del *pipelining*** en el rendimiento y la comparación con la ejecución secuencial, es el cálculo de la **aceleración (*speedup*)** y el **tiempo de ejecución** usando el concepto de **Tiempo de Ciclo del Reloj (Clock Cycle Time)**.

Este ejercicio te obliga a pensar en el tiempo total, no solo en los *stalls*.

---
## Ejercicio: Cálculo de Rendimiento y Aceleración del Pipeline MIPS

Considere el pipeline MIPS de 5 etapas (IF, ID, EX, MEM, WB) y un procesador sin pipeline (secuencial o de etapa única).

Suponga los siguientes tiempos de ejecución para cada etapa:

| Etapa | Descripción | Tiempo (nanosegundos, ns) |
| :---: | :---: | :---: |
| IF | Búsqueda de Instrucción | 10 ns |
| ID | Decodificación/Lectura de Registros | 12 ns |
| EX | Ejecución/Cálculo de Dirección | 15 ns |
| MEM | Acceso a Memoria de Datos | 20 ns |
| WB | Escritura en Registros | 8 ns |

### Procesador Secuencial (Sin Pipeline)

1.  **Tiempo de Instrucción Secuencial ($T_{sec}$):** Calcule el tiempo total que tarda en ejecutarse una sola instrucción en el procesador secuencial. (Sugerencia: el tiempo de ejecución de una instrucción es la suma de los tiempos de todas las etapas).

### Procesador Pipelined (Con Pipeline)

1.  **Tiempo de Ciclo de Reloj ($T_{clk}$):** En un pipeline, el tiempo de ciclo del reloj es determinado por la etapa más lenta (el **cuello de botella**). Calcule el tiempo mínimo de ciclo de reloj (incluyendo un margen de 1 ns para los registros del pipeline).
    $$T_{clk} = (\text{Tiempo de la etapa más lenta}) + 1 \text{ ns}$$
2.  **Tiempo Total de Ejecución:** Calcule el tiempo total ($T_{pipe}$) que tomaría ejecutar una secuencia de $\mathbf{N = 100}$ instrucciones:
    $$T_{pipe} = (\text{Latencia de la primera instrucción}) + ((N - 1) \times T_{clk})$$
    (Asuma que no hay riesgos ni *stalls* para simplificar el cálculo inicial).

### Aceleración (*Speedup*)

1.  **Cálculo de Aceleración ($S$):** Determine la aceleración obtenida al usar el pipeline con 100 instrucciones, en comparación con el procesador secuencial.
    $$S = \frac{\text{Tiempo de ejecución sin pipeline}}{\text{Tiempo de ejecución con pipeline}}$$

### Impacto de los Riesgos

1.  **Penalización por *Stall*:** Si en la secuencia de 100 instrucciones se produce un promedio de $\mathbf{0.2}$ ciclos de *stall* por cada instrucción (debido a riesgos como el *load-use hazard* o *branch hazards*):
    * Calcule el **número total de ciclos de *stall***.
    * Calcule el **nuevo tiempo total de ejecución ($T_{pipe\_con\_stall}$)**.
    * Calcule la **aceleración real ($S_{real}$)**, comparando el tiempo secuencial con el nuevo tiempo con *stalls*.

---
Este ejercicio es fundamental para entender la métrica clave de rendimiento en arquitectura de computadores: la **aceleración** ($S$) y cómo el **ciclo de reloj** ($T_{clk}$) y los **riesgos** (*stalls*) impactan directamente en el rendimiento final.
