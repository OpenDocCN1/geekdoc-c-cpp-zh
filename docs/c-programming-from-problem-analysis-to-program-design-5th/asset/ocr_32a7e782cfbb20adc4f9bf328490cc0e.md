# EXAMPLE 3-5

Consider the declaration:

```
int a, b;
```

and the input:

```
25 67 89 43 72
12 78 34
```

Now consider the following statements:

```
cin >> a;
cin.ignore(100, '\n');
cin >> b;
```

The first statement, cin >> a;, stores 25 in a. The second statement, cin.ignore(100, '\n');, discards all of the remaining numbers in the first line. The third statement, cin >> b;, stores 12 (from the next line) in b.

# EXAMPLE 3-6

Consider the declaration:

```
char ch1, ch2;
```

and the input:

```
Hello there. My name is Mickey.
```

+   a. Consider the following statements:

```
cin >> ch1;
cin.ignore(100, '.');
cin >> ch2;
```

The first statement, cin >> ch1;, stores 'H' in ch1. The second statement, cin.ignore(100, '.');, results in discarding all characters until . (period). The third statement, cin >> ch2;, stores the character 'M' (from the same line) in ch2. (Remember that the extraction operator >> skips all leading whitespace characters. Thus, the extraction operator skips the space after . [period] and stores 'M' in ch2.)

+   b. Suppose that we have the following statement:

```
cin >> ch1;
cin.ignore(5, '.');
cin >> ch2;
```