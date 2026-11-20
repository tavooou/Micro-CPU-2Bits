## Listado de Componentes:

Materiales y especificaciones técnicas del hardware utilizado para el ensamblaje físico de la Micro-CPU de 2 Bits.


1. (1) Placa de Desarrollo: RP2040 Zero, microcontrolador dual-core ARM Cortex-M0+, soporte para MicroPython, pines GPIO a 3.3V y LED RGB NeoPixel integrado en el GPIO16.
2. (1) Protoboard: De 2 galletas, placa de pruebas sin soldadura con rieles de alimentación divididos para montaje de componentes.
3. (7) Botones Pulsadores: Push Button táctil (2/4 pines), interruptores normalmente abiertos (NO) utilizados para entrada de datos (0, 1, 2, 3) y control (+, -, =). 4. (6) LEDs Monocromáticos: Diodos emisores de luz 5mm, indicadores visuales de estado: 4 para las fases del ciclo de instrucción (Fetch, Decode, Execute, Write-Back) y 2 para banderas (Zero, Negative).
5. (7) Resistencias: (1/4 W), valor de 220 Ohm, 6 utilizadas como limitadoras de corriente para los LEDs y 1 conectada entre GND y el segmento D del display.
6.  (1) Display de 7 Segmentos: 1 Dígito - Ánodo Común, LED de 7 segmentos y pin común (COM) conectado a 3V3 y activación de segmentos por nivel bajo (0).
7.  (1) Set de Cables: Cable UTP / Rígido para protoboard: cable para interconexiones limpias sobre la protoboard.
8. (5) Cables Jumper: Hembra - Macho, DuPont para conectar pines superiores/expuestos hacia la protoboard.
9. (1) Cable: USB Tipo-A a USB Tipo-C, utilizado para la alimentación de la placa y programar el firmware mediante el IDE Thonny.


### Notas
* **Adaptación a Ánodo Común:** A diferencia de un display de cátodo común tradicional, el componente utilizado comparte el terminal positivo (`3V3`). Esta característica fue contemplada tanto en el cableado físico como en la bandera `DISPLAY_ANODO_COMUN = True` dentro del código fuente (`CODE/main.py`).

