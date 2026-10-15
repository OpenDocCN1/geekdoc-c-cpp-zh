
PP 2.3 Write an application that prompts for and reads a person’s name, age, college, and pet’s name. Then print the following paragraph, inserting the appropriate data:
Hello, my name is name and I am age years old. I’m enjoying my time at college, though I miss my pet petname very much!

PP 2.4 Write an application that reads two floating point numbers and prints their sum, difference, and product.

PP 2.5 Create a version of the TempConverter application to convert from Fahrenheit to Celsius. Read the Fahrenheit temperature from the user.

PP 2.6 Write an application that converts miles to kilometers. (One mile equals 1.60935 kilometers.) Read the miles value from the user as a floating point value.

PP 2.7 Write an application that prompts for and reads integer values for speed and distance traveled, then prints the time required for the trip as a floating point result.

PP 2.8 Write an application that reads values representing a time duration in hours, minutes, and seconds and then prints the equivalent total number of seconds. (For example, 1 hour, 28 minutes, and 42 seconds is equivalent to 5322 seconds.)

PP 2.9 Create a version of the previous project that reverses the computation. That is, read a value representing a number of seconds, then print the equivalent amount of time as a combination of hours, minutes, and seconds. (For example, 9999 seconds is equivalent to 2 hours, 46 minutes, and 39 seconds.)

PP 2.10 Write an application that determines the value of the coins in a jar and prints the total in dollars and cents. Read integer values that represent the number of quarters, dimes, nickels, and pennies.

PP 2.11 Write an application that prompts for and reads a double value representing a monetary amount. Then determine the fewest number of each bill and coin needed to represent that amount, starting with the highest (assume that a ten-dollar bill is the maximum size needed). For example, if the value entered is 47.63 (forty-seven dollars and sixty-three cents), then the program should print the equivalent amount as:
4 ten dollar bills
1 five dollar bills
2 one dollar bills

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_136_0.png)

```
2 quarters
1 dimes
0 nickels
3 pennies
```

PP 2.12 Write an application that prompts for and reads an integer representing the length of a square’s side, then prints the square’s perimeter and area.

PP 2.13 Write an application that prompts for and reads the numerator and denominator of a fraction as integers, then prints the decimal equivalent of the fraction.

PP 2.14 Create a revised version of the Snowman applet with the following modifications:

- Add two red buttons to the upper torso.
- Make the snowman frown instead of smile.
- Move the sun to the upper-right corner of the picture.
- Display your name in the upper-left corner of the picture.
- Shift the entire snowman 20 pixels to the right.

PP 2.15 Write an applet that writes your name using the drawString method. Embed a link to your applet in an HTML document and view it using a Web browser.

PP 2.16 Write an applet that draws the Big Dipper. Add some extra stars in the night sky.

PP 2.17 Write an applet that draws some balloons tied to strings. Make the balloons various colors.

PP 2.18 Write an applet that draws the Olympic logo. The circles in the logo should be colored, from left to right, blue, yellow, black, green, and red.

PP 2.19 Write an applet that draws a house with a door (and doorknob), windows, and a chimney. Add some smoke coming out of the chimney and some clouds in the sky.

PP 2.20 Write an applet that displays a business card of your own design. Include both graphics and text.

PP 2.21 Write an applet that displays your name in shadow text by drawing your name in black, then drawing it again slightly offset in a lighter color.

PP 2.22 Write an applet that shows a pie chart with eight equal slices, all colored differently.

## SOFTWARE FAILURE

### NASA Mars Climate Orbiter and Polar Lander

### What Happened?

As part of a series of missions exploring Mars, NASA launched the Mars Climate Orbiter in December, 1998, and the Mars Polar Lander in January, 1999. The two-spacecraft mission was designed to observe the atmospheric conditions on Mars through each of its seasons. The orbiter and the lander would have collected data about temperature, dust, water vapor, clouds, and the amount of carbon dioxide (CO2) added and removed from the Martian pole regions.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_138_0.png)

After its nine-month journey, the orbiter arrived at Mars in September, 1999, and fired its main engines to establish an orbit. The orbiter passed behind the planet (from Earth’s perspective) five minutes later as planned, but NASA could not reestablish contact with it after expecting it to emerge. Review of the data showed that the altitude of the orbiter when it was entering orbit was only 57 kilometers, whereas the planned altitude was 140 kilometers. The minimum survivable altitude was between 85 and 100 kilometers. NASA concluded that the orbiter was destroyed by atmospheric friction.

The polar lander arrived at Mars in December, 1999, and all of the data indicated it was on target to make a successful soft landing within 10 kilometers of the target landing site on the Martian south pole. However, NASA lost contact with the lander just after it entered the atmosphere. Multiple attempts to reestablish contact with it over the following weeks and months were unsuccessful.

The total project cost for the orbiter and lander was $327.6 million.

### What Caused It?

The root cause of the orbiter’s problem was an embarrassing communication issue. The software that guided the navigation of the spacecraft used imperial units of measure (pound-force), while the spacecraft itself expected the data in metric units (newtons). Therefore the desired navigation changes and the actual effects were off by a factor of 4.45. This mismatch resulted in part because one team based in Colorado led the efforts on the spacecraft, while a California-based team managed issues of navigation.

Artist’s conception of the Mars Climate Orbiter

The cause of the lander’s communication problem is unresolved but is not believed to be related to the orbiter’s problem. The investigation concluded that the most likely cause was a software error that mistook the vibration caused by the deployment of the lander’s legs for the vibration caused by actually landing on the planet’s surface. That mistake would have caused the lander’s descent engines to cut off while it was still 40 meters above the ground. Other problem scenarios are possible, however.

### Lessons Learned

The mismatch of units in the Mars Climate Orbiter shows that seemingly obvious problems can be overlooked in a highly complex system. Mistakes are inevitable, but processes must be in place to catch them before they become critical. The investigation concluded that, in this case, the system for tracking and double-checking interconnected elements between subsystems was not robust enough. There was also inconsistent training of and communication with new members of the team, and some communication lines were too informal. In short, the mission lacked a rigorous total-system view that would have led to the discovery of the mismatched units problem before it was too late.

It’s difficult to draw strong conclusions from the lander’s problem given that the cause is not clearly understood. The fact that it remains an open question underscores the need for more evaluation, simulation, and testing in situations where critical resources are at stake.

> Source: nasa.gov

## Using Classes and Objects

### CHAPTER OBJECTIVES

- Discuss the creation of objects and the use of object reference variables.
- Explore the services provided by the String class.
- Describe how the Java standard class library is organized into packages.
- Explore the services provided by the Random and Math classes.
- Discuss ways to format output using the NumberFormat and DecimalFormat classes.
- Introduce enumerated types.
- Discuss wrapper classes and the concept of autoboxing.
- Introduce components and containers used in graphical user interfaces.
- Describe a label component and the use of images.

This chapter further explores the use of predefined classes and the objects we can create from them. Using classes and objects for the services they provide is a fundamental part of object-oriented software and sets the stage for writing classes of our own. In this chapter, we use classes and objects to manipulate character strings, produce random numbers, perform complex calculations, and format output. This chapter also introduces the concept of an enumerated type, which is a special kind of class in Java, and discusses the concept of a wrapper class. In the Graphics Track of this chapter, we lay the foundation for developing graphical user interfaces for our programs and discuss how to display images.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_140_0.png)
