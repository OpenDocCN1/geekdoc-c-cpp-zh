**Step 6**  Test your function.

Supply a program for testing this function only:

```
```cpp
int main()
{
    srand(time(0));
    for (int i = 1; i <= 10; i++)
    {
        cout << random_character("abcdef");
    }
    cout << endl;
    return 0;
}
```
```

When you run this program, you might get an output such as

```
```text
acfdfeefac
```
```

This confirms that the function works correctly.

# Repeat for the Second Helper Function

Finally, we implement the second helper function, which inserts a string containing a single character at a random location in a string.

**Step 1**  Describe what the function should do.

Suppose we have a string "arxcsw" and a string "8". Then the second string should be inserted at a random location in a string such as "ar8xcsw" or "arxcsw8". Actually, it doesn’t matter that the second string has length 1, so we will simply specify that our function should insert an arbitrary string into a given string.

**Step 2**  Determine the function’s “inputs”.

The first input is the string into which another string should be inserted. The second input is the string to be inserted.

**Step 3**  Determine the types of the parameter variables and the return value.

The inputs are both of type `string`. The return value is also a string. We can now fully describe our function:

```
```cpp
/**
    Inserts one string into another at a random position.
    @param str the string into which another string is inserted
    @param to_insert the string to be inserted
    @return the result of inserting to_insert into str
*/
string insert_at_random(string str, string to_insert)
```
```

**Step 4**  Write pseudocode for obtaining the desired result.

There is no predefined function for inserting a string into another. Instead, we need to find the insertion position and then “break up” the first string by taking two substrings: the characters up to the insertion position, and the characters following it.

How many choices are there for the insertion position? If `str` has length 6, there are seven choices:

+   1. `|arxcsw`
+   2. `a|rxcsw`
+   3. `ar|xcsw`
+   4. `arx|csw`
+   5. `arxc|sw`