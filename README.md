# PRACTICA-N-3_-ESP32-DHT11-LCD
Este repositorio muestra la tercera practica practica del diplomado de como podemos programar una ESP32 con el sensor DHT22 y mostrando el resutado en la LCD.

## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```DTH22```) para obtener temperatura y humedad, ademas agrgaremos un (```LCD 16X2 I2C```) para mostrar los resultados en la pantalla lcd; Esta practica se usara un simulador llamado [WOKWI](https://wokwi.com/).


## Material Necesario

A continuacion se utilizaron los siguientes materiales.

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor DHT22
- LCD 16X2 I2C



## Instrucciones

### Requisitos previos

Para realizar la practica de este repositorio se necesita entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente codigo:

```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");

  delay(1000);
}
```


2. Instalar la libreria de **Cristal líquido I2C**. 
   - Seleccionar pestaña de Librery Manager --> Add a New library --> Colocamos el nombre de libreria 

![](https://github.com/YasminZagal/PRACTICA-N-3_-ESP32-DHT11-LCD/blob/main/libreria.jpg)


3. Realizar la conexion de **DHT22** con la **ESP32** y de la **LCD** de la siguiente manera.

![](https://github.com/YasminZagal/PRACTICA-N-3_-ESP32-DHT11-LCD/blob/main/conexion%20lcd.jpg)

**Conexion lcd**
-GND
-VCC
-SDA --> esp:21
-SCL --> esp:22

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial y en la lcd .
3. Colocar la temperatura y humedad dando *doble click* al sensor **DHT22** 

## Resultados

Una vez terminado iniciamos simulacion y se observaran los valores en la lcd.

![](https://github.com/YasminZagal/PRACTICA-N-3_-ESP32-DHT11-LCD/blob/main/resultado%20practica%203.jpg)
