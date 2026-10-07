```
// file1
int errors = 20; // external declaration
...

// file2
int errors = 5; // ??known to file2 only
void froobish() {
    cout << errors; // fails
}
```

No, this attempt fails because it violates the one definition rule. The file2 definition attempts to create an external variable, the program winds up with two definitions of errors, which is an error.

But if a file declares a static variable with the same name as an ordinary external variable declared in another file, the static version is the one in scope for that file:

```
// file1
int errors = 20; // external declaration
...

// file2
static int errors = 5; // known to file2 only
void froobish() {
    cout << errors; // uses errors defined in file2
}
```

This does not violate the one definition rule because the keyword static establishes that the identifier errors has internal linkage, so no attempt is made to bring in an external definition.

> Note
In a multifile program, you can define an external variable in one and only one file. All others using that variable must declare that variable with the extern keyword.

You can use an external variable to share data among different parts of a multifile program.You use a static variable with internal linkage to share data among functions found in just one file.(Namespaces offer an alternative method for this.) If you also make a file-scope variable, you don't need to worry about its name conflicting with file-scope variables in other files.

List 9.7 and 9.8 show how C++ handles variables with external and internal linkage. Listing 9.7 (twofile.cpp) defines the external variables tom and the static external variable harry. The main() function in that file displays the addresses of the three variables and calls the remote_access() function, which is defined in a second file. Listing 9.8 (twofile.cpp) shows that file. In addition to defining remote_access(), the file uses the extern keyword to share tom with the first file. Next, the file defines a static