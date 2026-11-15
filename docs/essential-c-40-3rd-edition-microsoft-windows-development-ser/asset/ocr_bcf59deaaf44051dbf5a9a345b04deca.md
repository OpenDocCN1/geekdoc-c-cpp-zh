Output 4.8 shows the results of Listing 4.14.

# OUTPUT 4.8:

```
C:\Data\mark\bin\config\index.html
C:\WINDOWS\system32\Temp\index.html
C:\Data\HomeDir\index.html
```

In the first call to Combine(), four parameters are specified. The second call contains only three parameters. In the final call, parameters are passed using an array. In other words, the Combine() method takes a variable number of parameters, whether separated by a comma or as a single array. To allow this, the Combine() method

+   1. Places params immediately before the last parameter in the method declaration

+   2. Declares the last parameter as an array

With a parameter array declaration, it is possible to access each parameter as a member of the params array. In the Combine() method implementation, you iterate over the elements of the paths array and call System.IO.Path.Combine(). This method automatically combines the parts of the path appropriately using the platform-specific directory-separator-character. (PathEx.Combine() is identical to Path.Combine(), except that PathEx.Combine() handles a variable number of parameters rather than simply two.)

There are a few notable characteristics of the parameter array.

+   • The parameter array is not necessarily the only parameter on a method. However, the parameter array must be the last parameter in the method declaration. Since only the last parameter may be a parameter array, a method cannot have more than one parameter array.

+   • The caller can specify zero parameters for the parameter array, which will result in an array of zero items.