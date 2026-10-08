# CHAPTER 14: USING CONSTRUCTORS AND DESTRUCTORS

In the book, you will have come across these two terms. Well, they are not difficult to grasp. Here, we will be taking a look at each of them in turn.

# Constructors in C#

A class constructor can be said to be a special member function of the class. This will be executed whenever new objects are created by that class. A constructor will have the exact same name as its class. There are no return types for a constructor.

The following example demonstrates constructors.

```
using System;

namespace LineApplication
{
    class Line
    {
        private double length; // Length of a line
        public Line()
        {
            Console.WriteLine("Object is being created");
        }

        public void setLength( double len )
        {
            length = len;
        }
    }
```