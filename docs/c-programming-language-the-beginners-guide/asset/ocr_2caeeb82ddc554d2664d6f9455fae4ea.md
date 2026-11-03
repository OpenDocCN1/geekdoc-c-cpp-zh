This code is another version of the previous example. Here, the for loop moves through each pointer in the array. For each iteration, the pointer variable cptr is assigned to the base address of each string. A while loop then churns through the strings one character at a time. Build and run this code.

The output is the same, although the method of printing each string was different. Pointer variable cptr is used to display each character by walking through the memory locations where the characters are stored. Now something might bother you about this code. That's line 17, if you haven't picked it up already. It uses array notation.

A better solution would be to convert this heinous notation into pointer notation. To do so, make this change to the code:

```
```text
1 #include 2
3 int main()
4 {
```
```

+   - char *gang[5] = {
+   - "Spanky",
+   - "Buckwheat",
+   - "Alfalfa",
+   - "Darla",
+   - "Pete the Pup"

```
```text
11 };
```
```

+   - int x;
+   - char *cptr;