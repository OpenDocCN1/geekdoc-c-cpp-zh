The loop condition is essentially the same as you have seen in earlier code fragments. Within the loop body you update the indicators array element at position index to be a '^' character before incrementing index ready for the next iteration. When the loop ends, count contains the number of punctuation characters that were found, and indicators will contain '^' characters at the positions in sentence where such characters were found.

The output is produced by the statements:

```
Console::WriteLine(L"There are {0} punctuation characters in the string:",
    count);
Console::WriteLine(L"\n{0}\n{1}" sentence, gcnew String(indicators));
```

The second statement creates a new String object on the heap from the indicators array by passing the array to the String class constructor. A class constructor is a function that will create a class object when it is called. You'll learn more about constructors when you get into defining your own classes.

# Tracking References

A tracking reference provides a similar capability to a native C++ reference in that it represents an alias for something on the CLR heap. You can create tracking references to value types on the stack and to handles in the garbage-collected heap; the tracking references themselves are always created on the stack. A tracking reference is automatically updated if the object referenced is moved by the garbage collector.

You define a tracking reference using the % operator. For example, here's how you could create a tracking reference to a value type:

```
int value = 10;
int% trackValue = value;
```

The second statement defines stackValue to be a tracking reference to the variable value, which has been created on the stack. You can now modify value using stackValue:

```
trackValue *= 5;
Console::WriteLine(value);
```

Because trackValue is an alias for value, the second statement outputs 50.

# Interior Pointers

Although you cannot perform arithmetic on the address in a tracking handle, C++/CLI does provide a form of pointer with which it is possible to apply arithmetic operations; it's called an interior pointer and is defined using the keyword interior_ptr. The address stored in an interior pointer can be updated automatically by the CLR garbage collection when necessary. An interior point is always an automatic variable that is local to a function.