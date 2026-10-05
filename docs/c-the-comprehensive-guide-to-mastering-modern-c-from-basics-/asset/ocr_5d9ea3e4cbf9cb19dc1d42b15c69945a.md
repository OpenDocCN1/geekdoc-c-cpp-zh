```
}
```

But for Number, there is no operator<<. Therefore, the compilation of the print(seven); statement fails.

There is an important term you should remember: you instantiate a function template at the moment you actually call it with a specific type. This is important because it is only at that moment that the compiler checks whether the template's source code can be translated.

For example, you can make the listing compilable after the fact by adding:

```
std::ostream& operator<<(std::ostream& os, Number z) {
  return os << z.value;
}
```

Think of it roughly as the compiler looking at the content of the function only at the moment you use it concretely. “looking at” consists of the concrete type parameter being applied at all points and the function being truly generated—as if you had written into the source code. This may not be a completely accurate perspective, but it is useful and sufficient for getting started.

If your terminology is to be precise, then use the following terms:

+   - A function template is the blueprint.

+   - You instantiate the function template by specifying the template parameters.