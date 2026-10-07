# 7.8. OUR OWN VERSION OF FIND

This example returns the value 2.
You should remember from Section 5.4 that there can be more than one function with the same name, as long as they take a different number of parameters or different types. In this case, C++ knows which version of find to invoke by looking at the type of the argument we provide.

# 7.8 Our own version of find

If we are looking for a letter in an apstring, we may not want to start at the beginning of the string. One way to generalize the find function is to write a version that takes an additional parameter--the index where we should start looking. Here is an implementation of function.

```
int find(apstring s, char c, int i)
{
  while (i<s.length()) {
    if (s[i] == c) return i;
    i = i + 1;
  }
  return -1;
}
```

Instead of invoking this function on an apstring, like the first version of find, we have to pass the apstring as the first argument. Other arguments the character we are looking for and the index where we should start.

# 7.9 Looping and counting

The following program counts the number of times the letter 'a' appears in a string:

```
apstring fruit = "banana";
int length = fruit.length();
int count = 0;

int index = 0;
while (index < length) {
  if (fruit[index] == 'a') {
    count = count + 1;
  }
  index = index + 1;
}
cout << count << endl;
```

This program demonstrates a common idiom, called a counter. The variable count is initialized to zero then incremented each time we find an 'a'. (To