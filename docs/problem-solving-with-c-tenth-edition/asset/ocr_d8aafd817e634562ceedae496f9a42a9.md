# DISPLAY 5.6 Comparing Argument Mechanisms (part 2 of 2)

```
22      par1Value = 111;
23      cout << "par1Value in function call = "
24          << par1Value << endl;
25      par2Ref = 222;
26      cout << "par2Ref in function call = "
27          << par2Ref << endl;
28  }
```

# Sample Dialogue

```
par1Value in function call = 111
par2Ref in function call = 222
n1 after function call = 1
n2 after function call = 222
```

On the other hand, par2Ref is a call-by-reference parameter. When the function is called, the variable argument n2 (not just its value) is substituted for the formal parameter par2Ref. So that when the following code is executed:

```
par2Ref = 222;
```

it is the same as if the following were executed:

```
n2 = 222;
```

Thus, the value of the variable n2 is changed when the function body is executed, so as the dialogue shows, the value of n2 is changed from 2 to 222 by the function call.

If you keep in mind the lesson of Display 5.6, it is easy to decide which parameter mechanism to use. If you want a function to change the value of a variable, then the corresponding formal parameter must be a call-by-reference formal parameter and must be marked with the ampersand sign, &. In all other cases, you can use a call-by-value formal parameter.

# PITFALL Inadvertent Local Variables

If you want a function to change the value of a variable, the corresponding formal parameter must be a call-by-reference parameter and must have the ampersand, &, attached to its type. If you carelessly omit the ampersand, the function will have a call-by-value parameter where you meant to have a call-by-reference parameter, and when the program is run, you will discover that the function call does not change the value of the corresponding argument. This is because a formal call-by-value parameter is a local variable, so if it has its value changed in the function, then as with any local variable, that change has no effect outside of the function body. This is a logic error that can be very difficult to see because it looks right.