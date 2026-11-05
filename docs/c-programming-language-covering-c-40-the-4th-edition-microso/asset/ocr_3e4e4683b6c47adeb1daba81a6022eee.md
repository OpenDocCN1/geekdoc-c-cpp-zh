```
object IEnumerator.Current {
    get { return __current; }
}

public bool MoveNext() {
    switch (__state) {
        case 1: goto __state1;
        case 2: goto __state2;
    }
    i = __this.count - 1;
__loop:
    if (i < 0) goto __state2;
    __current = __this.items[i];
    __state = 1;
    return true;
__state1:
    --i;
    goto __loop;
__state2:
    __state = 2;
    return false;
}

public void Dispose() {
    __state = 2;
}

void IEnumerator.Reset() {
    throw new NotSupportedException();
}
}
```

In the preceding translation, the code in the iterator block is turned into a state machine and placed in the MoveNext method of the enumerator class. Furthermore, the local variable i is turned into a field in the enumerator object so it can continue to exist across invocations of MoveNext.

The following example prints a simple multiplication table of the integers 1 through 10. The FromTo method in the example returns an enumerable object and is implemented using an iterator.

```
using System;
using System.Collections.Generic;

class Test
{
    static IEnumerable<int> FromTo(int from, int to)
    {
        while (from <= to) yield return from++;
    }
}
```