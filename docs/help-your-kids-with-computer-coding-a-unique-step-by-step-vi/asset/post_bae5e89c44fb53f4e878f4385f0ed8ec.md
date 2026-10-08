
# How computer programs work

Computers might seem very smart, but they are actually just boxes that follow instructions very quickly and accurately. As intelligent humans, we can get them to carry out different tasks by writing programs, or lists of instructions.

- Computers can't do anything by itself. It's up to the computer programmer to give it instructions.

![](img/72d218a7a73c4d4abc7be582ebd85385_16_0.png)

Without instructions a computer is clueless

- Write a program
You can tell a computer what to do by writing a set of very detailed instructions called a program. Each instruction has to be small enough that the computer can understand it. If the instructions are incorrect, the computer won't behave the way you want to.

This is a computer program counting down to launch

- Programming languages
Computers can only follow instructions in a language they understand. It's up to the programmer to choose which language is best for the task.

![](img/72d218a7a73c4d4abc7be582ebd85385_16_1.png)

```
for count in range(10, 0, -1):
print("Counting down", count)
```

![](img/72d218a7a73c4d4abc7be582ebd85385_16_2.png)

```
for count in range(10, 0, -1):
print("Counting down", count)
```

All programs are finally converted into "binary code", a basic computer language that uses only ones and zeroes

![](img/72d218a7a73c4d4abc7be582ebd85385_16_3.png)

| 1010 | 1011 | 1000 | 1100 |
| 1000 | 0110 | 0100 | 1001 |
| 0100 | 1001 | 0001 | 0101 |

![](img/72d218a7a73c4d4abc7be582ebd85385_16_4.png)

# Hardware and software

"Hardware" means the physical parts of the computer that you can see or touch (all the wires, circuits, the keyboard, the display screen, and so on). "Software" means the programs that run on the computer and control how it works. Software and hardware work together to make computers useful things.

![](img/72d218a7a73c4d4abc7be582ebd85385_16_5.png)

# Think like a computer

A programmer must learn to think like a computer. All tasks must be broken down into small chunks so that they are easy to follow and impossible to get wrong.

# Thinking like a robot

Imagine a café where the waiter is a robot. The robot has a simple computer brain, and needs to be told how to get from the café kitchen to serve food to diners seated at tables. First the process has to be broken down into simple tasks the computer can understand.

SEE ALSO
| 14–15 What is a computer program? |
| Becoming 18–19 coder |

> Algorithm
An algorithm is a set of simple instructions for performing a task. A program is an algorithm that has been translated into a language that computers can understand.

- Waiter robot program 1
Using this program robot grabs the food from the plate, crashes straight through the kitchen wall into the dining area, and puts the food on the floor. This algorithm wasn't detailed enough.

- Pick up food
- Move from kitchen to diner's table
- Put food down

> Disaster!
The instructions weren't clear; we forgot to tell the robot to use the door. It might seem obvious to humans but computers can't think for themselves.

- Waiter robot program 2
This time we've told the robot to use the kitchen door. It makes through the door, but then hits the café cat, trips, and smashes the plate on the floor.

- Pick up a plate with food on it
- Move from kitchen to diner's table by:
- Move to door between kitchen and dining area
- Move from door to the table
- Put plate down on the table in front of the diner

> Still not perfect
The robot doesn't know how to deal with obstacles like the cat. The program needs to give the robot even more detailed instructions so it can move around safely.

# Waiter robot program 3

In this version of the program, the robot successfully delivers the food to the diner avoiding any obstacles. But after putting the plate down, the robot remains standing at the table while food piles up in the kitchen.

- 1. Pick up a plate with food holding it level at all times
- 2. Move from kitchen to diner's table by:
- Move to door between kitchen and dining area
- checking for obstacles and steering around them
- Move from door to the table
- checking for obstacles and steering around them

![](img/72d218a7a73c4d4abc7be582ebd85385_18_0.png)

> Success at last?
The robot can deliver the food safely. But we forgot to give it instructions to go back to the kitchen and get the next plate.

- 3. Put plate down on the table in front of the diner

# Real-world example

The waiter robot might be imaginary, but algorithms like this are in action all around us. For example, a computer-controlled elevator faces the same sort of problems. Should it go up or down? Which floor should it go to next?

![](img/72d218a7a73c4d4abc7be582ebd85385_18_1.png)

- 1. Wait until doors are closed
- 2. Wait for button to be pressed
- If button pressed is higher than current floor:
- Move lift upwards
- If button pressed is lower than current floor:
- Move lift downwards

> Elevator program
For the elevator to work correctly and safely, every step has to be precise, clear, and cover every possibility. The programmers have to make sure they create a suitable algorithm.

- 3. Wait until current floor equals button pressed
- 4. Open doors

# Becoming a coder

Coders are the people who write the programs behind everything.

# Programming languages

There are a huge range of programming languages to choose from. Each one can be used different tasks. Here are some of the most popular languages and what they are used for:

| C | MATLAB | Ideal for programs that need to carry out calculations. |
| Ada | A powerful language for building operating systems. | Used to control spacecraft, satellites, and airplanes. |
| Java | Works on computers, cell phones, and tablets. | Ruby | Automatically turns lots of information into web pages. |
| Scratch | A visual language that's ideal for learning programming. | Javascript | A language used to build interactive websites. |
| Python | A language that can build all kinds things. |

# What is Scratch?

Scratch is a great way to start coding. Programs are created by connecting blocks of code, instead of typing it out. Scratch is quick and easy to use, and also teaches you the key ideas you need to use other languages.

![](img/72d218a7a73c4d4abc7be582ebd85385_19_0.png)

The program appears on this side of the screen connecting colored blocks

# What is Python?

People around the world use Python to build games, tools, and websites. It's a great language to master because it can help you build all kinds of programs. Python looks like a mixture of recognizable words and characters, so it can be easily read and understood by humans.

```
IDLE File Edit Shell Debug Window Help
ghostgame
# Ghost Game
from random import randint
print('Ghost Game')
feeling_brave = True
score = 0
while feeling_brave:
    ghost_door = randint(1, 3)
    print('Three doors ahead...')
```

A program written in Python

# Getting started

It's time to start programming. All you need is a computer with an Internet connection. This book starts with Scratch—the perfect language to help you on your way to becoming a coding expert. Get ready to jump into the exciting world of computer coding.

![](img/72d218a7a73c4d4abc7be582ebd85385_20_0.png)

> EXPERT TIPS
Enjoy experimenting

As a programmer you should experiment with the code and programs you make. One of the best ways to learn programming is to play around and see what happens when you change different parts of the code. By tinkering and fiddling, you'll discover new ways of doing things. You'll learn much more about computer programming and have even more fun.
