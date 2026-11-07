# Program 19.12  Checking pairing of parentheses (Continued)

```
```cpp
17  getline(cin, expr);
18  int i = 0;
19  while (i < expr.size() && paired)
20  {
21      char next = expr[i];
22      if (next == '(')
23      {
24          stk.push(next);
25      }
26      else if (next == ')')
27      {
28          if (stk.empty())
29          {
30              paired = false; // If stack is empty here, no pairing
31          }
32          else
33          {
34              stk.pop();
35          }
36      }
37      i++;
38  }
39  // If stack is not empty at the end, parentheses are not paired
40  if (!stk.empty())
41  {
42      paired = false;
43  }
44  // Print the result
45  if (paired)
46  {
47      cout << "Parentheses are paired!" << endl;
48  }
49  else
50  {
51      cout << "Parentheses are not paired!" << endl;
52  }
53  return 0;
54  }
```
```

```
Run:
Enter an expression: 3 + (4 + 7 + 6)
Parentheses are paired!
```

```
Run:
Enter an expression: 2 + (4 + (6 + 7)
Parentheses are not paired!
```

```
Run:
Enter an expression: 6 + 7 + (10 * 2 - 4) + 8)
Parentheses are not paired!
```