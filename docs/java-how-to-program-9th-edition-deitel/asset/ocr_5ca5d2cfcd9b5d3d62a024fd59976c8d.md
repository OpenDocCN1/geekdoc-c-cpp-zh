more occurrences of the subexpression immediately preceding "+". So both "A*" and "A+" will match "AAA" or "A", but only "A*" will match an empty string.

If method validateFirstName returns true (line 29 of Fig. 16.21), the application attempts to validate the last name (line 31) by calling validateLastName (lines 13–16 of Fig. 16.20). The regular expression to validate the last name matches any number of letters split by spaces, apostrophes or hyphens.

Line 33 of Fig. 16.21 calls method validateAddress (lines 19–23 of Fig. 16.20) to validate the address. The first character class matches any digit one or more times (\d+). Two \ characters are used, because \ normally starts an escape sequence in a string. So \\d in a String represents the regular expression pattern \d. Then we match one or more white-space characters (\s+). The character "|" matches the expression to its left or to its right. For example, "Hi (John|Jane)" matches both "Hi John" and "Hi Jane". The parentheses are used to group parts of the regular expression. In this example, the left side of | matches a single word, and the right side matches two words separated by any amount of white space. So the address must contain a number followed by one or two words. Therefore, "10 Broadway" and "10 Main Street" are both valid addresses in this example. The city (lines 26–29 of Fig. 16.20) and state (lines 32–35 of Fig. 16.20) methods also match any word of at least one character or, alternatively, any two words of at least one character if the words are separated by a single space, so both Waltham and West Newton would match.

# Quantifiers

The asterisk (*) and plus (+) are formally called quantifiers. Figure 16.22 lists all the quantifiers. We’ve already discussed how the asterisk (*) and plus (+) quantifiers work. All quantifiers affect only the subexpression immediately preceding the quantifier. Quantifier question mark (?) matches zero or one occurrences of the expression that it quantifies. A set of braces containing one number ({n}) matches exactly n occurrences of the expression it quantifies. We demonstrate this quantifier to validate the zip code in Fig. 16.20 at line 40. Including a comma after the number enclosed in braces matches at least n occurrences of the quantified expression. The set of braces containing two numbers ({n,m}), matches between n and m occurrences of the expression that it qualifies. Quantifiers may be applied to patterns enclosed in parentheses to create more complex regular expressions.

| Quantifier | Matches |
|---|---|
| * | Matches zero or more occurrences of the pattern. |
| + | Matches one or more occurrences of the pattern. |
| ? | Matches zero or one occurrences of the pattern. |
| {n} | Matches exactly n occurrences. |
| {n,} | Matches at least n occurrences. |
| {n,m} | Matches between n and m (inclusive) occurrences. |

Fig. 16.22 | Quantifiers used in regular expressions.

All of the quantifiers are greedy. This means that they’ll match as many occurrences as they can as long as the match is still successful. However, if any of these quantifiers is