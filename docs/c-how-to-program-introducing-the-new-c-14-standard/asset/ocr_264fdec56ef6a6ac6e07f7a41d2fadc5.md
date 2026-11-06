The program has five options (Option 5 is for terminating the program). Option 1 calls function `createTextFile` to store a formatted list of all the account information in a text file called `print.txt` that may be printed. Function `createTextFile` (lines 76–109) takes an `fstream` object as an argument to be used to input data from the `credit.dat` file. Function `createTextFile` invokes `istream` member function `read` (lines 95–96) and uses the sequential-file-access techniques of **Fig. 14.12** to input data from `credit.dat`. Function `outputLine`, discussed in **Section 14.10**, outputs the data to file `print.txt`. Note that function `createTextFile` uses `istream` member function `seekg` (line 91) to ensure that the file-position pointer is at the beginning of the file before reading the file’s contents. After choosing Option 1, the `print.txt` file contains

| Account | Last Name | First Name | Balance |
|---:|---|---|---:|
| 29 | Brown | Nancy | -24.54 |
| 33 | Dunn | Stacey | 314.33 |
| 37 | Barker | Doug | 0.00 |
| 88 | Smith | Dave | 258.34 |
| 96 | Stone | Sam | 34.98 |

Option 2 calls `updateRecord` (lines 112–148) to update an account. This function updates only an *existing* record, so the function first determines whether the specified record is *empty*—we use function