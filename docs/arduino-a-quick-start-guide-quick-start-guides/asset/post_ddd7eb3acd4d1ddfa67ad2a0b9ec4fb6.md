
Building a new programming environment from scratch, the Arduino team decided to modify the Processing IDE. That's the reason why both IDEs look so similar and why Arduino sketches have the file extension .pde (Processing Development Environment), for example.

Using Processing as the basis for the Arduino project provided a good and well-tested IDE for free. Processing and the Arduino are a good team for several other reasons:

- The Arduino simplifies embedded computing, and Processing simplifies the creation of multimedia applications. So, you can easily visualize sensor data in often spectacular ways.
- Processing is easy to learn, especially if you already know Java.
- Processing has excellent support for serial communication.

So, for many reasons, Processing is well worth a look, but it’s especially useful when working with the Arduino. That’s why we’ll use it for several of the book’s examples.

## 5.6 Representing Sensor Data

We start with a Processing class that represents the current sensor data we return from the Arduino via serial port. Open a new file in the Processing IDE, and enter the following code:

```
class SensorData {
private float temperature;
private float distance;

SensorData(float temperature, float distance) {
this.temperature = temperature;
this.distance = distance;
}

float getTemperature() {
return this.temperature;
}

float getDistance() {
return this.distance;
}
}
```

If you are familiar with Java or C++, the SensorData class will be perfectly clear to you. It encapsulates a temperature value and a distance

as floating-point numbers and provides access to the data via accessor methods (getTemperature() and getDistance()). You can create new SensorData objects using the constructor, passing it the current temperature and distance.

Processing is an object-oriented programming language and allows us to define new classes using the **class** keyword. Classes have a name and they contain data (often called *attributes* or *properties*) and functions (often called *methods*). Our SensorData class contains two attributes named temperature and distance. They are both of type **float**, and we have declared them both **private**. Now only members of the SensorData class are allowed to access them. This is considered good style, because it prevents unwanted side effects and makes future changes much easier. A class should never expose its innards.

To set and get the values of our attributes, we have to use public methods, and our class has three of them: SensorData(), getTemperature(), and getDistance(). (Java and C++ programmers should note that in Processing everything is public if not specified otherwise!) A method that has the same name as the class is called a *constructor*, and you can use it for creating and initializing new objects of that particular class. Constructors do not have return values, but they may specify parameters. Ours, for example, takes two arguments and uses them to initialize our two attributes.

There’s a small problem, though: our method’s parameters have the same names as our classes’ attributes. What would happen if we simply assigned the method parameters to the attributes like this:

```
temperature = temperature;
distance = distance;
```

Right: we simply assigned every method parameter to itself, which is effectively a no-operation. That’s why we use the **this** keyword. It refers to the class itself, so we can distinguish between the method parameters and the classes’ attributes. Alternatively, we could have used different names for the method parameters or the attributes, but I prefer to use **this**.

After the constructor, we define the methods getTemperature and getDistance. Their definitions are very similar; we declare the method’s return type (**float**), the method’s name, and a list of parameters in parentheses. In our case, the parameter list is empty. In the methods, we return the

current value of the corresponding attributes using the **return** keyword. **return** stops the method and returns its argument to the method’s caller.

Now we can create and initialize new SensorData objects:

```
SensorData sensorData = new SensorData(31.5, 11.76);
```

The previous statement creates a new SensorData object named sensorData. It sets temperature to 31.5 and distance to 11.76. To read those values, we use the corresponding “get” methods:

```
sensorData.getTemperature(); // -> 31.5
sensorData.getDistance();    // -> 11.76
```

Because getTemperature() and getDistance() are members of the SensorData class, you can only invoke them using an instance of the class. Our instance is named sensorData, and to call the “get” methods we have to use the instance name, followed by a dot, followed by the method name.

Now that we can store sensor data, we’ll continue to build our inverted sonar application in the next section.

## 5.7 Building the Application’s Foundation

