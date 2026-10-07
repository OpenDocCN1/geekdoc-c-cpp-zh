# Chapter 17: Building Custom Collections

LISTING 17.9: Span<T> Examples

```
string[] languages = new[] {
  "C#", "COBOL", "Java",
  "TypeScript", "Python",
};

// Create a Span<string> from the arrays first 3 elements.
Span<string> languagesSpan = languages.AsSpan(0, 2);
languages[0] = "R";
Assert(languages[0] == languagesSpan[0]);
Assert("R" == languagesSpan[0]);
languagesSpan[0] = "Lisp";
Assert(languages[0] == languagesSpan[0]);
Assert("Lisp" == languages[0]);

int[] numbers = languages.Select(item => item.Length).ToArray();
// Create a Span<char> from the arrays first 3 elements.
Span<int> numbersSpan = numbers.AsSpan(0, 2);
Assert(numbers[1] == numbersSpan[1]);
numbersSpan[1] = 42;
Assert(numbers[1] == numbersSpan[1]);
Assert(42 == numbers[1]);
```

```
const string bigWord = "supercalifragilisticexpialidocious";
// Create a Span<char> from a suffix portion of the word.
#if NETB_0_OR_GREATER
ReadOnlySpan<char> expialidocious = bigWord.AsSpan(20..);
#else
ReadOnlySpan<char> expialidocious = bigWord.AsSpan(20, 14);
#endif
// NETB_0_OR_GREATER
Assert(expialidocious.ToString() == "expialidocious");
```

To demonstrate the behavior of shared memory, review how we can assign a new value to languages[0] and the corresponding element in languagesSpan will update, and vice versa. Furthermore, this behavior applies whether using a collection of reference types or value types.

There is also a ReadOnlySpan<T>, which allows the same construct on an immutable array such as a string, rather than allocating an entirely new string. that points to a slice of the original string, With ReadOnlySpan<T> we can have a new more performance-based approach when a slice of the original array is all that is needed.