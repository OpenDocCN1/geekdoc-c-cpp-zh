```
```cpp
  7      std::cout << "Default alignment with field width 10:\n"
  8                << std::format("[{:10f}]\n[{:10}]\n", 27, 3.5, "hello");
  9
 10      std::cout << "Specifying left or right alignment in a field:\n"
 11                << std::format("[{:<15d}]\n[{:<15f}]\n[{:>15}]\n",
 12                                27, 3.5, "hello");
 13
 14      std::cout << "Centering text in a field:\n"
 15                << std::format("[{:^7d}]\n[{:^7.1f}]\n[{:^7}]\n", 27, 3.5, "hello");
 16      }
```
```

```
```text
Default alignment with field width 10:
[        27]
[  3.500000]
[hello     ]

Specifying left or right alignment in a field:
[27           ]
[3.500000     ]
[         hello]

Centering text in a field:
[  27  ]
[ 3.5  ]
[ hello ]
```
```

**Fig. 19.21** | C++20 text-formatting with field widths and alignment. (Part 2 of 2.)

Recall that you can specify left-alignment and right-alignment with `<` and `>`. Lines 11–12 **left-align** the numeric values 27 and 3.5 and **right-align** the string `"hello"` in fields of 15 characters

The I/O streams output formatting shown earlier in this chapter does not support center-aligning text, but `std::format` can do this conveniently with `^`, as shown in line 15. Centering attempts to spread the unoccupied character positions equally to the left and right of the formatted value. `std::format` places the extra space to the right if an odd number of character positions remain, as you can see for the value 27, which has two spaces to its left and three to its right.

# ### 19.9.3 C++20 std::format Numeric Formatting

Figure 19.22 demonstrates various C++20 numeric formatting capabilities. By default, negative numeric values display with a - sign. Sometimes it's desirable to force a + sign to display for a positive number. A + in the format specifier (line 8) indicates that the numeric value should always be preceded by a sign (+ or -). To fill the field's remaining characters with 0s rather than spaces, place 0 before the field width and *after* the + if there is one, as in line 8's second format specifier. A space in the format specifier (as in line 11's second and third format specifiers) indicates that positive numbers should show a space character in the sign position. This is useful for aligning positive and negative values for display purposes. Note that the two values with a space in their format specifiers align. If a field width is specified, place the space before the field width. To precede a binary, octal or hexadecimal number with its base, use # in the format specifier as in line 14.