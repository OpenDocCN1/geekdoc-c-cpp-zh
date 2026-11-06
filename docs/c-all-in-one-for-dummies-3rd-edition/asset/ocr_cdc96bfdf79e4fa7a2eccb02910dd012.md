Book I
Chapter 7
Referring to Your Data through Pointers

string variable itself is off in the heap somewhere and has no name. And if it's going to make comments like those heard at a fine restaurant, it's probably best that it remain nameless.

![](bbox=[0.09, 0.21, 0.21, 0.28])

When you store a string of characters in a string variable that you allocated by using new, you are storing the string in the allocated memory, not in the pointer variable. The pointer variable still holds the address of the allocated memory. The pointer is simply the publicist for the memory, handling all its deals and transactions for it, whether ethical or not.

![](bbox=[0.09, 0.3, 0.21, 0.37])

When you are working with strings, you can use a shortcut to the somewhat cumbersome method of putting parentheses around the name, preceded by an asterisk, in order to call the various string functions. (That was even hard to type!) Instead of typing (*Password).length(), for example, you can use a shortcut notation that looks like the following line of code (the characters after Password are a minus sign and then a greater-than sign, which together resemble an arrow):

```
cout << Password->length() << endl;
```

![](bbox=[0.09, 0.44, 0.21, 0.51])

You can initialize a string by using parentheses when you call new for a string type. To do this, simply put the string in quotes and then in parentheses after the word string, as in the following line of code:

```
string *Password = new string("The egg salad is still not fresh.");
```

This line is equivalent to the first two lines of code inside main in Listing 7-9.

![](bbox=[0.09, 0.61, 0.21, 0.7])

Even though the pointer points to a string, the pointer itself still holds a number (in particular, the address of the string it's pointing to). This is a number, but do not confuse it with an integer. However, you can do some basic arithmetic with pointers, as detailed in Book I, Chapter 9.

# Freeing Pointers

When you allocate memory on the heap by calling the new function and you're finished using the memory, you need to let the computer know, whether it's just a little bit of memory or a lot. The computer doesn't look ahead into your code to find out whether you're still going to use the memory. So in your code, when you are finished with the memory, you free the memory.

The way you free the memory is by calling the delete function and passing the name of the pointer:

```
delete MyPointer;
```