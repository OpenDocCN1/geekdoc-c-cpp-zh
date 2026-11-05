The following statement is used to define the syntax to declare a value parameter.

```
<return type> MethodName ( <data type> variable name )
{
}
```

# 2.2 Passing parameters by reference -

This method copies the reference to the memory location, of an argument into, the formal parameter. This means that changes made to the parameter affect the argument.

A reference parameter is the reference to the memory location of a parameter. In reference parameter new storage location is not created. It stores the value in the same memory location as the variable passed is in the memory call.

The declaration of the reference parameter is done by using the ref keyword. The example for the reference parameters is as shown below,

```
void ShowReference( ref int Id, ref int age )
{
}
```

# 2.3 Passing parameters using output parameters -

In this method more than one value can be returned to the calling method.

A return statement is used for returning a value from the method. A return statement can be used to return only a single value. The output parameter is used to overcome this problem.

Output parameters are like reference parameters but they transfer data out of the method. An output parameter is reference to the storage location supplied by the caller. To declare an output parameter, the out keyword is used before the data type and the variable name.

Out parameter are specified as shown below,

```
static void Outsample( out int i )
{
    i=20;
}
```

# 2.4 Variable number of arguments to the method -

A method can take variable number of arguments. For this the params keyword is used. No additional parameters are permitted after the params keyword.

Only one params keyword is permitted in a method declaration.