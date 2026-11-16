
## STRUCTURES & UNIONS

- 1. Answer :
  - Compiler Error:
  - Explanation :
  - You cannot initialize variables in structure declaration.

- 2. Answer :
  - Compiler Error:
  - Explanation :
  - The structure Y is nested within structure X. Hence, the elements of structure Y are to be accessed through the instance of structure X, which needs an instance of Y to be known. If the instance is created after defining the structure the compiler will not know about the instance relative to X. Hence for nested structure Y a member have to be declared.

- 3. Answer :
  - Compiler Error:
  - Explanation :
  - Initialization should not be done for structure members inside the structure declaration.

- 4. Answer :
  - Compiler Error:
  - Explanation :
  - In the end of nested structure Y a member have to be declared.

- 5. Answer :
  - 2
  - Explanation :
  - All the above statements form a circular doubly linked list. The statement, abc.next -> next -> prev -> next -> points to 'ghi' node, the value at that particular node is 2.

- 6. Answer :
  - Value of ptr is 0 - 0
  - Value of ptr is 0 - 0
  - Explanation :
  - The variable ptr is a pointer to structure variable. We can access the elements of the structure either with an arrow mark or with indirection operator. Since structure A_A is globally declared, its members x and y are initialized to zeroes by default.

- 7. Answer :
  - Compiler Error: Undefined structure date
  - Explanation :
  - Inside the struct definition of 'student' the member of type struct date is given. The compiler doesn't have the definition of date structure before it is used, hence you get the above error.

- 8. Answer :
  - Compiler Error: Undefined structure date.
  - Explanation :
  - Only declaration of struct date is available inside the structure definition of 'student' but to have a variable of type struct date the definition of the structure is required.

- 9. Explanation :
  - The fread() function reads 10 records and prints the names successfully. It will return EOF only when the fread() function tries to read another record and fails while reading EOF. So it prints the last record again. After this only the condition feof(fp) becomes false, hence exits from the while loop.

- 10. Answer :
  - No.
  - Explanation :
  - It is not legal for a structure to contain a member of the same type as in this case. Because this will cause the structure declaration to be recursive without end.

- 11. Answer :
  - Yes.
  - Explanation :
  - "b is a pointer to type struct a and so is legal. The compiler knows, the size of the pointer to a structure even before the size of the structure is determined (as you know the pointer to any type is of same size). This type of structures is known as self-referencing structure.

- 12. Answer :
  - No.
  - Explanation :
  - The typename Type is not known at the point of declaring the structure (i.e., forward references are not made for typedefs).

- 13. Answer :
  - Yes.
  - Explanation :
  - The typename Type is known at the point of declaring the structure, because it is already typedefed.

- 14. Answer :
  - No.
  - Explanation :
  - When the declaration, (typedef struct a Type;) is encountered body of struct a is not known, these are referred as incomplete types.

- 15. Answer :
  - 10 20.5 10 20.5
  - Explanation :
  - Structure variable assignments are equivalent to the simple data type variable assignments. So the values of v1.x and v1.y into the v2.x and v2.y.

## ANSWERS III

- 1. (c) and (e)
- 2. (d), (e) and (f)
- 3. (a) Integer
  - (b) Unsigned integer
  - (c) Signed integer
  - (d) Long integer
  - (e) Unsigned short integer
  - (f) Unsigned long integer
- 4. (a) Integer
  - (b) Double
  - (c) String
  - (d) Character
  - (e) Character
  - (f) String
- 5. (a) and (d)
- 6. (a), (c) and (d)
- 7. (a) 6
  - (b) 20
  - (c) 8
  - (d) -3
  - (e) 99
  - (f) 4
- 8. (d)
- 9. (a) -6
  - (b) -3
  - (c) 2
  - (d) 3
  - (e) 1
  - (f) 5
- 10. (a) 1
  - (b) 0
  - (c) 1
  - (d) 0
- 11. (a) a == 0
  - (b) a <= b
  - (c) (a == 0) < b
  - (d) a == b == 0
- 12. (a) 0
  - (b) 1
  - (c) 0
  - (d) 0
- 13. (a) 2
  - (b) 2.5
  - (c) 1
  - (d) Compile Error: Illegal use of floating point
- 14. (a) -27536
  - (b) 38000.000
  - (c) -536
  - (d) 65000.000
- 15. (a) 'S'
  - (b) 'S'
  - (c) 'S'
  - (d) 'S'
- 16. (a), (b) and (d)
- 17. (a)
- 18. (a) and (d)
- 19. (a) size of operator
  - (b) Arithmetic operator
  - (c) Ternary operator
  - (d) Assignment operator
- 20. (b), (c) and (d)
- 21. (a), (b) and (c)
- 22. (a) 5
  - (b) 9
  - (c) 2
  - (d) 10
  - (e) 0
  - (f) 0
- 23. (a) 7
  - (b) 15
  - (c) 7
  - (d) 24
- 24. (a), (b) and (c)
- 25. (a)
- 26. (a) Signed integer
  - (b) Hexadecimal integer
  - (c) Unsigned integer
  - (d) Octal integer
  - (e) Unsigned long integer
  - (f) Signed long integer
