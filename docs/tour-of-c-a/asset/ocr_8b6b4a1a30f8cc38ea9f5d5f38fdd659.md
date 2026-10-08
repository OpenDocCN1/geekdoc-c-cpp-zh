```
Rand_int rnd {10,20};
for (int i = 0; i<10; ++i) cout << rnd() << ' '; // 16 13 20 19 14 17 10 16 15 14
cout << '\n';
rnd.seed(999);
for (int i = 0; i<10; ++i) cout << rnd() << ' '; // 11 17 14 19 20 13 20 14 16 19
cout << '\n';
rnd.seed(999);
for (int i = 0; i<10; ++i) cout << i+i << ' '; // 11 17 14 19 20 13 20 14 16 19
cout << '\n';
```