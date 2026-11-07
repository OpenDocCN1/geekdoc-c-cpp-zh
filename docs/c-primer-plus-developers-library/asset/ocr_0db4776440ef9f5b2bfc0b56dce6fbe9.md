```
~~~cpp
    cin >> by;
    cout << "Counting by " << by << "s:\n";
    for (int i = 0; i < 100; i = i + by)
        cout << i << endl;
    return 0;
}
~~~
```

Here is a sample run of the program in Listing 5.5:

```
~~~text
Enter an integer: 17
Counting by 17s:
0
17
34
51
68
85
~~~
```

When `i` reaches the value 102, the loop quits. The main point here is that the update expression can be any valid expression. For example, if you want to square `i` and add 10 in each cycle, you can use `i = i * i + 10`.

Another point to note is that it often is a better idea to test for inequality than equality. For example, the test `i == 100` would have failed in this case because `i` skips over the value 100.

Finally, this example illustrates the use of using declarations instead of a using directive.

# ### Inside Strings with the `for` Loop

The `for` loop provides a direct way to access each character in a string in turn. For example, Listing 5.6 enables you to enter a string and then displays the string character-by-character, in reverse order. You could use either a `string` class object or an array of `char` in this example because both allow you to use array notation to access individual characters in a string. Listing 5.6 uses a `string` class object. The `string` class `size()` method yields the number of characters in the string; the loop uses that value in its initializing expression to set `i` to the index of the last character in the string, not counting the null character. To count backward, the program uses the decrement operator (`--`) to decrease the array subscript by one in each loop. Also Listing 5.6 uses the greater-than-or-equal-to relational operator (`>=`) to test whether the loop has reached the first element. We'll summarize all the relational operators soon.

Listing 5.6   `forstr1.cpp`

```
~~~cpp
// forstr1.cpp -- using for with a string
#include <iostream>
#include <string>
int main()
{
~~~
```