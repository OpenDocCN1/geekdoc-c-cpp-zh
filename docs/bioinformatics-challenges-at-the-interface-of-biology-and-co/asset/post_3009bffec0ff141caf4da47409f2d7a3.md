
# Table 6.5

How common programming languages relate to the four paradigms of algorithm design: imperative, functional, logic and object-oriented. For a given language, a paradigm may be ✓ exemplified (the language was designed around it), ✓ supported (the language provides mechanisms for its use), or effectively unsupported if left blank.

| Language | Imperative | Functional | Logic | Object-oriented |
| :--- | :---: | :---: | :---: | :---: |
| C | ✓ | | | |
| C++ | ✓ | | | ✓ |
| Haskell | | ✓ | | |
| Java | ✓ | | | |
| JavaScript | | (✓) | | ✓ |
| Lisp | | | ✓ | |
| Oz | | | | | |
| Perl | ✓ | | | ✓ |
| Prolog | | | ✓ | |
| Python | ✓ | (✓) | | ✓ |
| Ruby | ✓ | (✓) | | ✓ |

although the same doesn't necessarily hold for the choice of programming language (see Section 6.6.2). Having said, paradigmatic choice is not without consequences. Which paradigm we choose – if a choice exists – depends on the nature of the problem, from which it's often evident which paradigm is the best fit. By 'better', we mean a number of immediate gains: choosing the correct paradigm can drastically speed development time, make code smaller, and allow it to run more efficiently. However, there are other reasons for choosing one paradigm over another; for example, some methods are easily implemented in some paradigms than others (see Section 6.6.4 for an example).

Not all programming languages are equal. Standard tools they make available can differ considerably in their expressivity and convenience. In most cases, the particular combination of regular-expression extensions is specific to this language and version. Whether those extensions provide better support for non-ASCII text, or are non-regular extensions to the language itself, knowing what's available helps us to choose an applicable language work; this isn't just a case of choosing a language that provides the tools we want; it is also a matter of recognising that, in future, the solution must be restated in a different language that has more regular-expression power, or may be possible to do a straight translation without substantial extra work.

## 6.6.2 Choice of language

In a formal sense, most programming languages have equivalent expressivity: *i.e.*, they are capable of solving the same set of problems, although potentially in different ways. There are, however, programming languages that are *less* expressive than their counterparts: *i.e.*, there are problems that such languages cannot solve. At first this might look like a disadvantage that would make such languages undesirable. After all, why would we want to use a language that is less able to solve? The answer lies in the Halting Problem introduced in Section 2.1, which stated that it is impossible to know whether an algorithm will complete in a finite time, or continue forever. In practice, software engineers strive to avoid such situations, so the fact that they seldom cause problems. The ability to prove mathematically that an algorithm will complete in a finite time is very important, especially in highly critical systems that require thorough verification (such as financial systems). In cases like these, standard programming languages are at least too unpredictable for the task. Knowing they exist can inform the creation of more predictable code.

For example, Ruby's regular-expression engine would allow recursive expressions (making them no longer regular), and can be used to parse recursive data structures with very little code. This is perfect if we are confident that Ruby will remain in the foreseeable future; but if we are using Ruby solely for rapid prototyping,

### Box 6.2 Regular expressions

It's common in bioinformatics to search for protein or nucleotide sequences for strings, or patterns, of amino acids or nucleotides (perhaps these residues or bases form functional sites). We may be looking for an exact match; at other times, we may want to allow a certain degree of 'fuzziness' that captures the ambiguities and substitutions that occur in the real world of biology. For example, the consensus sequence VRSPZ would allow this fuzziness.

By contrast the abstract computability concerns above, there are more concrete expressivity concerns in the field of bioinformatics. The most common come from the use of regular expressions for parsing textual data. Regular expressions (see Box 6.2) allow text patterns to be matched and extracted—they are often used when parsing some serialised data (either a data file or network traffic). They, however, have limited applicability, so it's important to understand when regular expressions are not applicable.

Regular expressions are capable of parsing any regular language, a term in language theory that describes mathematically the structures within the language ('language' covers not just programming languages, but any informational language). The most common example of such a structure is recursion: regular expressions are mathematically incapable of parsing recursive data structures. This is important, because there are many formats in use today that are not regular languages in the formal sense, and hence regular expressions are incapable of parsing them. XML, HTML and JSON, the three most pervasive formats in use today, are worth noting context-free languages that cannot be parsed with regular expressions. This is repeated because of the frequency with which it is attempted: regular expressions alone cannot parse XML, HTML or JSON. Having said that, most regular libraries provide extensions that, while not sufficiently powerful to invalidate the above statement, provide extra expressivity, and allow wider application.

## Paradigmatic reality

Furthermore, software-engineering courses tend to concentrate on imperative and object-oriented, and the most common languages in use follow those paradigms. On the one hand, for many users, the benefit of being able to code in multiple paradigms within the same code (the building blocks of functional paradigm) gives greater flexibility in how they can express their thoughts.
