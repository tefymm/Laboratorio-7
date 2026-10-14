
# Laboratorio ADC y DMA

**Universidad del Valle de Guatemala**  
**BE3029 - Electrónica Digital 2**  
**Nombre:** Stephany Mejía  
**Microcontrolador:** NUCLEO-F446RE

## 1. Descripción

En este laboratorio se implementó el módulo ADC del STM32 para realizar lecturas analógicas de tres potenciómetros. Se utilizó una resolución de 12 bits y el módulo DMA para almacenar los datos automáticamente en memoria. Además, se configuró la comunicación UART para visualizar las lecturas mediante una terminal serial WCH.

Para el Post Lab se desarrolló un sistema de monitoreo de variables biológicas simuladas, en el cual se utilizaron tres LEDs como indicadores de alerta.

## 2. Materiales

- STM32 NUCLEO-F446RE
- 3 potenciómetros
- 3 LEDs (verde, rojo y amarillo)
- 3 resistencias de 220 Ω
- Protoboard y cables jumper

## 3. Conexiones

| Componente | Pin STM32 |
|---|---|
| POT 1 | PA0 - ADC1_IN0 |
| POT 2 | PA1 - ADC1_IN1 |
| POT 3 | PA4 - ADC1_IN4 |
| LED verde | PA5 |
| LED rojo | PA6 |
| LED amarillo | PA7 |

## 4. Configuración

Se realizaron las siguientes configuraciones en STM32CubeMX:

- ADC1 con resolución de 12 bits y tres canales.
- Tiempo de muestreo de 84 ciclos.
- DMA2 Stream 0 en modo circular.
- USART2 con velocidad de 115200 baudios.
- Tres salidas GPIO para controlar los LEDs.

## 5. Desarrollo

### Parte 1. Lectura ADC

Se realizó la lectura del primer potenciómetro mediante el ADC1. Los valores digitales obtenidos variaron dentro del rango de 0 a 4095, correspondiente a una resolución de 12 bits. También se implementó el cálculo del voltaje de entrada.

### Parte 2. ADC con DMA

Se configuró una secuencia de tres canales ADC y se utilizó DMA para almacenar continuamente las lecturas en un arreglo, sin necesidad de consultar individualmente cada conversión.

### Parte 3. Comunicación UART

Se implementó la comunicación USART2 para transmitir las lecturas de los tres potenciómetros a una terminal serial WCH, donde se visualizaron los valores obtenidos.

### Parte 4. Rangos y alarmas

Se desarrolló una simulación de monitoreo de tres variables biológicas. Cada potenciómetro representó una variable y se establecieron rangos para identificar condiciones de alerta.

| Variable simulada | Rango normal establecido | LED |
|---|---|---|
| Temperatura corporal | 36–37.5 °C | Verde |
| Frecuencia cardíaca | 60–100 bpm | Rojo |
| Glucosa sanguínea | 70–140 mg/dL | Amarillo |

Se implementaron condiciones que permitieron activar el LED correspondiente cuando una variable se encontraba fuera del rango establecido. Al regresar al rango normal, el LED se apagaba automáticamente.

Los rangos fueron utilizados únicamente con fines de simulación académica.
