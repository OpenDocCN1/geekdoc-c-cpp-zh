# DISPLAY 3.15 Explicitly Nested Loops (part 2 of 2)

```
10      << "Each conservationist's report consists of\n"
11      << "a list of numbers. Each number is the count of\n"
12      << "the eggs observed in one"
13      << "green-necked vulture nest.\n"
14      << "This program then tallies"
15      << "the total number of eggs.\n";
16
17      int numberOfReports;
18      cout << "How many conservationist reports are there? ";
19      cin >> numberOfReports;
20
21      int grandTotal = 0, subtotal, count;
22      for (count = 1; count <= numberOfReports; count++)
23      {
24          cout << endl << "Enter the report of "
25              << "conservationist number " << count << endl;
26          cout << "Enter the number of eggs in each nest.\n"
27              << "Place a negative integer at the end of your list.\n";
28          subtotal = 0;
29          int next;
30          cin >> next;
31          while (next >= 0)
32          {
33              subtotal = subtotal + next;
34              cin >> next;
35          }
36          cout << "Total egg count for conservationist "
37              << " number " << count << " is "
38              << subtotal << endl;
39          grandTotal = grandTotal + subtotal;
40      }
41
42      cout << endl << "Total egg count for all reports = "
43          << grandTotal << endl;
44
45      return 0;
46      }
```

# SELF-TEST EXERCISES

36. Write a loop that will write the word Hello to the screen ten times (when embedded in a complete program).

37. Write a loop that will read in a list of even numbers (such as 2, 24, 8, 6) and compute the total of the numbers on the list. The list is ended with a sentinel value. Among other things, you must decide what would be a good sentinel value to use.