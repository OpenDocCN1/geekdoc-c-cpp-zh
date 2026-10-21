This is a very simple HTML page, and we'll focus on the JavaScript parts. In lines 4 to 12, we define two things: a global variable named serial and a function named setup(). setup() initializes serial and assigns a Seriality object to it. We embed a Seriality object into the web page using the <object> tag. Its ID is "seriality," so we can access it using getElementById().

As soon as we have a reference to the object, we call JavaScript's alert() function and output all serial ports we have found. You have to look up the index of the serial port your Arduino is connected to and use it in the following call to the begin() method. For simplicity, we always pass it the first serial device we can find and a baud rate of 9,600. Using the first serial device is only a guess, and you might have to adjust it. You already know that pattern from our Processing examples.

We invoke setup() in the onload event handler of the <body> element. Then we can access the Seriality object in the onclick handlers of our six <button> elements.

Upload sketch from Section 9.4, Building Your Own Apple Remote, on page 209 to your Arduino, and point your browser to the HTML page. After you have clicked the OK button of the alert box showing all serial ports, you should see a web page like Figure 9.7, on the following page. Click any button to perform the corresponding action. That's an interface even your Grandma could use, isn't it?

Please note that you cannot access the Arduino hardware directly using Seriality. You can only access the serial port, so all the things you'd like to happen on your Arduino have to be accessible via serial communication. But that's a common pattern anyway, so Seriality is really a useful tool that can greatly improve your project's user interface.

You still need to connect the Arduino to your computer's serial port to control it with a web browser. In the next section, you'll learn how to overcome this and control an Arduino, without a serial connection.



All our previous remote control approaches have one major drawback: they all depend on a serial connection to a PC. In this section, you'll learn how to replace this connection with an Ethernet connection, so you no longer need a PC but only Internet access. You will directly plug