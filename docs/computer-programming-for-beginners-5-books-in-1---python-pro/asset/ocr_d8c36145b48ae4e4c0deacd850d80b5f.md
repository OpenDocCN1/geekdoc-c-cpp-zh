only need to run a single statement in case the condition is true, so we have not used curly braces to indicate the function body. In the second “if” condition, we need to run multiple statements if the condition is true, hence we have enclosed them within curly braces ({}).

**]************

# Wrap the sensor value into a certain frequency

Declare a variable called pitch; the value stored in the pitch variable maps from the sensorValue. Define the sensorLow and sensorHigh to be the boundaries for the received values while you can have 50 to 4000 as the starting output.

# Play the frequency

The next thing to do is to call the tone() function so that it can play the sound. The tone() function accepts three arguments: the pin that will represent the sound, the frequency to play, as well as the period to play the tone. Finally, you can call the delay() function to create a delay of 10 milliseconds so that you create some time for the sound to play.

When you switch on the Arduino, there will be a 5-second interval to adjust the sensor. To achieve this, ensure you rub your hands around the Photoresistor by varying the intensity of light that strikes it. Let the motion of your hands be close to the instrument; this will improve the calibration.

After 5 seconds, calibration is over, and Arduino LED turns off. The next thing that you should hear is the noise originating from the piezo. When the intensity of light that strikes the sensor varies, the frequency of the piezo will also vary.