In this section, we’ll create all the boilerplate code we need for our application by importing some libraries and defining some global constants and variables:

Download ultrasonic/InvertedSonar/InvertedSonar.pde

```
import processing.serial.*;

final int WIDTH = 1000;
final int HEIGHT = 1000;
final int xCenter = WIDTH / 2;
final int yCenter = HEIGHT / 2;
final int LINE_FEED = 10;

Serial arduinoPort;
SensorData sensorData;
int degree = 0;
int radius = 0;
```

To communicate with the Arduino via a serial port, we import Processing’s support for serial communication in the first line. The **import** statement imports all classes from the processing.serial package and makes them available in our program.

Our application will have a 1000x1000 pixel screen, so we define constants for its width, height, and its center. We set the LINE_FEED constant to the ASCII value of a linefeed character, because we need it later to interpret the data sent by the Arduino.

Then we define a few global variables (yes, you Java programmers out there: Processing allows you to define global variables!):

- *arduinoPort*: An instance of Processing’s Serial class. It’s from the processing.serial package we have imported and encapsulates the serial port communication with the Arduino.
- *sensorData*: The current sensor data that have been transferred from the Arduino to our application. We use the SensorData class we defined in Section 5.6, *Representing Sensor Data*, on page 123.
- *degree*: We will visualize the current distance to the nearest object on a circle. This variable stores on which degree of the circle we are right now. Values range from 0 to 359.
- *radius*: The current distance to the nearest object is interpreted as a radius value.

## 5.8 Implementing Serial Communication in Processing

The following functions read data from the serial port the Arduino is connected to, and they interpret the data the Arduino is sending:

Download ultrasonic/InvertedSonar/InvertedSonar.pde

```
void setup() {
  size(WIDTH, HEIGHT);
  println(Serial.list());
  String arduinoPortName = Serial.list()[0];
  arduinoPort = new Serial(this, arduinoPortName, 9600);
  arduinoPort.bufferUntil(LINE_FEED);
}

void serialEvent(Serial port) {
  sensorData = getSensorData();
  if (sensorData != null) {
    println("Temperature: " + sensorData.getTemperature());
    println("Distance: " + sensorData.getDistance());
    radius = min(300, int(sensorData.getDistance() * 2));
  }
}

SensorData getSensorData() {
```

```
SensorData result = null;
if (arduinoPort.available() > 0) {
    final String arduinoOutput = arduinoPort.readStringUntil(LINE_FEED);
    result = parseArduinoOutput(arduinoOutput);
}
return result;
}

SensorData parseArduinoOutput(final String arduinoOutput) {
    SensorData result = null;
    if (arduinoOutput != null) {
        final int[] data = int(split(trim(arduinoOutput), ','));
        if (data.length == 2)
            result = new SensorData(data[0] / 100.0, data[1] / 100.0);
    }
    return result;
}
```

setup() is one of Processing’s standard functions and has the same meaning as the Arduino’s setup() method. The Processing runtime environment calls it only once at application startup time and initializes the application. With the size() method, we create a new screen having a certain width and height (by the way, you can find excellent reference material for all Processing classes online⁶).

After initializing the screen, we prepare the serial port communication. First we print a list of all serial devices that are currently connected to the computer using Serial.list(). Then we set the name of the serial port we are going to use to the first list entry. This might be the wrong port, so either you hard-code the name of your system’s serial port into the code or you have a look at the list of serial ports and choose the right one!

In line 5, we create a new Serial object that is bound to our application (that’s what this is for). We use the serial port name we have from the list of all serial ports and set the baud rate to 9600. If you’d like to communicate faster, you have to change both the baud rate here and in the Arduino sketch.

Finally, we tell the Serial object that we want to be notified of new serial data only when a linefeed has been detected. Whenever we find a linefeed, we know that a whole line of data was transmitted by the Arduino.

For our application, we chose an asynchronous programming model; that is, we do not poll for new data in a loop but get notified whenever

6. http://processing.org/reference/
