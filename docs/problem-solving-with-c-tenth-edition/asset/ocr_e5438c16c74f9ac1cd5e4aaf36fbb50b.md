# DISPLAY 14.1  A Recursive Output Function *(part 2 of 2)*

```
```cpp
15    cout << "writeVertical(12): " << endl;
16    writeVertical(12);
17
18    cout << "writeVertical(123):" << endl;
19    writeVertical(123);
20
21    return 0;
22 }
23
24 //uses iostream:
25 void writeVertical(int n)
26 {
27     if (n < 10)
28     {
29         cout << n << endl;
30     }
31     else //n is two or more digits long:
32     {
33         writeVertical(n / 10);
34         cout << (n % 10) << endl;
35     }
36 }
```
```

# Sample Dialogue

```
```text
writeVertical(3):
3
writeVertical(12):
1
2
writeVertical(123):
1
2
3
```
```

# Tracing a Recursive Call

Let’s see exactly what happens when the following function call is made:

```
```cpp
writeVertical(123);
```
```

When this function call is executed, the computer proceeds just as it would with any function call. The argument 123 is substituted for the parameter n in the function definition, and the body of the function is executed. After the substitution of 123 for n, the code to be executed is as follows: