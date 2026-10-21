
![](img/dcfd13a1bf99c4d3f9996627012a6526_84_0.png)

## Figure 3.12: We have a winner!

Bounce class for the first time. To determine the current state of our guess_button object, we have to call its update() method. afterward, we read its current status using the read() method.

If the button was pressed, its state is set to HIGH, and we increment the guess variable. To make sure that the guess is always in the range between 1 and 6, we use the modulus operator (%) in line 33. This operator divides two values and returns the remainder. For 6, it returns values between 0 and 5, because when you divide a number by 6, the remainder is always between 0 and 5. Add 1 to the result, and you get values between 1 and 6. Finally, we output the current guess using the three LEDs, and we also print it to the serial port.

The handling of the start button in handle_start_button() works exactly the same as the handling of the guess button. When the start button was pressed, we calculate a new result and output it on the serial port. Then we check whether the user has entered a guess (guess is greater than zero in this case) and whether the user has guessed the right result. In either case, we print a message to the serial port, and if the user guessed right, we also call the hooray() method. hooray() lets all three LEDs blink several times.

At the end of the method, we wait for two seconds until the game starts again, and we set back the current guess to zero.

After you’ve uploaded the software to the Arduino, start the IDE’s serial monitor. It will print the current value of the guess variable whenever you press the guess button. Press the start button, and the new result appears. In Figure 3.12, on the preceding page, you can see a typical output of our binary dice.

In this chapter, you completed your first really complex Arduino project. You needed a breadboard, LEDs, buttons, resistors, and wires, and you wrote a nontrivial piece of software to make all the hardware come to life.

In the next chapter, we’ll write an even more sophisticated program for generating Morse code. You’ll also learn how to create your own Arduino libraries that you can easily share with the rest of the world.

## 3.8 What If It Doesn’t Work?

A lot of things will probably go wrong when you work with breadboards for the first time. The biggest problem usually is that you didn’t connect parts correctly. It takes some time to find the right technique for plugging LEDs, wires, resistors, and buttons into the breadboard. You have to press firmly but not too hard—otherwise you’ll bend the connectors, and they won’t fit. It’s usually easier to plug parts in after you’ve shortened the connectors. When cutting the connectors, wear safety glasses to protect your eyes!

While fiddling around with the parts, don’t forget that some of them—LEDs, for example—need a certain direction. Pushbuttons are candidates for potential problems, too. Take a close look at the pushbuttons on page 74 and make sure that you’ve mounted them in the right direction.

Even simple things such as ordinary wires can lead to problems, especially if they aren’t the right length. If a wire is too short and might potentially slip out of its socket, replace it immediately. Wires are too cheap to waste your valuable time with unnecessary and annoying debugging sessions.

## 3.9 Exercises

- Binary dice are all very well when you're playing Monopoly with your geeky friends, but most people prefer more familiar dice. Try turning binary dice into decimal dice with seven LEDs. Arrange the LEDs like the eyes on regular dice.

- The 1kΩ resistors we have used to protect our LEDs in this chapter are rather big. Read Section A.1, *Resistors*, on page 239, and replace them with smaller ones. Can you see the difference in brightness?

- LEDs can be used for more than displaying binary dice results. Provided you have enough LEDs, you can easily build other things, such as a binary clock.²

You already know enough about electronics and Arduino programming to build your own binary clock. Try it or think about other things you could display using a few LEDs.

- Using a button to roll the dice seems a bit awkward, doesn't it? Usually, you take dice into both hands and shake them. You can easily simulate that with a tilt sensor.

Tilt sensors detect the tilting of an object and are perfect devices for simulating the roll of a dice. In principle, they work like a push-button, but you don't press them—you shake them. Try to add one to the binary dice by working your way through the tutorial on the Arduino website.³

2. http://www.instructables.com/id/LED-Binary-Clock/
3. http://www.arduino.cc/en/Tutorial/TiltSensor

