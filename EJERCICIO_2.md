¡Me alegra que te haya gustado\! Para un examen, un ejercicio más difícil debe combinar los conceptos de **riesgos (hazards)**, **detenciones (*stalls*)** y **cálculo de rendimiento** en un solo problema.

El siguiente ejercicio requiere analizar un fragmento de código específico y luego cuantificar su impacto en el rendimiento.

-----

## Ejercicio Avanzado: Riesgos, Stalls y CPI Promedio en el Pipeline MIPS

Considere el pipeline MIPS de 5 etapas estándar (IF, ID, EX, MEM, WB) con las siguientes características:

1.  **Forwarding (Anticipación):** Se implementa *forwarding* completo desde la salida de la etapa **EX** y **MEM** a la entrada de la etapa **EX** para resolver la mayoría de los riesgos de datos.
2.  **Load-Use Hazard:** El riesgo de uso después de una carga (`lw`) siempre requiere **un ciclo de *stall***.
3.  **Branch Hazard (Riesgo de Salto):** La unidad de control determina si un salto se toma o no durante la etapa **ID**. Esto causa una **penalización de 1 ciclo de *stall*** (una burbuja) para todos los saltos (`beq`, `bne`, etc.) que se inserta después de la etapa IF de la instrucción siguiente.

Analice la ejecución del siguiente ciclo de bucle MIPS (que suma elementos de un arreglo y almacena el resultado final):

```assembly
      li $t0, 100    # (I1) Carga la cuenta (N=100)
      li $t1, 0      # (I2) $t1 = 0 (Suma total)
      li $t2, 0x1000 # (I3) Dirección inicial del arreglo
Loop: lw $t3, 0($t2)   # (I4) Carga el elemento: $t3 = Mem[ $t2 ]
      add $t1, $t1, $t3  # (I5) Suma: $t1 = $t1 + $t3
      addi $t2, $t2, 4   # (I6) Avanza al siguiente elemento: $t2 = $t2 + 4
      addi $t0, $t0, -1  # (I7) Decrementa el contador: $t0 = $t0 - 1
      bne $t0, $zero, Loop # (I8) Salta si $t0 != 0
```

-----

### Preguntas

1.  **Análisis de Riesgos y Detenciones (Ciclo Interno):**

      * Para la secuencia de instrucciones **dentro del bucle (I4 a I8)**, identifique todos los **riesgos de datos**.
      * Para cada riesgo, determine si se resuelve con *forwarding* o si requiere una detención (*stall*). Especifique el número de *stalls* para cada iteración del bucle.

2.  **Cálculo del CPI por Iteración:**

      * Asumiendo que las instrucciones del bucle (I4 a I8) tardarían **5 ciclos de reloj** en un pipeline ideal (5 instrucciones / 1 instrucción por ciclo), calcule el **número total de ciclos de reloj** que tarda una sola iteración completa del bucle, incluyendo todos los *stalls* por datos y el *branch hazard*.
      * Calcule el **CPI (Ciclos Por Instrucción)** promedio para el código dentro del bucle.
        $$\text{CPI por iteración} = \frac{\text{Ciclos totales de reloj}}{\text{Número de instrucciones ejecutadas}}$$

3.  **Tiempo de Ejecución Total:**

      * Asumiendo que el tiempo de ciclo de reloj ($T_{clk}$) es de **2 ns** y el bucle se ejecuta $N=100$ veces.
      * Calcule el **tiempo total de ejecución** de todo el código (I1 a I8 repetido 100 veces).

-----

### Razonamiento (Solución)

Este ejercicio es más difícil porque:

  * Combina riesgos de datos y riesgos de control (salto).
  * Incluye el caso crítico del **Load-Use Hazard** (`lw` I4 y `add` I5).
  * Requiere calcular una métrica de rendimiento (*CPI* y *tiempo total*) que depende de un análisis de bajo nivel del pipeline.

| Pista para la solución: El número total de ciclos por iteración será $5$ (instrucciones) $+ (\text{stalls de datos}) + (\text{stalls de salto})$. |
| :---: |
