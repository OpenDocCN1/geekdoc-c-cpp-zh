For more regular-sized numbers, always adding an exponent component is typically not ideal, as can be seen from our example (where pi has exponent +00). This is where the **general formatting** option (g or G) comes in handy: by default it is equivalent to fixed-point formatting (f or F), only for very small or large numbers (the exact heuristic is not that important), it switches to scientific formatting (e or E) and adds the exponent. You can give it a run by assigning different values (large or small) to the pi constant in Ex2_06.

# Argument Indexes

Being the perceptive, critical reader that you are, you have of course been wondering why we put a colon in front of each format specifier. The reason, of course, is that there is still something that you can add to the left of this colon as well. And that something is an **argument index**. Until now all replacement fields were matched with arguments of `std::format()` in a left-to-right order. You can override this, however, by adding an argument index to each replacement field. To illustrate, consider the following variation of our favorite `format()` expression.

```
```cpp
std::cout << std::format(
    "{1:.2f} feet is the diameter required for a pond with {0} fishes.\n",
    fish_count, pond_diameter
);
```
```

By rephrasing our sentence we have swapped the order of the two replacement fields. To then keep the order of the other two arguments, fish_count and pond_diameter, the same, we had to add an argument index to both replacement fields. This index is separated from the format specifier by a colon. If no format specifier is required, the index is not followed by a colon.
The semantics of an argument index should be rather straightforward. The only thing to watch out for is that you have to start counting at zero: the first argument, fish_count, has index 0, the second index 1, and so on. This may seem odd as first, but that is just the way indexes always work in C++. In Chapter 5, for instance, you'll encounter the same phenomenon again when working with arrays.

> **Note** Of course, in our toy example the argument indexes are not really required. You could instead simply swap the order of the fish_count and pond_diameter arguments as well. It would even make the code clearer to do so. But the need for out-of-order formatting does arise in real-life scenarios, where you, as a developer, are not necessarily the one supplying the (final) format string. Instead, a technical writer may be entering user-facing text (where the order may change for grammatical reasons), or a translator may be providing translated messages (where the order may even differ between different languages). It would be a shame if a program had to be reworked each time one of these texts changes.

Besides reordering fields, you can also use argument indexes to format the same input value more than once. The second output statement of Ex2_06, for instance, could be written as follows (see Ex2_06B):

```
```cpp
std::cout << std::format("Default: {0}, binary: {0:b}, hex.: {0:x}\n", 314);
```
```