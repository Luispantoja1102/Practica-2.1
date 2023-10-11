##  Prueba


[Practica OLED Logo](PracticaOled.md)

[Practica Hora](PracticaHora.md)





##  HC-SR04
  
## Instituto Tecnológico de Tijuana <br> Depto de Sistemas y Computación <br> Ing. En Sistemas Computacionales <br> SISTEMAS PROGRAMABLES 23a <br> Autor : Pantoja Parra Luis Enrique <br> Repositorio: Pagina<br> Fecha de revisión:   13/09/2023  <br> Sensor  HC-SR04

## Descripcion
![Sensor HC-SR04](https://media.naylampmechatronics.com/741-superlarge_default/sensor-ultrasonido-hc-sr04.jpg)

El sensor HC-SR04 es un sensor de distancia de bajo costo que utiliza ultrasonido para determinar la distancia de un objeto en un rango de 2 a 450 cm. Destaca por su pequeño tamaño, bajo consumo energético, buena precisión y excelente precio. El sensor HC-SR04 es el más utilizado dentro de los sensores de tipo ultrasonido, principalmente por la cantidad de información y proyectos disponibles en la web. De igual forma es el más empleado en proyectos de robótica como robots laberinto o sumo, y en proyectos de automatización como sistemas de medición de nivel o distancia.

El sensor HC-SR04 posee dos transductores: un emisor y un receptor piezoeléctricos, además de la electrónica necesaria para su operación. El funcionamiento del sensor es el siguiente: el emisor piezoeléctrico emite 8 pulsos de ultrasonido(40KHz) luego de recibir la orden en el pin TRIG, las ondas de sonido viajan en el aire y rebotan al encontrar un objeto, el sonido de rebote es detectado por el receptor piezoeléctrico, luego el pin ECHO cambia a Alto (5V) por un tiempo igual al que demoró la onda desde que fue emitida hasta que fue detectada, el tiempo del pulso ECO es medido por el microcontrolador y asi se puede calcular la distancia al objeto. El funcionamiento del sensor no se ve afectado por la luz solar o material de color negro (aunque los materiales blandos acústicamente como tela o lana pueden llegar a ser difíciles de detectar).

La distancia se puede calcular utilizando la siguiente formula:

Distancia(m) = $\frac{{Tiempo del pulso ECO \times Velocidad del sonido=340m/s}}{2}$

El sensor  **[US-016]** es similar al HC-SR04 pero con salida de tipo analógico, otro sensor ultrasonido es el sensor  **[US-100]** con salida de tipo uart/serial.




| ESPECIFICACIONES TÉCNICAS                          |                         |
|---------------------------------------------------|-------------------------|
| Voltaje de Operación                              | 5V DC                   |
| Corriente de reposo                               | < 2mA                   |
| Corriente de trabajo                              | 15mA                    |
| Rango de medición                                 | 2cm a 450cm             |
| Precisión                                         | +- 3mm                  |
| Ángulo de apertura                                | 15°                     |
| Frecuencia de ultrasonido                         | 40KHz                   |
| Duración mínima del pulso de disparo TRIG (TTL)   | 10 μS                   |
| Duración del pulso ECO de salida (TTL)           | 100-25000 μS            |
| Dimensiones                                       | 45*20*15 mm             |
| Tiempo mínimo de espera entre una medida y el inicio de otra | 20ms (recomendable 50ms) |

| CONEXIÓN                       |
|--------------------------------|
| VCC (+5V DC)                   |
| TRIG (Disparo del ultrasonido) |
| ECHO (Recepción del ultrasonido)|
| GND (Tierra: 0V)               |


## Codigo

> const int Trigger = 2;   //Pin digital 2 para el Trigger del sensor
> const int Echo = 3;   //Pin digital 3 para el Echo del sensor
>
>void setup() {
>Serial.begin(9600);//iniciailzamos la comunicación
>pinMode(Trigger, OUTPUT); //pin como salida
>pinMode(Echo, INPUT);  //pin como entrada
>digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
>}
>
>void loop()
{
>
> long t; //timepo que demora en llegar el eco
> > long d; //distancia en centimetros
>
> digitalWrite(Trigger, HIGH);
>delayMicroseconds(10);          //Enviamos un pulso de 10us
>  digitalWrite(Trigger, LOW);
>  
 >t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
 > d = t/59;             //escalamos el tiempo a una distancia en cm
 >
 >Serial.print("Distancia: ");
 > Serial.print(d);      //Enviamos serialmente el valor de la distancia
  >Serial.print("cm");
  >Serial.println();
  >delay(100);          //Hacemos una pausa de 100ms
>}
