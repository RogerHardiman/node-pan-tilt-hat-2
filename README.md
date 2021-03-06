# node-pan-tilt-hat-2
NodeJS driver for the Pan-Tilt HAT from _Pimoroni_ and from _Waveshare_


There are two make of Pan-Tilt HAT board for the Raspberry Pi, one made by _Pimoroni_ in the UK and one made by _Waveshare_ in China.
Both boards have some similarities and some differences

|Feature|Pimoroni|Waveshare|
|-------|--------|---------|
|Designed for the Raspberry Pi|Yes|Yes
|Standard 3 Pin Servo Headers|Yes|Yes|
|Control Chip|PIC16F1503 with custom firmware on the i2c bus. PIC generates the PWM signals|Standard PCA9685 PWM/LED controller on the i2c bus|
|I2C address|0x15|0x40 (with ability to be changed)|
|Extra feature|Has a 3rd PWM output for PWM controlled LEDs and Lights (this driver does not control the LED/Light control)|Has a Light Sensor on the i2c bus (this driver does not read the light level sensor)|
|Extra features|Brings the I2C, UART, Broadcom PWM and SPI signals to the edge of the board|Has tall header pins to allow access to all of the 40 pin connector from the top and to allow boards to be stacked. Has resister pads to allow the i2c address to be changed|
|Pi HAT Standard Compliance|Yes, has the HAT EEPROM. The Pi device tree will show the Pimoroni Pan-Tilt HAT is connected|No. Does not implement the HAT identification EEPROM|
|Country of origin|UK|China|
|URLs|http://shop.pimoroni.com/products/pan-tilt-hat|http://www.waveshare.com/pan-tilt-hat.htm|

# USAGE
```
var PanTiltHAT = require('pan-tilt-hat');
var pan_tilt = new PanTiltHAT();
console.log('Goto position Pan 0, Tilt 0');
pan_tilt.pan(0);
pan_tilt.tilt(0);
```


# INITIALISAION
  The library autodetects Pimoroni and Waveshare boards by checking the I2C addresses (0x15 and 0x40)

# ABSOLUTE POSITIONING
* Pan=0, Tilt=0 has the camera looking forword.
* Pan of +90 makes the Pi Camera look to the left
* Pan of -90 makes the Pi Camera look to the right
* Tilt of -80 makes the Pi Cammera look up
* Tilt of +80 makes the Pi Cammera look down
* (The positive and negative directions are the same as the Pimoroni Python driver)

```
  pan(angle)                      // angle between -90 and 90
  servo_one(angle)                // angle between -90 and 90
  tilt(angle)                     // angle between -80 and 80
  servo_two(angle)                // angle between -80 and 80
  ```


# CONTINUOUS MOVE API (START AND STOP COMMANDS)
   The camera will start to turn at the specificated speed and continue to turn until told to stop
   ```
   pan_left(speed)                 // start moving with a speed from 0 to 15. 0 means stop
   pan_right(speed)                // start moving with a speed from 0 to 15. 0 means stop
   tilt_up(speed)                  // start moving with a speed from 0 to 15. 0 means stop
   tilt_down(speed)                // start moving with a speed from 0 to 15. 0 means stop
   stop()                          // stop the pan and the tilt
   ```

 # SHUTDOWN
 ```
   close()                         // closes the class and frees resources
```

# SERVO SIGNAL
  After 2 seconds the servo PWM drive signal on the Pimoroni board is turned off to save power
