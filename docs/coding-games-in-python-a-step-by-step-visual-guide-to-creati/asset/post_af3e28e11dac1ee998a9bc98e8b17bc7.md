
```python
lair["egg_hidden"] = False
lair["egg_hide_counter"] = 0
else:
    lair["egg_hide_counter"] += 1

def check_for_collisions():
    global lairs, eggs_collected, lives, reset_required, game_complete
    for lair in lairs:
        if lair["egg_hidden"] is False:
            check_for_egg_collision(lair)
        if lair["dragon"].image == "dragon-awake" and reset_required is False:
            check_for_dragon_collision(lair)

def check_for_dragon_collision(lair):
    x_distance = hero.x - lair["dragon"].x
    y_distance = hero.y - lair["dragon"].y
    distance = math.hypot(x_distance, y_distance)
    if distance < ATTACK_DISTANCE:
        handle_dragon_collision()

def handle_dragon_collision():
    global reset_required
    reset_required = True
    animate(hero, pos=HERO_START, on_finished=subtract_life)

def check_for_egg_collision(lair):
    global eggs_collected, game_complete
    if hero.colliderect(lair["eggs"]):
        lair["egg_hidden"] = True
        eggs_collected += lair["egg_count"]
        if eggs_collected >= EGG_TARGET:
            game_complete = True

def subtract_life():
    global lives, reset_required, game_over
    lives -= 1
    if lives == 0:
        game_over = True
    reset_required = False
```

![](img/3188b147f991a51de14dcd2bb4b4c42e_220_0.png)

## Glossary

- **animation** A process in which images are displayed one after another to make it look like something’s moving.
- **Boolean expression** A statement that is either True or False, leading to two possible outcomes.
- **branch** A point in a program where different options are available to choose from.
- **bug** An error in a program’s code that makes it behave in an unexpected way.
- **call** To use a function in a program.
- **command line** The screen that lets you enter commands into the Command Prompt or Terminal window.
- **Command Prompt** An application on Windows computers that allows a user to enter and execute commands.
- **comment** A text note added to a program that makes the code easier to understand and is ignored by the program when it runs.
- **condition** A “True or False” statement used to make a decision in a program. See also *Boolean expression*.
- **constant** A variable whose value should stay the same throughout a program. Programmers use capital letters when naming constants to let other programmers know that their values should not be changed. See also *variable*.
- **coordinates** A pair of numbers that pinpoint an exact location. Usually written as (x, y).
- **data** Information, such as text, symbols, and numerical values.
- **dictionary** A collection of data items stored in pairs, such as countries and their capital cities.
- **debug** To look for and correct errors in a program.
- **encryption** A way of encoding data so that only certain people can read or access it.
- **event** Something a computer program can react to, such as a key being pressed or the mouse being clicked.
- **file** A collection of data stored with a name.
- **flag variable** A variable that can take two states, such as True and False.
- **float** A number with a decimal point in it.
- **flowchart** A diagram that shows a program as a sequence of steps and decisions.
- **function** Code that carries out a specific task. Also called a procedure, subprogram, or subroutine.
- **global variable** A variable that can be used throughout every part of a program. See also *local variable*.
- **graphics** Visual elements on a screen, such as text, pictures, icons, and symbols.
- **GUI** The GUI, or graphical user interface, is the name for the buttons and windows that make up the part of a program you can see and interact with.
- **hack** An ingenious change to code that makes it do something new or simplifies it. (Also, accessing a computer without permission.)
- **hacker** A person who breaks into a computer system. “White hat” hackers work for computer security companies and look for problems in order to fix them. “Black hat” hackers break into computer systems to cause harm or to make profit from them.
- **indent** When a block of code is placed farther to the right than the previous block. An indent is usually four spaces. Every line in a particular block of code must be indented by the same amount.
- **index number** A number given to an item in a list. In Python, the index number of the first item will be 0, the second item 1, and so on.

## Index

Page numbers in **bold** refer to main entries.

### A

- **Actors** 52
- animations 126, 127
- admin access 18
- anchor 92
- animate() function 83, 93, 193
- animations 92, 126, 127, 181, 191
  - stopping 94
- audio files 141–42

### B

- **Balloon Flight** 116–35
  - coding 121–33
  - flowchart 120
  - hacks and tweaks 133–35
  - how it works 120
  - lives 133
  - project reference 205–207
  - scoring 123, 124, 130–33
  - what happens 118–19
  - *see also* obstacles
- **Big Quiz** 98–115
  - coding 103–12
  - flowchart 102
  - GUI 101
  - hacks and tweaks 113–15
  - how it works 102
  - interface 104–06
  - project reference 203–204
  - scoring 107
  - timer 107, 112
  - what happens 100–101
- birds 126, 127
- body, of function 122
- Boolean expressions 33
- Boolean values 32
- boxes 100–101, 105–06, 108
- branching 34–35
- bugs
  - bug-busting checklist 47
  - finding 44
  - fixing 25, 44–47
  - *see also* hacks and tweaks

### C

- calculations, shorthand 125
- clock tool 112
- code
  - colors in 19
  - indenting 23, 43, 55
- **Coin Collector** 58–67
  - flowchart 61
  - getting started 61–66
  - hacks and tweaks 67
  - how it works 61
  - project reference 198–199
  - what happens 60
- collidepoint() function 77, 93
- colliderect() function 165, 192, 194
- collisions 77, 129, 165, 172, 192–94
- colors 114–15
- conditions 34
- constants 86, 87, 182, 183
- coordinates 125
- count() function 41
- countdown() function 148
- cow 156, 160

### D

- **Dance Challenge** 136–53
  - coding 141–52
  - defining cards 143
  - flowchart 140
  - hacks and tweaks 153
  - how it works 140
  - input methods 145–51
  - music 140, 142, 152, 153
  - project reference 207–211
  - scoring 150
  - what happens 138–39
- decisions, making 32–35
- dictionaries 184
- dots, connecting 70–71, 77
- dragons 178–81, 184, 190, 193, 195
  - animation 181
- draw() function
  - Balloon Flight 124
  - Big Quiz 108
  - Coin Collector 63, 65
  - Dance Challenge 143
  - Follow the Numbers 75, 79
  - Happy Garden 172, 175
  - Red Alert 87
  - Shoot the Fruit 53
  - Sleeping Dragons 180, 186

### E

- editor window 21
  - messages in 44
- eggs 178, 184, 192
  - animation 191
- equals signs 32
- error messages 44
- errors, types 45–47
- event handling 151

### F

- fangflowers 156, 160, 168–75
- file handling 132, 134
- floats 29
- flowcharts 22
  - Balloon Flight 120
  - Big Quiz 102
  - Coin Collector 61
  - Dance Challenge 140
  - Follow the Numbers 72
  - Happy Garden 158
  - Red Alert 84
  - Shoot the Fruit 51
  - Sleeping Dragons 180–81
- flowers 163–69, 174
- folders 52
- **Follow the Numbers** 68–79
  - flowchart 72
  - getting started 73–77
  - hacks and tweaks 78–79
  - how it works 72
  - project reference 199–200
  - what happens 70–71
- “for” loops 36–37
- functions 30, 40–43, 122
  - body 122, 122
  - built-in 44–45
  - calling 40, 41
  - header 122
  - making 42–43
  - naming 42
  - using 40

### G

- Games, types 14
- garden, drawing 161
- global variables 74, 86, 123
- graphical user interface — see GUI
- graphics, in Pygame 54
- gravity 126
- GUI 101
  - Big Quiz 101

### H

- hacks and tweaks
  - Balloon Flight 133–35
  - Big Quiz 113–15
  - Coin Collector 67
  - Dance Challenge 153
  - Follow the Numbers 78–79
  - Happy Garden 174–75
  - Red Alert 96–97
  - Shoot the Fruit 57
  - Sleeping Dragons 199
- **Happy Garden** 154–75
  - coding 159–73
  - flowchart 158
  - hacks and tweaks 174–75
  - how it works 158
  - project reference 211–215
  - scoring 165
  - what happens 156–57
- header, of function 122
- hero 178, 185, 187, 188, 192–95
- hints 113
- houses 128

### I–J

- IDLE 16
  - colors in code 21
  - editor window 21
  - shell window 20
  - using 20–21
- indentation errors 43, 45
- input() function 41
- integers 29
- interface, planning 104
- join function 136

### K

- keys 184

### L

- lairs 184–85, 187, 189
- len() function 30
- levels 34, 78, 92, 135
- line() function 75
- list comprehension 97
- lists 31
  - looping over 37
- lives 133, 193–94
- local variables 74
- logic errors 47
- loop variable 36
- loops 36–39
  - escaping 37
  - for 36–37
  - infinite 39
  - while 38–39

### M

- Mac computers 17, 19
- modules 15
  - downloading 15
- modulo operator 135, 153
- motion, illusion of 119, 128
- music, adding 140

### N

- numbers, using 29

### O

- obstacles 118
  - collisions with 129
  - multiples of 134
  - preparing 122
  - on screen 123
  - spacing out 135
- on_key_up() function 113, 146, 151
- on_mouse_down() function 55, 72, 77, 93, 125
- open() function 40, 132

### P

- parameters 40
- “pass” keyword 64, 144
- patterns 62
- placeholders 64, 144
- pop() function 102, 108
- print() function 40
- programs
  - rerunning 25
  - running 24–25
- Pygame
  - graphics in 54
  - installing 18–19
- Pygame Zero
  - installing 18–19
- Python
  - first program 22–23
  - installing 16–17
  - why use 12
- Python 3 16

### Q

- Questions
  - adding 107
  - answering 110
  - comparing 32
  - skipping 113
- quizzes — see Big Quiz

### R

- rain 175
- randint() function 56, 64, 72, 96, 145
- Random module 56
- random numbers 56
- range 36
- Raspberry Pi
  - computers 17
- read() function 132
- Red Alert 80–97
