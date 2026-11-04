
```csharp
// create array for determining primes
primes = Enumerable.Repeat(true, maximum).ToArray();

// reset Canceled and GUI
Canceled = false;
getPrimesButton.Enabled = false; // disable getPrimesButton
cancelButton.Enabled = true; // enable cancelButton
primesTextBox.Text = string.Empty; // clear primesTextBox
statusLabel.Text = string.Empty; // clear statusLabel
percentageLabel.Text = $"{0:P}"; // display 0 %
progressBar.Value = progressBar.Minimum; // reset progressBar min
progressBar.Maximum = maximum; // set progressBar max

// show primes up to maximum
int count = await FindPrimes(maximum);
statusLabel.Text = $"Found {count} prime(s)";
}

// displays prime numbers in primesTextBox
private async Task<int> FindPrimes(int maximum)
{
    var primeCount = 0;

    // find primes less than maximum
    for (var i = 2; i < maximum && !Canceled; ++i)
    {
        // if i is prime, display it
        if (await Task.Run(() => IsPrime(i)))
        {
            ++primeCount; // increment number of primes found
            primesTextBox.AppendText($"{i}{Environment.NewLine}");
        }

        var percentage = (double)progressBar.Value /
            (progressBar.Maximum - progressBar.Minimum + 1);
        percentageLabel.Text = $"{percentage:P}";
        progressBar.Value = i + 1; // update progress
    }

    // display message if operation was canceled
    if (Canceled)
    {
        primesTextBox.AppendText($"Canceled{Environment.NewLine}");
    }

    getPrimesButton.Enabled = true; // enable getPrimesButton
    cancelButton.Enabled = false; // disable cancelButton
    return primeCount;
}
```

图 21.6 | 显示异步任务的进度和中间结果。（第 2 部分，共 3 部分。）

小于最大值的数。埃拉托斯特尼筛法接收一个整数列表，并从第一个素数开始，筛除该素数的所有倍数。然后它移到下一个尚未被筛除的数，也就是下一个素数，再消除它的所有倍数。如此继续，直到所有已知素数都被筛除。从算法上说，我们从 bool 数组的元素 2 开始（忽略元素 0 和 1），把所有是 2 的倍数的索引处的元素设为 false，表示它们能被 2 整除，因此不是素数。然后移到下一个数组元素，检查它是否为 true；如果是，就把它的所有倍数设为 false，表示它们能被当前索引整除。算法完成时，所有包含 true 的索引都是素数，因为它们没有除数。本示例中的埃拉托斯特尼筛法由方法 FindPrimes（第 48–77 行）和 IsPrime（第 81–99 行）实现。每当 IsPrime 确定某个特定数是素数时，它就会立即消除该数的所有倍数。

## 构造函数

类 FindPrimesForm 的构造函数（第 16–21 行）将 progressBar 的 Minimum 属性设置为 2——第一个素数——并将 percentageLabel 的 Text 设置为 0，格式化为整数百分比。在格式说明符 P0 中，P 表示该值应格式化为百分比，0 表示小数位数为零。

## async 方法 getPrimesButton_Click

当用户在 maxValueTextBox 中输入一个数字并按下 Get Primes Button 时，将调用方法 getPrimesButton_Click（第 24–45 行）。此方法声明为 async，因为它将等待 FindPrimes 方法的结果。第 27 行获取用户输入的最大值，然后第 30 行创建一个包含该数量元素的 bool 数组，并用 true 值填充。索引不是素数的元素最终将被设置为 false。Enumerable 静态方法 Repeat 创建一个元素列表，其中包含其第一个参数的值。第二个参数指定列表的长度。然后我们对结果调用 ToArray，以获得这些元素的数组表示。Repeat 是一个泛型方法——它返回的列表类型由第一个参数的类型决定。

第 33–40 行将 Cancelled 属性重置为 false，并重置 GUI，以准备确定素数。第 39–40 行将 progressBar 的 Value 重置为 Minimum 值，并将 Maximum 设置为用户输入的新值。当我们测试从 2 到最大值的每个数以确定它是否为素数时，我们会将 progressBar 的 Value 属性设置为当前正在测试的数。随着这个数增大，progressBar 将按比例填充颜色，以显示异步任务的进度。

第 43 行调用 async 方法 FindPrimes，开始查找素数的过程。完成后，FindPrimes 返回小于用户输入最大值的素数个数，随后应用在第 44 行显示该数量。

- 1. 访问 https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes 以进一步了解埃拉托斯特尼筛法。图 21.6 中实现的算法是高效的——即使在数组已经表示用户输入最大值以内的所有素数之后，它仍会继续消除素数的倍数。一旦消除了所有小于或等于最大值平方根的素数的倍数，算法就完成了。作为练习，你可以更新该算法，然后修改更新 progressBar 和 percentage Label 的代码，使它们指示算法的进度，而不是检查该范围内每个数是否为素数的进度。

## async 方法 FindPrimes

async 方法 FindPrimes 实现埃拉托斯特尼筛法算法，显示找到的素数，并更新 progressBar 和完成百分比。第 50 行最初将 primeCount 设置为 0，表示尚未找到任何素数。第 53–66 行遍历从 2 到用户输入的最大值（不包括该最大值）的值。对于每个值，第 56 行启动一个异步 Task 以确定该值是否为素数，并等待该 Task 的结果。当该结果返回时，如果为 true，第 58 行将 primeCount 递增，表示找到了一个素数，第 59 行将该数字的字符串表示追加到 primesTextBox 的文本中——从而显示一个中间结果。无论某个值是否为素数，第 62–64 行都会计算到目前为止循环完成的百分比并显示该百分比，第 65 行更新 progressBar 的 Value。

在 FindPrimes 执行期间的任何时候，用户都可以单击应用的 Cancel Button，此时属性 Canceled 将被设置为 true，循环将提前终止。如果发生这种情况，第 69–72 行会在 primesTextBox 中显示“Canceled”。

## 方法 IsPrime

方法 IsPrime（第 81–99 行）由 async 方法 FindPrimes 调用，以执行埃拉托斯特尼筛法的一部分。IsPrime 通过检查数组 primes 中的相应元素（第 85 行）来测试其 value 参数是否为素数。如果 value 是素数，第 88–91 行将所有是 value 的倍数的索引处的 primes 元素设置为 false，然后第 93 行返回 true，表示 value 是素数；否则，该方法返回 false。

## 方法 cancelButton_Click

当用户单击 Cancel 按钮时，方法 cancelButton_Click（第 102–107 行）将属性 Canceled 设置为 true，然后启用 Get Primes Button 并禁用 Cancel Button。当下一次计算第 53 行的条件时，方法 FindPrimes 中的循环将终止。

## 21.8 小结

在本章中，你学习了如何使用 async 修饰符、await 运算符和 Task 来异步执行长时间运行或计算密集型任务。你了解到，彼此独立进行的任务称为异步执行，并称为异步任务。

我们展示了多线程使线程能够与其他线程并发执行，同时共享应用程序级资源，如内存和处理器。为了充分利用多核体系结构，我们编写了异步处理任务的应用程序。你了解到，异步编程是一种编写包含可异步执行任务的应用程序的技术，对于具有长时间运行或计算密集型任务的应用程序，它可以提高应用性能和 GUI 响应能力。

为了提供有说服力的异步编程演示，我们展示了几个应用程序：

- - 第一个示例展示了如何在 GUI 应用中异步执行计算密集型计算，使 GUI 在计算执行期间保持响应。
