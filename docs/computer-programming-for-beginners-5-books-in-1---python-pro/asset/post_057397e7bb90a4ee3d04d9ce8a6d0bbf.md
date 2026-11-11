
## Turn your Arduino into a Machine

While switches and buttons are an excellent thing, still there is a lot more to do than turn it on and off. Although Arduino is a digital device, it can receive information from an analog sensor so that it can measure light, temperature and so on. Various inputs and programming languages give different results, so the outputs are dependent on coding and the sensors you choose. To find more sensors, visit the Arduino website. To create this, you use the built-in Analog-to-Digital Converter of the Arduino.

You will use a temperature sensor to determine the warmth of your skin. This device releases a changing voltage based on the temperature it detects. It comes with three pins: the first pin connects to the ground while the other connects to the power. The third pin transfers the voltage of the variable into the Arduino.

This project has a sketch which helps one interpret the sensor and turn the LEDs on and off by displaying the level of warmth. Temperature sensors are of different types. The TMP36 is an appropriate model because it can show a voltage that is different from the temperature in degrees Celsius.

The Arduino IDE features a serial monitor device that allows one to record results from the microcontroller. Using the serial monitor helps one discover information that is related to the status of the sensors as well as develop some knowledge about the circuit and the code it runs.

### Create the Circuit

![](img/239ff1e8a63502805c86c4dfbd71509a_325_0.png)

![](img/239ff1e8a63502805c86c4dfbd71509a_326_0.png)

Now, you are doing it manually, but you can achieve that by calibration. You can use the button to define the reference temperature, or let the Arduino pick a sample before a loop() starts and have it as the point of reference.

- 1. First, connect your breadboard to the ground.
- 2. Connect the cathode of every LED you have to the ground using a resistor. Join the anodes of the LEDs to pins 2 through 4. These are the project indicators.

Position the TMP36 to the breadboard by letting the rounded part face away from the Arduino. Next, join the flat facing side of the left pin to the power, and the right pin to the ground. Connect the central pin to the A0 on the Arduino.

Build an interface for the sensor to help people use it. You can use a paper cutout that resembles a hand of a good indicator. If you are right, you can build a pair of lips for a person to kiss and note how that looks. You might also want to mark the LEDs so that it can reveal some meanings.

![](img/239ff1e8a63502805c86c4dfbd71509a_327_0.png)

- 1. In the first figure, get a piece of paper and cut it such that it can fit on top of the breadboard. Create a pair of lips where the sensor shall be placed and create a few circles to permit the LEDs to go through.
- 2. Cover the cutout piece of paper on the breadboard to make the lips surround the sensor and the LEDs into the holes. Press the lips to see how it feels.

Let’s examine the Code.

### Useful constants

Constants allow someone to give unique names to things in the program. This is similar to variables except that they cannot change. Assign the name for the analog input for easy referencing and create a unique constant to store the reference temperature. After every 2 degrees past the reference temperature, the LED will switch on. Temperature is written and stored in a floating-point number. A floating-point number is one that has a decimal point.

### Initialization of the serial port

In the setup, you will interact with a new command called Serial.begin(). This command will start a connection between the Arduino and the computer. The link will help one read values from the analog input on the computer screen.

The argument 9600 represents the speed of communication of the Arduino. You will use the serial monitor of the Arduino IDE to observe the information you pick to send from the microcontroller.

### Initialize the digital pin and switch it off

The next thing is the for() loop that sets a few pins as the output. These pins were previously connected to the LEDs. Instead of assigning each a unique name and using the pinMode() function, you can choose to use the for() loop, which is much more efficient. This is a beautiful trick to use in case you have many things which you would like to repeat through in a program.

### Reading the sensor temperature

While in the loop(), use the variable called sensorValue to hold the sensor reading. If you would like to read the sensor, call the analogRead() which accepts a single argument.

### Transfer the sensor values to the PC

The Serial.print() function transfers data from the Arduino to the PC. You can check this information in the serial monitor. If you assign the Serial.print() a parameter in the quotation marks, it displays the text typed. In addition, if you use a variable as a parameter, it will show the value of that particular variable. Below is the code for the program:

Part of the program.

```cpp
// convert the ADC reading to voltage
float voltage = (sensorValue / 1023.0) * 5.0;

Serial.print("Volts = ");
Serial.println(voltage);

Serial.print(" degrees C ");
// convert the voltage to temperature in degrees
float temperature = (voltage - .5) * 100;
Serial.println(temperature);

if (temperature < baselineTemp) {
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);
}
```

Source: the database

### Turn on the LED to create a low temperature

The && operator stands for “and” in the logical sense. It allows one to check for multiple conditions.

### To create a medium temperature, turn on the two LEDs

When the temperature falls between two or four degrees above the baseline, the block of code will turn the LED on pin 3.

## C Language Basics and Functions

When you create an Arduino program, it is essential to have some knowledge about the working of computer systems. Even though C programming is the language that is close to the machines, how certain things are done when the program runs will become clear. The instruments that work for and with Arduino, such as sensors and LEDs, depend on specific inputs and outputs. Many programming languages are equipped with this ability, but C is our choice.

A primary system consists of the control device referred to as the CPU or microcontroller. There are a few differences when it comes to some of these. We shall dig deep into this later. Just to mention, microcontrollers may not be that powerful compared to the standard microprocessor. However, it still contains input, output ports, as well as hardware functions.

Microprocessors are connected to the external memory. Generally, microcontrollers contain a sufficient amount of onboard memory. However, it should be noted that we are not referring to the large sizes; it is possible for a microcontroller to have only a few hundred bytes or so of memory for the simple applications. Don’t forget that a memory byte has 8 bits, and each bit can either be true or false, high or low and I/O.

The register is the only place where we can have logical and mathematical operations carried out. For example, if you would like to carry out an addition of two variables, the value of the variables has to be moved over to the register.

### Memory Maps

Each memory byte in the computer system has a connected address. Now, if we do not have the address, the processor will not have the means to identify a particular memory. In general, the memory address begins from 0 as it increases. Even though we have specific addresses with a private or unique system, a particular address may not point to the input and output port of external communication.

Most of the time, you will find it necessary to map out the memory. This is merely a massive array of memory slots. We have people who develop a memory map and have the address with the least value positioned at the top while others who
