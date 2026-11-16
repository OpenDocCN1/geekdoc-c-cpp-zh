# # Comma Operator

Once in a while, you find yourself in a situation in which C expects a single expression, but you have two things you want to say. The most common (and in fact the only common) example is in a `for` loop, specifically the first and third controlling expressions. What if, for example, you want to have a loop in which `i` counts up from 0 to 10 at the same time that `j` is counting down from 10 to 0? You could manipulate `i` in the loop header and `j` “by hand":

```
```c
// comma1.c
...
j = 10;
for(i = 0; i < 10; i++) {
    ... rest of loop ...
    j--;
}
```
```

But here it's harder to see the parallel nature of `i` and `j`, and it also turns out that this won't work right if the loop contains a `continue` statement. (A `continue` would jump back to the top of the loop, and `i` would be incremented but `j` would _not_ be decremented.) You could compute `j` in terms of `i`:

```
```c
// comma2.c
...
for(i = 0; i < 10; i++) {
    j = 10 - i;
    ... rest of loop ...
}
```
```

but this also makes `j` needlessly subservient. The usual way to write this loop in C would be:

```
```c
// comma3.c
...
for(i = 0, j = 10; i < 10; i++, j--) {
    ... rest of loop ...
}
```
```