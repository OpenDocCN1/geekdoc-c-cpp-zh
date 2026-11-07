# Chapter Review

+   1. Use a member function to overload the multiplication operator for the Stonewt class; have the operator multiply the data members by a type double value. Note that this will require carryover for the stone–pound representation. That is, twice 10 stone 8 pounds is 21 stone 2 pounds.

+   2. What are the differences between a friend function and a member function?

+   3. Does a nonmember function have to be a friend to access a class’s members?

+   4. Use a friend function to overload the multiplication operator for the Stonewt class; have the operator multiply the double value by the Stone value.

+   5. Which operators cannot be overloaded?

+   6. What restriction applies to overloading the following operators? =, (), [], and ->

+   7. Define a conversion function for the Vector class that converts a Vector object to a type double value that represents the vector’s magnitude.

# Programming Exercises

+   1. Modify Listing 11.15 so that it writes the successive locations of the random walker into a file. Label each position with the step number. Also have the program write the initial conditions (target distance and step size) and the summarized results to the file. The file contents might look like this:

```
Target Distance: 100, Step Size: 20
0: (x,y) = (0, 0)
1: (x,y) = (-11.4715, 16.383)
2: (x,y) = (-6.88807, -3.42232)
...
26: (x,y) = (42.2919, -78.2594)
27: (x,y) = (58.6749, -89.7309)
After 27 steps, the object has the following location:
(x,y) = (58.6749, -89.7309)
or
(m,a) = (107.212, -56.8194)
Average outward distance per step = 3.97081
```

+   2. Modify the Vector class header and implementation files (Listings 11.13 and 11.14) so that the magnitude and angle are no longer stored as data components. Instead, they should be calculated on demand when the magval() and angval() methods are called. You should leave the public interface unchanged (the same public methods with the same arguments) but alter the private section, including some of the private methods and the method implementations. Test the modified version with