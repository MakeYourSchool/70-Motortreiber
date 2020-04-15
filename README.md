Motortreiber
----
*(Seeed Studio Grove – I2C Motor Driver V1.3)*

<img src=https://www.makeyourschool.de/wp-content/uploads/2018/10/70_motortreiber-1024x1024.jpg width=400px>

Bildquelle: *Wissenschaft im Dialog*

Im Allgemeinen reichen die Stromstärken, die ein Mikrocontroller liefern kann, nicht aus, um einen Motor direkt anzusteuern. Deshalb gibt es unterschiedliche Arten von sogenannten Motortreibern. Diese werden eingangsseitig am Mikrocontroller und ausgangsseitig am Motor angeschlossen. Sie übersetzen die Kommandos des Mikrocontrollers in die vom Motor benötigten Stromstärken. Gleichzeitig wird der Mikrocontroller von etwaigen Kurzschlüssen oder Überspannungen, die seitens des Motors entstehen könnten, geschützt.

Die vorliegende Ausführung kann einen vieradrigen Schrittmotor oder bis zu zwei Gleichstrommotoren ansteuern. Falls zwei Gleichstrommotoren angeschlossen werden, können diese unabhängig voneinander sowohl bezüglich der Richtung und Geschwindigkeit gesteuert werden.

Der Motortreiber wird direkt oder mithilfe des Grove Shields an einen Arduino oder Raspberry Pi über die serielle Schnittstelle I2C  angeschlossen. Der Treiber benötigt dabei eine separate Stromversorgung zwischen 6V und 15V.

Ein Beispielprojekt könnte ein Roboter sein, der ein frei drehbares und zwei angetriebene Räder besitzt. Die zwei Räder können mithilfe des Motortreibers sowohl vorwärts als auch rückwärts gesteuert werden. So kann der Roboter in alle Richtungen navigiert werden.

Im Folgenden ist die grundlegende Verwendung des Motortreibers zusammengefasst (bisher nur in englischer Sprache):

---

## Usage

Simply copy the Grove_I2C_Motor_Driver_v1_3 folder to your Arduino library collection. For example, arduino-1.6.12/libraries. Next time you run the Arduino IDE, you'll have a new option in Sketch -> Include Library -> Grove_I2C_Motor_Driver_v1_3. Review the included examples in Grove_I2C_Motor_Driver_v1_3/examples.

### 1. Set the address of the I2C Motor Driver

- Set the address by dial switch is a new function added to the new I2C Motor Driver.

    ![](https://raw.githubusercontent.com/SeeedDocument/Grove-I2C_Motor_Driver_V1.3/master/img/I2CMotorDriver-9.jpg)

- Then keep the address setup in the program the same as the address setup on the I2C motor driver. The default address setup in the program is 0x0f.
    ```
    // default I2C address is 0x0f
    #define I2C_ADDRESS 0x0f

    void setup() {
      Motor.begin(I2C_ADDRESS);
    }
    ```

### 2. Drive 2 DC motors

- There are 2 functions to control DC motors:
    ```
    // Set the speed of a motor, speed is equal to duty cycle here
    void speed(unsigned char motor_id, int _speed);

    // Stop one motor
    void stop(unsigned char motor_id);
    ```
With speed() function, you are able to drive one motor at the speed you want.

**motor_id** represents which motor to use. You can fill MOTOR1 or MOTOR2.

**_speed** represents the speed you set to the motor. You can fill -100~100 here. When _speed>0, DC motor runs clockwise, while _speed<0, DC motor runs anticlockwise. And the bigger the absolute value of _speed, the faster the speed of DC motor.

With stop() function, you are able to stop a running DC motor.

**motor_id** represents which motor to use. You can fill MOTOR1 or MOTOR2.


### 3. Drive a Stepper Motor

- We provide a function to drive a stepper motor. 
```
// Drive a stepper motor
void StepperRun(int _step, int _type=0, int _mode=0);
```
- **_step** represents the steps you set to the stepper motor to run. You can fill -1024~1024. When _step>0, stepper motor runs clockwise, while _step<0, stepper motor runs anticlockwise. When _step is 512/-512, the stepper motor will run a complete turn and if _step is 1024/-1024, the stepper motor will run 2 turns. The stepper motor will stop automatically after it finishes its steps.
**_type** represents the type of stepper motor, __0 is for 4 phase stepper motor(default)__ and __1 for 2 phase stepper motor__.
**_mode** represents the operation mode. 0 for compatible mode (_step=1 corresponds 4 steps of motor), and 1 for fine mode (_step=1 corresponds 1 step of motor)

eg:

1. Set step as 512 and drive a 4 phase stepper motor.
```    
StepperRun(512, 0);
```
Or
```    
StepperRun(512);
```
2. Set step as 512 and drive a 2 phase stepper motor.
```    
StepperRun(512, 1);
```

Note that number of pulses for "__step" is 4 (for 2-phase motor), and the number of steps of one motor turn is dependent on the spec of the stepping motor. For example, for the motor with 100 pulse per turn (3.6 degree per pulse), __step=25 will make one turn of the motor.

----

Im Rahmen von [*Make Your School*](https://www.makeyourschool.de/) finden an Schulen Hackdays statt. Dabei überlegen sich Schülerinnen und Schüler, wie sie ihre Schule mitgestalten und mit technischen und digitalen Tools noch besser machen können. Unterstützt werden sie dabei von Mentorinnen und Mentoren, die die Veranstaltung begleiten und fachliche Impulse geben. *Make Your School* ist ein Projekt von *Wissenschaft im Dialog*. Die Klaus Tschira Stiftung ist bundesweiter Förderer.

Mit diesen **Bibliotheken und Beispiel-Codes** kann der euch vorliegende Sensor/Aktor getestet werden. Den **Mentorinnen und Mentoren von *Make Your School*** steht es frei, die hier zusammengestellten Codes **nach Bedarf und den individuell gemachten Erfahrungen anzupassen**. Beispiele können einfach im Ordner „examples“ hinzugefügt oder bearbeitet werden. Wir werden eure Beiträge regelmäßig prüfen und das Repository mithilfe eurer Änderungsvorschläge aktualisieren.

Das Repository basiert grundlegend auf den veröffentlichten Informationen und Codes von Seeed Studio. Die deutsche Übersetzung stammt von *Make Your School*, Fehlinterpretationen und Änderungen vorbehalten. Die Informationen dürfen frei genutzt, angepasst und verbreitet werden, solange die Lizenzrechte (siehe License.txt) beachtet werden.


**Weitere Informationen:**

[Repository von Seeed Studio](https://github.com/Seeed-Studio/Grove_I2C_Motor_Driver_v1_3)

[Offizielles Wiki von Seeed Studio](http://wiki.seeedstudio.com/Grove-I2C_Motor_Driver_V1.3/)

[Materialkoffer von *Make Your School*](https://www.makeyourschool.de/material/motortreiber/)
