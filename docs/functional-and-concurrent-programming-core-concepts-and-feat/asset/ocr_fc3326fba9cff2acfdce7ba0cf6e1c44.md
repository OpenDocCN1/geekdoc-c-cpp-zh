For the purpose of our discussion, types can be thought of as sets of values: The type Boolean contains two values, true and false; Int has 2^32 possible values; and String has an infinite number of values. Here, we rely on two small types: Stooge, with three values, and Digit, with ten values.

Product types are used for aggregation. For instance, the pair type (Stooge, Digit) contains values that consist of one stooge and one digit:

```
type StoogeAndDigit = (Stooge, Digit)
```

This type contains 30 values—("Moe", 5), ("Larry", 1), etc.—which is the product of the number of stooges and the number of digits (hence the name). Instead of a pair, you might use casts to join a stooge and a digit in an object-oriented language. In the context of this note, all the types that aggregate one stooge with one digit are equivalent, and denoted as Stooge × Digit.

Types can be aggregated in arbitrary ways. For instance, the type StoogeLink = (Stooge, Stooge, Boolean), denoted as Stooge × Stooge × Boolean, contains all 18 values that consist of two stooges and one Boolean.

Support for product types is almost universal in programming languages, whether through classes, records, or tuples. Functional languages, and many hybrid languages, also support sum types, which represent alternatives. A value that can be a stooge or a digit can be given a type StoogeOrDigit, defined as follows:

```
enum StoogeOrDigit:
    case S(stooge: Stooge)
    case D(digit: Digit)
```

This type contains 13 values—S("Larry"), S("Curly"), S("Moe"), D(0), D(1), …, D(9)—which is the sum of the number of stooges and the number of digits. The names S and D are irrelevant, and the type is denoted as Stooge + Digit. Note that sums can be built from types that are not disjoint sets:

```
enum Number:
    case Zero
    case Pos(digit: Digit)
    case Neg(digit: Digit)
```

Pos(3) and Neg(3) are different values, and the Number type contains 21 values. The name Zero is no more relevant than the names Pos and Neg, and the type can be denoted as Digit + Digit + 1, where “1” represents the single-valued type that contains Zero.