
## Who's to blame?

![](img/dcfd13a1bf99c4d3f9996627012a6526_229_0.png)

Figure 10.5: The Blaminatr: blaming has never been easier.

A class named Team that represents the members of our team; that is, the potential “blamees”:

Download Motors/Blaminat/Blaminat.pde

```
const unsigned int MAX_MEMBERS = 10;
class Team {
    char** _members;
    int _num_members;
    int _positions[MAX_MEMBERS];

public:

    Team(char** members) {
        _members = members;

        _num_members = 0;
        char** member = _members;
        while (*member++)
            _num_members++;

        const int share = 180 / _num_members;
        int pos = share / 2;
        for (int i = 0; i < _num_members; i++) {
            _positions[i] = pos;
            pos += share;
        }
    }

    int get_position(const char* name) const {
        int position = 0;
        for (int i = 0; i < _num_members; i++) {
            if (!strcmp(_members[i], name)) {
                position = _positions[i];
                break;
            }
        }
        return position;
    }
};
```

The code defines several member variables: _members contains a list of up to ten team member names, _num_members contains the actual number of people on the team, and we store the position (angle) of the team member's name on the Blaminatr display in _positions.

The constructor expects an array of strings that contains the team members' names and that is terminated by a NULL pointer. We store a reference to the list, and then we calculate the number of team members. We iterate over the array until we find a NULL pointer. All this happens in lines 13 to 16.

Then we calculate the position of each team member's name on the Blaminatr's display. Every team member gets their fair share on the 180-degree display, and the Blaminatr will point to the share's center, so we divide the share by 2. We store the positions in the _positions array that corresponds to the _members array. That means the first entry of _positions contains the position of the first team member, and so on.

With the get_position() method, we get back the position belonging to a certain name. We walk through the _members array and check whether we have found the right member using the strcmp() function. As soon as we've found it, we return the corresponding entry of the _positions array. If we couldn't find a team member with the name we are looking for, we return 0.

Implementing a Blaminatr class is easy now:

```
#include <Servo.h>

const unsigned int MOTOR_PIN = 9;
const unsigned int MOTOR_DELAY = 15;

class Blaminatr {
    Team _team;
    Servo _servo;

public:

    Blaminatr(const Team& team) : _team(team) {}

    void attach(const int sensor_pin) {
        _servo.attach(sensor_pin);
        delay(MOTOR_DELAY);
    }

    void blame(const char* name) {
        _servo.write(_team.get_position(name));
        delay(MOTOR_DELAY);
    }
};
```

A Blaminatr object aggregates a Team object and a Servo object. The constructor initializes the Team instance while we can initialize the Servo instance by calling the attach() method.

The most interesting method is blame(). It expects the name of the team member to blame, calculates his position, and moves the servo accordingly. Let’s put it all together now:

```
const unsigned int MAX_NAME = 30;
const unsigned int BAUD_RATE = 9600;
const unsigned int SERIAL_DELAY = 5;

char* members[] = { "nobody", "Bob", "Alice", "Maik", NULL };
Team team(members);
Blaminatr blaminatr(team);

void setup() {
    Serial.begin(BAUD_RATE);
    blaminatr.attach(MOTOR_PIN);
    blaminatr.blame("nobody");
}

void loop() {
    char name[MAX_NAME + 1];

    if (Serial.available()) {
        int i = 0;
        while (Serial.available() && i < MAX_NAME) {
            const char c = Serial.read();
            if (c != -1 && c != '\n')
                name[i++] = c;
            delay(SERIAL_DELAY);
        }
        name[i] = 0;
        Serial.print(name);
        Serial.println(" is to blame.");
        blaminatr.blame(name);
    }
}
```

We define a list of member names that is terminated by a NULL pointer. The list's first entry is "nobody," so we don't have to deal with the rare edge case when nobody is to blame. Then we use members to initialize a new Team object and pass this object to the Blaminatr's constructor.

In the setup() function, we initialize the serial port and attach the Blaminatr's servo motor to the pin we defined in MOTOR_PIN. Also, we initialize the Blaminatr by blaming "nobody."

