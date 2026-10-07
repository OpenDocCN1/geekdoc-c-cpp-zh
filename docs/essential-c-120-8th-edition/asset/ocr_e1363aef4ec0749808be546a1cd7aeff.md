# 286 Chapter 5: Parameters and Methods

```
if (is null) throw new ArgumentNullException(...)
```

You can accomplish this in a single statement using the null coalescing assignment operator with a throw ArgumentNullException expression if the parameter value is null (see Listing 5.32).

LISTING 5.32: Parameter Validation by Throwing ArgumentNullException

```
httpsUrl = httpsUrl ??
throw new ArgumentNullException(nameof(httpsUrl));
fileName = fileName??
throw new ArgumentNullException(nameof(fileName));
```

```
// ...
```

With .NET 7.0, you can use the ArgumentNullException.ThrowIfNull() method (see Listing 5.33).

LISTING 5.33: Parameter Validation with ArgumentNullException.ThrowIfNull

```
ArgumentNullException.ThrowIfNull(httpsUrl);
ArgumentNullException.ThrowIfNull(fileName);
```

```
// ...
```

Internally, the ArgumentNullException.ThrowIfNull() method also throws the ArgumentNullException.

> Guidelines
DO verify that non-null reference types parameters are not null and throw an ArgumentNullException when they are.
DO use ArgumentNullException.ThrowIfNull() to verify values are null in .NET 7.0 or later.