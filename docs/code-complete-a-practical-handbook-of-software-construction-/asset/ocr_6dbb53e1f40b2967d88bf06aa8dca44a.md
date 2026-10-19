# ## 12.1 Numbers in General

> > **Cross-Reference** For more details on named constants instead of magic numbers, see Section 12.7, “Named Constants,” later in this chapter.

Here are several guidelines for making your use of numbers less error-prone:

**Avoid “magic numbers”** Magic numbers are literal numbers, such as *100* or *47524*, that appear in the middle of a program without explanation. If you program in a language that supports named constants, use them instead. If you can’t use named constants, use global variables when it’s feasible to do so.

Avoiding magic numbers yields three advantages:

+   - Changes can be made more reliably. If you use named constants, you won’t overlook one of the *100*s or change a *100* that refers to something else.
+   
+   - Changes can be made more easily. When the maximum number of entries changes from *100* to *200*, if you’re using magic numbers you have to find all the *100*s and change them to *200*s. If you use *100+1* or *100-1*, you’ll also have to find all the *101*s and *99*s and change them to *201*s and *199*s. If you’re using a named constant, you simply change the definition of the constant from *100* to *200* in one place.
+   
+   - Your code is more readable. Sure, in the expression
+   
+     ```
+     for i = 0 to 99 do ...
+     ```
+   
+     you can guess that 99 refers to the maximum number of entries. But the expression
+   
+     ```
+     for i = 0 to MAX_ENTRIES-1 do ...
+     ```
+   
+     leaves no doubt. Even if you’re certain that a number will never change, you get a readability benefit if you use a named constant.

**Use hard-coded 0s and 1s if you need to** The values *0* and *1* are used to increment, decrement, and start loops at the first element of an array. The *0* in

```text
for i = 0 to CONSTANT do ...
```

is OK, and the *1* in

```text
total = total + 1
```

is OK. A good rule of thumb is that the only literals that should occur in the body of a program are *0* and *1*. Any other literals should be replaced with something more descriptive.

**Anticipate divide-by-zero errors** Each time you use the division symbol (/ in most languages), think about whether it’s possible for the denominator of the expression to be 0. If the possibility exists, write code to prevent a divide-by-zero error.