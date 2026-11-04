*Exercise.* Complete the steps for the generation of this logic pattern for every row 1 to 5 by showing output on the computer screen diagram.

| Steps for pattern generation(row = 1 to 5) | Computer Screen |
|---|---|
| For row = 1 | Computer screen diagram: columns 1–9 and rows 1–5; arrow points to row 2. |
| For row = 2 | Computer screen diagram: columns 1–9 and rows 1–5; arrow points to row 3. |
| For row = 3 | Computer screen diagram: columns 1–9 and rows 1–5; arrow points to row 4. |
| For row = 4 | Computer screen diagram: columns 1–9 and rows 1–5; arrow points to row 5. |
| For row = 5 | Computer screen diagram: columns 1–9 and rows 1–6; arrow points to row 6. |

# **Let’s convert steps into C program.**

| Use of C in-built method | |
|---|---|
| Move to the next row | `printf("\n");` |
| Move to the next (row, col) position and print space " " character in the same row | `Print (" ");` |
| Move to the next (row, col) position and print star "*" character in the same row | `Print ("*");` |

Mentioned methods are bound to get repeat many a times in a program in order to output these characters repeatedly. Hence we will use these within *for-loop* for such repetitive task in a program.