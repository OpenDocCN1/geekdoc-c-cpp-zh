# COMPUTER REPRESENTATION OF NUMBERS

```
for(int i = 15; i >= 0; i--)
  if(val & (1 << i))
    cout << "1";
  else
    cout << "0";
```

Listing 2.2 shows some elementary bitwise operations in a function called printBinary to pick off the internal representation of an integer. The first thing is that the listing is a prototype or declaration of the basic form for printBinary that appears prior to the main function. The return type of the function (i., the keyword that immediately precedes the function's name) is designated as void which means it does not return a value to the calling program. In C/C++ it is necessary to tell the compiler about the essential details (i.e., return type and type for the arguments) in a function before it can be used. Because printBinary is to be used in the main function, we need to define it main or finish a prototype or sketch of the function prior to calling it. The second option was chosen here. But, the program would have compiled and produced the same results if the entire definition of printBinary was moved from the bottom of the listing and placed before main.

The first line concerns the variable that will hold the integer binary representation will be determined. The line consists of a type declaration which states that inval is of type unsigned. In C++ every variable's type must be explicitly stated when it is introduced into the program. Failure to do so would produce a compilation error. Mission of the unsigned short inval; from your program would have generated a message such as

```
binary.rep.cpp: In function int main()
binary.rep.cpp:10: error: 'inval' was not declared in this scope
```

from the compiler.
The main Listing 2.2 also illustrates the use of cout's input partner cin to read a value for inval from the command line. The printBinary function is applied to inval with being written to the shell before the program terminates.

We now arrive at the actual definition of the printBinary function. It takes as input an unsigned short integer that is two bytes size. Some numbers can be seen as having 16 possible slots corresponding to 2^0 all to 2^15. The program then steps through each of these slots using a for loop that has a look at 16 (i.e., the 2^15 slot) and works backwards to the front (or 2^0 slot).

The C++ version of a do or for loop consists of specifying three variables. A starting value is for the index variable governs the iteration. The case variable is i whose type is designated before setting it to 15. Then, there is loop condition (i.e., i > 0) that terminates the loop when it evaluates to false. Finally, direction is provided on how the loop should move through the values of the index variable. This is accomplished with the i-- syntax which shows that i is decremented by one at each step through the loop. Section 3.4 provides more details about

The printBinary function picks off the binary representation of the unsigned int supplied for its argument by first shifting the integer 1 (=2^0) over i=15 slots when the i < 15. We have also used << in a very different context in conjunction with this question. how one operator can be used for two completely different purposes. The answer is that this is example of polymorphism accomplished via a feature called operator overloading that will be developed in more detail