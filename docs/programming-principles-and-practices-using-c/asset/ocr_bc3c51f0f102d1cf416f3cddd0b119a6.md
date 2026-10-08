first you often look at a blank screen (or window), wondering why your program could have failed to produce any output. A common first problem with a Windows console-mode program is that the console window disappears before you have had a chance to see the output (if any). One solution is to call `keep_window_open()` from our **std_lib_facilities.h** at the end of **main()**. Then the program will ask for input before exiting and you can look at the output produced before giving it the input that will let it close the window.

When looking for a bug, carefully follow the code statement by statement from the last point that you are sure it was correct. Pretend you’re the computer executing the program. Does the output match your expectations? Of course not, or you wouldn’t be debugging.

+   Often, when you don’t see the problem, the reason is that you “see” what you expect to see rather than what you wrote. Consider:

```
for (int i = 0; i<=max; ++i) {          // oops! (test)
    for (int i=0; i<max; ++i);            // print the elements of v
    cout << "v[" << i << "]==" << v[i] << '\n';
    // ...                                      // ...
}
```

This last example came from a real program written by experienced pro-grammers (we expect it was written very late some night).

+   Often when you do not see the problem, the reason is that there is too much code being executed between the point where the program pro-duced the last good output and the next output (or lack of output). Most programming environments provide a way to execute (“step through”) the statements of a program one by one. Eventually, you’ll learn to use such facilities, but for simple problems and simple programs, you can just temporarily put in a few extra output statements (using `cerr`) to help you see what’s going on. For example:

```
int my_fct(int a, double d)
{
    int res = 0;
    cerr << "my_fct(" << a << "," << d << ")\n";
    // ... misbehaving code here ...
    cerr << "my_fct() returns " << res << "\n";
    return res;
}
```

+   Insert statements that check invariants (that is, conditions that should always hold; see §9.4.3) in sections of code suspected of harboring bugs. For example: