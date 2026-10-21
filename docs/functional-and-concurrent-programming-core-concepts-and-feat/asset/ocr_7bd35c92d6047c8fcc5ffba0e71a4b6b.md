Other list functions could be reimplemented using pattern matching—for instance, isEmpty:

```
def isEmpty[A](list: List[A]): Boolean = list match
  case Nil => true
  case _ => false

def isEmpty[A](list: List[A]): Boolean = list match
  case _ :: _ => false
  case _ => true
```

Listing 5.7: Reimplementing isEmpty using pattern matching.

The first variant uses Nil to match the empty list, and “_” to match every other—and therefore non-empty—list. The second variant matches non-empty lists first, using pattern “_ :: _”, which matches any list with a head and a tail. The next pattern matches only the list without a head and tail—the empty list—and could have used Nil instead of “_” for clarity. Either approach is correct.

In the implementation of function isEmpty, patterns are used only to distinguish between empty and non-empty lists, while in head and tail they also extract a component from a non-empty list. Depending on your needs, you can match a non-empty list with any of the following patterns:

```
_ :: _            // nothing captured
head :: _          // capture head only
_ :: tail          // capture tail only
head :: tail       // capture head and tail
all @ head :: tail // capture head, tail, and the entire list
all @ head :: _    // capture head and the entire list
all @ _ :: tail    // capture tail and the entire list
all @ _ :: _       // capture the entire list
```

Patterns can be nested arbitrarily. In particular, you can use “@” to capture a component of a composite type while breaking it into its own components at the same time. For instance, if an expression is a list of options of pairs, pattern matching can be applied to the list, and to an option inside the list, and to a pair inside an option, all within the same pattern:

```
List(Some(("foo", 42)), None) match
  case (head @ Some(str, n)) :: tail => <expr>
```

Inside expression <expr>, variables head, str, n, and tail denote the following values: