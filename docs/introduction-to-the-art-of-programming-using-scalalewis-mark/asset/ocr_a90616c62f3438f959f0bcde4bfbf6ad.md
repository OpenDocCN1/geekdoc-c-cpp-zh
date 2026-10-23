```
assertEquals(5,queue.dequeue)
queue.enqueue(3)
assertEquals(3,queue.dequeue)
}

@Test def enqueueEnqueueDequeueDequeue {
queue.enqueue(5)
queue.enqueue(3)
assertEquals(5,queue.dequeue)
assertEquals(3,queue.dequeue)
}

@Test def enqueue100Dequeue100 {
val nums = Array.fill(100)(util.Random.nextInt)
nums.foreach(queue.enqueue(_))
nums.foreach(assertEquals(_,queue.dequeue))
}
}
```

You can check these as well and see that our array-based implementation of a queue passes all of these tests.

# 24.7.3 Test Suites

The purpose of automated testing is to make it easy to run all the tests regularly during development. Having the ability to run all of your tests on a regular basis makes you more confident when you go to make changes to your code. If you run the tests and they pass, then make a change and one or more fail, you know exactly what caused the failure and it will be easier to locate and diagnose.

Unfortunately, going through every test class and running it would be just as much of a pain as going through a large number of objects that have a main defined for testing. To consolidate your test runs, you can make a test suite. This lets you specify a group of different classes that contain test code that should be run together. To build a test suite you make a class and annotate it with the @RunWith and @Suite.SuiteClasses annotations. Here is an example of a suite that contains the two tests we just wrote.

```
package test

import org.junit.runner.RunWith
import org.junit.runners.Suite

@RunWith(classOf[Suite])
@Suite.SuiteClasses(Array(
    classOf[scalabook.adT.TestArrayStack],
    classOf[scalabook.adT.TestArrayQueue],
    classOf[scalabook.util.TestRPNCalc]
))
class AllTests
```

Note that the class does not actually contain anything at all. It is the annotations that tell JUnit all the work that should be done here. As we add more test classes, we will also add them to our suite.