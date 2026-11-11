Table 5.1 The Authors Table

| Author_ID | Name | Fname |
| --- | --- | --- |
| ALEX | Alexander | Christopher |
| BROO | Brooks | Frederick P. |
| . . . | . . . | . . . |

Table 5.2 The Books Table

| Title | ISBN | Publisher_ID | Price |
| --- | --- | --- | --- |
| A Guide to the SQL Standard | 0-201-96426-0 | 0201 | 47.95 |
| A Pattern Language: Towns, Buildings, Construction | 0-19-501919-9 | 019 | 65.00 |
| . . . | . . . | . . . | . . . |

Table 5.3 The BooksAuthors Table

| ISBN | Author_ID | Seq_No |
| --- | --- | --- |
| 0-201-96426-0 | DATE | 1 |
| 0-201-96426-0 | DARW | 2 |
| 0-19-501919-9 | ALEX | 1 |
| . . . | . . . | . . . |

Table 5.4 The Publishers Table

| Publisher_ID | Name | URL |
| --- | --- | --- |
| 0201 | Addison-Wesley | www.aw-bc.com |
| 0407 | John Wiley & Sons | www.wiley.com |
| . . . | . . . | . . . |

Figure 5.3 shows a view of the *Books* table. Figure 5.4 shows the result of *joining* this table with the *Publishers* table. The *Books* and the *Publishers* tables each contain an identifier for the publisher. When we join both tables on the publisher code, we obtain a *query result* made up of values from the joined tables. Each