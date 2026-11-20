## Asignación de Pines - Micro-CPU 2Bits:

Se detalla las conexiones físicas exactas entre la placa de desarrollo RP2040 Zero y los periféricos del sistema, correspondiendo al código implementado en CODE/main.py y al diagrama en HARDWARE/Diagrama_Circuito.png.

1. Alimentación y Referencias Comunes

| Pin en RP2040 Zero | Destino / Conexión | Descripción |
| :--- | :--- | :--- |
| 3V3 | Pin COM del Display 7 Segmentos | Alimentación positiva común (configuración de Ánodo Común). |
| GND | Riel negativo de Protoboard | Tierra común para botones, cátodos de LEDs (vía resistencias) y resistencia pull-down en segmento D. |

2. Entradas: Botones Pulsadores

Todos los pines de entrada están configurados en MicroPython con resistencia PULL_UP interna (machine.Pin.PULL_UP). Al presionar un botón, el pin se conecta a GND (estado lógico 0).

| Pin GPIO | Componente | Función en el Sistema |
| :--- | :--- | :--- |
| GPIO0 | Botón Pulsador 0 | Ingreso del operando numérico 0 (00 en binario). |
| GPIO1 | Botón Pulsador 1 | Ingreso del operando numérico 1 (01 en binario). |
| GPIO2 | Botón Pulsador 2 | Ingreso del operando numérico 2 (10 en binario). |
| GPIO3 | Botón Pulsador 3 | Ingreso del operando numérico 3 (11 en binario). |
| GPIO4 | Botón Pulsador + | Selección de operación: Suma. |
| GPIO5 | Botón Pulsador - | Selección de operación: Resta. |
| GPIO6 | Botón Pulsador = | Ejecución de cálculo / Reinicio del sistema tras mostrar resultado. |

3. Salidas: Ciclo de Instrucción y Banderas de Estado (LEDs)

Cada LED monocromático externo está conectado en serie con una resistencia limitadora de 220 Ohm hacia GND.

| Pin GPIO | Componente | Categoría | Descripción |
| :--- | :--- | :--- | :--- |
| GPIO7 | LED Indicador | Ciclo de Instrucción | FETCH: Se enciende al capturar cada operando numérico. |
| GPIO8 | LED Indicador | Ciclo de Instrucción | DECODE: Se enciende al interpretar la operación (+ o -). |
| GPIO9 | LED Indicador | Ciclo de Instrucción | EXECUTE: Se enciende durante el procesamiento en la ALU. |
| GPIO10 | LED Indicador | Ciclo de Instrucción | WRITE-BACK: Se enciende al escribir el resultado en el display. |
| GPIO11 | LED Indicador | Bandera (Flag) | ZERO: Se activa si el resultado de la operación es igual a 0. |
| GPIO12 | LED Indicador | Bandera (Flag) | NEGATIVE: Se activa si el resultado es menor a 0. |
| GPIO16 | LED NeoPixel RGB | Bandera (Flag) | OVERFLOW: LED integrado en la placa; enciende en color rojo si el resultado excede el rango de 2 bits (<0 o >3). |

4. Salidas: Display de 7 Segmentos (Ánodo Común)

Debido a que el display utilizado es de Ánodo Común (COM conectado a 3V3), la lógica de control en main.py (DISPLAY_ANODO_COMUN = True) es invertida:
- 0 lógico (LOW): Enciende el segmento.
- 1 lógico (HIGH): Apaga el segmento.

| Pin GPIO | Pin del Display | Notas de Conexión |
| :--- | :--- | :--- |
| GPIO13 | Segmento A | Conexión directa. |
| GPIO14 | Segmento B | Conexión directa. |
| GPIO15 | Segmento C | Conexión directa. |
| GPIO26 | Segmento D | Cuenta con una resistencia de 220 Ohm conectada entre el segmento D y GND. |
| GPIO27 | Segmento E | Conexión directa. |
| GPIO28 | Segmento F | Conexión directa. |
| GPIO29 | Segmento G | Conexión directa. |
