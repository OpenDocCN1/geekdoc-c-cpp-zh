"presentation".

The WriteTable() method first prints out the "headers".

```
```
Write("     ");
for (var v = low; v < high; v++) {
    Write($"{v,4}");
}
WriteLine("");
```
```

In this example, we use 4 spaces for the width of each "table cell", as indicated by the format specifier {v,4} in the string interpolation. Note that Console.Write() is essentially the same method as Console.WriteLine(), but it does not automatically add a newline at the end.

Then, the "divider":

```
```
Write("     ---");
for (var v = low; v < high; v++) {
    Write(" ---");
}
WriteLine("");
```
```

Again, 4 spaces per "cell". (We could have used a const for this fixed length.)

How does one know if this prints out what one wants? It's generally done via "trial and errors". Print out something first and, based the result, change the formatting slightly, etc.

It sounds tedious. But, a lot of programming tasks involve tedious work in case you are new to programming and have romantic ideas. ☺

Finally, the body of the table is printed with "row headers" for each row: