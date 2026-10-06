```
[c1 print]; NSLog("+"); [c2 print];
NSLog("-------");
compResult = [c1 add: c2];
[compResult print];
NSLog("\n");

// add and print 2 fractions
[f1 print]; NSLog("+"); [f2 print];
NSLog("-------");
fracResult = [f1 add: f2];
[fracResult print];
}
return 0;
```

# Program 9.1. Output

```
18 + 2.5i
+
-5 + 3.2i
------
13 + 5.7i

1/10
+
2/15
----
7/30
```

Note that both the Fraction and Complex classes contain add: and print methods. So when executing the message expressions