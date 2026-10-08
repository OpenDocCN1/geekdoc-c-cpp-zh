# CHAPTER 13 Strings

(continued)

| Input | Processing | Output |
| --- | --- | --- |
| annual income | Processing items: character subscript (o) | annual income with no commas or spaces |

```
Algorithm:
1. enter the annual income
2. repeat while (the annual income is not '-1')
   repeat while (the character subscript is less than the length of the annual income)
   if (the current character in the annual income is either a comma or a space)
     remove the current character from the annual income
   else
     add 1 to the character subscript to look at the next character in the annual income
   end if
repeat
display the annual income with no commas or spaces
```

```
enter the annual income
reset the character subscript to O
end repeat
```

![](bbox=[0.312, 0.546, 0.843, 0.563])

# Removing Characters from a string Variable

At times, you may need to remove one or more characters from an item of data entered by the user, such as a digit sign from the beginning of a sales amount or a percent sign from the de tax rate. In C++, you can use the string class's erase function to remove one or more characters located within a string variable. Figure 13-25 shows the function's syntax. In the syntax, the name of a string variable, and the subscript argument is the subscript of the first character you want to remove (erase) the variable's contents. Returns The first character in a string has a subscript of 0. The count argument is an integer that specifies the number of characters you want to remove. If you omit the count argument, the erase function removes all characters from the subscript position to the end of the string. Figure 13-25 also shows examples of using the erase(0, 7); statement in Example 1 tells the computer to remove the first seven characters from the string stored in the place variable. In this case, the computer removes the letters S, a, l, e, and space characters. After the string is processed, the place variable contains "Oregon". The place.erase(5); statement in Example 2 tells the computer to remove all of characters from the place variable, beginning with the character whose subscript is 5. In this case, the statement removes the "Oregon" portion of the string variable.