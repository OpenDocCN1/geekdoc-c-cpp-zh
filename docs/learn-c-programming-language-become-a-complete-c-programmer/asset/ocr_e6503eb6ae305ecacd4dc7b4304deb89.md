```
Token_stream ts {cin};
int main(int argc, char * argv[]) {
switch (argc) {
case 1: // read from standard input break;
case 2: // read from argument string ts.set_input(new istringstream{argv[1]});
break;
default:
error("too many arguments");
return 1;
}
table["pi"] = 3.1415926535897932385; // insert predefined names table["e"] = 2.7182818284590452354;
calculate();
return no_of_errors;
}
```

To use an **istringstream**, include **<sstream>**.

It would be easy to modify **main()** to accept several command-line arguments, but this does not appear to be necessary, especially as several expressions can be passed as a single argument:

```
dc "rate=1.1934;150/rate;19.75/rate;217/rate"
```

I use quotes because **;** is the command separator on my UNIX systems. Other systems have different conventions for supplying arguments to a program on startup.

Simple as they are, **argc** and **argv** are still a source of minor, yet annoying, bugs. To avoid those and especially to make it easier to pass around the program arguments, I tend to use a simple function to create a **vector<string>**:

```
vector<string> arguments(int argc, char * argv[])
{
vector<string> res;
for (int i = 0; i!=argc; ++i)
res.push_back(argv[i]);
return res;
}
```

More elaborate argument parsing functions are not uncommon.

# 10.2.8 A Note on Style

To programmers unacquainted with associative arrays, the use of the standard-library **map** as the symbol table seems almost like cheating. It is not. The standard library and other libraries are meant to be used. Often, a library has received more care in its design and implementation than a