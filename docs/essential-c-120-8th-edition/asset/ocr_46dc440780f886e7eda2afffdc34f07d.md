# Parameters and Arguments

A method can take any number of parameters, and each parameter is of a specific data type. The values that the caller supplies for parameters are called the arguments; every argument must correspond to a particular parameter. For example, the following method has three arguments:

```
System.IO.File.Copy(
oldFileName, newFileName, false)
```

The method is found on the class File, which is in the namespace System.IO. It is declared to have three parameters, with the first and second of type string and the third being of type bool. In this example, we use variables (oldFileName and newFileName) of type string for the old and new filenames, and then specify false to indicate that the copy should fail if the new filename exists.

# Method Return Values

In contrast to Console.WriteLine(), the method call Console.ReadLine() in Listing 5.2 does not have any arguments because the method is declared to take no parameters. However, this method happens to have a method return value. The method return value is a means of transferring results from a called method back to the caller. Because Console.ReadLine() has a return value, it is possible to assign the return value to the variable firstName. In addition, it is possible to pass this method return value itself as an argument to another method call, as shown in Listing 5.3.

> LISTING 5.3: Passing a Method Return Value as an Argument to Another Method Call

```
public static void main(){
    Console.Write("Enter your first name: ");
    Console.WriteLine("Hello " + Console.ReadLine() + "!");
}
```

Instead of assigning the return value to a variable and then using that as an argument to the call to Console.WriteLine(), Listing 5.3 calls the Console.ReadLine() method within the call to Console.WriteLine(). At