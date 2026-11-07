The variable `cin` can access the stream function `get`, which is used to read character data. The `get` function inputs the very next character, including whitespace characters, from the input stream and stores it in the memory location indicated by its argument. The function `get` comes in many forms. Next, we discuss the one that is used to read a character.

The syntax of `cin`, together with the `get` function to read a character, follows:

```
`cin.get(varChar);`
```

In the `cin.get` statement, `varChar` is a `char` variable. `varChar`, which appears in parentheses following the function name, is called the **argument** or **parameter** of the function. The effect of the preceding statement would be to store the next input character in the variable `varChar`.

Now consider the following input again:

```
    A 25
```

To store 'A' in `ch1`, the blank in `ch2`, and `25` in `num`, you can effectively use the `get` function as follows:

```
    cin.get(ch1);
    cin.get(ch2);
    cin >> num;
```

Because this form of the `get` function has only one argument and reads only one character and you need to read two characters from the input stream, you need to call this function twice. Notice that you cannot use the `get` function to read data into the variable `num` because `num` is an `int` variable. The preceding form of the `get` function reads values of only the `char` data type.

The preceding set of `cin.get` statements is equivalent to the following statements:

```
    cin >> ch1;
    cin.get(ch2);
    cin >> num;
```

> > **NOTE**
> >
> > The function `get` has other forms, one of which you will study in Chapter 8.
> > For the next few chapters, you need only the form of the function `get` introduced here.

# ## `cin` and the `ignore` Function

When you want to process only partial data (say, within a line), you can use the stream function `ignore` to discard a portion of the input. The syntax to use the function `ignore` is:

```
`cin.ignore(intExp, chExp);`
```