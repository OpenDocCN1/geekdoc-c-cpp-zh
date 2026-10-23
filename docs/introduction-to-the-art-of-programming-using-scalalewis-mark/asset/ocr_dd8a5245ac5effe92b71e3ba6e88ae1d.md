elements of each type were on the different sides of a chemical equation. You should recall that the output of that program was something like the following.

```
C: a\*1=d\*1
H: a\*4=c\*2
O: b\*2=c\*1+d\*2
```

We want to treat this as a system of linear equations and solve it to find the proper values of a, b, c, and d. These particular formulas give you three equations for four unknowns. If you remember systems of equations, that is typically not a good thing as the system is underdetermined so there are an infinite number of solutions. The easy way to fix that is to assume that a certain number of the coefficients are 1 so that we are left with equal numbers of equations and unknowns.

The form given above would be fine for solving this equation by hand, but for solving it on a computer we will want to move things around a bit. The idea is that we want to get it into the form $Ax = y$, where $A$ is a matrix giving the explicit numbers in the equations, $x$ is a vector with the variables we are solving for, and $y$ is a vector with whatever constants wind up being on the right side of the equal sign. Let us make this more explicit by rearranging the equations above into something more like the form we want.

```
1\*a-1\*d=0
4\*a-2\*c=0
2\*b-1\*c-2\*d=0
```

Now we have to pick a coefficient to set to 1 so we get down to equal numbers of equations and coefficients. Any will do equally fine, but programmatically you will probably find it is easiest to set the last coefficient to a constant value (so everything is still zero indexed in your code). In this case that is d. If we do that and move constants to the right side we get the following equations.

```
1\*a=1
4\*a-2\*c=0
2\*b-1\*c=2
```

This can be transformed into $Ax = y$ if

![](bbox=[0.43, 0.68, 0.6, 0.74])

and

![](bbox=[0.43, 0.77, 0.58, 0.83])

Both $x$ and $y$ are column vectors here so they have a single column and multiple rows. Remember that

![](bbox=[0.43, 0.87, 0.55, 0.92])

and that is what we want to solve for. The way you will do this is through a process