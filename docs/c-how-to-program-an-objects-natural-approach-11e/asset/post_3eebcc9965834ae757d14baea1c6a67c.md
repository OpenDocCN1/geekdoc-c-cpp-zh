
Of the survivors, about two-thirds were women, and first-class passengers survived at a higher rate than the other passenger classes.

```cpp
// percentages who survived by male/female, 1st/2nd/3rd class
std::cout << std::format("Female survivor percentage: {:.2f}%\n",
    100.0 * survivingFemales / survivorCount)
    << std::format("Male survivor percentage: {:.2f}%\n",
        100.0 * survivingMales / survivorCount)
    << std::format("1st class survivor percentage: {:.2f}%\n",
        100.0 * surviving1st / survivorCount)
    << std::format("2nd class survivor percentage: {:.2f}%\n",
        100.0 * surviving2nd / survivorCount)
    << std::format("3rd class survivor percentage: {:.2f}%\n",
        100.0 * surviving3rd / survivorCount);
```

```text
Female survivor percentage: 67.80%
Male survivor percentage: 32.20%

1st class survivor percentage: 40.00%
2nd class survivor percentage: 23.80%
3rd class survivor percentage: 36.20%
```

## Checkpoint

1. *(Fill-in)* The first row of a CSV file typically contains ________.  
   **Answer:** column names.

2. *(Fill-in)* In a CSV file representing a dataset, the rows contain the data and the columns are often called the dataset’s ________.  
   **Answer:** features.

3. *(True/False)* A benefit of the `std::ranges` algorithms is that you do not need to specify the beginning and end of the container—the `std::ranges` algorithms handle this for you, simplifying your code.  
   **Answer:** True.

## 8.20 Objects—Natural Data Science Case Study: Intro to Regular Expressions

Sometimes you’ll need to recognize patterns in text, like phone numbers, e-mail addresses, ZIP codes, webpage addresses, Social Security numbers and more. A regular expression string describes a search pattern for matching characters in other strings. Regular expressions can help you extract data from unstructured text, such as social media posts. They’re also important for ensuring that data is in the proper format before you attempt to process it.

### Validating Data

Before working with text data, you’ll often use regular expressions to validate it. For example, you might check that:

- A U.S. ZIP code consists of five digits (such as 02215) or five digits followed by a hyphen and four more digits (such as 02215-4775).

### Matching Literal Characters

The `<regex>` function `regex_match` returns true if the entire string in its first argument matches the pattern in its second argument. By default, pattern matching is case-sensitive. Later, you’ll see how to perform case-insensitive matches. Let’s begin by matching literal characters—that is, characters that match themselves. Line 9 creates a regex object `r1` for the pattern `"02215"`, containing only literal digits that match themselves in the specified order. Line 12 calls `regex_match` for the strings `"02215"` and `"51220"`. Each has the same digits, but only `"02215"` has them in the correct order for a match.

```cpp
// fig08_16.cpp
// Matching entire strings to regular expressions.
#include <format>
#include <iostream>
#include <regex>

int main() {
    // fully match a pattern of literal characters
    std::regex r1{"02215"};
    std::cout << std::format("Matching against: 02215\n"
        "02215: {}; 51220: {}\n\n",
        std::regex_match("02215", r1), std::regex_match("51220", r1));
}
```

```text
Matching against: 02215
02215: true; 51220: false
```

**Fig. 8.16**  Matching entire strings to regular expressions.

### Metacharacters, Character Classes and Quantifiers

Regular expressions typically contain various special symbols called metacharacters:

