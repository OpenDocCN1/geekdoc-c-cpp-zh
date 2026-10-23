

```
val ret = data(front)
front = (front+1)%data.length
ret
}

def peek:A = data(front)

def isEmpty:Boolean = front==back
}
```

这段代码与我们之前为栈编写的代码非常相似。你可能会觉得奇怪的唯一元素是，从数组末尾回绕到开头是通过取模完成的。`dequeue` 中的回绕以及 `enqueue` 结尾处的回绕完全可以用一个 `if` 来完成。对于另外两种情况，回绕需要在表达式中进行。这使得取模更加有效。

所有操作摊还成本均为 O(1)。与栈上的 `push` 一样，`dequeue` 方法在需要扩容的调用中会是 O(n)。然而，这些情况很少，以至于平均下来为常数时间。

## 24.7 单元测试

到目前为止你应该已经很清楚，代码能够编译并不意味着代码是正确的。代码中仍可能存在运行时和逻辑错误。为了找到这些错误，你需要对代码进行测试。测试的主题最早在第 8.5 节中被讨论过。那时描述的测试是手动测试。每个测试都必须由开发者显式运行，如果我们想测试代码的话。此外，其中一些测试会打印出需要由程序员验证正确性的值。在大规模开发中，这些方法不足以帮助我们生产出可靠的代码。在本节中，我们将通过引入自动化单元测试的概念来解决这个问题。

单元测试是对程序中某个特定单元的功能进行检查的测试。通常它类似于一个单一的类，甚至是类中的某些方法。单元测试旨在自动运行，因此不依赖于程序员的交互来判断测试是否通过或失败。这种逻辑应该内置于测试中。这使得单元测试可以频繁运行。思路是，每当你对代码进行更改时，都重新运行所有单元测试，以确保更改没有破坏任何东西。

有许多类型的单元测试框架。其中一些，如 ScalaTest、ScalaCheck 和 Specs，是专门为 Scala 编写的。在本书中，我们将使用 JUnit，即 Java 的主要单元测试框架。选择它的原因包括 JUnit 被广泛使用，使用简单，并且在 Eclipse 和其他 IDE 中有内置支持。

### 24.7.1 设置

为了在 Eclipse 中让 JUnit 与我们的项目一起运行，我们需要执行几个步骤。首先，访问 http://www.junit.org/ 并点击 “Download JUnit”。这会带你到一个包含许多不同下载的页面。你应该获取最新版本的 “Basic jar”。将此文件保存在你的 Eclipse 工作区或某个容易找到的位置。

现在进入 Eclipse，右键点击你想要添加测试的项目。从弹出菜单中选择 “Build Path” > “Configure Build Path...”。转到 “Libraries” 选项卡并点击 “Add External JARs...” 按钮。导航到该文件并选择它后，你就完成了为该项目设置运行 JUnit 测试的工作。

### 24.7.2 编写测试

与我们会放在伴生对象 `main` 方法中的测试不同，单元测试放在单独的文件中，甚至放在单独的包或项目中。我们将采用的方法是把所有测试代码放在以 `test` 开头的并行包层次结构中。由于 `ArrayStack` 和 `ArrayQueue` 位于 `scalabook.adt` 包中，我们的测试将位于 `test.scalabook.adt` 中。要创建测试，我们只需编写包含方法和使用 JUnit 的 `@Test` 注解来注解测试方法的类。为此能够编译，你应该执行 `import org.junit._`。你放置 `@Test` 注解的每个方法都将作为单元测试的一部分运行。

在测试方法内部，你需要调用 JUnit 的断言方法。有诸如 `assertTrue`、`assertFalse` 和 `assertEquals` 等方法。通常，测试是从测试非常简单需求的测试开始构建到更重要的测试。 为了理解其简单程度，请考虑以下示例。

```
@Test def emptyOnCreate {
  val stack = new ArrayStack[Int]
  assertTrue(stack.isEmpty)
}
```

```
@Test def nonEmptyOnPush {
  val stack = new ArrayStack[Int]
  stack.push(5)
  assertFalse(stack.isEmpty)
}
```

```
@Test def pushPop {
  val stack = new ArrayStack[Int]
  stack.push(5)
  assertEquals(5,stack.pop)
}
```

前两个测试只检查新栈是否为空，以及在推送某些内容后是否不为空。直到第三个测试，我们才真正弹出栈并检查是否得到正确的值。

