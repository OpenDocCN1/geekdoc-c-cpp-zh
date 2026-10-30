Suppose we think of each letter as being contained inside a rectangle. It is customary to call this rectangle the bounding-box of the letter. Then we will make it a convention that the turtle must be brought to the bottom left corner of the bounding box, and point towards the direction in which the writing is to be done. Where would we like the turtle to be at the end of writing one character so that the next character can be written easily? Clearly, the most convenient final position is pointing away from the right bottom corner, pointing in the direction of writing. We must also clearly state in the precondition whether we expect the pen to be up or down. Also whether the inter-character space is a part of the bounding box or not. If the space is a part of the bounding box, a natural question arises: is it on both sides of the character or only on one side (which?)?. We should not only answer these questions, but must also include the answers in the specification.

Based on the above considerations, drawI could be defined as follows.

```
void drawI(double ht, double sp){
/*Draws the letter I of height ht, leaving sp/2 units of space on both sides. Bounding box includes space.
PRECONDITION: The turtle must be at the left bottom of the bounding-box in which the character is to be drawn, facing in the direction of writing. Pen must be up.
POSTCONDITION: The turtle is at the bottom right corner of the bounding-box, facing the writing direction, with pen up. */

forward(sp/2);
penDown();
left(90);
forward(ht);
penUp();
left(180);
forward(ht);
left(90);
forward(sp/2);
return;
}
```

Functions for other letters are left as exercise for you. So assume that you have written them. Then to write our message, our main program could be as follows.

```
main_program{
int ht=100, sp=10;
turtleSim();
left(90);  // turtle is pointing East at the beginning.
drawI(ht,sp);
drawI(ht,sp);
drawT(ht,sp);
forward(sp);
drawM(ht,sp);
```