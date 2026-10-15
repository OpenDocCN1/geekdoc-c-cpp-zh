Step 1: Before main calls cubeByValue:

```
int main()
{
    int number = 5;
    number = cubeByValue( number );
}
```

```
int cubeByValue( int n )
{
    return n * n * n;
}
```

Step 2: After cubeByValue receives the call:

```
int main()
{
    int number = 5;
    number = cubeByValue( number );
}
```

```
int cubeByValue( int n )
{
    return n * n * n;
}
```

Step 3: After cubeByValue cubes parameter n and before cubeByValue returns to main:

```
int main()
{
    int number = 5;
    number = cubeByValue( number );
}
```

```
int cubeByValue( int n )
{
    return n * n * n;
}
```

Step 4: After cubeByValue returns to main and before assigning the result to number:

```
int main()
{
    int number = 5;
    number = cubeByValue( number );
}
```

```
int cubeByValue( int n )
{
    return n * n * n;
}
```

Step 5: After main completes the assignment to number:

```
int main()
{
    int number = 5;
    number = cubeByValue( number );
}
```

```
int cubeByValue( int n )
{
    return n * n * n;
}
```