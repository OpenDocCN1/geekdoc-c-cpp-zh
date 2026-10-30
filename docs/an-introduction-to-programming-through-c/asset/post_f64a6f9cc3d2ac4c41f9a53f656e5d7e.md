
moves to the position of segment *i − 1*, for *i ≥ 1*. The player can change the direction of the head movement to a new direction, say by typing 'n', 'e', 's', 'w'.

Here we will develop the core logic of the game, i.e. show the snake on the screen and enable the player to change its direction. The addition of prizes etc. are left for the exercises.

### 18.4.1 Specification

We have more or less described the specifications above. Perhaps only one clarification is needed: the segments of the snake will move on a two dimensional grid, with the grid separation being `gridsep`.

### 18.4.2 Classes

As we have mentioned, we should have a class for all the important entities contained in our program. So clearly we must have a Snake class.

The snake will have a body which consists of several segments. So it is natural to consider an array named `body` consisting of `Circles`, where we have arbitrarily decided that the segments be circular. We will use a constant length to denote the number of segments in the body. Each segment will maintain its own position, so we need not have an additional position attribute for the snake. However, it is useful to keep a data member giving the current direction of movement. Since the movement is only along the four directions, we have chosen type char for this member, and it is expected to take values ’n’, ’e’, ’s’, ’w’.

When the snake moves, segments 1 through `length−1` move into the positions of segments 0 through `length−2`. So in effect, because the segments are visually identical, it might seem that the segments 1 through `length−2` stay fixed, while segment `length−1` moves to the position where segment 0 is expected to move. Our code in fact does this. Note that this means that what was previously segment *i* becomes segment *i − 1 % length*. So instead of copying around the segments within the array body, we merely keep a data member `headindex` which gives the index of the segment which is the head of the snake.

The way in which the segment which was the tail earlier becomes the head can be handled in many ways. We do this as follows. We make the erstwhile tail segment become a copy of the erstwhile head. At this point we move the erstwhile tail segment in the direction of motion.

The code for the class Snake is given in Figure 18.1.

```
const int gridsep = 20, xinit = 30, yinit = 20, length = 10, npts = 40;

struct Snake{
Circle body[length];
int headindex;  // which body element is the head of the snake
char dir;       // current direction of motion.
Snake(){
// head at (xinit,yinit) in the coarse grid.
headindex = 0;
for(int i=0; i<length; i++)
body[i].reset((xinit+0.5+i)*gridsep, (yinit+0.5)*gridsep, gridsep*0.5);
dir = 'w';
}
void move(){
move(dir);    // continue along old direction
}
void move(char command){
if(command != 'w' && command != 'n' &&
command != 'e' && command != 's') command = dir;
// if user typed illegal letter, keep moving in old direction

int newhead = (headindex +length - 1) % length; // old tail
body[newhead] = body[headindex];  // old tail now on top of head
headindex = newhead;              // old tail element becomes head

// move new head in direction of motion.
if(command == 'w')      body[headindex].move(-gridsep, 0);
else if (command == 'n') body[headindex].move(0, -gridsep);
else if (command == 'e') body[headindex].move(+gridsep, 0);
else if (command == 's') body[headindex].move(0, +gridsep);

dir = command;              // save new motion direction
}
};
```

Figure 18.1: The Snake class

### 18.4.3 User interaction

The main point of the example is of course how the user interacts with the snake. This happens in the main program given below.

The main program sets up the canvas and the snake. It then goes into an endless loop in which every 0.1 seconds the program checks if the user has typed anything in order to change the direction of the snake. This is done using the function `checkEvent`. If the user has indeed typed a key, then its value is extracted using the `charFromEvent` function. This key is then used as an argument to the member function `move` of the snake, so that the movement happens in the required direction. If the user did not type anything, then an argumentless form of the move member function is called, which causes the snake to continue in the direction which it was originally moving.

```
int main(){
    initCanvas("Snake", gridsep*npts, gridsep*npts);
    Snake s;
    while(true){
        XEvent event;
        if(checkEvent(event)){
            if(keyPressEvent(event)){
                char c = charFromEvent(event);
                s.move(c);                    // new direction?
            }
        }
        else s.move();                        // keep moving as before.
        wait(0.1);
    }
}
```

### 18.5 Exercises

- 1. Modify the drawing program discussed in the chapter so that it “beautifies” what the user draws. Specifically, if the user draws something that nearly looks like a straight line, you should draw it as a straight line. Or a circular arc. Try to come up with some protocols so that the user can draw beautiful pictures without too much effort.
- 2. Another use of “dragging”, in addition to drawing, is to drag objects around on the screen. In particular, the user can move the cursor to an object, then click a button, drag the mouse, and finally release the button (drop). This should cause the object to get selected and moved and dropped at the new position. This idea will be useful in building graphical editors, as you must have seen. Modify the drawing program of the previous exercise so that it does not imprint the lines on the canvas, but merely shows them creating suitable line and circle objects. Keep track of these objects in suitable arrays. Allow them to be dragged and dropped.
- 3. Add prizes/food/walls to the snake game. Also make the snake’s length increase by one every time it eats food. Also assign a score to the player depending upon how much food/prizes the snake has eaten, and even just how long the snake has stayed around. Display the score suitably.

## Chapter 19: Representing variable length entities

We continue with the idea of building classes to represent entities that we might want in our programs. In many cases, the entities we wish to represent do not have a standard length, e.g. a piece of text such as the name of a person. Indeed, human beings have names which can be very short, or very long. We may also wish to represent entities such as polygons, where the number of vertices might be different, or polynomials, where the number of coefficients might be different. We may also be called upon to represent graphs (e.g. road networks) or the set of sets of students in different classes; in general we might want to represent several instances of each such collections, and the instances will typically have different lengths.

One natural strategy is to allocate the maximum possible length to represent the entity in question. We used this idea for representing text strings in Section 14.1: if we want to store names of people, we allocated char arrays of what we supposed was the maximum possible length. This clearly uses memory inefficiently. People have names of widely varying lengths, e.g. the actor Om Puri and the freedom fighter/scholar Chakravarti Rajagopalachari. So in general we will be forced to allocate long arrays, but most of the time we will use only small portions of these.

In this chapter, we will see how to design a data type for storing text strings, such that it does not waste memory. We cannot directly use structures/classes/arrays the way we have described them so far. This is because the size of a class/structure/array must be fixed once for all, typically without the knowledge of the size of the text string to be stored in it. The most convenient way of representing entities whose size is not known when we write the program is to use the so called heap memory allocation. This is also referred to as dynamic memory allocation. Using this heap memory, we will construct a String class using which you will be able to store and manipulate text strings efficiently and conveniently.

In general the heap memory will be useful in building representations for entities whose sizes may not be known at the time of writing the program, or whose sizes may even vary over time. We will see examples of such representations in the Exercises.

The Standard Library of C++ contains several classes which use heap memory to accommodate entities of variable sizes. In fact one of the classes in the library is a string class, which can be considered to be an advanced version of the String class we discuss in this chapter. We will study the Standard Library including the string class in Chapter 20. Chapter 20 will not discuss how these classes are implemented; however the implementation of the String class in this chapter will provide some clues.
