```
set<int> s = {1, 3, 4, 7, 9};
s.insert(5);
for (int i = 0; i < 6; ++i)
cout << i << " appears " << s.count(i) << " time(s).\n";
```