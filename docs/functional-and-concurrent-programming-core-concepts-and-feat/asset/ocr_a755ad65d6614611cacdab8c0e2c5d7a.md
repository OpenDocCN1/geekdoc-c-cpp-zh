of those “boxes” from our earlier discussion of map in Section 10.9. Indeed, the computation that calculates the factorial of n is factorial(n - 1).map(x => x * n). So, what we need is to add a map method to the Computation type. It could be implemented naively as follows:

```
// DON'T DO THIS!
trait Computation[A]:
    @tailrec
    final def result: A = this match
      case Done(value) => value
      case Call(thunk) => thunk().result

    def map[B](function: A => B): Computation[B]

case class Done[A](value: A) extends Computation[A]:
    def map[B](f: A => B): Computation[B] = Done(f(value))

case class Call[A](thunk: () => Computation[A]) extends Computation[A]:
    def map[B](f: A => B): Computation[B] = Call(() => Done(f(thunk().result)))
```

Invoking map(f) on a Done object simply applies f to the value inside. On a Call object, map produces a new computation that will apply f to the result of the current computation.

The problem with this approach is that the execution stack grows when you compute the result of a computation. If c2 = c1.map(f), then the evaluation of c2.result involves computing f(c1.result).result. In other words, before the tail-call to result—which is still optimized as a loop—the execution reenters result to apply f. If you evaluate a long enough chain of calls to map, you will still run out of stack space.

To avoid this, the implementation of Computation needs to be refined. The remainder of this section focuses on the implementation of flatMap instead of map. The reason is that flatMap is needed to handle functions with multiple recursive calls, and map can always be derived from flatMap.

# NOTE

The implementation developed here follows a strategy defined by Rúnar Óli Bjarnason in his article “Stackless Scala with Free Monads.” The same strategy is implemented, more robustly, in the standard Scala library as scala.util.control.TailCalls.

The implementation of Computation just given runs into problems because the map method in class Call uses result to generate a suitable input for function f. This can be avoided by delaying the creation of the computation that uses f until you are inside the implementation of result. There, you can deal with chained calls to flatMap explicitly, in ways that avoid growing the execution stack: