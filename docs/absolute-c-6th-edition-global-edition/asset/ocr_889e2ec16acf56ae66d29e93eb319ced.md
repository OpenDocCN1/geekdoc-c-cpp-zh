# Display 16.2 A Generic Sorting Function (part 2 of 2)

```
29  for (i = 0; i < 10; i++)
30    cout << a[i] << " ";
31  cout << endl;
32  sort(a, 10);
33  cout << "In sorted order the integers are:\n";
34  for (i = 0; i < 10; i++)
35    cout << a[i] << " ";
36  cout << endl;
37  double b[5] = {5.5, 4.4, 1.1, 3.3, 2.2};
38  cout << "Unsorted doubles:\n";
39  for (i = 0; i < 5; i++)
40    cout << b[i] << " ";
41  cout << endl;
42  sort(b, 5);
43  cout << "In sorted order the doubles are:\n";
44  for (i = 0; i < 5; i++)
45    cout << b[i] << " ";
46  cout << endl;
47  char c[7] = {'G', 'E', 'N', 'E', 'R', 'I', 'C'};
48  cout << "Unsorted characters:\n";
49  for (i = 0; i < 7; i++)
50    cout << c[i] << " ";
51  cout << endl;
52  sort(c, 7);
53  cout << "In sorted order the characters are:\n";
54  for (i = 0; i < 7; i++)
55    cout << c[i] << " ";
56  cout << endl;
57  return 0;
58 }
```

# Sample Dialogue

```
Unsorted integers:
9 8 7 6 5 1 2 3 0 4
In sorted order the integers are:
0 1 2 3 4 5 6 7 8 9
Unsorted doubles:
5.5 4.4 1.1 3.3 2.2
In sorted order the doubles are:
1.1 2.2 3.3 4.4 5.5
Unsorted characters:
G E N E R I C
In sorted order the characters are:
C E E G I N R
```