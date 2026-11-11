| Functional Interface | Parameter Types | Return Type | Abstract Method Name | Description | Other Methods |
|---|---|---|---|---|---|
| Runnable | none | void | run | Runs an action without arguments or return value | |
| Supplier<T> | none | T | get | Supplies a value of type T | |
| Consumer<T> | T | void | accept | Consumes a value of type T | andThen |
| BiConsumer<T, U> | T, U | void | accept | Consumes values of types T and U | andThen |
| Function<T, R> | T | R | apply | A function with argument of type T | compose, andThen, identity |
| BiFunction<T, U, R> | T, U | R | apply | A function with arguments of types T and U | andThen |
| UnaryOperator<T> | T | T | apply | A unary operator on the type T | compose, andThen, identity |
| BinaryOperator<T> | T, T | T | apply | A binary operator on the type T | andThen, maxBy, minBy |
| Predicate<T> | T | boolean | test | A boolean-valued function | and, or, negate, isEqual, not |
| BiPredicate<T, U> | T, U | boolean | test | A boolean-valued function with two arguments | and, or, negate |

Note that the body of the lambda expression is executed when action.run() is called.