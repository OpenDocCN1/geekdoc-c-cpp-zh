```
Please enter city:
**Some City**
Please enter state:
**SS**
Please enter zip:
123
Please enter phone:
**123-456-7890**

Validate Result:
Invalid zip code
```

```
Please enter first name:
Jane
Please enter last name:
**Doe**
Please enter address:
**123 Some Street**
Please enter city:
**Some City**
Please enter state:
**SS**
Please enter zip:
12345
Please enter phone:
**123-456-7890**

Validate Result:
Valid input. Thank you.
```

Fig. 16.21 | Inputs and validates data from user using the ValidateInput class. (Part 2 of 2.)

Figure 16.20 validates user input. Line 9 validates the first name. To match a set of characters that does not have a predefined character class, use square brackets, []. For example, the pattern "[aeiou]" matches a single character that’s a vowel. Character ranges are represented by placing a dash (-) between two characters. In the example, "[A-Z]" matches a single uppercase letter. If the first character in the brackets is "^", the expression accepts any character other than those indicated. However, "[^Z]" is not the same as "[A-Y]", which matches uppercase letters A—Y—"[^Z]" matches any character other than capital Z, including lowercase letters and nonletters such as the newline character. Ranges in character classes are determined by the letters’ integer values. In this example, "[A-Za-z]" matches all uppercase and lowercase letters. The range "[A-z]" matches all letters and also matches those characters (such as [ and ]) with an integer value between uppercase Z and lowercase a (for more information on integer values of characters see Appendix B). Like predefined character classes, character classes delimited by square brackets match a single character in the search object.

In line 9, the asterisk after the second character class indicates that any number of letters can be matched. In general, when the regular-expression operator "*" appears in a regular expression, the application attempts to match zero or more occurrences of the subexpression immediately preceding the "*". Operator "+" attempts to match one or