| Method Reference | Equivalent Lambda Expression | Notes |
|---|---|---|
| `separator::equals` | `x -> separator.equals(x)` | This is a method expression with an object and an instance method. The lambda parameter is passed as the explicit parameter of the method. |
| `String::trim` | `x -> x.strip()` | This is a method expression with a class and an instance method. The lambda parameter becomes the implicit parameter. |
| `String::concat` | `(x, y) -> x.concat(y)` | Again, we have an instance method, but this time, with an explicit parameter. As before, the first lambda parameter becomes the implicit parameter, and the remaining ones are passed to the method. |
| `Integer::valueOf` | `x -> Integer.valueOf(x)` | This is a method expression with a static method. The lambda parameter is passed to the static method. |
| `Integer::sum` | `(x, y) -> Integer.sum(x, y)` | This is another static method, but this time with two parameters. Both lambda parameters are passed to the static method. The Integer.sum method was specifically created to be used as a method reference. As a lambda, you could just write `(x, y) -> x + y`. |
| `String::new` | `x -> new String(x)` | This is a constructor reference—see Section 6.2.5. The lambda parameters are passed to the constructor. |
| `String[]::new` | `n -> new String[n]` | This is an array constructor reference—see Section 6.2.5. The lambda parameter is the array length. |