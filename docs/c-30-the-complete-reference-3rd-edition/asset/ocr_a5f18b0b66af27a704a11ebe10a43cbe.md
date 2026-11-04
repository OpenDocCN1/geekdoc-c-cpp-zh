# Missing Pieces

Some interesting for loop variations are created by leaving pieces of the loop definition empty. In C#, it is possible for any or all of the initialization, condition, or iteration portions of the for loop to be empty. For example, consider the following program:

```
// Parts of the for can be empty.

using System;

class Empty {
    static void Main() {
        int i;

        for(i = 0; i < 10; ) {
            Console.WriteLine("Pass #" + i);
            i++; // increment loop control var
        }
    }
}
```

Here, the iteration expression of the for is empty. Instead, the loop control variable i is incremented inside the body of the loop. This means that each time the loop repeats, i is tested to see whether it equals 10, but no further action takes place. Of course, since i is incremented within the body of the loop, the loop runs normally, displaying the following output:

```
Pass #0
Pass #1
Pass #2
Pass #3
Pass #4
Pass #5
Pass #6
Pass #7
Pass #8
Pass #9
```

In the next example, the initialization portion is also moved out of the for:

```
// Move more out of the for loop.

using System;

class Empty2 {
    static void Main() {
        int i;

        i = 0; // move initialization out of loop
        for(; i < 10; ) {
            Console.WriteLine("Pass #" + i);
            i++; // increment loop control var
        }
    }
}
```