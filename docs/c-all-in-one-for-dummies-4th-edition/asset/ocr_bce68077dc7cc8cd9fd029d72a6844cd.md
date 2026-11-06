![](bbox=[0.165, 0.08, 0.23, 0.15])

Although you can specify the field width, you're actually specifying a minimum. If the characters in the output are less than the field width, the runtime library will pad them with spaces to make them that minimum size. If they are bigger than that width, the library doesn't chop them off to make them fit. If you add letters to the Hank Williams line in Listing 2-4 (like this: `sals << setw(20) << "Hank WilliamsABCDEFGHIJ"`);, the output looks like the following example instead. The Hank Williams line runs beyond the 20 characters into the next field.

| Name | Salary |
|---|---|
| Hank WilliamsABCDEFGHIJ | 28422 82 |
| Buddy Holly | 39292.22 |
| Otis Redding | 43838.55 |