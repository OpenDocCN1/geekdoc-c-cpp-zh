A more professional approach is to state the looping condition in the test of the loop:

```
// search for whitespace character
for (i = 0; s[i] != ' ' && s[i] != '\t' && s[i] != '\n'; ++i) {
}
```

We can also generalize the idea of whitespace:

```
for (i = 0; !isspace(s[i]); ++i) {
}
```

We'll soon be taking a closer look at strings.

recursion: 递归 (回溯) (拼音)
f(n) = g(f(n-1))   called : factorial

+   2!
+   3!
+   4!
+   n!

```
int fact(int n)
{
    if (n == 1)
        return 1;
    else
        return n * fact(n-1);
}
```

5! = 5 * 4 * 3 * 2 * 1