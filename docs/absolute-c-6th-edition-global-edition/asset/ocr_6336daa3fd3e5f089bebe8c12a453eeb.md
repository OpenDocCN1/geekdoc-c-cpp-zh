# Display 8.6 Overloading ++ (part 2 of 3)

```
22      cout << a.getFirst( ) << " " << a.getSecond( ) << endl;
23      IntPair b = a++;
24      cout << "Value returned: ";
25      cout << b.getFirst( ) << " " << b.getSecond( ) << endl;
26      cout << "Changed object: ";
27      cout << a.getFirst( ) << " " << a.getSecond( ) << endl;
28
29      a = IntPair(1, 2);
30      cout << "Prefix ++a: Start value of object a: ";
31      cout << a.getFirst( ) << " " << a.getSecond( ) << endl;
32      IntPair c = ++a;
33      cout << "Value returned: ";
34      cout << c.getFirst( ) << " " << c.getSecond( ) << endl;
35      cout << "Changed object: ";
36      cout << a.getFirst( ) << " " << a.getSecond( ) << endl;
37      return 0;
38  }
```

```
39  IntPair::IntPair(int firstValue, int secondValue)
40      : first(firstValue), second(secondValue)
41  {/*Body intentionally empty*/}
42  IntPair IntPair::operator++(int ignoreMe) //Postfix version
43  {
44      int temp1 = first;
45      int temp2 = second;
46      first++;
47      second++;
48      return IntPair(temp1, temp2);
49  }
```

```
50  IntPair IntPair::operator++( ) //Prefix version
51  {
52      first++;
53      second++;
54      return IntPair(first, second);
55  }
```

```
56  void IntPair::setFirst(int newValue)
57  {
58      first = newValue;
59  }
60  void IntPair::setSecond(int newValue)
61  {
62      second = newValue;
63  }
```