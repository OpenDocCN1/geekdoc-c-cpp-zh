```
else {
  cout << "Enter your NAAQ: ";
  float you;
  cin >> you;
  int count = 0;
  for (int j = 0; j < i; j++) {
    if (naaq[j] > you)
      count++;
  }
  cout << "* of your neighbors have greater awareness of\n";
  cout << "the New Age than you do.\\n";
}
return 0;
```

Note that the program in Listing 6.5 places input into the temporary variable temp. Only after it verifies that the input is valid does the program assign the value to the array. 
Here are a couple of sample runs of the program. One terminates after six entries:

Enter the NAAQs (New Age Awareness Quotients) of your neighbors. Program terminates when you make
6 entries or enter a negative value.
First value: 28
Next value: 72
Next value: 15
Next value: 6
Next value: 110
Next value: 145
Enter your NAAQ: 50
3 of your neighbors have greater awareness of
The New Age than you do.

The second run terminates after a negative value is entered:
Enter the NAAQs (New Age Awareness Quotients) of your neighbors. Program terminates when you make
6 entries or enter a negative value.
First value: 123
Next value: 119
Next value: 4
Next value: 89
Next value: -1
ter your NAAQ: 123.031
0 of your neighbors have greater awareness of
The New Age than you do.