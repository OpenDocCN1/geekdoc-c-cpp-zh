```
```java
23    while (i * i <= N)
24    {
25        if (b.test(i))
26        {
27            count++;
28            int k = 2 * i;
29            while (k <= N)
30            {
31                b.reset(k);
32                k += i;
33            }
34        }
35        i++;
36    }
37    while (i <= N)
38    {
39        if (b.test(i))
40            count++;
41        i++;
42    }
43
44    clock_t cend = clock();
45    double millis = 1000.0 * (cend - cstart) / CLOCKS_PER_SEC;
46
47    cout << count << " primes\n" << millis << " milliseconds\n";
48
49    return 0;
50 }
```
```

This completes our tour through the Java collections framework. As you have seen, the Java library offers a wide variety of collection classes for your programming needs. In the next chapter, you will learn how to write graphical user interfaces.