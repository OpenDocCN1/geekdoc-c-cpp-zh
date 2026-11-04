```
// The following line is inherently ambiguous!
// Does it refer to CountDown in Counter or
// to CountDown in AnotherCounter?
CountDown cd1 = new CountDown(10); // Error! !
// ...
}
```

If you try to compile this program, you will receive an error message stating that this line in Main() is ambiguous:

```
CountDown cd1 = new CountDown(10); // Error! !
```

The trouble is that both namespaces, Counter and AnotherCounter, declare a class called CountDown, and both namespaces have been brought into view. Thus, to which version of CountDown does the preceding declaration refer? The :: qualifier was designed to handle these types of problems.

To use the ::, you must first define an alias for the namespace you want to qualify. Then, simply qualify the ambiguous element with the alias. For example, here is one way to fix the preceding program:

```
// Demonstrate the :: qualifier.

using System;

using Counter;
using AnotherCounter;

// Give Counter an alias called Ctr.
using Ctr = Counter;

// Declare a namespace for counters.
namespace Counter {
    // A simple countdown counter.
    class CountDown {
        int val;

        public CountDown(int n) {
            val = n;
        }

        // ...
    }
}

// Another counter namespace.
namespace AnotherCounter {
    // Declare another class called CountDown, which
    // is in the AnotherCounter namespace.
    class CountDown {
        int val;
```