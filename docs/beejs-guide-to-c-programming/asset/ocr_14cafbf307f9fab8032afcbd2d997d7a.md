```
for (int j = 0; j < 3; j++) {
    for (int k = 0; k < 3; k++) {
        printf("%d, %%d, %%d\n", i, j, k);
    }
}
```

```
continue; // Gets us to the next iteration of k
break; // Gets us to the next iteration of j
????; // Gets us to the next iteration of i???
```

```
}
}
```

The goto statement offers us a way!

```
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        for (int k = 0; k < 3; k++) {
            printf("%d, %%d, %%d\n", i, j, k);
        }
    }
```

```
goto continue_i; // Now continuing the i loop!
```

```
continue_i;
}
```

We have at the end here—that's because you can't have a label pointing to the plain end of a compound statement (or before a variable declaration).

# 31.3 Bailing Out

When you're super nested in the middle of code, you can use goto to get out of it in a manner that's often cleaner than nesting more ifs and using flag variables.

```
// Pseudocode
```

```
for(...) {
    for (...) {
        while (...) {
            do {
                if (some_error_condition)
                    goto bail;
            } while(...);
        }
    }
```

bail:

```
// Cleanup here
```

Without goto, you'd have to check an error condition flag in all of the loops to get all the way out.