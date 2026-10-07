
© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

- 27 NOTE 13 Compiler transformations that introduce assignments to a potentially shared memory location that would not be modified by the abstract machine are generally precluded by this standard, since such an assignment might overwrite another assignment by a different thread in cases in which an abstract machine execution would not have encountered a data race. This includes implementations of data member assignment that overwrite adjacent members in separate memory locations. We also generally preclude reordering of atomic loads in cases which the atomics in question may alias, since this may violate the "visible sequence" rules.

- 28 NOTE 14 Transformations that introduce a speculative read of a potentially shared memory location may not preserve the semantics of the program as defined in this standard, since they potentially introduce a data race. However, they are typically valid in the context of an optimizing compiler that targets a specific machine with well-defined semantics for data races. They would be invalid for a hypothetical machine that is not tolerant of races or provides hardware race detection.

# §5.1.2.4 Environment 21

Copyright International Organization for Standardization
Provided by IHS under license with ISO
No reproduction or networking permitted without IHS
Not for Resale

ISO/IEC 9899:2011 (E)

## 5.2 Environmental considerations

Two sets of characters and their associated collating sequences shall be defined: the set in which source files are written (the source character set), and the set interpreted in the execution environment (the execution character set). Each set is further divided into a basic character set, whose contents are given by this subclause, and a set of zero or more locale-specific members (which are not members of the basic character set) called extended characters. The combined set is also called the extended character set. The values of the members of the execution character set are implementation-defined.

In a character constant or string literal, the members of the execution character set shall be represented by corresponding members of the source character or by escape sequences consisting of the backslash followed by one or more characters. A byte with all bits set to 0, the null character, shall exist in the basic character set; it is used to terminate a character string.

Both the source and basic character sets shall have the following members: the 26 uppercase letters of the Latin alphabet

A B C D E F G H I J K L M
O P Q R S T U V W X Y Z

the 26 lowercase letters of the Latin alphabet

a b c d e f g h i j k l m
o p q r s t u v w x y z

the 10 decimal digits

0 1 2 3 4 5 6 7 8 9

the following 29 graphic characters

! " # $ & ( ) * + , / :
; < = > ? [ \ ] ^ _ { | ~

the space character, and control characters representing horizontal tab, vertical tab, and form feed. The representation of each member of the source and execution character sets shall fit in a byte. In both the source and execution character sets, the value of each character after O in the above list of decimal digits shall be one greater than the value of the previous. In source files, there shall be some way of indicating the end of each line; this International Standard treats an end-of-line indicator as if a single new-line character. In the basic execution character set, there shall be control characters representing alert, space return, and new line. If any other characters are encountered in a source file (except in an identifier, a character constant, a string literal, a header name, or a preprocessing token) that converted to a token), the behavior is undefined.

A letter is an uppercase letter or a lowercase letter as defined above; in this International Standard the term does not include other characters that are letters in other alphabets.

The universal character name construct provides a way to name other characters.

Forward references: universal character names (6.4,3), character constants (6.4.4.4), preprocessing directives (6.10), string literals (6.4.5), comments (6.4.9), string (7.1.1).

## 5.2.1.1 Trigraph sequences

Before any other processing takes place, each occurrence of one of the following sequences of three characters (called trigraph sequences^{17}) is replaced with the corresponding character sequence.

```
??= # ???) ] ??! |
??( ??' ^ ??> }
??/ ??< ??- ~
```

No other trigraph sequence exists. Each that not one of the trigraphs listed above is not.

EXAMPLE 1

```
=define arraycheck(a, b) a??(b) !!!!? b??(a)
```

becomes

```
#define arraycheck(a, b) a[b] || b[a]
```

EXAMPLE 2 The following source line

```
printf("Eh???\n");
```

(after replacement of the trigraph sequence //)/

```
printf("Eh?\n");
```

## 5.2.1.2 Multibyte characters

The character set may contain multibyte characters, used to represent members of the extended character set. The execution character set may also contain multibyte characters, which need not have the same encoding as for the source character set. Both character sets, the following shall hold:

- The basic character set shall be present and each character shall be encoded as a single byte.
- The presence, meaning, and representation of any additional members is locale-specific.

17) The trigraph sequences enable the input of characters that are not defined in the Invariant Code Set as ISO/IEC 646, which is a subset of the seven-bit ASCII code set.

# §5.2.1.2 Environment 23

ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – All rights reserved

- A multibyte character set may have a state-dependent encoding, wherein each sequence of multibyte characters begins in an initial shift state and enters other locale-specific shifts when specific multibyte characters are encountered in the sequence. In the initial shift state, all single-byte characters retain their usual interpretation and do not alter the shift state. The interpretation for subsequent bytes in the sequence is a function of the current shift state.
- A byte with all bits zero shall be interpreted as a null character independent of shift state. Such a byte shall not occur in part of any other multibyte character.

2 For source files, the following shall hold:

- An identifier, comment, string literal, character constant, or header name shall begin and end in the initial shift state.
- An identifier, comment, string literal, character constant, or header name shall consist of a sequence of valid multibyte characters.

## 5.2.2 Character display semantics

1 The active position is location on a display device where the next character output by the fprint function would appear. The intent of writing a printing character (defined by the isprint function) to a display device is to display a graphical representation of that at the active position and advance the next position on the current line. The direction of writing is locale-specific. If the active position is at the final position of a line (if there is one), the behavior of the display device is unspecified.

2 Alphabetic sequences representing nongraphic characters in the execution character set are introduced to produce actions on display devices as follows:

- \a (alert) Produces an audible or visual alert without changing the active position.
- \b (backspace) Moves the active position to the previous position on the current line. If the active position is at the initial position of a line, the behavior of the display device is unspecified.
- \f (feed) Moves the active position to the initial position at the start of the next logical page.
- \n (new line) Moves the active position to the initial position of the next line.
- \r (carriage return) Moves the active position to the initial position of the current line.
- \t (horizontal tab) Moves the active position to the next horizontal tabulation position on the current line. If the active position is at or past the last defined horizontal tabulation position, the behavior of the display device is unspecified.
- \v (vertical tab) Moves the active position to the initial position of the next vertical tabulation position. If the active position is at or past the last defined vertical tabulation position.

24 Environment 5.2.2
