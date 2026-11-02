number is used as the record key in this application—the file will be created and maintained in account-number order. This program assumes the user enters the records in account-number order. In a comprehensive accounts receivable system, a sorting capability would be provided so the user could enter the records in any order. The records would then be sorted and written to the file. [Note: Figures 11.6–11.7 use the data file created in Fig. 11.2, so you must run the program in Fig. 11.2 before the programs in Figs. 11.6–11.7.]

```
```c
1 // Fig. 11.2: fig11_02.c
2 // Creating a sequential file
3 #include <stdio.h>
4
5 int main(void)
6 {
7    FILE *cfPtr; // cfPtr = clients.txt file pointer
8
9    // fopen opens file. Exit program if unable to create file
10   if ((cfPtr = fopen("clients.txt", "w")) == NULL) {
11      puts("File could not be opened");
12   }
13   else {
14      puts("Enter the account, name, and balance.");
15      puts("Enter EOF to end input.");
16      printf("%s", " ");
17
18      unsigned int account; // account number
19      char name[30]; // account name
20      double balance; // account balance
21
22      scanf("%d%29s%lf", &account, &name, &balance);
23
24      // write account, name and balance into file with fprintf
25      while (!feof(stdin)) {
26         fprintf(cfPtr, "%d %s %.2f\n", account, name, balance);
27         printf("%s", " ");
28         scanf("%d%29s%lf", &account, &name, &balance);
29      }
30
31      fclose(cfPtr); // fclose closes file
32   }
33 }
```
```

```
```text
Enter the account, name, and balance.
Enter EOF to end input.
? 100 Jones 24.98
? 200 Doe 345.67
? 300 White 0.00
? 400 Stone -42.16
? 500 Rich 224.62
? ^Z
```
```

Fig. 11.2 | Creating a sequential file.