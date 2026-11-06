This macro would be listed in the rule for the final executable file. That way, when you make the executable file, the make utility first sees whether these two `.o` files are up-to-date. If not, make first makes these two `.o` files, based on the rules you supplied earlier. Nice and simple; it’s too bad that Makefiles are so ugly.

# Creating multiple files

Before two source files can work together, they must somehow find out about each other. Just because they’re both sitting on the computer doesn’t mean that they know about each other. Computers are kind of goofy about that sort of thing. To get two source files to finally open up and get to know each other, you need to tell each of them about what’s in the other file.

When you write a function, normally the function must appear before any calls to it appear within the same source file. That’s because of the way the compiler parses the code: If the compiler encounters a call to a function but has not yet heard of that function, it issues an error. But the way around this is to use a function prototype. A function prototype is simply the header line from a function, ending with a semicolon, as in the following:

```
```cpp
void BigDog(int KibbleCount);
```
```

Later in the source file is the actual function, with this header line duplicated. But instead of a semicolon, the function would have an open brace, the function code, and a closing brace, as in the following:

```
```cpp
void BigDog(int KibbleCount)
{
    cout << "I'm a lucky dog" << endl;
    cout << "I have " << KibbleCount << " pieces of food" << endl;
}
```
```

So, after the function prototype, you can call the function whether the function code itself is before or after the call.

![](bbox=[0.154, 0.696, 0.228, 0.765])

For the compiler to understand a function call, all it needs at the point that the code makes the call is a function prototype. It’s up to the linker to determine whether that function really exists.

Because the function call needs only a function prototype, you can put the function itself in another source code file. You could, therefore, have two separate source code files, as in the MultipleSourceFiles example, shown in Listings 6-1 and 6-2. (The first source code file — main.cpp — is shown in Listing 6-1, and the second source code file — mystuff.cpp — is shown in Listing 6-2.)