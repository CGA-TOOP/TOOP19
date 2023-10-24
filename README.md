# TOOP17 Working with Pololu Motors and Gyro
Now that we can use the OLED and Push Buttons, it's time to make the robot move and turn!

## References
- [Pololu Motor Library Documentation](https://pololu.github.io/pololu-3pi-plus-32u4-arduino-library/class_pololu3pi_plus32_u4_1_1_motors.html)
- [Pololu IMU Library Documentation](https://pololu.github.io/pololu-3pi-plus-32u4-arduino-library/class_pololu3pi_plus32_u4_1_1_i_m_u.html)

## Working with Motors
Your Pololu robot comes with two micro motors. These can be made to turn clockwise or counterclockwise from zero to a maximum speed. The speed of your robot will vary with battery charge.  Like the OLED and Buttons, you must include the Pololu library and create a motor object from the `Motors` class:

`Motors motor`

Here are some of the commands you may frequently use:
```
void calibrate()  //calibrated the bump sensors
uint8_t read()  //Reads both sensors
void leftChanged()  //Indicates a state change of left bump sensor since last read
void rightChanged()  //Indicates a state change of right bump sensor since last read
void leftisPressed() //Indacates left bump sensor is pressed
void rightisPressed() //Indacates right bump sensor is pressed
```

## Working with the IMU (Inertial Measurement Unit)
The 3pi+ 32U4 includes on-board inertial sensors that allow it to determine its own orientation by implementing an inertial measurement unit (IMU). The first chip, an ST LSM6DS33, combines a 3-axis accelerometer and 3-axis gyro into a single package. The second chip is an ST LIS3MDL 3-axis magnetometer.
To utilize the IMU working we have to explicitly include the Pololu IMU library `#include <Pololu3piPlus32U4IMU.h>`.  We also must create an IMU object from the `IMU` class:

`IMU imu`

Working direclty with the IMU library can be a bit cumbersome.  To assist, you will want to utilize the provided TurnSensor.h header file.  Download this file and save in the `include` drectory of your PlatformIO project.  The purpose of this file is to allow you use predefined functions in your main.cpp to better control the gyro heading sensor. After you have created your objects, then be sure to include the TurnSensor.h file. 

Here are some of the command you may frequently use:
```
void turnSensorSetup()  //This should be called in setup() to calibrate your robot. 
void turnSensorReset() //This resets the starting point for measuring a turn.
void turn SensorUpdate()  //This reads the gyro and updates the heading.
```

## Putting it all together
Here is a basic starting point for future projects that need to use buttons, display, motors, and IMUs.
```
#include <Arduino.h>
#include <Pololu3piPlus32U4.h>
#include <Pololu3piPlus32U4IMU.h>

using namespace Pololu3piPlus32U4;

OLED display;
ButtonA buttonA;
ButtonB buttonB;
ButtonC buttonC;
Motors motor;
IMU imu;

#include "TurnSensor.h"

void setup(){

}

void loop(){

}

```
## Exercise
The goal of this exercise is to properly display heading and test the different speeds of your motors.

1. Create a new Platform IO project:
- Use the starter code in this repository to get a head start.
- Ensure your `platform.ini` file has the proper library dependancies configured.
- Place the `TurnSensor.h` header file in this repository in the `include` directory of your Platform IO project.
2. In `setup()`:
- Initialize your display.
- Initilaize your turn sensor.
- Display a warning message `DO NOT MOVE ROBOT` during the gyro initilization.
3. In `loop()`:
- Update your turn sensor heading and display the heading on the first line of your display
- Drive your robot forward at a slow speed for 1 second if button A is pressed.
- Drive your robot forward at a medium speed for 1 second if button B is pressed.
- Drive your robot forward at a fast speed for 1 second if button C is pressed.








