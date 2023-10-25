# TOOP19 Working with the Linse Sensor
The line sensor is the last sensro we will utilize with the Pololu robot.

## References
- [Pololu Line Sensor Library Documentation](https://pololu.github.io/pololu-3pi-plus-32u4-arduino-library/class_pololu3pi_plus32_u4_1_1_line_sensors.html)

## Working with Line Sensors
The 3pi+ 32U4 features five downward-facing line sensors. The five line sensors are on the underside of the board along the front edge and can help the 3pi+ distinguish between light and dark surfaces. Each reflectance sensor consists of a down-facing infrared (IR) emitter LED paired with a phototransistor that can detect reflected infrared light from the LED. Use the below to create a lineSensor object:

`LineSensors lineSensors;`

Here are some of the commands you may frequently use:
```
void calibrate()  //calibrated the bump sensors
uint8_t read()  //Reads both sensors
void leftChanged()  //Indicates a state change of left bump sensor since last read
void rightChanged()  //Indicates a state change of right bump sensor since last read
void leftisPressed() //Indacates left bump sensor is pressed
void rightisPressed() //Indacates right bump sensor is pressed
```
## Sensor Calibration
```
void calibrateSensors()
{
  // Wait 1 second and then begin automatic sensor calibration
  // by rotating in place to sweep the sensors over the line
  delay(1000);
  for(uint16_t i = 0; i < 80; i++)
  {
    if (i > 20 && i <= 60)
    {
      motors.setSpeeds(-60, 60);
    }
    else
    {
      motors.setSpeeds(60, -60);
    }

    lineSensors.calibrate();
  }
  motors.setSpeeds(0, 0);
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








