is used in place of

```
```cpp
cin.get(c);
```
```

![](bbox=[0.138, 0.183, 0.204, 0.231])

> **NOTE:** *Try using both of them and compare the results.*

The **get(void)** version is used as follows:

```
```cpp
....
char c;
c = cin.get();    // cin.get(c); replaced
....
....
```
```

The value returned by the function **get()** is assigned to the variable **c.**

The function **put()**, a member of **ostream** class, can be used to output a line of text, character by character. For example,

```
```cpp
cout.put('x');
```
```

displays the character **x** and

```
```cpp
cout.put(ch);
```
```

displays the value of variable **ch.**

The variable **ch** must contain a character value. We can also use a number as an argument to the function **put()**. For example,

```
```cpp
cout.put(68);
```
```

displays the character D. This statement will convert the **int** value 68 to a **char** value and display the character whose ASCII value is 68.