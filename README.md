## Lokaverkefni-vesm
Diljá, Gabríel, Hjörvar, Ingþór  2/28/2023


9 php Rör, 33 skrúfur, 1 arduino uno, 289 motor controller, breadboard, 3D prentaðar haus og hendur, 1 þrýstiplötu, vírar, málninga og raf teypi, tréplata


Við byrjuðum að teikna út hvernig fígúran okkar ætti að vera og ná í þá hluti sem við þurftum í verkenfið. Eftir að við vorum með allt sem að við þurftum í verkenfið settum við allt saman samkvæmt teikningu okkar frá byrjun. Fyrsta sem að við gerðum var að bora og setja saman rörin sem á að vera líkaminn við plötuna, eftir líkamann var borað grunnfestingu í plötuna sem inniheldur 12 volt DC motor fyrir hreyfingu fígúrunnar. Á meðan var Diljá og Gabrél að leggja hugsun sína á LED augun og servo mótorinn með vír tengdann við kjálkann. Eftir að kjálkinn virkaði og byrjaði að hreyfast þurftum við að fá samsvörun við hreyfingu kjálkans og MP3 spilarann (Speakers). 3D prentaðar hendur og hausinn var sett á líkamann og á meðan var Hjörvar að setja saman þrýstiplötuna svo að mótorinn virki þegar stigið er á plötuna. Það var lóðaða saman alla í hausinum víra fyrir betri skilaboð og tengingu á milli hausins og arduino. Við tengdum allar snúrur saman í brauðbrettið okkar til þess að prufa hvort að allt virki eins og það átti að virka. Eftir allar tengingarnar og kóðann virkaði allt saman í lokin.

[Myndband](https://youtu.be/SZJ2jEFvygw)


[<img src="https://img.youtube.com/vi/SZJ2jEFvygw.jpg" width="50%" height="50%">](https://youtu.be/SZJ2jEFvygw)


---

![image_50392577](https://user-images.githubusercontent.com/123474820/222184169-98a115d0-eedc-4d68-bd62-619794939c9f.JPG)
![image_50414593](https://user-images.githubusercontent.com/123474820/222184179-b9fcc1e0-9368-426e-b40f-410246f52045.JPG)
![image_50389761](https://user-images.githubusercontent.com/123474820/222184189-5327c98f-0c2a-464c-a905-593f7946032e.JPG)


---

**Kóði**
```C++
#include "Arduino.h"
#include "SoftwareSerial.h"
#include "DFRobotDFPlayerMini.h"
#include <Servo.h>
#include <MyDelay.h>

void ledBlink();
void mouth();
void body();
void body2();

MyDelay SERVOtime(15, mouth, 6);
MyDelay LEDtime(15, ledBlink, 6);
MyDelay BODY2time(10000, body2, 2);

MyDelay BODYtime(100, body, 2);


int enA = 11;
int in1 = 10;
int in2 = 9;

int ledState = LOW;

Servo myservo; 

int pos = 0;

const int ServoPin = 3;
int LEDpin = 13;

void setup()
{
  myservo.attach(ServoPin);
  pinMode(LEDpin,OUTPUT);
  LEDtime.start();
  SERVOtime.start();
  BODYtime.start();
  BODY2time.start();

  pinMode(enA, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);

  digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);

}


void loop() 
{
  SERVOtime.update();
  LEDtime.update();
  BODYtime.update();
 
  BODY2time.update();
}

void mouth() {
  for (pos = 90; pos <= 160; pos += 6){
    myservo.write(pos);
    delay(15);
    }
  for (pos = 160; pos >= 90; pos -= 6) { 
    myservo.write(pos); 
    delay(15);
    }
}

void ledBlink()
{
  if (ledState == LOW) 
    ledState = HIGH;
  else
    ledState = LOW;
  digitalWrite(LEDpin, ledState);

}

void body() {
  analogWrite(enA, 255);
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);
}

void body2() {
  digitalWrite(in1, LOW);
  digitalWrite(in2, LOW);
  digitalWrite(LEDpin, LOW);
}
```
