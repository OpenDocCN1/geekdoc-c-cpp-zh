
# Introduction to Programming and Problem-Solving Using Scala

and

$y = \begin{bmatrix} 1 \\ 0 \\ 2 \end{bmatrix}$

Both $x$ and $y$ are column vectors so they have a single column and multiple rows. Remember that

$x = \begin{bmatrix} a \\ b \\ c \end{bmatrix}$

and is what we want to solve for. It turns out there are many methods of doing this that have different numerical properties. Gaussian elimination is not the best, but it is the simplest to decide and sufficient for our purposes. Gaussian elimination is also exactly what you would do if you were solving this problem on paper; hopefully it will make sense.

What we do in Gaussian elimination is multiply and add together rows in $A$ and $y$ to remove de coefficients and turn $A$ into a triangular matrix. We might also have to swap rows at certain times. In fact, we will do generally to improve numerical stability. To begin with, we remove the term from everything but the first row. We could do this with $A$ as is, but for numerical reasons it is best if we keep the largest coefficient. We will see other reasons for when we remove $b$. So, the first time the coefficient of $a$ is 4, and it is in the second row; we swap the first and second rows. Note that we swap both in $A$ and $y$. This gives the following values.

$A = \begin{bmatrix} 4 & 0 & -2 \\ 1 & 0 & 0 \\ 0 & 2 & -1 \end{bmatrix}$

and

$y = \begin{bmatrix} 0 \\ 1 \\ 2 \end{bmatrix}$

We eliminate the terms in the second and third rows by multiplying their values appropriately so that when we subtract them from the top column we do not have anything left. If a term is already zero in a row we can leave it alone. In the first case we will remove the term from the middle row by multiplying it by 4 and subtracting the top row from it. We will do nothing with the bottom row. This gives the following values.

$A = \begin{bmatrix} 4 & 0 & -2 \\ 0 & 0 & 0 \\ 0 & 2 & -1 \end{bmatrix}$

and

$y = \begin{bmatrix} 4 \\ 2 \end{bmatrix}$

Now the top row is set so we look at the smaller nested matrix ignoring the first row and column. We want to eliminate the $b$ coefficients from that. Here it really matters

> The fact that both $A$ and $y$ need to be swapped at the same time that their implementation could represent both $A$ and $y$ in a single `Array[Double[]]` where each inner array stores a row of $A$ followed by the corresponding $y$ value.

# Object-Orientation

that we swap the row with the largest coefficient because what is there right now as a zero coefficient that will cause division by zero if we do not move it. We do not swap and the last row has a zero in the $b$ coefficient we will not do anything else. That leaves us with the following values.

```
A = \begin{bmatrix} 4 & 0 & -2 \\ 0 & 2 & -1 \\ 0 & 0 & 2 \end{bmatrix}
```

and

```
y = \begin{bmatrix} 0 \\ 2 \\ 4 \end{bmatrix}
```

This can be solved by working up our map. The bottom row tells us that $c = 2$. We plug that into the next row and $2*b-1*c = 2b-2 = 2$ and find $b = 2$. It is easy to say that, but we should probably examine how the computer finds these values. For the first one, the computer simply does $c = y(2)/A(2)$. Then as we move up we have to do some loops to subtract things before we do the division. In this case $b = (y(1)-c*A(1))/A(1)$. Note that we are always dividing by the coefficient on the diagonal, and we are now down to our top equation which is $a = 2*c/4$ so $a = 1$. In the program that will be $a = (y(0)-c*A(0))/b*A(0)$. The values of $y(0)$ and $A(0)$ are both zero, but the math in the program will end, and it will not matter.

Your program should take an input like the previous project where you type in a chemical equation. It should then print out the same output as that assignment follow with that solution. In this case it would print out "a=1 b=2 c=2 d=1" as the line of output. While this example does not show it, there might be some decimals in place. If you want an extra challenge you can scale things up so they are integers.

Make this object oriented by making an application and having a class that represents a chemical formula. You can add methods to access the information that is calculated using the approach described above.

- 7. It is time to make your map program into a true adventure game. It does not matter how you do this, but you need to add a goal to the game and have to inform the player if he/she wins or loses. Most of the original text adventure games have rooms with types of puzzle solving where the items interact with one another or with You probably do not want to go the RPG role and equipment, combat, and the though simple combat might be feasible. You must add a "help" command.

- 8. You should build a ray tracer that includes spheres, planes, and lights. To make this easy, you need to add a class that represents the scene. You should also add a function that takes a ray and returns the color it hits.

- 9. You can make the scheduling script from 15.6 into an object-oriented application. To do this, you want to put body on your Course class.
