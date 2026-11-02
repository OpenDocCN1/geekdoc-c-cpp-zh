can be abbreviated as

```
with
    Depends => ((Found, Position) => (Text, Letter, Start))
```

The understanding is that each output mentioned in an output list depends on all of the inputs mentioned in the associated input list.

For the case of in out parameters or global variables that are In_Out, it is common for the output value of the parameter or variable to depend on its own input value. The parameter Value in the previously shown procedure Get_Value is like this. In that case, the symbol =>+ can be used to indicate that each output on the left side depends on itself as well as on all inputs on the right side. For example, the contract

```
with
    Depends => (Value => (Text, Name, Value))
```

can be abbreviated as

```
with
    Depends => (Value =>+ (Text, Name))
```

In the important case where an in out parameter or In_Out global variable depends on only itself, a flow dependency contract such as Value => Value can be abbreviated to Value =>+ null. The abbreviated form can be read as, “Value depends on itself and nothing else.”

Sometimes an output depends on no inputs whatsoever. This occurs when a subprogram writes a value from “out of the blue” to initialize an output. For example,

```
procedure Initialize (Value : out Integer)
with
    Depends => (Value => null);
```

The flow dependency contract Value => null can be read as, “Value depends on nothing.” It means the subprogram sets the value without reference to any input.

Finally, it is also possible to give a flow dependency contract that uses null on the output side of a dependency as shown in the following example:

```
procedure Update (Value : in out Integer ;
                Adjust : in Integer)
with
    Depends => (Value =>+ null,
                null => Adjust);
```

Here, Value depends only on itself, and nothing depends on Adjust. Thus, Adjust is not used in the computation of any results. Such a flow dependency contract