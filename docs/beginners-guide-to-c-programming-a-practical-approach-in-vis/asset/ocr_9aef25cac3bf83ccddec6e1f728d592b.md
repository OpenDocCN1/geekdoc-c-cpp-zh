6. Double-click the Button to create its Click event handler method. We will insert our code inside this method as usual. Let's first take the Text of the checkTextBox and then assign it to a string type variable named input as follows:

```
```
string input = usernameTextBox.Text;
```
Code 8.24
```

7. We'll switch the input variable against the usernames we decide in this example. Let us use the strings John and James as the reference usernames in the switch statements as follows:

```
```
switch (input)
{
    case "John":
        MessageBox.Show("Successful entry");
        break;
    case "James":
        MessageBox.Show("Successful entry");
        break;
    default:
        MessageBox.Show("Username not found");
        break;
}
```
Code 8.25
```

> Note that the switch-case structure is automatically formed in Visual Studio when we write switch and then press the Tab key twice on the keyboard.

In this code, we compare the input variable against two cases. If input is "John", then the block inside the case "John": statement is executed. Note that the case statements do not have curly brackets but just use semicolons to state the blocks. Also note the usage of the break keyword in each of the case blocks. They indicate a break, i.e. exit when the respective case is satisfied. We need to use the break keyword in case blocks, otherwise the compiler would give an error. If none of the cases is satisfied, then the default block will be executed. Therefore, if the user enters a username other than John or James, the program will display a message box with the text "Username not found".