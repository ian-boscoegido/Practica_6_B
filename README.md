# Práctica 6B - Escritura y Lectura RFID con ESP32-S3 y RC522

## Descripción

Práctica de escritura y lectura RFID mediante SPI con ESP32-S3 y RC522, almacenando un mensaje en una tarjeta MIFARE y verificando su contenido desde el monitor serie.

## Objetivo

El objetivo de esta práctica es utilizar el bus SPI del ESP32-S3 para comunicarse con un módulo RFID RC522 y realizar una operación completa de escritura y lectura sobre una tarjeta RFID compatible.

El programa escribe un mensaje en un bloque de memoria de una tarjeta MIFARE Classic y posteriormente lee ese mismo bloque para comprobar que la escritura se ha realizado correctamente.

## Material utilizado

- ESP32-S3
- Módulo RFID RC522
- Tarjeta o llavero RFID compatible con MIFARE Classic
- Cables Dupont
- Cable USB
- Visual Studio Code
- PlatformIO
- Framework Arduino

## Conexiones

| RC522 | ESP32-S3 |
|------|----------|
| SDA / SS | GPIO 10 |
| SCK | GPIO 12 |
| MOSI | GPIO 11 |
| MISO | GPIO 13 |
| RST | GPIO 9 |
| 3.3V | 3.3V |
| GND | GND |

Importante: el módulo RC522 debe alimentarse a 3.3V. No se recomienda conectarlo a 5V.

## Librerías utilizadas

- Arduino.h
- SPI.h
- MFRC522.h

## Funcionamiento

Al iniciar el programa, el ESP32-S3 configura el monitor serie, inicializa el bus SPI y comprueba que el módulo RFID RC522 responde correctamente.

Cuando se acerca una tarjeta RFID al lector, el programa realiza los siguientes pasos:

1. Detecta la tarjeta RFID.
2. Muestra el UID de la tarjeta.
3. Identifica el tipo de tarjeta.
4. Autentica el bloque de memoria seleccionado.
5. Escribe un mensaje en el bloque 4.
6. Lee de nuevo el mismo bloque.
7. Muestra el mensaje leído por el monitor serie.
8. Finaliza la comunicación con la tarjeta.

## Mensaje escrito

El mensaje que se escribe en la tarjeta es:

VIVA ESPANYA

Este mensaje se guarda en un bloque de 16 bytes.

## Bloque de memoria utilizado

El programa utiliza el bloque 4 de la tarjeta RFID:

BLOCK_ADDR = 4

Este bloque pertenece al sector 1 de una tarjeta MIFARE Classic.

Importante: no se deben utilizar bloques trailer como 3, 7, 11, 15, etc., ya que contienen información de control y claves de acceso.

## Clave utilizada

Para autenticar el bloque se utiliza la clave por defecto de muchas tarjetas MIFARE Classic:

FF FF FF FF FF FF

## Configuración de pines

SS_PIN = GPIO 10  
SCK_PIN = GPIO 12  
MOSI_PIN = GPIO 11  
MISO_PIN = GPIO 13  
RST_PIN = GPIO 9  

## Velocidad del monitor serie

SERIAL_BAUD = 115200

El monitor serie debe abrirse a 115200 baudios.

## Comandos de PlatformIO

Compilar el proyecto:

pio run

Subir el programa a la placa:

pio run --target upload

Abrir el monitor serie:

pio device monitor

## Ejemplo de salida

======================================  
 EJERCICIO 2 - ESCRIBIR Y LEER RFID  
 ESP32-S3 + RC522 + SPI  
======================================  

[OK] SPI inicializado  
[OK] RC522 inicializado  
Version RC522: 0x92  

Acerca una tarjeta RFID para escribir el mensaje...

======================================  
 TARJETA DETECTADA  
======================================  

UID detectado: 04 A1 B2 C3 D4  
Tipo de tarjeta: MIFARE 1KB  
Bloque usado para escritura/lectura: 4  
[OK] Autenticacion correcta  
[OK] Mensaje escrito correctamente  
[OK] Mensaje leido correctamente  
Mensaje guardado: VIVA ESPANYA  
Datos en HEX: 56 49 56 41 20 45 53 50 41 4E 59 41 20 20 20 20  

======================================  
 FIN DE OPERACION  
Retira la tarjeta y vuelve a acercarla si quieres repetir.  
======================================  

## Resultado

La práctica permite comprobar correctamente la comunicación SPI entre el ESP32-S3 y el módulo RFID RC522. Además, demuestra el uso de autenticación, escritura y lectura de bloques de memoria en una tarjeta RFID MIFARE Classic.

## Conclusión

Con esta práctica se ha aprendido a utilizar un lector RFID RC522 mediante comunicación SPI, a detectar tarjetas RFID, autenticar bloques de memoria, escribir información en una tarjeta y comprobar posteriormente que los datos han sido almacenados correctamente.
