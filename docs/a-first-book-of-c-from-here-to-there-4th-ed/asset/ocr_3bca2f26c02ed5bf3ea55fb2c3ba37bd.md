# Table 15.3 Character Library Functions (Require the Header Files string and cctype) (continued)

| Function Prototype | Description | Example |
|---|---|---|
| int isalnum(charExp) | Returns a true (non-zero integer) if charExp evaluates to a letter or a digit; otherwise, it returns a false (zero integer) | isalnum(key); |
| int isupper(charExp) | Returns a true (non-zero integer) if charExp evaluates to an uppercase letter; otherwise, it returns a false (zero integer) | isupper('A') |
| int islower(charExp) | Returns a true (non-zero integer) if charExp evaluates to a lowercase letter; otherwise, it returns a false (zero integer) | islower('a') |
| int isdigit(charExp) | Returns a true (non-zero integer) if charExp evaluates to a digit (0 through 9); otherwise, it returns a false (zero integer) | isdigit('5') |
| int isascii(charExp) | Returns a true (non-zero integer) if charExp evaluates to an ASCII character; otherwise, returns a false (zero integer) | isascii('a') |
| int isspace(charExp) | Returns a true (non-zero integer) if charExp evaluates to a space; otherwise, returns a false (zero integer) | isspace(' ') |
| int isprint(charExp) | Returns a true (non-zero integer) if charExp evaluates to a printable character; otherwise, returns a false (zero integer) | isprint('a') |