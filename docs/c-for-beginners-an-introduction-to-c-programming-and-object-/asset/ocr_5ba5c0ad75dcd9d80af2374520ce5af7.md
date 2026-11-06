# 6. User Interaction

In the previous sections we have seen how *cout* is used to display data on the screen. In this section, we will see how to interact with the user, how to accept inputs from the user.

The *iostream* header provides an object called *cin* which is used to accept input from the user. *cin* just as *cout* is a member of the *std* namespace. Usage is slightly different, the *cin* object should be followed by the *extraction operator ( >> )* and a variable. General Syntax:

```
cin >> [variable];
eg:
string name;
cin >> name;
```

The usage of *cin* is a blocking I/O operation. That is, when a *cin* statement is encountered, the program will halt the execution and wait for the user to enter something through the keyboard. In the above example, when the execution control reaches *cin >> name;* statement, the program will wait for the user to enter some text. Once the user does so and hits Enter, whatever the user has entered will be extracted and stored in the variable *name*. You can read multiple values into multiple variables by using the *extraction operator ( >> )* multiple times as follows:

```
cin >> [variable] // --> variable 1 --> ...
[variable n];
eg:
cin >> first_name >> last_name ;
```