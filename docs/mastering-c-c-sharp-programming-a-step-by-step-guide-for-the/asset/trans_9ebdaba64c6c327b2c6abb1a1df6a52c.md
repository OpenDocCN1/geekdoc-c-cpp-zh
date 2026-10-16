
| 异常 | 说明 |
|---|---|
| Exception | 你的文本格式错误，无法转换为其他内容，例如字符串中包含了你想要转换为数字的字母。 |
| UnsupportedException | 你尝试执行了不支持的操作，例如在不允许调用方法的地方调用方法。 |
| ReferenceException | 对象类型（任意类型）的变量中包含的是 null 而不是对象，而你想要执行的操作并不需要 null；它需要其他内容。 |
| OverflowException | 如果你因为多调用了一两个方法而导致栈空间（内存）不足，就会抛出此异常——这通常是递归出现了严重错误。 |
| DivideByZeroException | 你尝试除以零并被捕获。 |
| ArgumentException | 你发送给方法的参数与该方法所需的参数不匹配。 |
| ArgumentNullException | 你传递给方法的参数是 null，但方法需要的是其他内容。 |
| ArgumentOutOfRangeException | 参数的值超出了方法能够合理处理的范围。例如，某个方法需要一个 1 到 9 之间的数字，而你提供了一个数字 -10——这将抛出此类型的异常。 |

如果你恰好没有找到你想要的异常类型，只需自己创建一个。你只需要从 Exception 类派生一个类，或者创建一个从 Exception 类派生出的类再派生的类。例如，如果你愿意，可以从名为 ArgumentNullException 的类派生一个类。

代码如下：

```
// For those of you over the pond, if you really want to and it makes you feel better,
// they can still be called sausages if you want!
public class AteTooManyHotdogsException : Exception
{
    public int HotdogsEaten { get; set; }

    public AteTooManyHotdogsException(int hotdogsEaten)
    {
        HotdogsEaten = hotdogsEaten;
    }
}
```

使用这个类时，你通常会写：

```
throw new AteTooManyHotdogsException(125);
```

以及：

```
try
{
    EatSomeHotdogs(32);
}
```

```
catch(AteTooManyHotdogsException hotdogsException)
{
    Console.WriteLine(hotdogsException.HotdogsEaten + " is far too many hotdogs.");
}
```

## finally 关键字

在我们继续之前，我想谈谈与异常相关的 finally 关键字。在任何 try-catch 块的末尾，你可以添加一个 finally 块，这样它就变成了 try-catch-finally 块。在 finally 部分中，无论发生什么，你的代码都会被执行。如果代码正常通过了 try 块，它会执行。如果抛出了异常，它也会执行。

让我们看看它是如何工作的：

```
try
{
    // Do something that could potentially throw an exception here
}
catch (Exception)
{
    // The exception gets handled here
}
finally
{
    // This code is always going to be executed, no matter what goes on in the try-catch block.
}
```

现在，你可能在想，为什么我不能简单地把 finally 块中的代码放在 try-catch 块之后单独放入程序中呢？为什么不能这样做呢？

```
try
{
    // Do something that could potentially throw an exception here
}
catch (Exception)
{
    // The exception gets handled here
}
```

```
// This code is always going to be executed, no matter what goes on in the try-catch block.
```

你说得很对——无论 try-catch 块内部发生了什么，这段代码总是会执行。然而，这里有一个细微的差别。无论块中是否使用了 return 关键字，finally 块中的内容都会被执行。

看看这段代码，了解一下我在说什么：

```
public static void TestFinally(bool throwException)
{
    try
    {
        Console.WriteLine("in try");

        if (throwException)
        {
```

```
throw new Exception();
}
return;
}
catch (Exception)
{
	Console.WriteLine("in catch");
}
finally
{
	Console.WriteLine("in finally");
}
}
```

尝试运行一下这段代码，看看会发生什么。你会发现，如果执行流程正常且没有遇到任何错误，你会到达 try 块中的 return 语句。然而，由于它在返回任何内容之前离开了该块，finally 块中的内容会被执行。

这意味着 return 语句不能包含在 finally 块中。它们不是这样工作的——当它们被执行时，可能已经在返回了。

这引出了另一个有趣的点。不知何故，finally 块与异常处理绑定了，许多编程书籍只是将它视为异常处理的一部分，纯粹是为了确保无论是否发生错误，代码都会被执行。

这并不是它的真正用途，至少不完全是。如果你只是想达到那个目的，你只需在 try-catch 块完全结束后放置代码即可。

它实际上是在不管方法如何返回的情况下，运行特定代码。你可能有一条正常返回路径，可能有一条错误返回路径，甚至可能找到许多正常返回的方式，但通过强制执行指定的代码，确保它总会运行。例如，你可以做像这样的蠢事：

```
private int numberOfTimesMethodHasBeenCalled = 0;

public static int RandomMethod(int input)
{
    try
    {
        if(input == 0) return 17;
        if(input == 1) return -2;
        if(input == 2) return -11;
        if(input == 3) return 8;
        if(input == 4) return 6;

        return 5;
    }
    finally
    {
        numberOfTimesMethodHasBeenCalled++;
    }
}
```

无论发生什么，无论方法返回什么，finally 块中的代码总是会执行。现在我们也可以用另一种方式来写这段代码，不使用 try-finally 块；例如，你可以把 numberOfTimesMethodHasBeenCalled++ 放在方法的开头，那样也能达到目的。

编写相同代码有很多不同的方式。

## 快速入门

- 当程序中出错时，异常提供了一种方式，让发现问题的代码告诉你出了问题，然后将执行发送回另一段能够处理所报告问题的代码。
- 如果你正在运行一段你认为可能引发问题的代码，你应该将代码包装在 try-catch 块中，并确保将异常类型放在 catch 块括号内。例如，try {/* code that could throw errors goes here */} catch (Exception e) {/* the code that will handle the problem will go here */}.
- 你并不局限于使用 Exception 类；你也可以使用任何从该类派生的类型，例如 FormatException 类。如果这样做，你只会处理指定类型的异常，而其他异常则会被抛到调用栈的更高层。
- 多个 catch 块可以串联在一起，从最具体的异常类型开始，到最不具体的类型。例如，try {} catch(FormatException e) {/* format errors are handled here */} catch(Exception e) {/* all other errors get handled here */}.
- 你可以从 Exception 类派生来创建你自己的异常类型。
- 要在你的代码中启动这一过程，需要使用 throw 关键字。例如，throw new Exception ("An error occurred").

## 接下来是什么？

一开始，使用异常来处理错误可能看起来并不是那么容易。到处都是大量的 try-catch 代码块，而且事情往往看起来和感觉起来比实际需要的更复杂。你不用担心；你可以一点一点地学习。

自己试试吧。当你认为正在编写的一段代码可能会出问题时，使用 try-catch 块。如果你的程序崩溃并抛出异常，也同样处理。

通过错误处理，你可以处理出现的许多问题，而且，可能更重要的是，它能让那些发现问题的方法将问题传递给问题发生的所在位置，或传递给能够处理它的某个地方。

接下来，我们将了解如何像对待对象一样对待方法，以便我们可以在需要时传递它们。这种方式称为委托（delegates），它是下一节——事件（events）——中非常重要的一部分。事件允许一段代码在发生某件事时通知另一段代码。首先，我们将讨论委托。
