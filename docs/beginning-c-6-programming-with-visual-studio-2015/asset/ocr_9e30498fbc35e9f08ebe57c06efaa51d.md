Obviously, this iterator isn't a particularly useful one, but it does show how this works in action and how simple the implementation can be. Looking at the code, you might wonder how the code knows to return string type items. In fact, it doesn't; it returns object type values. As you know, object is the base class for all types, so you can return anything from the yield statements.

However, the compiler is intelligent enough that you can interpret the returned values as whatever type you want in the context of the foreach loop. Here, the code asks for string type values, so those are the values you get to work with. You should change one of the yield lines so that it returns, say, an integer, you would get a bad cast exception in the foreach loop.

One more thing about iterators. It is possible to interrupt the return of information to the foreach loop by using the following statement:

```
yield break;
```

When this statement is encountered in an iterator, the iterator processing terminates immediately, as does the foreach loop using it.

Now it's time for a more complicated — and useful! — example. In this Try It Out, you'll implement an iterator that obtains prime numbers.

# TRY IT OUT Implementing an Iterator: Ch11Ex03

+   1. Create a new console application called Ch11Ex03 and save it in the directory C:\BegVCSharp\Chapter11.
+   2. Add a new class called Primes and modify the code in Primes.cs as follows:

```
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace Ch11Ex03
{
public class Primes
{
private long min;
private long max;
public Primes() : this(2, 100) {}
public Primes(long minimum, long maximum)
{
if (minimum < 2)
min = 2;
else
min = minimum;
max = maximum;
}
public IEnumerator GetEnumerator()
{
for (long possiblePrime = min; possiblePrime <= max; possiblePrime++)
```