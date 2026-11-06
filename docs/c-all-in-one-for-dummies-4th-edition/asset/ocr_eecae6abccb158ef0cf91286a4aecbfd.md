# ARGUING OVER PARAMETERS

Technically, the term *parameter* refers to the inputs to the function, from the function's perspective. When you call the function, the things you place in parentheses in the call line are not parameters; rather, they are described as *arguments*. Thus, in the following function header:

```
```
string ConnectNames(string first, string last)
```
```

the variables first and last are parameters. But in the following call to a function (found in Listing 6-7)

```
```
ConnectNames("Bill", "Murray")
```
```

the strings "Bill" and "Murray" are arguments of the call.

# ## Understanding the AddOne() name and type

Look at the AddOne() header again:

```
```
int AddOne(int start)
```
```

The word AddOne is the name of the function, as you've probably figured out already. And that leaves the thing at the beginning — the int. That's the type of the return value. The final line in the function before the closing brace is

```
```
return newnumber;
```
```

The variable newnumber inside the function is an integer. And the return type is int. That's no accident: As programmers have all heard before, friends don't let friends return something other than the type specified in the function header. The two must match in type. And further, examine this line from inside main():

```
```
int result = AddOne(testnumber);
```
```

The type of result is also an integer. All three match. Again, no accident. You can copy one thing to another (in this case, the function's return value to the variable called result) only if they match in type. And here, they do — they're both integers.