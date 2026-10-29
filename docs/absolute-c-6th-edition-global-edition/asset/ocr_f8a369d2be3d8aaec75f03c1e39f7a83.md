# Display 3.8 Local Variables (part 2 of 2)

# Sample Dialogue

```
Enter minimum and maximum number of peas in a pod: 4 6
Enter the number of pods: 10
Enter the weight of an average pea (in ounces): 0.5
Min number of peas per pod = 4
Max number of peas per pod = 6
Pod count = 10
Average pea weight = 0.500 ounces
Estimated average yield = 25.000 ounces
```

The variable subtotal is local to the function totalCost. The named constant TAXRATE is also local to the function totalCost. (A named constant is in fact nothing but a variable that is initialized to a value and that cannot have that value changed.)

# Local Variables

Variables that are declared within the body of a function definition are said to be local to that function or to have that function as their scope. If a variable is local to a function, then you can have another variable (or other kind of item) with the same name that is declared in another function definition; these will be two different variables, even though they have the same name. (In particular, this is true even if one of the functions is the main function.)

# Procedural Abstraction

A person who uses a program should not need to know the details of how the program is coded. Imagine how miserable your life would be if you had to know and remember the code for the compiler you use. A program has a job to do, such as compiling your program or checking the spelling of words in your paper. You need to know what the program’s job is so that you can use the program, but you do not (or at least should not) need to know how the program does its job. A function is like a small program and should be used in a similar way. A programmer who uses a function in a program needs to know what the function does (such as calculate a square root or convert a temperature from degrees Fahrenheit to degrees Celsius), but should not need to know how the function accomplishes its task. This is often referred to as treating the function like a black box.

black box

Calling something a black box is a figure of speech intended to convey the image of a physical device that you know how to use but whose method of operation is a mystery because it is enclosed in a black box that you cannot see inside of (and cannot pry open).