# Accumulating the Values Stored in a Two-Dimensional Array

Figure 12-11 shows the problem specification, IPO chart information, and C++ instructions for Jenko Booksellers program. The program uses a two-dimensional array to store the sales in each of the company's three bookstores. The array contains three rows and two columns. The first column contains the sales amounts for paperback books in each of the three stores. The second column contains the sales amounts for hardcover books. The program calculates the total sales by accumulating the amounts stored in the array. It then displays the total sales on the computer screen. Figure 12-12 shows the code for the entire program, and Figure 12-13 shows the result of running the program.

Problem specification
Jenko Booksellers wants a program that calculates and displays the total of its previous month's sales. The sales, which are shown here, are stored in a two-dimensional double array named sales. The sales array contains three rows and two columns. The first column contains the sales amounts for paperback books sold in each of the stores. The second column contains the sales amounts for hardcover books sold in each of the three stores.

| Paperback sales (S) | Hardcover sales (S) |
|---|--|
| Store 1 | 1203.39 | 2350.75 |
| Store 2 | 3677.80 | 2456.05 |
| Store 3 | 750.67 | 1345.99 |

IPO chart information

store sales (made in each of 3 stores for 2 types of books)

C++ instructions

the sales are stored in the array

Processing

array (3 store rows, 2 columns)

```
double sales[3][2] =
{1203.39, 2350.75},
{3677.80, 2456.05},
{750.67, 1345.99}};
```

store subscript counter (0 to 2) book subscript counter (0 to 1)

declared and initialized in the for clause deared and initialized in the for clause

Output

total sales (accumulator)

```
double total = 0.0;
```

Figure 12-11 Problem specification, IPO chart information, and C++ instructions for Jenko Booksellers program (continues)