- 27. (a) Floating point value in exponent form
  - (b) Float type
  - (c) Floating point value in exponent type or float type depending on value
  - (d) Double type
- 28. (a) Pointer to integer
  - (b) Unsigned Hexadecimal integer
    - (With A, B, C, D, E, F)
  - (c) Pointer
  - (d) Unsigned octal integer
  - (e) Signed decimal integer
  - (f) Unsigned Hexadecimal integer
    - (With a, b, c, d, e, f)
- 29. (b)
- 30. (b)
- 31. (c)
- 32. (a), (b), (c) and (e)
- 33. (a) 32769
  - (b) 0
  - (c) Infinite Loop
  - (d) Infinite Loop
  - (e) 1
  - (f) Infinite Loop
- 34. (b) and (c)
- 35. (a)
- 36. (b)
- 37. (b)
- 38. (b)
- 39. (b)
- 40. (a)
- 41. (a), (c) and (d)
- 42. (b), (c) and (d)
- 43. (e), (c), (e) and (f)
- 44. (a)
- 45. (d)
- 46. (a) 5.0
  - (b) 5.0
  - (c) 5.5
  - (d) 5.44
  - (e) 0.0 (ANSI C does not support fabsll())
  - (f) -0.0 (ANSI C does not support fabsll())
- 47. (a) 5
  - (b) 6
  - (c) 5
  - (d) 6
  - (e) 5
  - (f) 6
- 48. (a) 40.0
  - (b) 41
  - (c) 0.1
  - (d) 0.2
  - (e) 200
  - (f) 250.00
- 49. (a)
- 50. (b)
- 51. (a)
- 52. (a) a
  - (b) A
  - (c) g
  - (d) G
  - (e) 5
  - (f) 5
- 53. (a), (c) and (d)
- 54. (a), (b) and (e)
- 55. (d) and (e)
- 56. (a)
- 57. (a) and (d)
- 58. (a), (c) and (d)
- 59. (a), (c) and (d)
- 60. (d)
- 61. (d)
- 62. (b) and (d)
- 63. (d)
- 64. (b)
- 65. (a), (b) and (c)
- 66. (a), (b) and (c)
- 67. (a), (c) and (d)
- 68. (d)
- 69. (a)
- 70. (a) 1
  - (b) 2
  - (c) 4
  - (d) 8
- 71. (a) 2
  - (b) 2
  - (c) 4
  - (d) 4
- 72. (a) and (d)
- 73. (d)
- 74. (c)
- 75. (b)

## I. ASCII TABLE

Table lists the ASCII characters and its ASCII codes in decimal. The first 32 ASCII characters and the last character are control characters. These characters are non-printable characters, which are enclosed in parentheses (e.g., (null)).

| Character | ASCII code | Character | ASCII code | Character | ASCII code | Character | ASCII code |
|---|---|---|---|---|---|---|---|
| (nul) | 0 | (sp) | 32 | @ | 64 | ` | 96 |
| (soh) | 1 | ! | 33 | A | 65 | a | 97 |
| (stx) | 2 | " | 34 | B | 66 | b | 98 |
| (etx) | 3 | # | 35 | C | 67 | c | 99 |
| (eot) | 4 | $ | 36 | D | 68 | d | 100 |
| (enq) | 5 | % | 37 | E | 69 | e | 101 |
| (ack) | 6 | & | 38 | F | 70 | f | 102 |
| (bel) | 7 | ' | 39 | G | 71 | g | 103 |
| (bs) | 8 | ( | 40 | H | 72 | h | 104 |
| (ht) | 9 | ) | 41 | I | 73 | i | 105 |
| (nl) | 10 | * | 42 | J | 74 | j | 106 |
| (vt) | 11 | + | 43 | K | 75 | k | 107 |
| (np) | 12 | , | 44 | L | 76 | l | 108 |
| (cr) | 13 | - | 45 | M | 77 | m | 109 |
| (so) | 14 | . | 46 | N | 78 | n | 110 |
| (si) | 15 | / | 47 | O | 79 | o | 111 |
| (dle) | 16 | 0 | 48 | P | 80 | p | 112 |
| (dc1) | 17 | 1 | 49 | Q | 81 | q | 113 |
| (dc2) | 18 | 2 | 50 | R | 82 | r | 114 |
| (dc3) | 19 | 3 | 51 | S | 83 | s | 115 |
| (dc4) | 20 | 4 | 52 | T | 84 | t | 116 |
| (nak) | 21 | 5 | 53 | U | 85 | u | 117 |
| (syn) | 22 | 6 | 54 | V | 86 | v | 118 |
| (etb) | 23 | 7 | 55 | W | 87 | w | 119 |
| (can) | 24 | 8 | 56 | X | 88 | x | 120 |
| (em) | 25 | 9 | 57 | Y | 89 | y | 121 |
| (sub) | 26 | : | 58 | Z | 90 | z | 122 |
| (esc) | 27 | ; | 59 | [ | 91 | { | 123 |
| (fs) | 28 | < | 60 | \ | 92 | \| | 124 |
| (gs) | 29 | = | 61 | ] | 93 | } | 125 |
| (rs) | 30 | > | 62 | ^ | 94 | ~ | 126 |
| (us) | 31 | ? | 63 | _ | 95 | (del) | 127 |
