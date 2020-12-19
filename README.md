Sensoren
--------
***

> [⇧ **Home**](https://github.com/iotkitv4/intro)

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/Messysteme.png)

Source: Prof. Dr.-Ing. Michael Weyrich, http://wiki.zimt.uni-siegen.de/fertigungsautomatisierung

- - -


Sensoren sind technische Bauteile, die Eigenschaften der Umgebung (z. B.: Wärmestrahlung, Temperatur, Feuchtigkeit, Druck, Schall, Helligkeit oder Beschleunigung) erfassen und in ein weiter verarbeitbares elektrisches Signal umformen.

### Beispiele

* [Hall Sensor](#hall-sensor)
* [PIR Sensor](#pir-sensor)
* [Ultraschall Abstandsmesser](#ultraschall-abstandsmesser)
* [Temperatur Sensor](#temperatur-sensor) externe Variante
* [Übungen](#Übungen)

## Hall Sensor 
***

> [⇧ **Nach oben**](#beispiele)

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/HallEffectSensor.png) 

Hall Sensor auf Kit und für Durchsteckmontage

- - - 

Ein [Hall Sensor](http://de.wikipedia.org/wiki/Hall-Sensor) (auch Hall-Sonde oder Hall-Geber, nach Edwin Hall) nutzt den Hall-Effekt zur Messung von Magnetfeldern.

Der auf dem IoTKit verwendetete Hall Sensor kann zur Lage Erfassung eines Permanentmagnetes genutzt werden, d.h. es kann der Nordpol oder Südpol des Magneten bestimmt werden.

Beim IoTKitV3 K64F: schaltet der  eine Pol das Signal auf > 0.9 und der andere Pol setzt das Signal wieder zurück.

Beim DISCO_L475VG_IOT01A: wird ein Wert < 0.4 oder > 0.6 für Nord- oder Südpool des Magneten angezeigt.

Das [Beispiel](HallSensor/src/main.cpp) bringt, je nach Signal, LED 1 oder LED 2 zum Leuchten.

**Achtung**: Beim IoTKitV3 K64F muss der DIP-Switch, neben dem Hall Sensor, nach oben (on) zeigen.  

### Anwendungen

*   Alarmanlagen, z.B. zum Sichern von Fenstern.
*   Im Auto zur Kontrolle ob der Sicherheitsgurt geschlossen ist, als Raddrehzahlsensoren, zur Erkennung des Zündzeitpunkts.
*   Zur Geschwindigkeitsmessung, z.B. für E-Bikes.
*   In der Kraftwerkstechnik zur Erfassung der Turbinendrehzahl.

### Beispiel(e)

Das [Beispiel](main.cpp) bringt je nach Magnet Pool eine LED zu leuchten.


## PIR Sensor 
***

> [⇧ **Nach oben**](#beispiele)

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/PIRSensorUse.png)

Reichweite/Funktionsweise 

- - - 

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/PIRSensity.png) 

Empfindlichkeit 3 - 7 Meter 

- - -

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/PIRTime.png) 

Signal von 3 Sekunden bis 5 Minuten

- - -

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/PIRSensor.png) 

Anschlüsse

- - -

Ein Bewegungsmelder ist ein elektronischer Sensor, der Bewegungen in seiner näheren Umgebung erkennt und dadurch als elektrischer Schalter arbeiten kann. Ein Bewegungsmelder kann aktiv mit elektromagnetischen Wellen (HF oder Doppelradar), mit Ultraschall (Ultraschall-Bewegungsmelder) oder passiv anhand der Infrarotstrahlung der Umgebung arbeiten; es gibt auch Kombinationen davon.

Der [PIR Sensor (Bewegungsmelder)](http://de.wikipedia.org/wiki/Bewegungsmelder) (englisch passive infrared) ist der am häufigsten eingesetzte Typ von Bewegungsmeldern. Er reagiert optimal auf Winkeländerungen, wenn also eine Person am Sensor vorbeigeht. Der PIR Sensor wird mittels 3-adrigen Kabel mit dem Shield verbunden.

### Anwendungen

*   Einschalten einer Beleuchtung
*   Auslösen eines Alarms

### Anschlussbelegung (Sensor - Shield) 

*   VCC - +5V (5 Volt)
*   OUT - A5
*   GND - GND (Ground)

### Beispiel(e)

Das Beispiel bei Erkennung einer Bewegung wird eine LED eingeschaltet.

<details><summary>main.cpp</summary>  

    /** PIR Sensor (Bewegungsmelder)
     */
    #include "mbed.h"
    
    DigitalIn pirSensor( A5 );
    DigitalOut licht( MBED_CONF_IOTKIT_LED1 );
    
    int main()
    {
        while(1) 
        {
            if  ( pirSensor )
            {
                licht = 1;
                thread_sleep_for( 10000 );
            }
            else
                licht = 0;
        }
    }
    
</p></details>

### Links 

* [Arduino HC-SR501 Motion Sensor Tutorial](http://henrysbench.capnfatz.com/henrys-bench/arduino-sensors-and-input/arduino-hc-sr501-motion-sensor-tutorial/#attachment wp-att-2120/0/)

## Ultraschall Abstandsmesser 
***

> [⇧ **Nach oben**](#beispiele)

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/UltrasonicSensorTiming.png)

Timing

- - -

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/UltrasonicSensor.png)

HC-SR04 

- - - 

Unter Entfernungsmessung, Abstandsmessung oder Längenmessung versteht man die Messung des Abstandes zweier Punkte im Raum durch direkten oder indirekten Vergleich mit einer Längenmasseinheit wie beispielsweise dem Meter.

Ein [Ultraschall Abstandsmesser](http://de.wikipedia.org/wiki/Entfernungsmessung) misst die Entfernung zu einem Objekt (z.B. Wand) in cm.

Der Erkennungszyklus wird mittels eines Impulses von min. 10 Mikrosekunden auf der "pulse trigger" Leitung (Trig) gestartet. Sobald diese Leitung wieder tief wird, sendet der Sensor eine Serie von acht Schaltimpulsen, wartet einen kurzen Moment und setzt dann die Leitung Echo hoch. Das erste Ultraschallecho welches Empfangen wird, setzt die Echo Leitung wieder tief. Durch die Zeitspanne dazwischen, lässt sich den Abstand zu einem Objekt bestimmen.

Die Ganze Arbeit nimmt uns die [SR04](http://developer.mbed.org/users/ejteb/code/HC_SR04_Ultrasonic_Library/) Library ab.

### Anwendungen 

*   Erkennen von Hindernissen bei Robotern

### Anschlussbelegung (Sensor - Shield)

*   VCC - V (5 Volt)
*   Trig - A4
*   Echo - A5
*   GND - G (Ground)

### Beispiel(e)

Das Beispiel UltraschallSensor_LowLevelV2 zeigt, wie der Sensor ohne eine zusätzliche Library angesprochen werden kann.

<details><summary>UltraschallSensor_LowLevelV2</summary>  

    #include "mbed.h"
    #include "OLEDDisplay.h" 
     
    DigitalIn echo( A4 );
    DigitalOut trigger( A5 );
    Timer t;
    OLEDDisplay oled;
     
    float i;
     
    int main() 
    {
        t.start();
        printf(" ===[ Ultrasonic Range ]===");
     
        // OLED Display
        oled.clear();
     
        while (1) 
        {
            oled.clear();
            oled.printf( "Ultrasonic Range" );
    
            // send pulse
            trigger=1;
            ThisThread::sleep_for( 4ms );
            trigger=0;
     
            // wait for the echo line to go high
            while (!echo);
     
            // measure the length of the pulse
            t.reset();
            while (echo);
            i = t.elapsed_time().count();
     
            // display result
            printf("\n\n\rPulselength %6.0f uS",i);
            oled.printf("\n\rPulselength %6.0f uS",i);
            i=i/58;
            printf("\n\n\rDistance %4.0f cm",i);
            oled.printf("\rDistance %4.0f cm",i);
            ThisThread::sleep_for( 2000ms );
        }
    }    
</p></details>


## Temperatur Sensor 
***

> [⇧ **Nach oben**](#beispiele)

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/TemperatureSensorUse.png)

Beispiel Anwendung

- - -

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/sensors/TemperatureSensor.png)

DHT11

- - -

Der DHT11 ist ein multifunktionaler Sensor, der [Temperatur](http://de.wikipedia.org/wiki/Temperatursensor) und relative Luftfeuchte gleichzeitig misst. Er liefert zuverlässige Messwerte bei einer Luftfeuchtigkeit zwischen 20 % und 90 % und einer Temperatur zwischen 0 ° bis 50 ° Celsius.

Der Sensor benötigt die [DHT Library](http://developer.mbed.org/teams/components/code/DHT/)

**Tip:** zum Testen der Temperatur den Sensor zwischen die Hände halten. Zum Testen der Luftfeuchtigkeit, Sensor anhauchen.

### Anwendungen 

*   Überwachen Temperatur und Luftfeuchtigkeit
*   Ein- / Ausschalten der Heizung, Klimaanlage etc.

### Anschlussbelegung 

*   "+" - +5V (5 Volt)
*   OUT - A5
*   "-" - GND (Ground)

### Beispiel(e)

Das Beispiel TemperaturSensorExtern gibt Temperatur und Luftfeuchtigkeit auf der Console aus.


<details><summary>main.cpp</summary>  

    /** Temperatur Sensor (extern)
     */
    #include "mbed.h"
    #include "DHT.h"
    
    DHT sensor( A5, DHT11 );
    
    int main()
    {
        int rc = 0;
        float h = 0.0f, c = 0.0f, k = 0.0f, dp = 0.0f;
    
        while( 1 )
        {
            thread_sleep_for( 2000 );
            rc = sensor.readData();
            if ( rc == 0 )
            {
                c   = sensor.ReadTemperature(CELCIUS);
                k   = sensor.ReadTemperature(KELVIN);
                h   = sensor.ReadHumidity();
                dp  = sensor.CalcdewPoint(c, h);
                printf("Temperator in Kelvin: %4.2f, Celcius: %4.2f, ", k, c);
                printf("Luftfeuchtigkeit is %4.2f, Taupunkt: %4.2f\n", h, dp);
            }
            else
                return  ( -1 );         // Fehler - Programm beenden
        }
    }

</p></details>

## Übungen
***

> [⇧ **Nach oben**](#beispiele)

**Hinweis**: Ein paar der Übungen funktionieren nur mit dem IoTKitV3 K64F, weil der Encoder benötigt wird.

| **PIR Sensor, Summer**Wenn sich jemand nähert, Licht einschalten und Akustisches Signal Anwendung: Alarmanlage. |  |
|  **Hall Sensor**Sobald kein magnetisches Feld mehr vorhanden, Akustisches Signal auslösen. Anwendung: Fenstersicherung.  |  |

