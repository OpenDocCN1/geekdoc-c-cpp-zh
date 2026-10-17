# Notice: In flowcharts, in order to calculate the quotient of an integer division, you can use the popular DIV operator. An example is shown here.

![](bbox=[0.381, 0.126, 0.646, 0.191])

# Exercise 13.1-2 — Finding the Sum of Digits

Write a PHP script that prompts the user to enter a four-digit integer and then calculates the sum of its digits.

# Solution

What you should keep in mind here is that statements like this one

```
```php
$number = trim(fgets(STDIN));
```
```

assign the given four-digit integer to one single variable, `$number`, and not to four individual variables.

So, first you must split the integer into its four digits and assign each digit to a separate variable. Then you can calculate the sum of these four variables and get the required result. There are two approaches available.

# First Approach

Let’s try to understand the first approach using an arithmetic example. Take the number 6753, for example.

| Step | Explanation |
|---|---|
| **First digit = 6** | The first digit can be isolated if you divide the given number by 1000 to get the integer quotient  
`$digit1 = intval(6753 / 1000)` |
| **Remaining digits = 753** | The remaining digits can be isolated if you divide the given number by 1000 to get the integer remainder  
`$r = 6753 % 1000` |
| **Second digit = 7** | The second digit can be isolated if you divide the remaining digits by 100 to get the integer quotient  
`$digit2 = intval(753 / 100)` |
| **Remaining digits = 53** | The remaining digits are now  
`$r = 753 % 100` |
| **Third digit = 5** | The third digit can be isolated if you divide the remaining digits by 10 to get the integer quotient  
`$digit3 = intval(53 / 10)` |