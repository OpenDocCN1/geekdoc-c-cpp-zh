# CHAPTER 5 — Scalars and Formatting

use `sprintf()`, you can first master the features of `printf()`. Both functions represent different and more powerful versions of the `print()` function.

Formatting encompasses a variety of activities. For example, you can use `printf()` to cast your data in different ways. Casting might involve making a number appear as a letter, or you can make a letter appear as a number. You can transform an integer into a float or a float into an integer. You can also control strings so that they are of uniform length, allowing you to create columns in a table. Figure 5.7 illustrates the main features of the `printf()` function.

![](bbox=[0.076, 0.277, 0.727, 0.439])

If you have worked with the C programming language, you recognize the `printf()` function as a familiar, powerful entity. The Perl interpreter incorporates most of the features of the `printf()` function from the C programming language. As Figure 5.7 illustrates, two sets of arguments characterize the `printf()` function. The first consists of information you provide inside quotation marks. The other consists of data that you provide in the form of identifiers. A comma separates the two sets of arguments.

# Conversion Specifiers

To use the `printf()` function, you employ one or more output specifiers to format the data you want to print. A specifier both designates the location in the output string at which you want to locate data and identifies the type and other characteristics of the data. As for the arguments pertaining to the data you provide to the `printf()` function, you can use as many identifiers or literal strings or values as you want, so long as you include a specifier inside the quotes to cover each value you introduce. Consider the examples in Listing005_07.

```
```text
#Listing005_07

#1 Use of decimals, scientific notation, and display

#1 Initialize identifiers
$LightYear = 9.6 * (10 ** 12); #kilometers
$DToProximaCentauri = 4.26; #light years
```
```