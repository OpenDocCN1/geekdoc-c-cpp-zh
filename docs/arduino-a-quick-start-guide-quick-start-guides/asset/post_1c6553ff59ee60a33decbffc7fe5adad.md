
## 2.6 Exercises

- Add new commands to the sample program. For example, the command 3 could make the LED blink for a while.
- Try to make the commands more readable; that is, instead of 1, use the command on, and instead of 2, use off.

If you have problems solving this exercise, read Chapter 4, Building a Morse Code Generator Library, on page 88 first.

## Part II

## Eight Arduino Projects

## Chapter 3

## Building Binary Dice

Things will really start to get interesting now that you've learned the basics of Arduino development. You now have the skills to create your first complex, stand-alone projects. After you have worked through this chapter, you'll know how to work with LEDs, buttons, breadboards, and resistors. Combining these parts with an Arduino gives you nearly endless opportunities for new and cool projects.

Our first project will be creating an electronic die. While regular dice display their results using one to six dots, ours will use LEDs instead. For our first experiments, a single LED has been sufficient, but for the dice we need more than one. You need to connect several external LEDs to the Arduino. Because you cannot attach them all directly to the Arduino, you'll learn how to work with breadboards. Also, you need a button that rolls the dice, so you'll learn how to work with pushbuttons, too. To connect pushbuttons and LEDs to the Arduino, you need another important electronic part: the resistor. So, at the end of the chapter, you'll have many new tools in your toolbox.

