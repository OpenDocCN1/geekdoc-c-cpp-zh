This code snippet compiles. Problems will arise, however, when we call f:

```
int i = 3;
const int ci = 4;

f(3);
f(i);
f(ci);
```

All three function calls are ambiguous because the best matches are in every case the first overload with the value argument and one of the reference-argument overloads respectively. Mixing overloads of reference and value arguments almost always fails. Thus, when one overload has a reference-qualified argument, then the corresponding argument of the other overload should be reference-qualified as well. We can achieve this in our toy example by omitting the value-argument overload. Then f(3) and f(ci) will resolve to the overload with the constant reference and f(i) to that with the mutable one.

# 1.5.5 main Function

The main function is not fundamentally different from any other function. There are two signatures allowed in the standard:

```
int main()

or

int main(int argc, char* argv[])
```

The latter is equivalent to

```
int main(int argc, char** argv)
```

The parameter argc contains the list of arguments and argc its length. The first argument (argv[0]) is on most systems the name of the called executable (which may be different from the source code name). To play with the arguments, we can write a short program called argc_argv_test:

```
int main (int argc, char* argv[])
{
    for (int i = 0; i < argc; ++i)
        cout << argv[i] << '\n';
    return 0;
}
```

Calling this program with the following options

```
argc_argv_test first second third fourth
```

yields:

```
argc_argv_test
first
second
third
fourth
```