
# Object-Orientation

While converting scripts to applications has some general use too, keep in mind that not all classes need to be changed. The case classes exist in Scala for a reason that goes beyond the educational purposes that have benefited us in this book. It is quite possible that a number of your classes should ideally remain that way over the long term. Practice with changing them is good for you to see how that matters, but it is not always something you want to do.

## 16.6.3 Projects

All the projects in this switch comes from running scripts to running as applications. That means that you need to run scalac first to compile the application, then run scala on just the name of the object you put the main method. This also allows you to split code into separate files for different classes and objects. All code must be inside of a class or for this approach to work. If you put the files in the project then directory you can compile them all by running scalac *.scala.

- One way to build on top of project 15.3 is to give the user the ability to plot functions. For this to work, the formula parser needs to support variables. In the formula parser, there were possible cases where you did not find an operator and a parenthesis. The variable becomes a third possibility. To keep things simple for now, the only variable allowed in a formula is x. If you do not find an operator and the variable you are parsing is "x", you will say it is a variable. To use variables, you need an extra argument to the evaluation, Double represents the value of the variable x.

To fit with the contents of this chapter, you are to make code for this object oriented by having it as an application and including two separate classes called Plot and Formula. The Formula class is where your earlier code will go. The class should take one argument that is a String for the formula. You will put the code into a method in that class. The method should take a single argument of x:Double. It does not need to accept a String the class as a whole knows what formula is being used. You could also add things like trigonometric support function so that you can plot more interesting cases.

The Plot will keep a var List that tells it all the formulas that are to be plotted. This list could contain instances of Formula or of some class that groups a Formula with a Color so that functions are drawn in different colors. The Plot also needs to keep bounds for the x and y axes. You should put a draw(Graphics) method into Plot that can be called from the application itself. That method will loop through the different Formula objects, evaluating them at proper inside the range to be plotted, and connecting the points to draw a line for the function.

You can decide how to include a JFrameApp The object will need to have a main and a Canvas as a GraphicsContext with code that calls draw on a Plot object. If you want an extra challenge to make the application more useful you can add the capability for the user to edit settings on the Plot. As with previous plotting work, it is recommended that you try not to support labels on axes. However, if the range or domain crosses zero, you might consider drawing lines for the axes themselves.

2. If you project 15.3 and you did gravity integrations before, then you can consider this option. The basic idea is that you will add variable support to your formula as described in the previous project, and then the user will use in a formula that is instead used of gravity.

In the GUI for your integrator you should have a text field that users input a formula. You should use "x" for the distance between the bodies. You can also define standard variables that are used, like "ma" and "mb" for the masses of the first and second particles in an interaction. Using gravity, this would be input as "ma*mb/(x**)". A spring connection would be "-x". You can play with other options as well and see how they change the way particles move.

To work with the Formula type described, you will need to use a String where the variables ma and mb have been replaced by the proper values for the particles being considered. You might even consider keeping formulas in an Array[Array[String]] so that they do not have to be rebuilt each time. Then you will have the Formula evaluate using the proper distance between the particles.

You could also extend the Formula type so that it accepts variables for x, ma, mb, and possibly others that you want to define. This second approach is less ideal than the Formula type as it makes it generic, but is probably the easiest way for you to get some flexibility is user functions.

Note that this version of the integrator is going to be significantly slower than what you did before every force calculation involves Parsing.

3. If you did the Tron game in an earlier project, you could update it to be oriented. For Tron you make a class that represents a light cycle including its position, direction, and color. It could have a method move that alters the position appropriately for the direction. Other methods could include turning left or right that are called by handlers for key presses or a draw method that puts a point at the appropriate location. You might also encapsulate whether a cycle is alive or not the class.

With this change it is now feasible to add in more players and walls from one player disappear when that player dies. Extend the game to have three players (or add a computer player) and make it so that when a player dies, the line for that goes away.

4. If you worked any other type of graphical game in earlier chapters, you should also be able to convert it to be an application with an object-oriented approach by making the different elements of the game into Classes that store the relevant information and have appropriate methods.

5. If you implemented the Mandelbrot set calculation and display previously, this is the project for you. First, use what you learned in this chapter to make a class called Complex that represents complex numbers and alter your original Mandelbrot calculations to use. Once you do that, you will take further advantage of it by adding the ability to display Julia sets of quadratic polynomials.

Every point in the Mandelbrot corresponds to one of these Julia sets. The equation for a Julia set looks much like that for the Mandelbrot set, $z_{n+1} = z_n^2 + c$ with $c$ being a fixed value and $z_0$ being the point in the plane you are calculating for. For contrast, the Mandelbrot set used a different $c$ value for each point and $z_0 = 0, z_1 = c$. Again, you iterate until the value leaves the area around the origin until some pre-specified number of iterations.

If the user clicks on a location (the `MouseClicked` event) then you should pop up another window (use `Stage` with a different panel that will draw the Julia set associated with the point clicked. You can decide what functionality you want to put into window. It should start with a bounds of $r\in[-2,2]$ and $i\in[-2,2]$ for the real and imaginary axes, respectively. It should not be hard to zooming, but that is not required.

- 6. This project continues 8.5, where you have to figure out how many elements of each type were on the different sides a chemical equation. You should recall that the output of that program was something like the following:

```
C: a-1*d=0
H: a+4*c=0
O: b-c=2
```

We want to treat this as a system of linear equations and solve to find proper values of a, b, c, and d. These particular formulas give you three equations for four unknowns. If you remember systems of equations, which is typically not a good thing as the system is underdetermined so there are an infinite number of solutions. The easy way to fix that is to assume a certain number of the are 1 so that you are left with equal numbers of equations and coefficients.

The given form above be for solving this by by,, for solving solving on computer we we will to around around around around. The idea is to get it it the the $Ax==y where isA$ is the matrix numbers in the numbers in $x, isx$ is the variables we are solving for, and $y$ and a vector with whatever constants wind up being on the right side of the equal sign. Let us make this more explicit by rearranging the equations into something like the:

```
1*a-1*d=0
4*a-2*c=0
2*b-1*c-2*d=0
```

Now we have to pick a coefficient to set to 1 to get down to equal numbers of equations and coefficients. Any will do fine, but programmatically you will find it is easiest to set the last coefficient to a constant value (so everything is still zero indexed in your code). In this case it is d. If we do that and move to the right side we get the following equations.

```
1*a=1
4*a-2*c=0
2*b-1*c=2
```

This can be transformed into $Ax=y$ if

![](img/06d4e84f27a8884ea40ba6182ec7c778_543_0.png)
