All we have to do next is sort them.... Hmmmmm..... This is awful! There seems to be no way of doing it. Just deciding whether score1 is the largest value would take an IF construction with 10 comparisons! Clearly there has to be a better way of doing this, after all, we know that computers are very good at sorting this kind of thing.

C# provides us with a thing called an *array*. An array allows us to declare a whole row of a particular kind of box. We can then use things called *subscripts* to indicate which box in the row that we want to use. Consider the following:

```
```csharp
using System;
class ArrayDemo
{
    public static void Main ( )
    {
        int [ ] scores = new int [11] ;
        for ( int i=0; i<11; i++)
        {
            scores [i] = readInt ( "Score : " , 0,1000);
        }
    }
}
```
```

The `int [ ] scores` part tells the compiler that we want to create an array variable. You can think of this as a tag which can be made to refer to a given array.

The bit which makes the array itself is the `new int [11]`. When C# sees this it says "Aha! What we need here is an array.", it then gets some pieces of wood and makes a long thin box with 11 compartments in it, each large enough to hold a single integer. It then paints the whole box red - because boxes which can hold integers are red. It then gets a piece of rope and ties the tag `scores` to this box. If you follow the rope from the `scores` tag you reach the array box. Actually, it probably doesn't use wood or rope, but you should get a picture of what is going on here.

# ### 3.3.2 Array Elements

Each compartment in the box is called an *element*. In the program you identify which element you mean by putting its number in square brackets `[ ]` after the array name. This part is called the *subscript*. Note that the thing which makes arrays so wonderful is the fact that you can specify an element by using a variable. In fact you can use any expression which returns an integer result as a subscript, i.e.

```
```csharp
scores [i+1]
```
```

- is quite OK. (as long as you don't fall off the end of the array). When an array is created all the elements in the array are set to 0.

# #### *Array Element Numbering*

C# numbers the boxes starting at 0. This means that you specify the element at the start of the array by giving the subscript 0. There is consequently no element `scores [11]`. If you look at the part of the program which reads the values into the array you will see that we only count from 0 to 10. This is very important. An attempt to go outside the array bounds of `scores` cause your program to fail as it runs. If you find this confusing "The first element has the subscript 0" then the best way to regard the subscript is as the distance down the array you have to travel to get to the element that you need.

One thing adding to this confusion is the fact that this numbering scheme is not the same in other languages. Visual Basic numbers array elements starting at 1. I'm sorry about this; it just goes to show that not everything about programming is consistent.