## Chapter 4

## Building a Morse Code Generator Library

You now know enough about the Arduino development environment and about blinking LEDs to start a bigger project. In this chapter, we’ll develop a Morse code generator that reads text from the serial port and outputs it as light signals using an LED.

By building this project, you’ll deepen your understanding of serial communication between the Arduino and your computer. You’ll also learn a lot about the typical Arduino development process: how to use existing libraries and how to structure bigger projects into your own libraries. At the end, you’ll be able to create a library that is ready for publishing on the Internet.

## 4.1 What You Need

- An Arduino board such as the Uno, Duemilanove, or Diecimila
- A USB cable to connect the Arduino to your computer
- An LED
- A speaker or a buzzer (they are optional)

## 4.2 Learning the Basics of Morse Code

Morse code was invented to turn text into sounds.¹ In principle, it works like a character set encoding such as ASCII. But while ASCII

encodes characters as numbers, in Morse code they're sequences of dots and dashes (also called dits and dahs). Dits are shorter in length than dahs. An A is encoded as · – and – – · · is Z.

Morse code also specifies a timing scheme that defines the length of the dits and dahs. It also specifies how long the pauses between symbols and words have to be. The base unit of Morse code is the length of a dit, and a dah is as long as three dits. You insert a pause of one dit between two symbols, and you separate two letters by three dits. Insert a pause of seven dits between two words.

To transmit a message encoded in Morse code, you need a way to emit signals of different lengths. The classic approach is to use sounds, but we will use an LED that is turned on and off for varying periods of time. Sailors still transmit Morse code using blinking lights.

Let’s implement a Morse code generator!

## 4.3 Building a Morse Code Generator

The main part of our library will be a C++ class named Telegraph. In this section, we'll define its interface, but we will start with a new sketch that looks as follows:

Download Telegraph/telegraph.pde

```
void setup() {
}

void loop() {
}
```

This is the most minimalistic Arduino program possible. It does not do anything except define all mandatory functions, even if they are empty. We do this so we can compile our work in progress from time to time and check whether there are any syntactical errors. Save the sketch as Telegraph, and the IDE will create a folder named Telegraph and a file named Telegraph.pde in it. All the files and directories we need for our library will be stored in the Telegraph folder.

Now open a new tab, and when asked for a filename, enter telegraph.h. Yes, we will create a good old C header file (to be precise, it will even be a C++ header file). The listing in on the next page.

```
```cpp
#ifndef __TELEGRAPH_H__
#define __TELEGRAPH_H__

class Telegraph {
public:
	Telegraph(const int output_pin, const int dit_length);
	void send_message(const char* message);
private:
	void dit();
	void dah();
	void output_code(const char* code);
	void output_symbol(const int length);
	int _output_pin;
	int _dit_length;
	int _dah_length;
};
#endif
```
```

Ah, obviously object-oriented programming is not only for the big CPUs anymore! This is an interface description of a Telegraph class that you could use in your next enterprise project (provided that you need to transmit some information as Morse code, that is).

We start with the classic double-include prevention mechanism; that is, the body of header file defines a preprocessor macro with the name __TELEGRAPH_H__. We wrap the body (that contains this definition) in an #ifndef, so that the body is only compiled if the macro has not been defined. That way, you can include the header as many times as you want, and the body will only be compiled once.

The interface of the Telegraph class consists of a public part that users of the class have access to and a private part only members of the class can use. In the public part, you find two things: a constructor that creates new Telegraph objects and a method named send_message() that sends a message by emitting it as Morse code. In your applications, you can use the class as follows:

```
```cpp
Telegraph telegraph(13, 200);
telegraph.send_message("Hello, world!");
```
```

In the first line, we create a new Telegraph object that communicates on pin 13 and emits dits that are 200 milliseconds long. Then we emit the message "Hello, world!" as Morse code. This way, we are able to send
