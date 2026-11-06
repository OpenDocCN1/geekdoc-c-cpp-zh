**P3.21** *Unit conversion.* Write a unit conversion program that asks the users from which unit they want to convert to (fl. oz, gal, oz, lb, in, ft, mi) and to which unit they want to convert (ml, l, g, kg, mm, cm, m, km). Reject incompatible conversions (such as gal → km). Ask for the value to be converted, then display the result:

```
Convert from? gal
Convert to? ml
Value? 2.5
2.5 gal = 9462.5 ml
```

**P3.22** Write a program that prompts the user to provide a single character from the alphabet. Print Vowel or Consonant, depending on the user input. If the user input is not a letter (between a and z or A and Z), or is a string of length > 1, print an error message.

**P3.23** *Roman numbers.* Write a program that converts a positive integer into the Roman number system. The Roman number system has digits

| Roman numeral | Value |
|---|---:|
| I | 1 |
| V | 5 |
| X | 10 |
| L | 50 |
| C | 100 |
| D | 500 |
| M | 1,000 |

Numbers are formed according to the following rules. (1) Only numbers up to 3,999 are represented. (2) As in the decimal system, the thousands, hundreds, tens, and ones are expressed separately. (3) The numbers 1 to 9 are expressed as

| Roman numeral | Value |
|---|---:|
| I | 1 |
| II | 2 |
| III | 3 |
| IV | 4 |
| V | 5 |
| VI | 6 |
| VII | 7 |
| VIII | 8 |
| IX | 9 |

As you can see, an I preceding a V or X is subtracted from the value, and you can never have more than three I’s in a row. (4) Tens and hundreds are done the same way, except that the letters X, L, C, and D, M are used instead of I, V, X, respectively. Your program should take an input, such as 1978, and convert it to Roman numerals, MCMLXXVIII.

![](bbox=[0.605, 0.745, 0.892, 0.881])