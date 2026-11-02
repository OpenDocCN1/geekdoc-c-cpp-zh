# 5.5 Functions Without Return Values

Use a return type of void to indicate that a function does not return a value.

![](bbox=[0.55, 0.22, 0.92, 0.48])

© jgroup/Stockphoto.

*A void function returns no value, but it can produce output.*

Sometimes, you need to carry out a sequence of instructions that does not yield a value. If the instruction sequence occurs multiple times, you will want to package it into a function. In C++, you use the return type void to indicate the absence of a return value. Here is a typical example. Your task is to print a string in a box, like this:

```
------
!Hello!
------
```

However, different strings can be substituted for Hello. A function for this task can be declared as follows:

```
void box_string(string str)
```

Now you develop the body of the function in the usual way, by formulating a general method for solving the task.

+   - n = the length of the string
+   - Print a line that contains the - character n + 2 times.
+   - Print a line containing the string, surrounded with ! to the left and right.
+   - Print another line containing the - character n + 2 times.

Here is the function implementation:

```
/**
Prints a string in a box.
@param str the string to print
*/
void box_string(string str)
{
  int n = str.length();
  for (int i = 0; i < n + 2; i++) { cout << "-"; }
  cout << endl;
  cout << "!" << str << "!" << endl;
  for (int i = 0; i < n + 2; i++) { cout << "-"; }
  cout << endl;
}
```