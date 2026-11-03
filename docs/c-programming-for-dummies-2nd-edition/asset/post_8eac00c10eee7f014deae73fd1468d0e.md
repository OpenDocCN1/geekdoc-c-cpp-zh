
So the value of variable a equals positive n? The compiler may buy that argument, but it's not what you intended.

Also, don't forget the increment and decrement operators, ++ and --, which are quite popular in loops.

## When You Get Stuck, Read Your Code Out Loud

![](img/dcc0cd79d4a45cfce24fa49d85442884_424_0.png)

To help you track down that bug, start reading your code aloud. Pretend that a programmer friend is sitting right next to you. Explain what your code is doing and how it works. As you talk through your code, you'll find the problem. If you don't, have your imaginary friend ask you questions during your explanation.

Don't worry about going mental. You're a programmer. You're already mental.

As a bonus, talking through your code also helps you identify which portions need to have comments and what the comments should be. For example:

```
a++;    /* increment a */
```

In the preceding line, you see a terrible example of a comment. Duh. Of course, a is incremented. Here's a better version of that comment:

```
a++;    /* skip the next item to align output */
```

Don't just comment on what the code is doing — comment on why. Again, pretend that you're explaining your code to another programmer — or to future-you. Future-you will thank present-you for the effort.

## 7 Appendices

## IN THIS PART . . .

- Codes and keywords
- Operators and data types
- Escape sequences and conversion characters
- Order of precedence

| Decimal | Hex | Character | Comment |
|---|---|---|---|
| 22 | 0x16 | ^V |  |
| 23 | 0x17 | ^W |  |
| 24 | 0x18 | ^X |  |
| 25 | 0x19 | ^Y |  |
| 26 | 0x1A | ^Z |  |
| 27 | 0x1B | ^[ | Escape |
| 28 | 0x1C | ^\ |  |
| 29 | 0x1D | ^] |  |
| 30 | 0x1E | ^^ |  |
| 31 | 0x1F | ^_ |  |
| 32 | 0x20 |  | Space, start of visible characters |
| 33 | 0x21 | ! | Exclamation point |
| 34 | 0x22 | " | Double quote |
| 35 | 0x23 | # | Pound, hash |
| 36 | 0x24 | $ | Dollar sign |
| 37 | 0x25 | % | Percent sign |
| 38 | 0x26 | & | Ampersand |
| 39 | 0x27 | ' | Apostrophe |
| 40 | 0x28 | ( | Left parenthesis |
| 41 | 0x29 | ) | Right parenthesis |
| 42 | 0x2A | * | Asterisk |
| 43 | 0x2B | + | Plus |
| 44 | 0x2C | , | Comma |
| 45 | 0x2D | - | Hyphen, minus |
| 46 | 0x2E | . | Period |
| 47 | 0x2F | / | Slash |
| 48 | 0x30 | 0 | Numbers |
| 49 | 0x31 | 1 |  |
| 50 | 0x32 | 2 |  |
| 51 | 0x33 | 3 |  |
| 52 | 0x34 | 4 |  |
| 53 | 0x35 | 5 |  |
| 54 | 0x36 | 6 |  |
| 55 | 0x37 | 7 |  |
| 56 | 0x38 | 8 |  |
| 57 | 0x39 | 9 |  |
| 58 | 0x3A | : | Colon |
| 59 | 0x3B | ; | Semicolon |
| 60 | 0x3C | < | Less than, left angle bracket |
| 61 | 0x3D | = | Equals |
| 62 | 0x3E | > | Greater than, right angle bracket |
| 63 | 0x3F | ? | Question mark |
| 64 | 0x40 | @ | At sign |
| 65 | 0x41 | A | Uppercase alphabet |
| 66 | 0x42 | B |  |
| 67 | 0x43 | C |  |
| 68 | 0x44 | D |  |
| 69 | 0x45 | E |  |
| 70 | 0x46 | F |  |
| 71 | 0x47 | G |  |
| 72 | 0x48 | H |  |
| 73 | 0x49 | I |  |
| 74 | 0x4A | J |  |
| 75 | 0x4B | K |  |
| 76 | 0x4C | L |  |
| 77 | 0x4D | M |  |
| 78 | 0x4E | N |  |
| 79 | 0x4F | O |  |
| 80 | 0x50 | P |  |
| 81 | 0x51 | Q |  |
| 82 | 0x52 | R |  |
| 83 | 0x53 | S |  |
| 84 | 0x54 | T |  |
| 85 | 0x55 | U |  |
| 86 | 0x56 | V |  |
| 87 | 0x57 | W |  |
| 88 | 0x58 | X |  |
| 89 | 0x59 | Y |  |
| 90 | 0x5A | Z |  |
| 91 | 0x5B | [ | Left square bracket |
| 92 | 0x5C | \ | Backslash |
| 93 | 0x5D | ] | Right square bracket |
| 94 | 0x5E | ^ | Caret |
| 95 | 0x5F | _ | Underscore |
| 96 | 0x60 | \` | Back tick, accent grave |
| 97 | 0x61 | a | Lowercase alphabet |
| 98 | 0x62 | b |  |
| 99 | 0x63 | c |  |
| 100 | 0x64 | d |  |
| 101 | 0x65 | e |  |
| 102 | 0x66 | f |  |
| 103 | 0x67 | g |  |
| 104 | 0x68 | h |  |
| 105 | 0x69 | i |  |
| 106 | 0x6A | j |  |
| 107 | 0x6B | k |  |
| 108 | 0x6C | l |  |
| 109 | 0x6D | m |  |
| 110 | 0x6E | n |  |
| 111 | 0x6F | o |  |
| 112 | 0x70 | p |  |
| 113 | 0x71 | q |  |
| 114 | 0x72 | r |  |
| 115 | 0x73 | s |  |
| 116 | 0x74 | t |  |
| 117 | 0x75 | u |  |
| 118 | 0x76 | v |  |
| 119 | 0x77 | w |  |
| 120 | 0x78 | x |  |
| 121 | 0x79 | y |  |
| 122 | 0x7A | z |  |
| 123 | 0x7B | { | Left brace, left curly bracket |
| 124 | 0x7C | \| | Vertical bar |
| 125 | 0x7D | } | Right brace, right curly bracket |
| 126 | 0x7E | ~ | Tilde |
| 127 | 0x7F |  | Delete |

- ASCII 0 through ASCII 31 represent control code values. These characters are accessed by pressing the Ctrl key on the keyboard and typing the corresponding symbol or letter key.
- Code 32 is the code for the space character.
- Code 127 is the Delete character, which is different from Code 8, Backspace. The reason is that Code 8 is defined as nondestructive, which means that it only moves the cursor back a space.
- Many of the control codes manipulate text on the screen, such as Ctrl+I for the Tab key.
- A keen eye can spot three repetitions in the ASCII code lists. Look at codes 0 through 26 and then 64 through 90. Also look at codes 97 through 122.
- The difference between uppercase and lowercase characters in the table is 32, a computer holy number. The hexadecimal difference is 0x20. Therefore, by using simple math, or bitwise logic, you can convert between upper- and lowercase.
- The digits 0 through 9 are equal to the values 0 through 9 when you subtract 48 (0x30) from the ASCII code values. Likewise, to convert values 0 through 9 into their corresponding ASCII characters, add 48 or 0x30.
- Any ASCII character can be represented as an escape sequence. Follow the backslash with the character's code value, as in \33 for the exclamation point (!) character. The hexadecimal value can also be used, as in \x68 for the little H.

## Appendix B

### Keywords

### C Language Keywords, C17 Standard

|  |  |  |  |
|---|---|---|---|
| _Alignas | break | float | signed |
| _Alignof | case | for | sizeof |
| _Atomic | char | goto | static |
| _Bool | const | if | struct |
| _Complex | continue | inline | switch |
| _Generic | default | int | typedef |
| _Imaginary | do | long | union |
| _Noreturn | double | register | unsigned |
| _Static_assert | else | restrict | void |
| _Thread_local | enum | return | volatile |
| auto | extern | short | while |

### Deprecated C Language Keywords, No Longer Standard

|  |  |  |
|---|---|---|
| asm | entry | fortran |

### C++ Language Keywords

|  |  |  |  |  |
|---|---|---|---|---|
| asm | dynamic_cast | new | requires | typeid |
| bool | export | not | static_cast | typename |
| catch | false | operator | template | using |
| class | friend | private | this | virtual |
| concept | inline | protected | throw | xor |
| const_cast | mutable | public | true |  |
| delete | namespace | reinterpret_cast | try |  |

- The C17 standard is the current C language standard as this book goes to press. The standard was established in 2017.
- You don't need to memorize the C++ keywords, and not all of them are listed in this appendix. Still, it's important to be aware of them. I strongly recommend that you not use any of them as function names or variable names in your code.
- The most frequent C++ reserved word that C programmers tend to use is new. Just don't use it; use something else, like new_item or newSomething instead.
- The bool keyword in C++ is effectively the same thing as the _Bool keyword in C.

## Appendix C

### Operators

Also see Appendix G for the order of precedence.

| Operator | Type | Function |
|---|---|---|
| + | Math | Addition |
| - | Math | Subtraction |
| * | Math | Multiplication |
| / | Math | Division |
| % | Math | Modulo |
| ++ | Math | Increment |
| -- | Math | Decrement |
| + | Math | Unary plus |
| - | Math | Unary minus |
| = | Assignment | Assigns a value to a variable |
| += | Assignment | Addition |
| -= | Assignment | Subtraction |
| *= | Assignment | Multiplication |
| /= | Assignment | Division |
| %= | Assignment | Modulo |
| != | Comparison | Not equal |
| < | Comparison | Less than |
| <= | Comparison | Less than or equal to |
| == | Comparison | Is equal to |
| > | Comparison | Greater than |
| >= | Comparison | Greater than or equal to |
