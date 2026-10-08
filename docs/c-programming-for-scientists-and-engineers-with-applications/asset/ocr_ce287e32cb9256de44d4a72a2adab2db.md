# Program Warning: Identifiers with more than 31 characters may be acceptable but the ANSI standard requires the first 31 characters to be unique.

Note that in identifiers, the uppercase letters are distinguished from the lowercase letters. For example the name BALANCE is different from balance. C has many reserved words, which must not be used as identifiers.

| VALID IDENTIFIERS | INVALID IDENTIFIERS | COMMENT |
| :--- | :--- | :--- |
| stress | 5identity | first character cannot be a digit |
| velocity | axl1 dig | blank space not allowed |
| balance | con*st | illegal character |
| maximum_value | any,value | illegal character |
| total_count | while | reserved word |
| xa125c20 | struct | reserved word |

It is possible to write long names for identifiers provided that the first 31 characters are unique. If an identifier name has more than one word, the words can be separated by an underscore character. For example, the quantity "compression stress" can be written as compression_stress. It is important to write meaningful names for identifiers. Writing meaningful names is self-documenting and easy for other programmers to understand. Names that are similar or differ by one character should not be used because they are not only confusing and too close to distinguish, but may lead to errors in the code.

Programming Hint: Make it a practice to write meaningful names for the identifiers.

Declaration of Variables and Constants All variables and named constants in C must appear in declaration statements. The declaration of a variable instructs the computer to allocate storage for the variable or constant, and associate the name of the variable or constant with the allocated storage. A declaration is also the definition of the variable or constant if it assigns a value. A constant must be defined at the same time it is declared. In C, the storage associated with a variable or constant is a storage cell. A storage cell can be one byte, two bytes, four bytes, or eight bytes depending on the declared data type. In C the