你会注意到所有这些方法都以同一行开头。测试中的代码重复与在正常代码开发中一样令人反感。然而，由于 JUnit 每次单独运行测试，你必须使用一个标签来确保你想要运行的代码在每次测试之前都发生。用于此目的的标签是 `@Before` 标签。如果你在 “before” 方法中发生的事情之后需要代码在每次测试后进行清理，还有一个 `@After` 标签。你可以在下面的代码中看到这些用法，以及对 `ArrayStack` 的更完整的测试集。

```
package test.scalabook.adt
```

```
import org.junit._
import org.junit.Assert._
import scalabook.adt._
```

```
class TestArrayStack {
  var stack:Stack[Int] = null

  @Before def initStack {
    stack = new ArrayStack[Int]
  }

  @Test def emptyOnCreate {
    assertTrue(stack.isEmpty)
  }

  @Test def nonEmptyOnPush {
    stack.push(5)
    assertFalse(stack.isEmpty)
  }

  @Test def pushPop {
    stack.push(5)
    assertEquals(5,stack.pop)
  }

  @Test def pushPopPushPop {
    stack.push(5)
    assertEquals(5,stack.pop)
    stack.push(3)
    assertEquals(3,stack.pop)
  }

  @Test def pushPushPopPop {
    stack.push(5)
    stack.push(3)
    assertEquals(3,stack.pop)
    assertEquals(5,stack.pop)
  }

  @Test def push100Pop100 {
    val nums = Array.fill(100)(util.Random.nextInt)
    nums.foreach(stack.push(_))
    nums.reverse.foreach(assertEquals(_,stack.pop))
  }
}
```

这些测试是不完整的。把更多的测试想出来并实现作为学生的练习留给读者。

现在这些测试已经写好，我们只需要运行它们并确保我们的实现通过了所有测试。如果你选择在 Eclipse 中为该文件运行选项，你应该会看到 “JUnit Test” 选项。如果你选择它，你应该会看到类似于图 24.5 所示的内容。这显示了上面六个测试全部通过。当一切通过时，我们得到绿色条。如果任何测试失败，就会显示红色条，并且失败的测试会以红色显示。你可以点击失败的测试来找出导致失败的断言。

类似的测试也可以为我们的队列编写。它们可能看起来像以下内容。

```
package test.scalabook.adt
```

![](img/157fcf510c119278e4b1267c62717fa8_682_0.png)

图 24.5：当 JUnit 测试运行且所有测试都通过时，Eclipse 会显示此内容。绿色条意味着一切正常。如果出现红色条，则一个或多个测试失败，它们会为你列出。

```
import org.junit._
import org.junit.Assert._
import scalabook.adt._

class TestArrayQueue {
  var queue:Queue[Int] = null

  @Before def initQueue {
    queue = new ArrayQueue[Int]
  }

  @Test def emptyOnCreate {
    assertTrue(queue.isEmpty)
  }

  @Test def nonEmptyOnEnqueue {
    queue.enqueue(5)
    assertFalse(queue.isEmpty)
  }

  @Test def enqueueDequeue {
    queue.enqueue(5)
    assertEquals(5,queue.dequeue)
  }

  @Test def enqueueDequeueEnqueueDequeue {
    queue.enqueue(5)
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

你也可以检查这些，并会发现我们基于数组的队列实现通过了所有这些测试。

### 24.7.3 测试套件

自动化测试的目的是使在开发过程中定期运行所有测试变得容易。能够定期运行所有测试的能力让你在对代码进行更改时更有信心。如果你运行测试并且它们通过，然后进行更改并导致一个或多个测试失败，你就知道确切导致失败的原因，并且更容易定位和诊断。

不幸的是，遍历每个测试类并运行它与遍历大量定义了 `main` 用于测试的对象一样痛苦。为了整合你的测试运行，你可以创建一个测试套件。这让你可以指定一组包含应一起运行的测试代码的不同类。要构建测试套件，你创建一个类并用 `@RunWith` 和 `@Suite.SuiteClasses` 注解进行注解。这里是一个包含我们刚刚编写的两个测试的套件示例。

```
package test

import org.junit.runner.RunWith
import org.junit.runners.Suite

@RunWith(classOf[Suite])
@Suite.SuiteClasses(Array(
    classOf[scalabook.adt.TestArrayStack],
    classOf[scalabook.adt.TestArrayQueue],
    classOf[scalabook.util.TestRPNCalc]
))
class AllTests
```

请注意，该类实际上什么也没包含。正是注解告诉 JUnit 这里应该完成的所有工作。随着我们添加更多测试类，我们也会将它们添加到我们的套件中。

