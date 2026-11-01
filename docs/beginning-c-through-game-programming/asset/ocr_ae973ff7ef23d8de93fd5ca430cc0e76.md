```
void access_global()
{
    cout << "In access_global() glob is: " << glob << "\n\n";
}
```

```
void hide_global()
{
    int glob =0;  // hide global variable glob
    cout << "In hide_global() glob is:" << glob << "\n\n";
}
```

```
void change_global()
{
    glob = -10;  // change global variable glob
    cout << "In change_global() glob is:" << glob << "\n\n";
}
```

# Declaring Global Variables

You declare global variables outside of any function in your program file. That's what I do in the following line, which creates a global variable named glob initialized to 10.

```
int glob =10;  // global variable
```

# Accessing Global Variables

You can access a global variable from anywhere in your program. To prove it, I display glob in main() with:

```
cout << "In main() glob is: " << glob << "\n\n";
```

The program displays 10 because as a global variable, glob is available to any part of the program. To show this again, I next call access_global(), and the computer executes the following code in that function:

```
cout << "In access_global() glob is: " << glob << "\n\n";
```

Again, 10 is displayed. That makes sense because I'm displaying the exact same variable in each function.