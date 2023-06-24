# Practica ultrasonico y DHT22 
En este repositorio muestra como podemos programar una ESP32 con sensores de distancia (HC-SR04 Ultrasonic Distance Sensor), de humedad y temperatura (DHT22) y se muestren en un lcd 16x2 (I2C) .

## Introducción

### Descripción
La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```HC-SR04 Ultrasonic Distance Sensor```) para adquirir la distancia y el sensor ```DHT22``` para adquirir temperatura y Humedad del medio ambiente; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/)
.

## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/) como simulador.
- Tarjeta ```ESP 32```.
- Sensor ```HC-SR04 Ultrasonic Distance Sensor```.
- Sensor ```DHT22```
- LCD 16x2 (I2C)


## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Entramos al simulador [WOKWI](https://https://wokwi.com/) y selecionamos la tarjeta ```ESP 32``` como se muestra en la siguiente imagen.

![](https://github.com/jorgelopezquiroz/Ultrasonic_dht22/blob/main/ESP32.png?raw=true)


2. Posteriormente se abrirá la terminal de programación y se coloca la siguente programación:

```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;
const int Trigger = 12;   //Pin digital 2 para el Trigger del sensor
const int Echo = 13;   //Pin digital 3 para el Echo del sensor
DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
}

void loop() {
   lcd.setCursor(0,0);
  lcd.print(" Sensor de Hum, ");
  lcd.setCursor(0,1);
  lcd.print("   tem y dist   ");
  delay (1000);
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
  
  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(3000); 
   lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (d)+ "cm");
  lcd.setCursor(0,1);
  lcd.print("   Jorge Lopez  ");
  delay (1000);         //Hacemos una pausa de 100ms
}
```
3. Se necesita instalar las librerias de **DHT sensor library for ESPx**, y **LiquidCrystal I2C** en el simulador como se muestra en la siguiente imagen.

![](https://github.com/jorgelopezquiroz/Ultrasonic_dht22/blob/main/Captura%20de%20Pantalla%202023-06-23%20a%20la(s)%2023.52.01.png?raw=true)
 
4. Hacer la conexion de **HC-SR04 Ultrasonic Distance Sensor**, **DHT22** y con la **ESP32** como se muestra en la siguente imagen.

![](https://github.com/jorgelopezquiroz/Ultrasonic_dht22/blob/main/diagram.png?raw=true)

### Instrucciónes de operación

1. Iniciar la simulación.
2. Visualizar los datos en el monitor serial.
3. Colocar la temperatura y humedad dando *doble click* al sensor **HC-SR04 Ultrasonic Distance Sensor** para simular la distancia y al sensor **DHT22** para simular humedad y temperatura.


## Resultados

Cuando haya compilado, verás los valores dentro del  en el  monitor serial.

## Monitor serial
![](https://github.com/jorgelopezquiroz/Ultrasonic_dht22/blob/main/Monitor%20Serial.png?raw=true)


## Evidencias


Evidencia 1
![](https://github.com/jorgelopezquiroz/Ultrasonic_dht22/blob/main/1.png?raw=true)

Evidencia 2


![](https://github.com/jorgelopezquiroz/Ultrasonic_dht22/blob/main/2.png?raw=true)

Evidencia 3


![](https://github.com/jorgelopezquiroz/Ultrasonic_dht22/blob/main/3.png?raw=true)


# Créditos

Desarrollado por Jorge Esteban Lopez Quiroz

- [GitHub](https://github.com/jorgelopezquiroz)