
# Laboratorio ADC y DMA

**Universidad del Valle de Guatemala**  
**BE3029 - Electrónica Digital 2**  
**Nombre:** Stephany Mejía  
**Microcontrolador:** NUCLEO-F446RE

## Descripción

En este laboratorio utilizamos el ADC de 12 bits para leer tres potenciómetros, DMA para guardar las lecturas automáticamente y UART para mostrar los valores en una terminal serial WCH.

Para el Post Lab simulamos tres variables biológicas y utilizamos LEDs para indicar cuando alguna se encuentra fuera de su rango normal.

## Materiales
- NUCLEO-F446RE
- 3 potenciómetros
- 3 LEDs y resistencias de 220 Ω
- Protoboard y jumpers

## Conexiones

| Componente | Pin |
|---|---|
| POT 1 | PA0 - ADC1_IN0 |
| POT 2 | PA1 - ADC1_IN1 |
| POT 3 | PA4 - ADC1_IN4 |
| LED verde | PA5 |
| LED rojo | PA6 |
| LED amarillo | PA7 |

## Configuración

- ADC1: 12 bits, 3 canales, 84 ciclos de muestreo.
- DMA2 Stream 0: Peripheral to Memory, modo Circular.
- USART2: 115200 baudios.
- LEDs: GPIO_Output.

## Desarrollo

### Parte 1 - Lectura ADC
Leímos el primer potenciómetro y mostramos su valor de 0 a 4095, además de calcular su voltaje.

### Parte 2 - ADC con DMA
Utilizamos DMA para almacenar continuamente las lecturas de los tres potenciómetros en un arreglo.

```c
volatile uint16_t adcValores[3] = {0};
HAL_ADC_Start_DMA(&hadc1, (uint32_t*)adcValores, 3);
```

### Parte 3 - Comunicación UART
Enviamos las tres lecturas a WCH mediante USART2, utilizando `HAL_UART_Transmit()`.

### Parte 4 - Rangos y alarmas

Simulamos tres variables biológicas:

| Variable | Rango normal simulado | LED |
|---|---|---|
| Temperatura | 36–37.5 °C | Verde |
| Frecuencia cardíaca | 60–100 bpm | Rojo |
| Glucosa | 70–140 mg/dL | Amarillo |

Cuando una variable sale de su rango, se enciende su LED correspondiente. Cuando vuelve al rango normal, el LED se apaga.

Los valores biológicos son simulados mediante potenciómetros.

## Conclusión

Aprendimos a utilizar ADC para convertir señales analógicas a digitales, DMA para almacenar las lecturas sin consultar cada conversión y UART para enviar los resultados. También implementamos alarmas mediante LEDs, relacionando el laboratorio con una aplicación de ingeniería biomédica.
