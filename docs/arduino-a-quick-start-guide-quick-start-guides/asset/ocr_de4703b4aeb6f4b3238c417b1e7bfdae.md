there’s new data on the serial port (to be concise, we want to be notified only if a new linefeed was found). This way, we can change our application’s state in real time and can prevent disturbing delays between the arrival of data and graphics updates on the screen.

When new data arrives, serialEvent() gets called automatically and is passed the serial port the data was found on. We have only one port, so we can ignore this parameter. We try to read the current sensor data using getSensorData(), and if we find some, we print them to the console for debugging purposes and set the radius to the measured distance. To make the visualization more appealing, we multiply the distance by two, and we cut values bigger than 300 centimeters.

getSensorData()’s implementation is fairly simple. First it checks to see if data is available on the serial port in line 20. This might look redundant, because this method gets called only if data is available, but if we’d like to reuse it in a synchronous context, the check is necessary. Then we read all data until we find a linefeed character and pass the result to parseArduinoOutput().

Parsing the output is easy because of Processing’s split() method. We use it in line 30 to split the line of text we get from the Arduino at the comma (trim() removes trailing and leading whitespace characters). It returns a two-element array containing the textual representation of two integer values. These strings are turned into integers afterward using int(). Please note that in our case int() takes an array containing two strings and returns an array containing two int values.

Because it’s possible that we have an incomplete line of text from the Arduino (the serial communication might start at an arbitrary byte position), we’d better check whether we actually got two sensor values. If yes, we create a new SensorData object and initialize it with the temperature and distance (after we have divided them by 100).

That’s all we need to read the sensor data asynchronously from the Arduino. From now on, sensor data will be read whenever it’s available, and the global sensorData and radius variables will be kept up-to-date automatically.

# 5.9 Visualizing Sensor Data

Now that the serial communication between our computer and the Arduino works, let’s visualize the distance to the nearest object: