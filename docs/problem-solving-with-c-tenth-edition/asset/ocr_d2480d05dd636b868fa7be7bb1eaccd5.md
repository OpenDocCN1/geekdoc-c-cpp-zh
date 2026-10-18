4. Suppose you wish to add a friend function for subtraction to the class Money defined in Display 11.3. What do you need to add to the description of the class Money that we gave in Display 11.3? The subtraction function should take two arguments of type Money and return a value of type Money whose value is the value of the first argument minus the value of the second argument.

5. Notice the member function output in the class definition of Money given in Display 11.3. In order to write a value of type Money to the screen, you call output with cout as an argument. For example, if purse is an object of type Money, then to output the amount of money in purse to the screen, you write the following in your program:

```
purse.output(cout);
```

It might be nicer not to have to list the stream cout when you send output to the screen.

Rewrite the class definition for the type Money given in Display 11.3. The only change is that this rewritten version overloads the function name output so that there are two versions of output. One version is just like the one shown in Display 11.3; the other version of output takes no arguments and sends its output to the screen. With this rewritten version of the type Money, the following two calls are equivalent:

```
purse.output(cout);
```

and

```
purse.output();
```

but the second is simpler. Note that since there will be two versions of the function output, you can still send output to a file. If outs is an output file stream that is connected to a file, then the following will output the money in the object purse to the file connected to outs:

```
purse.output(outs);
```

6. Notice the definition of the member function input of the class Money given in Display 11.3. If the user enters certain kinds of incorrect input, the function issues an error message and ends the program. For example, if the user omits a dollar sign, the function issues an error message. However, the checks given there do not catch all kinds of incorrect input. For example, negative amounts of money are supposed to be entered in the form −$9.95, but if the user mistakenly enters the amount in the form $−9.95, then the input will not issue an error message and the value of the Money object will be set to an incorrect value. What amount will the member function input read if the user mistakenly enters $−9.95? How might you add additional checks to catch most errors caused by such a misplaced minus sign?