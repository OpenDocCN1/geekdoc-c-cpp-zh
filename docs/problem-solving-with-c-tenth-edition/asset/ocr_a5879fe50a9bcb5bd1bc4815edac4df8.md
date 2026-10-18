# DISPLAY 2.1 A C++ Program (part 2 of 2)

```
23  cout << "Then press return.\n";
24  cin >> numberOfBars;
25  cin >> oneWeight;
26
27  totalWeight = oneWeight * numberOfBars;
28
29  cout << numberOfBars << " candy bars\n";
30  cout << oneWeight << " ounces each\n";
31  cout << "Total weight is " << totalWeight << " ounces.\n";
32
33  cout << "Perhaps an apple would be healthier.\n";
34
35  return 0;
36  }
```

# Sample Dialogue

```
Enter the number of candy bars in a package and the weight in ounces of one candy bar.
Then press return.
11 2.1
11 candy bars
2.1 ounces each
Total weight is 23.1 ounces.
Try another brand.
Enter the number of candy bars in a package and the weight in ounces of one candy bar.
Then press return.
12 1.8
12 candy bars
1.8 ounces each
Total weight is 21.6 ounces.
Perhaps an apple would be healthier.
```

# Names: Identifiers

The first thing you might notice about the names of the variables in our sample programs is that they are longer than the names normally used for variables in mathematics classes. To make your program easy to understand, you should always use meaningful names for variables. The name of a variable (or other item you might define in a program) is called an identifier.