The loop() function is nearly the same as in Section 10.3, First Steps with a Servo Motor, on page 225. The only difference is that we do not control a servo directly but call blame() in line 28.

That's it! You can now start to draw your own display and create your own arrow. Attach them directly to the motor or—even better—put everything into a nice box. Compile and upload the software and start to blame.

Of course, you can use motors for more serious projects. For example, you can use them to build robots running on wheels or similar devices. But you cannot attach too many motors to a "naked" Arduino, because it is not meant for driving bigger loads. So if you have a project in mind that needs a significant number of motors, you should consider buying a motor shield⁶ or use a special shield such as the Roboduino.⁷

## 10.5 What If It Doesn't Work?

Working with motors is surprisingly easy, but still a lot of things can go wrong. The biggest problem is that motors consume a lot of power, so you cannot simply attach every motor to an Arduino. Also, you cannot easily drive more than one motor, especially not with the small amount of power you get from a USB port. If your motor does not run as expected, check its specification, and attach an AC or DC adapter to your Arduino if necessary.

### More Motors Projects

Motors are fascinating. Search the 'net and you’ll find numerous projects combining the Arduino with them. A fun project is the Arduino Hypnodisk.\* It uses a servo motor to rotate a hypno disc—a rotating disk with a spiral printed on it that has a hypnotic effect. An infrared rangefinder changes the motor’s speed, so the closer you get to the disc, the faster it spins.

A useful and exciting project is the USB hourglass.† It uses an Arduino and a servo motor to turn a sand timer, and it observes the falling sand using an optical sensor. Whenever all the sand has fallen through, the device turns the timer automatically.

That’s all nice, but the device’s main purpose is to generate true random numbers. Falling sand is a perfect basis for generating true randomness (see the sidebar on page 73), and the USB hourglass uses the signals from its optical sensor to generate random numbers, sending them to the serial port.

You also shouldn’t attach too much weight to your motor. Moving an arrow made of paper is no problem, but you might run into problems if you attach bigger and heavier things. Also, be careful not to put any obstacles into the motor’s way. The motor’s shaft always needs to move freely.

Some motors have to be adjusted from time to time, and usually you have to do that with a very small screw driver. Refer to the motor’s specification for detailed instructions.

## 10.6 Exercises

- Add an Ethernet shield to the Blaminatr so you can blame people via Internet and not only via the serial port. Pointing your web browser to an address such as http://192.168.1.42/blame/Maik should blame me, for example.

- Create a thermometer based on a TMP36 temperature sensor and a servo motor. Its display could look like Figure 10.6; that is, you have to move an arrow that points to the current temperature.

  ![](img/dcfd13a1bf99c4d3f9996627012a6526_234_0.png)

- Use an IR receiver to control the Blaminatr. For example, you could use the channel key of your TV set's remote control to proceed the Blaminatr from one name to the other.

## Appendix A: Basics of Electronics

We didn’t need a lot of theory or background to create our first Arduino projects. But it’s a good idea to learn a bit about electricity and about soldering if you want to build bigger and more sophisticated projects.

In this appendix, you’ll learn the basics of electricity, and you’ll learn about Ohm’s law, which is probably the most important law in electronics. Also, you’ll learn more about resistors, and you’ll see that soldering isn’t as difficult as it might seem.

### A.1 Current, Voltage, and Resistance

To build your first projects with the Arduino, you didn’t need to know much about electricity. But at some point, you’ll need to understand what current, voltage, and resistance is all about. For example, you already know that you always have to put a resistor in front of an LED, but you might not know exactly why, and you might not know how to calculate the resistor’s size for a given LED. Let’s remedy that.

An electrical circuit resembles a water circuit in many respects. In Figure A.1, on the following page, you can see a water circuit on the left and an electrical circuit on the right. Isn’t it fascinating how similar they are and that you can even find a connection between them when you use a water-driven dynamo that acts as a power supply? Let’s take a closer look at their most important attributes.

While water flows in a water circuit, electrons flow in an electrical circuit. Voltage is electricity’s equivalent of water pressure and is measured in volts (V). Voltage is the initial cause for a current, and the higher the voltage, the faster the current flows.
