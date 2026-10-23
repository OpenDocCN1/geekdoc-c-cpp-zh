2^n/nThreads * (2^n/nThreads+1)*... When n is not divisible by nThreads, we need to make some of the groups bigger. Here is code that does that.

```
```
def parallelFactorial(n:BigInt,es:ExecutorService,nThreads:Int):BigInt = {
  val block = n/nThreads
  val rem = n%nThreads
  var i=BigInt(1)
  val futures = Array.tabulate(nThreads)(j => es.submit(new Callable[BigInt] {
    def call():BigInt = {
      val start = i
      val end = start + block + (if(BigInt(j)<rem) 1 else 0)
      i = end
      (start until end).product
    }
  }))
  futures.map(_.get).product
}
```
```

This function starts with calculations of the base size for each block as well as how many blocks need to be one bigger. It then creates a variable i that helps us keep track of where in the range we are. A call to Array.tabulate is used to submit the proper number of tasks to the ExecutorService. Each task uses i as the start value and adds an appropriate offset to get the end value. It then updates i and uses the standard product method to multiply the values in that chunk. The last thing this code does is map the various Future[BigInt] objects with get. This will block until they are done and give us a collection of the results. Another call to product produces the final result.

You can put this in a script or load it into the REPL to test it. When you do this, you probably want to start off with an import, then make your Executor Service.

```
```
import java.util.concurrent._
val es = Executors.newCachedThreadPool()
```
```

Now you can call the function and compare it to the non-parallel version above. Ideally you would specify the number of threads to be equal to the number of cores in your computer, but you can play with this to see how it impacts execution time. Either at the end of the script or before you exit the REPL you need to call es.shutdown().

This approach to breaking up the work is not the only option we have. One potential problem with this approach is that the different threads we created really do not have equal workloads. The way the BigInt works, dealing with large numbers is slower than dealing with small numbers. Given the way the work was broken up here, the first thread winds up with a much smaller value than the last one and, as such, has a smaller work load. An alternate approach would be to have each thread work with numbers spread out through the whole range. Specifically, the first thread does 1*(nThreads+1)*(2*nThreads+1)*... while the second thread does 2*(nThreads+2)*(2*nThreads+2)*..., etc. The methods of Range types in Scala actually makes this version a lot shorter.

```
```
def parallelFactorial(n:BigInt,es:ExecutorService,nThreads:Int):BigInt = {
  val futures = Array.tabulate(nThreads)(j => es.submit(new Callable[BigInt] {
    def call():BigInt = {
      (BigInt(j+1) to n by nThreads).product
    }
  }))
  futures.map(_.get).product
}
```
```