- `[]`  `{}`  `()`  `\`  `*`  `+`  `^`  `$`  `?`  `.`  `|`

The `\` metacharacter begins each of the predefined character classes, several of which are shown in the following table with the groups of characters they match.

| Character class | Matches |
|---|---|
| `\d` | Any digit (0–9). |
| `\D` | Any character that is not a digit. |
| `\s` | Any whitespace character (such as spaces, tabs and newlines). |
| `\S` | Any character that is not a whitespace character. |
| `\w` | Any word character (also called an alphanumeric character)—that is, any uppercase or lowercase letter, any digit or an underscore. |
| `\W` | Any character that is not a word character. |

To match any metacharacter as its literal value, precede it by a backslash. For example, `\$` matches a dollar sign (`$`) and `\` matches a backslash (`\`).

### Matching Digits

Let’s validate a five-digit ZIP code. In the regular expression `\d{5}` (created by the raw string literal in line 15), `\d` is a character class representing a digit (0–9). A character class is a regular expression escape sequence that matches one character. To match more than one, follow the character class with a quantifier. The quantifier `{5}` repeats `\d` five times as if we had written `\d\d\d\d\d` to match five consecutive digits. Line 18’s second call to `regex_match` returns false because `"9876"` contains only four consecutive digits.

```cpp
// fully match five digits
std::regex r2{R"(\d{5})"};
std::cout << R"(Matching against: \d{5})" << "\n"
    << std::format("02215: {}; 9876: {}\n",
        std::regex_match("02215", r2), std::regex_match("9876", r2));
```

```text
Matching against: \d{5}
02215: true; 9876: false
```

### Custom Character Classes

Characters in square brackets, `[]`, define a custom character class that matches a single character. For example, `[aeiou]` matches a lowercase vowel, `[A-Z]` matches an uppercase letter, `[a-z]` matches a lowercase letter, and `[a-zA-Z]` matches any lowercase or uppercase letter. Line 21 defines a custom character class to validate a simple first name with no spaces or punctuation.

```cpp
// match a word that starts with a capital letter
std::regex r3{"[A-Z][a-z]*"};
std::cout << "Matching against: [A-Z][a-z]*\n"
    << std::format("Angel: {}; tina: {}\n",
        std::regex_match("Angel", r3), std::regex_match("tina", r3));
```

```text
Matching against: [A-Z][a-z]*
Angel: true; tina: false
```

A first name might contain many letters. In the regular expression `r3` (line 21), `[A-Z]` matches one uppercase letter, and `[a-z]*` matches any number of lowercase letters. The `*` quantifier matches zero or more occurrences of the subexpression to its left (in this case, `[a-z]`). So `[A-Z][a-z]*` matches `"Vivian"`, `"An"` or even `"A"`.

When a custom character class starts with a caret (`^`), the class matches any character that’s not specified. So `[^a-z]` (line 27) matches any character that’s not a lowercase letter.

```cpp
// match any character that's not a lowercase letter
std::regex r4{"[^a-z]"};
std::cout << "Matching against: [^a-z]\n"
    << std::format("A: {}; a: {}\n\n",
        std::regex_match("A", r4), std::regex_match("a", r4));
```

```text
Matching against: [^a-z]
A: true; a: false
```

Metacharacters in a custom character class are treated as the characters themselves. So `[*+$]` (line 33) matches a single `*`, `+` or `$` character.

```cpp
// match metacharacters as literals in a custom character class
std::regex r5{"[*+$]"};
std::cout << "Matching against: [*+$]\n"
    << std::format("*: {}; !: {}\n\n",
        std::regex_match("*", r5), std::regex_match("!", r5));
```

```text
Matching against: [*+$]
*: true; !: false
```

### * vs. + Quantifier

To require at least one lowercase letter in a first name, replace the `*` quantifier in line 21 with `+` (line 39). This matches at least one occurrence of a subexpression to its left.

```cpp
// matching a capital letter followed by at least one lowercase letter
std::regex r6{"[A-Z][a-z]+"};
std::cout << "Matching against: [A-Z][a-z]+\n"
    << std::format("Angel: {}; T: {}\n\n",
        std::regex_match("Angel", r6), std::regex_match("T", r6));
```

```text
Matching against: [A-Z][a-z]+
Angel: true; T: false
```

Both `*` and `+` are greedy—they match as many characters as possible. So the regular expression `[A-Z][a-z]+` matches any word that begins with a capital letter followed by at least one lowercase letter. You can make `*` and `+` lazy, so they match as few characters as possible by appending a question mark (`?`) to the quantifier, as in `*?` or `+?`.

### Other Quantifiers

The `?` quantifier by itself matches zero or one occurrence of the subexpression to its left. In the regular expression `labell?ed` (line 45), the subexpression is the literal character `"l"`. So in the `regex_match` calls in lines 48-49, the regular expression matches `labelled` (the U.K. English spelling) and `labeled` (the U.S. English spelling), but in the `regex_match` call in line 50, the regular expression does not match the misspelled word `label1ed`.
