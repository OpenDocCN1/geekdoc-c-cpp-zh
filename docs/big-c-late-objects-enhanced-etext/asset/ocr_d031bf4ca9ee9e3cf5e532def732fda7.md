```
40      j++;
41      }
42      counts[i][j]++;
43  }
44  }
45
46  // Print all counts
47  for (int i = 0; i < SIZE; i++)
48  {
49      for (int j = 0; j <= i; j++)
50      {
51          cout << setw(4) << counts[i][j];
52      }
53      cout << endl;
54  }
55
56  // Deallocate the rows
57  for (int i = 0; i < SIZE; i++)
58  {
59      delete[] counts[i];
60  }
61
62  return 0;
63 }
```

# Program Run

1000
480 520
241 500 259
124 345 411 120
68 232 365 271 64
32 164 283 329 161 31
16 88 229 303 254 88 22
9 47 147 277 273 190 44 13
5 24 103 203 288 228 113 33 3
1 18 64 149 239 265 186 61 15 2

# 7.6 Problem Solving: Draw a Picture

When designing programs that use pointers, you want to visualize how the pointers connect the data that you are working with. In most situations, it is essential that you draw a diagram that shows the connections.

Start with the data that will be accessed or modified through the pointers. These may be account balances, counters, character strings, or other items. Focus on what is being pointed at.

Then draw the variable or variables that contain the pointers. These will be the front-end to your system. Processing usually starts with a pointer, then locates the actual data.

Finally, draw the pointers as arrows. If the pointers will vary as the program executes, draw a typical arrangement. It can also be useful to draw several diagrams that show how the pointers change.

Draw the data that is being processed, then draw the pointer variables. When drawing the pointer arrows, illustrate a typical situation.