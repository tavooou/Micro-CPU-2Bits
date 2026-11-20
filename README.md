# Micro-CPU-2Bits

Universidad Panamericana (UPANA) 
Curso: Arquitectura del Computador I  
Catedrático: Ing. Josué Morataya  
* **[Katlin María González López]** – ID: `[000161273]`
* **[Gustavo Ernesto Torres González]** – ID: `[000157551]`


El sistema simula de forma visual e interactiva:
1. El Ciclo de Instrucción: Secuencia de etapas (Fetch, Decode, Execute, Write-Back) mediante LEDs indicadores.
2. Banderas de Estado (Flags): Detección automática de resultados nulos (Zero), negativos (Negative) y desbordamiento de rango (Overflow).
3. Calculadora Aritmética de 2 Bits: Operaciones de suma (+) y resta (-) con operandos enteros en el rango de 0 a 3.


## Instrucciones de Uso
1. Conecta la placa RP2040 Zero a la computadora mediante el cable USB-C. (Si es la primera vez, hay que mantener presionado el botón BOOT al conectarla para instalar el firmware de MicroPython).
2. Abrir el entorno de desarrollo Thonny IDE.   
3. En la esquina inferior derecha, selecciona el intérprete MicroPython (Raspberry Pi Pico) y el puerto COM correspondiente.
4. Abre el archivo CODE/main.py en Thonny.
5. Guarda el archivo directamente en la placa (Archivo luego, Guardar como... y el dispositivo MicroPython) con el nombre main.py para que ejecute automáticamente al energizar el circuito.


## Operación de la Calculadora
El sistema funciona mediante una máquina de estados secuencial:   
1. Primer Operando (INPUT 1): Presionar un botón numérico del 0 al 3. Se encenderá brevemente el LED azul FETCH y el dígito aparecerá en el display de 7 segmentos.
2. Operación (OPERATION): Presiona el botón + (suma) o - (resta). Se iluminará el LED verde DECODE.
3. Segundo Operando (INPUT 2): Presiona el segundo dígito del 0 al 3. Se encenderá nuevamente el LED FETCH y se mostrará el segundo número en el display.
4. Cálculo y Resultado (CALCULATE): Presiona el botón =:
   - Fase Execute: Se enciende el LED amarillo EXECUTE durante 2 segundos mientras la ALU evalúa la operación y actualiza las banderas (Zero, Negative u Overflow en el LED RGB integrado).
   - Fase Write-Back: Se enciende el LED rojo WRITE-BACK durante 2 segundos y se escribe el resultado en el display (si ocurre Overflow, el display permanece apagado).
6. Reinicio: Presionar de nuevo el botón = para limpiar el display, apagar las banderas y comenzar una nueva operación.


## Notas Técnicas y Adaptaciones del Proyecto

Respecto al diseño base de referencia, se realizaron los siguientes ajustes de hardware y software para asegurar el funcionamiento óptimo con los componentes ensamblados:

Modificaciones de Hardware
- Display de Ánodo Común: Se implementó un display de 7 segmentos de Ánodo Común conectando su pin COM directamente a la salida de 3V3 de la RP2040 Zero.
- Resistencia de Protección: Se añadió una resistencia de 220 Ohm conectada entre GND y el pin del segmento D del display.


Cambios en el Código (CODE/main.py)
1. Soporte para Ánodo Común (DISPLAY_ANODO_COMUN = True): Se agregó esta bandera de configuración para adaptar el controlador al tipo de display físico utilizado.
2. Inversión de Lógica de Segmentos (display_digit()): Dado que en un display de Ánodo Común los LEDs cierran circuito a tierra, se invirtió la salida digital (0 lógico para encender el segmento y 1 lógico para apagarlo).
3. Estado Inicial Apagado (SEGMENTO_APAGADO): Se inicializaron los pines GPIO13–GPIO15 y GPIO26–GPIO29 en estado alto (value=1) desde el arranque para evitar que los segmentos inicien encendidos al energizar la placa.
4. Calibración del LED de Overflow (COLOR_OVERFLOW = (60, 0, 0)): Se corrigió la tupla RGB del NeoPixel integrado (GPIO16), sustituyendo (0, 255, 0) por (60, 0, 0) para que la bandera de desbordamiento se ilumine efectivamente en color rojo y con intensidad adecuada.
