Here is the function's implementation:

```
int rotations_needed(point p)
// Postcondition: The value returned is the number of 90-degree
//     clockwise rotations needed to move p into the upper-right
//     quadrant (where x >= 0 and y >= 0).
{
    int answer;

    answer = 0;
    while ((p.get_x( ) < 0) || (p.get_y( ) < 0))
    {
        p.rotate90( );
        ++answer;
    }
    return answer;
}
```

In C++, a value parameter is declared by placing the type name followed by the parameter name. So, we have written point p in the parameter list. The effect of a value parameter is that any change made to the parameter within the body of the function does not change the actual argument from the calling program. Let's look at an example in a program:

```
point sample(6, -4); // Constructor places the point at x = 6, y = -4.
cout << " x coordinate is " << sample.get_x( )
     << " y coordinate is " << sample.get_y( ) << endl;
cout << " Rotations: " << rotations_needed(sample) << endl;
cout << " x coordinate is " << sample.get_x( )
     << " y coordinate is " << sample.get_y( ) << endl;
```

After the constructor, the code prints a message with the point's coordinates. Then, in the second output statement, rotations_needed is called. The function's parameter (p in this case) is referred to as the formal parameter to distinguish it from the value that is passed in during the function call. The passed value (sample in this case) is the argument (sometimes called the actual argument or the actual parameter).

With a value parameter, the argument provides the initial value for the formal parameter. To be more precise, the formal parameter is implemented as a local variable of the function, and the class's copy constructor is used to initialize the formal parameter as a copy of the actual argument. This is the only connection between the argument and the formal parameter. So, if the formal parameter p changes in our function body, the argument sample remains unchanged in the calling program. In our example, p will rotate three times, ending up at x = 4 and y = 6. The function returns the number of rotations (3), and sample still has its