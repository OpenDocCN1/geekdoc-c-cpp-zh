When writing a macro, it is not unusual to need a new name for something. A string can be created by concatenating two strings using the ## macro operator. For example:

```
#define NAME2(a,b) a##b

int NAME2(hack,cah)();
```

will produce

```
int hackcah();
```

A single # before a parameter name in a replacement string means a string containing the macro argument. For example:

```
#define printx(x) cout << "x" << " = " << x << '\n';

int a = 7;
string str = “asdf”;
void f() {
    printx(a); // cout << “a” << " = " << a << '\n';
    printx(str); // cout << “str” << " = " << str << '\n';
}
```

Writing #x = “ rather than #x << ” = “ is obscure “clever code” rather than an error. Adjacent string literals are concatenated (§7.3.2).

The directive

```
#undef X
```

ensures that no macro called X is defined – whether or not one was before the directive. This affords some protection against undesired macros. However, it is not always easy to know what the effects of X on a piece of code were supposed to be.

The argument list (“replacement list”) of a macro can be empty:

```
#define EMPTY() std::cout<<“empty\n”
EMPTY(); // print”empty\n”
EMPTY; // error : macro replacement list missing
```

I have a hard time thinking of uses of an empty macro argument list that are not error-prone or malicious.

Macros can even be variadic. For example:

```
#define err_print(...) fprintf(stderr,“error: %s %d\n”, __VA_ARGS__)
err_print(“The answer”,54);
```

The ellipsis (...) means that __VA_ARGS__ represents the arguments actually passed as a string, so the output is:

```
error: The answer 54
```

# 12.6.1 Conditional Compilation

One use of macros is almost impossible to avoid. The directive

```
#ifdef IDENTIFIER
```

does nothing if IDENTIFIER is defined, but if it is not, the directive causes all input to be ignored until a #endif directive is seen. For example: