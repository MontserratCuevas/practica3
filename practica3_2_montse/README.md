# Práctica 3 parte 2

## Código:

```c++
    #include <Arduino.h>

    //This example code is in the Public Domain (or CC0 licensed, at your option.)
    //By Evandro Copercini - 2018
    //
    //This example creates a bridge between Serial and Classical Bluetooth (SPP)
    //and also demonstrate that SerialBT have the same functionalities of a normal Serial

    #include "BluetoothSerial.h"

    #if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
    #error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
    #endif

    BluetoothSerial SerialBT;

    void setup() {
        Serial.begin(115200);
        SerialBT.begin("ESP32test"); //Bluetooth device name
        Serial.println("The device started, now you can pair it with bluetooth!");
    }

    void loop() {
        if (Serial.available()) {
         SerialBT.write(Serial.read());
    }
    if (SerialBT.available()) {
        Serial.write(SerialBT.read());
    }
    delay(20);
    }
```
En este código se ha incluido una biblioteca nueva para proporcionar la comunicación Bluetooth en el ESP32.

Luego verifica antes de compilar si el Bluetooth está habilitado en la configuración del ESP32 y si no lo está muestra un mensaje de error.

En la función **setup()** se iniciañoza la comunicación serie a una velocidad de 115200 baudios y luego se inicia la comunicación Bluetooth con el nombre del dispositivo ESP32test, a través del objeto, que ha sido creado con anterioridad, SerialBT. Después se imprime un mensaje en el puerto serie que indica que el dispositivo se ha iniciado y que puede emparejarse con Bluetooth.

En la función **loop()** se verifica si hay datos  disponibles en el puerto serie y si los hay los lee y los envía a través de Bluetooth utilizando la Serial.write(), Finalmente, se intreduce un retraso de 20 milisegundos antes de repetir las mismas acciones una y otra vez. Este bucle perimtie la comunicación bidireccional entre el dispositivo conectado a Bluetooth y el puerto serie.

## Conclusión

En conclusión, este código crea una comunicación Bluetooth, lo que significa que podrás escribir en el dispositivo que tengas emparejado y lo que escribas saldra por mensaje en el puerto serie y viceversa.
