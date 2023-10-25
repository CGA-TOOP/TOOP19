# TOOP19 Working with the Line Sensor
The line sensor is the last sensor we will utilize with the Pololu robot.

## References
- [Pololu Line Sensor Library Documentation](https://pololu.github.io/pololu-3pi-plus-32u4-arduino-library/class_pololu3pi_plus32_u4_1_1_line_sensors.html)

## Working with Line Sensors
The 3pi+ 32U4 features five downward-facing line sensors. The five line sensors are on the underside of the board along the front edge and can help the 3pi+ distinguish between light and dark surfaces. Each reflectance sensor consists of a down-facing infrared (IR) emitter LED paired with a phototransistor that can detect reflected infrared light from the LED. Use the below to create a lineSensor object:

`LineSensors lineSensors;`

Here are some of the commands you may frequently use:
```
void calibrate()  //calibrated the line sensors
void read(uint16_t*sensorValues)  //Reads raw sensor values inat an array
void readCalibrated(uint16_t*sensorValues)  //Reads che sensors and provided calibrated values between 0 and 1000
uint16_t readLineBlack(uint16_t*sensorValues) // Reads the sensors, provides calibrated values, and returns an estimated black line position.

```
## Sensor Calibration
Prior to utilizing your line sensors, it is a good idea to calibrate the sensors using the function below. When you call this function, the robot will rotate back and forth over the line to determine the max and min thresholds for the IR sensors.  

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
2. In `setup()`:
- Initialize your display.
- Wait for the user to press a button and then calibrate your line sensors.
- Display a warning message once calibration is complete.
- Wait for the user to press a button untill you continue onto the loop.
3. In `loop()`:
- Move your robot forward continuously, untill your robot senses a line.
- Consider the speed that you want to move forward.
- Consider the conditions under which you want your robot to stop.