- 1. A half-size breadboard
- 2. Three LEDs (for the exercises you'll need additional LEDs)
- 3. Two 10kΩ resistors (see Section A.1, Current, Voltage, and Resistance, on page 237 to learn more about resistors)
- 4. Three 1kΩ resistors
- 5. Two pushbuttons
- 6. Some wires

![](img/dcfd13a1bf99c4d3f9996627012a6526_63_0.png)

Figure 3.1: All the parts you need for this chapter

- 7. An Arduino board such as the Uno, Duemilanove, or Diecimila
- 8. A USB cable to connect the Arduino to your computer
- 9. A tilt sensor (optional)

Figure 3.1 shows the parts needed to build the projects in this chapter. You'll find such photos in most of the following chapters. The numbers in the photo correspond to the numbers in the parts list. The photos do not show standard parts such as the Arduino board or an USB cable.

### 3.2 Working with Breadboards

Connecting parts such as LEDs directly to the Arduino is only an option in the most trivial cases. Usually, you will prototype your projects on a breadboard that you connect to the Arduino. A breadboard “emulates”

![](img/dcfd13a1bf99c4d3f9996627012a6526_64_0.png)

# Figure 3.2: A collection of breadboards

a circuit board. You don't have to solder parts to the board; instead, you can simply plug them into it.

Breadboards come in various types and sizes (in Figure 3.2, you can see two of them), but they all work the same way. They have a lot of sockets that you can use for plugging in through-hole parts or wires. That alone wouldn't be a big deal, but the sockets are connected in a special way. In Figure 3.3, on the next page, you can see how.

As you can see, most sockets are connected in columns. If one socket of a column is connected to a power supply, then automatically all the other sockets in this column are powered, too. On the bigger board in the photo, you can also see four rows of connected sockets. This is convenient for bigger circuits. Usually, you connect one row to your power supply and one to the ground. This way, you can distribute power and ground to any point on the board. Now let's see how to put parts on a breadboard.

![](img/dcfd13a1bf99c4d3f9996627012a6526_65_0.png)

Figure 3.3: How sockets on a breadboard are connected

### 3.3 Using an LED on a Breadboard

Up to now, we used the LEDs that are installed on the Arduino board, and we connected one LED directly to the Arduino. In this section, we'll plug an LED into a breadboard and then connect the breadboard to the Arduino.

In Figure 3.4, on the following page, you can see a photo of our final circuit. It consists of an Arduino, a breadboard, an LED, three wires, and a 1kΩ resistor (more on that part in a few minutes). Connect the Arduino to the breadboard using two wires. Connect pin 12 with the ninth column of the breadboard, and connect the ground pin with the tenth column. This automatically connects all sockets in column 9 to pin 12 and all sockets in column 10 to the ground. This choice of columns was arbitrary, and you could have used other columns instead.

Plug the LED's negative connector (the shorter one) into column 10 and its positive connector into column 9. When you plug in parts or wires into a breadboard, you have to press them firmly until they slip in. You

![](img/dcfd13a1bf99c4d3f9996627012a6526_66_0.png)

Figure 3.4: Connecting an LED on a breadboard to the Arduino

might need more than one try, especially on new boards, and it often comes in handy to shorten the connectors before plugging them into the breadboard. Make sure that you can still identify the negative and the positive connector after you have shortened them. Shorten the negative one a bit more, for example. Also wear safety glasses to protect your eyes when cutting the connectors!

The things we have done until now have been straightforward. That is, in principle we have only extended the Arduino's ground pin and its IO pin number 12. Why do we have to add a resistor, and what is a resistor? A resistor limits the amount of current that flows through an electric connection. In our case, it protects the LED from consuming too much power, because this would destroy the LED. You always have to use a resistor when powering an LED! In Section A.1, Current, Voltage, and Resistance, on page 237, you can learn more about resistors and their color bands. In Figure 3.5, you can see a resistor in various stages: regular, bent, and cut.

![](img/dcfd13a1bf99c4d3f9996627012a6526_67_0.png)

Figure 3.5: A resistor in various processing stages

You might ask yourself why we didn't have to use a resistor when we connected the LED directly to the Arduino. The answer is simple: pin 13 comes with an internal resistor of 1kΩ. Now that we use pin 12, we have to add our own resistor.

We don't want to fiddle around too much with the connectors, so we build the circuit as shown in Figure 3.6, on the next page. That is, we use both sides of the breadboard by connecting them with a short wire. Note that the resistor bridges the sides, too.

![](img/dcfd13a1bf99c4d3f9996627012a6526_68_0.png)

Figure 3.6: You can use both sides of a breadboard.

### 3.4 First Version of a Binary Die

You’re certainly familiar with regular dice displaying results in a range from one to six. To emulate such dice exactly with an electronic device, you’d need seven LEDs and some fairly complicated business logic. We’ll take a shortcut and display the result of a die roll in binary.

For a binary die, we need only three LEDs that represent the current result. We turn the result into a binary number, and for every bit that is set, we will light up a corresponding LED. The following diagram shows how the die results are mapped to LEDs (a black triangle stands for a shining LED).

![](img/dcfd13a1bf99c4d3f9996627012a6526_69_0.png)

We already know how to control a single LED on a breadboard. Controlling three LEDs is similar and requires only more wires, LEDs, 1kΩ resistors, and pins. In Figure 3.7, on the following page, you can see the first working version of a binary die.

The most important difference is the common ground. When you need ground for a single LED, you can connect it to the LED directly. But we need ground for three LEDs now, so we’ll use the breadboard’s rows for the first time. Connect the row marked with a hyphen (-) to the Arduino’s ground pin, and all sockets in this row will work as ground pins, too. Then you can connect this row’s sockets to the LEDs using short wires.

Everything else in this circuit should look familiar, because we only had to clone the basic LED circuit from the previous section three times. Note that we have connected the three circuits to pins 10, 11, and 12. The only thing missing is some software:

```
Download BinaryDice/BinaryDice.pde
Line 1 const unsigned int LED_BIT0 = 12;
const unsigned int LED_BIT1 = 11;
const unsigned int LED_BIT2 = 10;
5 void setup() {
    pinMode(LED_BIT0, OUTPUT);
    pinMode(LED_BIT1, OUTPUT);
    pinMode(LED_BIT2, OUTPUT);
10    randomSeed(analogRead(A0));
    long result = random(1, 7);
    output_result(result);
}
15 void loop() {
}
void output_result(const long result) {
    digitalWrite(LED_BIT0, result & B001);
20    digitalWrite(LED_BIT1, result & B010);
    digitalWrite(LED_BIT2, result & B100);
}
```
