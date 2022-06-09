# DIY-SMD-Resistor-cutting-machine

![yt](https://user-images.githubusercontent.com/19898602/172761463-f377ba89-3a4f-4990-a336-672c4392723e.png)



Hello friends in this video I will make a Automatic SMD resistor cutting machine.
those who daily deals with smd comoponents knows the struggle of cutting such small resistors.
and if you need to cut them in bulk them job is even harder.

for that reason I made a mini compact machine that can cut n numbers of resistors for you.


# Components used

> Nema 17 Stepper motor
> High torque 12V DC motor
> linear rails
> 6mm Acrylic sheet
> 20 x 20 Alu. profile
> 8mm cutter blade
> shaft 
> 3D printed parts
> Custom PCB

# CIRCUIT & CUSTOM PCB


![image](https://user-images.githubusercontent.com/19898602/172763367-df5d7602-8237-401e-827b-db75f10aa6b9.png)


![b](https://user-images.githubusercontent.com/19898602/164375961-2278b4e2-0209-49fa-a1ea-0588c8e57c32.JPG)![c](https://user-images.githubusercontent.com/19898602/164375975-362c836c-359e-436e-a462-8bcb1155d997.JPG)

![d](https://user-images.githubusercontent.com/19898602/164376092-7663a81f-8dc3-4922-9d52-6a5f5c74cd94.JPG)


I have design circuit and PCB ineasy EDA and ordered PCB from [JLCPCB.com](https://jlcpcb.com/IAT)




[JLCPCB.com](https://jlcpcb.com/IAT) are the world leader in PCB manufacturing there PCB production rates are very much affordable and they have world class PCB production unit results fast PCB production.

I have provided the link of circuit desgin so that you can modify it as per your need if you need to change any thing.

https://oshwlab.com/sharmaz747/multipurpose-pcb_copy_copy_copy


![image](https://user-images.githubusercontent.com/19898602/159014034-3c9a50c3-61c3-40d2-836d-9cadc2317d33.png)


SMT Assembly service of [JLCPCB.com](https://jlcpcb.com/IAT) is cherry on top now get your PCB fully assembled and save your time and money
Select components for your PCB from there Parts Library of 200k+ in-stock components
they are offering $30 valued New User coupons  & $24 SMT coupons every month
$8.00 setup fee, and $0.0017  per joint

Now no need to order components separately for you PCB and get free from stress of soldering them on PCB just try PCB SMT assembly service and get you PCB with components pre assembled and ready for the project


👉 Try PCBA service of [JLCPCB.com](https://jlcpcb.com/IAT) and save your time and money, get PCB ready for project, 200K+ components in library of [JLCPCB.com](https://jlcpcb.com/IAT) as well as 3rd party         parts to choose from. 
    Assembly will support 10M+ parts from Digikey, mouser
    
👉 $30 valued New User coupons 

👉 $24 SMT coupons every month


For more detials & offers please visit [JLCPCB.com](https://jlcpcb.com/IAT)


First i have used my homemade CNC router machine to cut the acrylic parts.

I have used 6mm cast Acrylic sheet because they are router friendly and easy to machine.
I made two parts here one for stepper motor mount and one for DC gear motor mount.


![image](https://user-images.githubusercontent.com/19898602/172765383-cd5cb286-90a3-4c5e-a811-6030ec3b768b.png)
![image](https://user-images.githubusercontent.com/19898602/172763600-67301825-21bb-42f2-b6a9-bea11f2c9672.png)



Then I cut the 12mm wooden sheet to make the based of machine. I also attached 4 rubber legs the the base to reduce any mechanical vibration
here I have used two 20x20 Alu. extrusion profile. one I place horizontally ans on vertically.

On horizontal one I will attached stepper motor and on vertical one Resistor reel has been attached.


![image](https://user-images.githubusercontent.com/19898602/172765748-9068fd5a-922c-4f21-9b18-2e4a686d6228.png)
![image](https://user-images.githubusercontent.com/19898602/172765809-47d5513a-9de7-42fc-b04c-3d93bacf2aae.png)



Stepper motor attached to the smaller acrylic part and DC gear motor is attached to the bigger acrylic part.



![image](https://user-images.githubusercontent.com/19898602/172766276-56b4d0fb-b1c3-4e3e-bba3-19f5d9f832b7.png)
![image](https://user-images.githubusercontent.com/19898602/172766303-649f94d1-68f5-498a-9fcc-1c4fd7436e47.png)



Now here I have choosen the MGH9N means 9mm linear rails which the best option for such purpose
I have screw the rail vertially to the DC gear motor acrylic part.



![image](https://user-images.githubusercontent.com/19898602/172766579-ae1e7cea-6fed-419e-b244-4309485cde7d.png)
![image](https://user-images.githubusercontent.com/19898602/172766635-1f0a5a8b-d815-459c-bcf9-53c62d4597d2.png)


This are some 3D printed parts used to slide the resistor reel to the cutter blade and to hold cutter blade along with linear rails.


![image](https://user-images.githubusercontent.com/19898602/172766952-55d00508-e6db-4c95-8aa7-db1690ae15b3.png)
![image](https://user-images.githubusercontent.com/19898602/172767052-c4828912-fe0e-4417-96bb-07af3d0f2bc4.png)







At last I completed the wiring thanks to the custom pcb is very quick and neat and clean also.

I attached stepper motor DC motor and HMI to its ports and now we are readyfor the action


![image](https://user-images.githubusercontent.com/19898602/172767594-5b45ab6c-a19a-42ca-abf1-b0c4b87a2db5.png)
![image](https://user-images.githubusercontent.com/19898602/172767676-7bdb7f6c-f4d0-46f1-9471-fc477a4ff4ca.png)



# Arduino Code

```
#include <Stepper.h>
#include <Arduino.h>
#include "BasicStepperDriver.h"
#include "L298N_MotorDriver.h"
#include <SoftwareSerial.h>
SoftwareSerial mySerial(2, 3); // RX, TX
int A = 0;
int B = 0;
int state = 0;
int EN = 12;
String message;
int QTY, numMessages, endBytes;
byte inByte;
int flag = 0;
volatile long temp, counter = 0;
float MTR = 0;  
int K = 1;
int sens = A4;
L298N_MotorDriver motor(5,7,8);

#define DIR  14
#define STEP  15
#define MICROSTEPS 16
#define MOTOR_STEPS 200
#define RPM 60

int count = 0;
BasicStepperDriver stepper(MOTOR_STEPS, DIR, STEP);










void setup()
{ 


  pinMode(sens,INPUT);
  pinMode(EN,OUTPUT);
motor.setSpeed(255);         // Sets the speed for the motor. 0 - 255
             // Turns the motor on
  
  
  numMessages, endBytes = 0;
  Serial.begin(115200);
 mySerial.begin(115200);
  stepper.begin(RPM, MICROSTEPS);
  
  delay(500);
  

  

 

 
}

void loop()
{

data();

if (A > 0 && B > 0) {
    delay(1000);

digitalWrite(EN,LOW);
for (int i = 0; i < B; i++){   
stepper.rotate(31*A);
delay(500);

while(!digitalRead(sens)){
motor.setDirection(false);  
motor.enable();
}
motor.setDirection(true);
motor.enable();
delay(5);
motor.disable();
delay(500);
}

 digitalWrite(EN,HIGH);
A=0;
 B=0;
}

 

}

void data() {
    if (state < 1) {
      if (numMessages == 1) { //Did we receive the anticipated number of messages? In this case we only want to receive 1 message.
        A = QTY;
        Serial.println(A);//See what the important message is that the Arduino receives from the Nextion
        numMessages = 0; //Now that the entire set of data is received, reset the number of messages received
        state = 1;
      }
    }

    if (state > 0) {
      if (numMessages == 1) { //Did we receive the anticipated number of messages? In this case we only want to receive 1 message.
        B = QTY;
        Serial.println(B);//See what the important message is that the Arduino receives from the Nextion
        numMessages = 0; //Now that the entire set of data is received, reset the number of messages received
        state = 0;
      }
    }






    if (mySerial.available()) { //Is data coming through the serial from the Nextion?
      inByte = mySerial.read();

      // Serial.println(inByte); //See the data as it comes in

      if (inByte > 47 && inByte < 58) { //Is it data that we want to use?
        message.concat(char(inByte)); //Cast the decimal number to a character and add it to the message
      }
      else if (inByte == 255) { //Is it an end byte?
        endBytes = endBytes + 1; //If so, count it as an end byte.
      }

      if (inByte == 255 && endBytes == 3) { //Is it the 3rd (aka last) end byte?
        QTY = message.toInt(); //Because we have now received the whole message, we can save it in a variable.
        message = ""; //We received the whole message, so now we can clear the variable to avoid getting mixed messages.
        endBytes = 0; //We received the whole message, we need to clear the variable so that we can identify the next message's end
        numMessages  = numMessages + 1; //We received the whole message, therefore we increment the number of messages received.

        //Now lets test if it worked by playing around with the variable.

      }
    }
  }



 void cutter (){
   motor.setDirection(false);
  motor.enable();
  delay(1100);
  motor.setDirection(true);
  delay(50);
  motor.disable();

 }
```



![Nested Sequence 01](https://user-images.githubusercontent.com/19898602/172768076-7550b09b-9fdb-4795-9ec8-8a9cbe500523.gif)





























