# Object-Oriented Programming with C++

```
void main()
{
    Distance d1,d2,d3;
    d1.setFoot(1);
    d1.setInches(1.1);
    d2.setFoot(2);
    d2.setInches(2.2);
    d3=d1.add(d2);
    cout<<d3.getFoot()<<" '"<<d3.getInches()<<" '"\n";
}
```

/*End of Distain.cpp*/

# Output

3-3.3'

The definition of Distance :: add() function, after the previously described version by the compiler is carried out, as follows:

```
Distance add(Distance * const this, Distance dd)
{
    Distance temp;
    temp.Foot=this->Foot+dd.Foot;
    temp.Inches=this->Inches+dd.Inches;
    return temp;
}
```

When this function is called from the main() function with respect to 'd1', this pointer points at 'd1'. Thus, it is the private data member of 'd1' that is being accessed in the third and third lines of the add() function.

So, now we can

+   - Declare a class
- Define member private and member functions
- Make members private and public
- Declare objects and call member functions with respect to objects

What advantages does all this lead to? The advantage that library programmers can now derive from this arrangement is epitomized in the following observation:

> An executable file will not be created from a source code in which private data members of an object have been accessed by non-member functions.

Once again, the importance of compile-time errors over run-time errors is emphasized. Suppose, if an block exists in a function that is not intended by the library programmer to access the data members of a structure. This block contains a bug (say 'd1.month' has been assigned the value of 13, where 'd1' is a variable of the structure 'date'). A pure compiler will not recognize this statement as an invalid access.

During testing, the condition of this if might never become true. The bug would remain undetected; the executable will get created with bugs. Thus, creating bug-free executables is difficult and unreliable in C. This is due to the absence of language constructs that enforce data security.

On the other hand, a C++ compiler that also detects invalid access of private data members would immediately throw an error during compile time itself and prevent the creation of the executable. Thus, creating bug-free executables is easier and more reliable in C++ than in C. This is due to the presence of language constructs that enforce data security.