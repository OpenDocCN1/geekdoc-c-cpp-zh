chosen file format. For example, one can directly test the values of the string elements. Hence, if you want to filter out comment lines, which start by a '#' character, you can test whether `s[0] == #`. If yes, then one can continue with the next line.

A very convenient way to process strings is available if they follow some format, e.g. in case they were generated using `fprintf()` or similar functions. In this case one can use `sscanf()` which is basically the inversion of `sprintf()`: One has to supply as parameters an input string, which is to be analyzed, and a format string which may contain printable characters, escape sequences, and conversion specifiers. Depending on the conversion specifiers, pointers to variables also have to be supplied, one for each conversion specifier indicating a value to be read in.^10 The string is analyzed by comparing it to the format string. Whenever a conversion specifier in the format string is encountered, the corresponding value is extracted from the input string and stored in the given variable. This processing continues until the full input string is analyzed, or until the first mismatch between format string and input string is detected. For example, if the string s contains "particles: 20 runs: 100", then the call to

```
    int num_read;
    int num_part = 0, num_runs = 0;
```

```
    num_read= sscanf(s, "particles: %d runs: %d", &num_part, &num_runs);
```

will assign the value 20 to num_part and 100 to num_runs, and will return the value 2, which is assigned to num_read. If the format string contains a mismatch, then the processing stops. Thus

```
    num_read= sscanf(s, "particles: %d Runs: %d", &num_part, &num_runs)
```

will only assign the first variable num_part, while num_runs remains at its initial value 0, and num_read will be 1. Therefore, if you are only interested in the number of particles anyway, you may also use

```
    num_read = sscanf(s, "particles: %d", &num_part)
```

The conversion specifiers are the same as for `printf()`. There is one important point: When you print a variable of type float or double, you can use a conversion specifier `%f` in both cases. But when reading in

10 There may also appear the conversion specifier modification `*` right behind the '%' character which results in skipping the corresponding value; hence, no pointer should be supplied for this item.