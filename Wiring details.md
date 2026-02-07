# **Circuit Documentation**

## **Summary**

This circuit is a complex system integrating multiple sensors, a motor, a motor driver, a power distribution board, and a Raspberry Pi 4B as the central processing unit. The circuit is designed to manage power distribution, sensor data acquisition, and motor control. It includes components such as VL53L0X Flight Time Sensors, an MPU6050 Accelerometer \+ Gyroscope, a BTS7960 Motor Driver, and a PCA9865 for PWM control. The system is powered by Zeee 7.4V LiPo batteries and includes a buck converter for voltage regulation.

## **Component List**

1. **VL53L0X Flight Time Sensor**  
   * Description: Time-of-flight distance sensor.  
   * Pins: VIN, GND, SCL, SDA, XSHUT, GPIO1  
2. **Power Distribution Board**  
   * Description: Distributes power to various components.  
   * Pins: Output 1+, Input \+, Input \-, Output 2+, Output 2-, Output 3+, Output 4+, Output 5+, Output 1-, Output 4-, Output 3-, Output 5-, Output 6+, Output 6-, Output 7+, Output 7-, Output 8+, Output 8-, Output 9+, Output 9-, Output 10+, Output 10-, Output 11+, Output 11-, Output 12+, Output 12-, Output \+, Output \-  
3. **Raspberry Pi 4B**  
   * Description: Central processing unit for the circuit.  
   * Pins: 3V3, 5V, GPIO2, GPIO3, GND, GPIO4, GPIO14, GPIO15, GPIO17, GPIO18, GPIO27, GPIO22, GPIO23, GPIO24, GPIO10, GPIO9, GPIO25, GPIO11, GPIO8, GPIO7, ID\_SD, GPIO5, GPIO6, GPIO12, GPIO13, GPIO19, GPIO16, GPIO26, GPIO20, GPIO21, ID\_SC, TR01\_TAP, TR00\_TAP, TR03\_TAP, TR02\_TAP, RUN, GLOBAL\_EN  
4. **MPU6050 Accelerometer \+ Gyroscope**  
   * Description: Measures acceleration and angular velocity.  
   * Pins: INT, AD0, XCL, XDA, SDA, SCL, GND, VCC  
5. **Switch**  
   * Description: Controls power flow.  
   * Pins: Vin, GND, Vout  
6. **Motor type 540-J**  
   * Description: DC motor for mechanical movement.  
   * Pins: V+, GND  
7. **24/5v Buck Converter**  
   * Description: Converts voltage levels.  
   * Pins: VIN+, VIN-, 5V, GND, VCC+, GND-  
8. **BTS7960 Motor Driver**  
   * Description: Controls motor operation.  
   * Pins: VM-, VM+, M+, M-, GND, VCC, L\_IS, R\_IS, R\_EN, L\_EN, R\_PWM, L\_PWM  
9. **Zeee 7.4V 4000mAh 50C 2S LiPo Battery**  
   * Description: Provides power to the circuit.  
   * Pins: \+, \-  
10. **MG996R Servo Motor**  
    * Description: Servo motor for precise control.  
    * Pins: GND, VCC, SIG  
11. **PCA9865**  
    * Description: PWM controller for servo and motor control.  
    * Pins: GND, OE, SCL, SDA, VCC, V+, PWM0, PWM1, PWM2, PWM3, PWM4, PWM5, PWM6, V, PWM7, PWM8, PWM9, PWM10, PWM11, PWM12, PWM13, PWM14, PWM15

## **Wiring Details**

### **VL53L0X Flight Time Sensors**

* **Sensor 1**  
  * VIN connected to Power Distribution Board Output 3+  
  * GND connected to Power Distribution Board Output 3-  
  * SCL connected to Raspberry Pi 4B GPIO3  
  * SDA connected to Raspberry Pi 4B GPIO2  
  * XSHUT connected to Raspberry Pi 4B GPIO26  
* **Sensor 2**  
  * VIN connected to Power Distribution Board Output 4+  
  * GND connected to Power Distribution Board Output 4-  
  * SCL connected to Raspberry Pi 4B GPIO3  
  * SDA connected to Raspberry Pi 4B GPIO2  
  * XSHUT connected to Raspberry Pi 4B GPIO21  
* **Sensor 3**  
  * VIN connected to Power Distribution Board Output 2+  
  * GND connected to Power Distribution Board Output 2-  
  * SCL connected to Raspberry Pi 4B GPIO3  
  * SDA connected to Raspberry Pi 4B GPIO2  
  * XSHUT connected to Raspberry Pi 4B GPIO20  
* **Sensor 4**  
  * VIN connected to Power Distribution Board Output 1+  
  * GND connected to Power Distribution Board Output 1-  
  * SCL connected to Raspberry Pi 4B GPIO3  
  * SDA connected to Raspberry Pi 4B GPIO2  
  * XSHUT connected to Raspberry Pi 4B GPIO16

### **Power Distribution Board**

* Input \+ connected to Raspberry Pi 4B 3V3  
* Input \- connected to Raspberry Pi 4B GND

### **Raspberry Pi 4B**

* 5V connected to Switch Vout  
* GPIO2 connected to SDA of all VL53L0X Sensors, MPU6050, and PCA9865  
* GPIO3 connected to SCL of all VL53L0X Sensors, MPU6050, and PCA9865  
* GND connected to Switch GND and Power Distribution Board Input \-

### **MPU6050 Accelerometer \+ Gyroscope**

* VCC connected to Power Distribution Board Output 7+  
* GND connected to Power Distribution Board Output 7-  
* SDA connected to Raspberry Pi 4B GPIO2  
* SCL connected to Raspberry Pi 4B GPIO3

### **Switch**

* Vin connected to 24/5v Buck 5V  
* GND connected to Raspberry Pi 4B GND and 24/5v Buck GND

### **Motor type 540-J**

* V+ connected to BTS7960 Motor Driver M+  
* GND connected to BTS7960 Motor Driver M-

### **24/5v Buck Converter**

* VIN+ connected to Zeee 7.4V LiPo Battery \+  
* VIN- connected to Zeee 7.4V LiPo Battery \-  
* 5V connected to Switch Vin  
* GND connected to Switch GND

### **BTS7960 Motor Driver**

* VM+ connected to 24/5v Buck VIN+  
* VM- connected to 24/5v Buck VIN-  
* VCC connected to 24/5v Buck 5V  
* GND connected to 24/5v Buck GND  
* M+ connected to Motor type 540-J V+  
* M- connected to Motor type 540-J GND  
* R\_EN and L\_EN connected to PCA9865 V+  
* R\_PWM connected to PCA9865 PWM0  
* L\_PWM connected to PCA9865 PWM1

### **Zeee 7.4V 4000mAh 50C 2S LiPo Battery**

*   
  * connected to 24/5v Buck VIN+  
*   
  * connected to 24/5v Buck VIN-

### **MG996R Servo Motor**

* VCC connected to PCA9865 V+  
* GND connected to PCA9865 GND  
* SIG connected to PCA9865 PWM15

### **PCA9865**

* VCC connected to Power Distribution Board Output 6+  
* GND connected to Power Distribution Board Output 6-  
* SDA connected to Raspberry Pi 4B GPIO2  
* SCL connected to Raspberry Pi 4B GPIO3

ci	