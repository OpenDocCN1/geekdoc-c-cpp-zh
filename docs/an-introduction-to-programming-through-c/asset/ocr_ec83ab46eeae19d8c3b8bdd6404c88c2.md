for any value. The command `forward` is predefined for you, but you can also define new functions or commands that do something and do but do not return a value.
For example, you might wish to build a function which draws a polygon with a given number of sides, and having a certain given sidelength. Clearly, it must take two arguments, an integer giving the number sides, and a double giving the side length. Suppose we name it polygon. The function does not return any value, so we are required to specify the return type in the definition to be void. Also, since nothing is being returned, we merely write `return` with no value following it.

```
void polygon(int nsides, double sidelength)
// draws polygon with specified sides and specified sidelength.
// PRE-CONDITION: The pen must be down, and the turtle must be
// positioned at a vertex of the polygon, pointing in the clockwise
// direction along an edge.
// POST-CONDITION: At the end the turtle is in the same position and
// orientation as at the start. The pen is down.
{
    for(int i=0; i<nsides; i++){
        forward(sidelength);
        right(360.0/nsides);
    }
    return;
}
```

Note the precondition: it states where the polygon is drawn in comparison to where the turtle is pointing. Similarly, we should mention where the turtle is at the end, this will be needed in order to know how to draw subsequently. A condition such as this one, which will be true after the execution of the function, is said to be a post-condition of the function. A post-condition is also a part of the specification.

# 9.5  A text drawing program

We would like to develop a program using which it is possible to write on the screen using our turtle. For example, we might want to write “IIT MUMBAl”. How should we organize such a program?
A natural (but not necessarily the best, see the exercises) way of organizing this program is to have a separate function for writing each letter. For example, we will have a function drawI for drawing the letter ‘I’. Suppose we decide that we will write in a simple manner, so that the letter ‘I’ is just a line, without the serifs (horizontal lines at the top and bottom), i.e. as I.
What is the specification of drawI? Clearly it must draw the line as needed. But where should the line get drawn? This must be mentioned in the specifications. It is tempting to say that the line will get drawn at the current position of the turtle, in the direction the turtle is pointing. Is this really what we want? Keep in mind that you dont just want to draw one letter, but a sequence of letters. So it is important to bring the turtle to a convenient position for drawing subsequent letters. And what is that convenient position?