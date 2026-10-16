We can use the Either for validation. For example, we can chain validation functions that when are not validated return a Left with the appropriate validation error. For example, let us say that we have an isDigit function that checks if a given input string consists of digits only:

```
Either<TestError, string> isDigit(string str) =>
    str.ForAll(Char.IsDigit)
    ? Right<TestError, string>(str)
    : Left<TestError, string>(new TestError("must be a valid number"));
```

We can also have a function that checks for the maximum length of a string (notice that this is a curried function)

```
Func<string, Either<TestError, string>> maxStrLength(int maxlenght) => str =>
    str.Length < maxlenght
    ? Right<TestError, string>(str)
    : Left<TestError, string>(new TestError("failed max length"));
```

Then could chain those two validations, making sure that a string input satisfies both validations:

```
var res = maxStrLength(3)("abcd").Bind(s => isDigit(s));
```

```
res.Match(
    Right: _ =>
    {
        Console.WriteLine("no errors");
    },
    Left: error =>
    {
        Console.WriteLine(error);
    });
```

Run This: .Net Fiddle

The problem with the use of either for validation is that we cannot accumulate errors from each validation, instead the composite validation fails at the first unsuccessful validation and returns the error of this validation.

To accumulate errors, we must use the Validation Type from the Language-ext library.

# 5.6 Validation Monad

In this this section we are going to take a brief look at the validation type. The Validation behaves like the Either but also has an operation to accumulate validation erros.