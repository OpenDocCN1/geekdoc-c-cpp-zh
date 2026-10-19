
第1-16步：将restingRate改为restingHeartRate，如图5-11所示。在调用ComputeTrainingRate的语句处设置一个断点。
运行窗体。输入静息心率和年龄的值。单击按钮btnTrainingRate。
当程序在调用语句处中断时，检查restingHeartRate的值。
当程序在方法内部的左花括号处中断时，验证方法内的restingRate与调用方法中的restingHeartRate具有相同的值。

## 复习题

5.6 什么是实参？

5.7 什么是形参？

5.8 当一个方法有多个参数时，C#如何确定哪个参数与某个实参相关联？

5.9 参数的作用域是什么？

5.10 判断正误：实参的名称必须与对应形参的名称相同。

5.11 下面的代码展示了一个名为Greetings的方法，以及一个按钮的Click事件处理器，该事件处理器调用了这个方法：

```
private void btnGreeting_Click(object sender, EventArgs e)
{
    string word1 = "Hi", word2 = "There", word = "Hello";
    Greetings(word1);
    Greetings(word2);
}

private void Greetings(string word)
{
    lstDisplay.Items.Add(word);
}
```

当你单击按钮时，列表框中显示的输出是什么？

## 5.3 按值传递参数

当程序调用ComputeTrainingRate(float restingRate, float age)时，默认情况下，调用程序会将每个实参的值传递给对应的形参。这称为按值传递参数，这是向方法传递数据的默认方式。

当实参按值传递时，如果被调用方法中对应形参的值发生了改变，这不会影响调用程序中实参的值——也就是说，如果在ComputeTrainingRate方法中改变了age的值，这对调用程序btnGrade_Click中的age值不会有任何影响。

第1-17步：在ComputeTrainingRate中把age的值改为999（第58行），并在左、右花括号处设置断点，如图5-12所示。

图5-12：修改age值的ComputeTrainingRate

```
private void ComputeTrainingRate(float restingRate, float age)
{
    float maximumRate, trainingRate;
    // Compute maximum heart rate:
    maximumRate = 220 - age;
    // Compute training heart rate
    trainingRate = 0.6F * (maximumRate - restingRate) + restingRate;
    age = 999; // This statement is for testing purposes only
    // Display training heart rate:
    MessageBox.Show("Your Training Heart Rate is: " + trainingRate.ToString("N0"));
}
```

在调用语句（第59行）和调用程序的右花括号处设置断点，如图5-13所示。

图5-13：调用程序中的断点

```
private void btnTrainingRate_Click(object sender, EventArgs e)
{
    float restingHeartRate, age;
    // Get resting rate and age from Textboxes:
    restingHeartRate = float.Parse(txtRestingRate.Text);
    age = float.Parse(txtAge.Text);
    
    // Call ComputeTrainingRate
    ComputeTrainingRate(restingHeartRate, age);
}
```

第1-18步：运行窗体。输入静息心率和年龄的值。单击btnTrainingRate按钮。

当程序在调用语句（第59行）处中断时，检查age的值；当程序在方法内的左花括号（第40行）处中断时，检查age的值，以验证它是你输入的值。当程序在方法末尾（第49行）中断时，检查age的值，观察age为999。

当程序返回到调用程序（第60行）时再次检查age，观察age的值并未从原值发生改变。在被调用方法中赋值为999对调用程序中的实参age没有影响，因为从调用程序传给方法中形参age的只是age的值。
从方法中删除语句“age=999”。

## 默认参数

你可以为一个或多个参数指定默认值（实参）。例如，你可以在ComputeTrainingRate方法的方法头中为age指定默认值（20）：

```
private void ComputeTrainingRate(float restingRate, float age = 20)
```

默认值必须是字面值或常量。

当你调用一个为一个或多个参数指定了默认值的方法时，你可以选择不为age传递实参，如下面的调用语句所示：

```
ComputeTrainingRate(restingRate)
```

在这种情况下，age将取默认值20。

或者，你可以为age传递一个值来覆盖默认值，例如：

```
ComputeTrainingRate(restingRate, age)
```

如果并非所有参数都有默认值，那么带默认值的参数必须声明在最后。

第1-19步：修改ComputeTrainingRate，使其为age包含一个默认实参，并修改调用语句，使其不为age传递实参。运行窗体并检查方法内age的值。重复操作，传递一个与默认值不同的age实参。

是时候练习了！做练习5-1。

## 内聚方法与可重用性

考虑你之前开发的ComputeTrainingRate方法：

```
private void ComputeTrainingRate(float restingRate, float age)
{
    float maximumRate, trainingRate;
    // Compute maximum heart rate:
    maximumRate = 220 - age;
    // Compute training heart rate
    trainingRate = 0.6F * (maximumRate - restingRate) + restingRate;
    // Display Training heart rate:
    MessageBox.Show("Your Training Heart Rate is: " + trainingRate.ToString("N0"));
}
```

上述方法计算训练心率并显示结果。这种组合了多项任务的方法可重用性不高。例如，另一个需要通过调用此方法来计算训练心率的程序，可能不希望结果在消息框中显示。

当每个方法执行单一、明确的任务（如计算训练心率），并将结果返回给调用程序，以便调用程序可以随意处理这些结果时，方法就具有更高的可重用性。这样的方法被称为内聚方法。

## 5.4 按引用传递参数

按引用传递参数允许被调用方法修改调用程序中的实参值。这使方法中计算出的结果可以被调用程序使用（或返回给调用程序）。

应注意，从被调用方法向调用方法返回值的另一种方式是使用不使用引用参数的值返回方法，这将在5.6节中讨论。使用值返回方法相比使用引用参数有一些优点，比如易于维护。然而，要从方法返回多个值，不能使用简单变量作为参数；需要使用更高级的选项，如类、结构体、元组或数组。类和数组将在后面的章节中讨论。

当变量按引用传递时，变量的内存位置（地址或引用）被传递给形参，这样实参和形参访问同一内存位置的数据，如下所示：

![](img/143bad48262566137acc9c41f668a88f_172_0.png)

因此，如果形参的值在方法内发生了改变，实际上就是改变了对应实参的值。

类似地，调用方法前赋给实参的值，在方法被调用时就成了形参的值。也就是说，实际上数据既可以从调用程序传递给被调用方法，也可以从被调用方法传递给调用程序。

让我们使用按引用传递，将计算出的训练心率从ComputeTrainingRate返回给调用程序，而不是在消息框中显示它。修改后的方法如图5-15所示。

应注意，5.6节稍后讨论的值返回方法是按引用传递参数的一种替代方案。

## 图5-15：按引用传递参数

```
38
39    private void ComputeTrainingRate(float restingRate, float age,
40                                    ref float trainingRate)
41    {
42        float maximumRate;
43        // Compute maximum heart rate:
44        maximumRate = 220 - age;
45        // Compute training heart rate
46        trainingRate = 0.6F * (maximumRate - restingRate) + restingRate;
47
48        // Training rate is not displayed; it is returned to the calling method
49    }
```

在第40行，关键字ref指定trainingRate是一个引用参数。注意，因为trainingRate被声明为参数，所以它从方法内的声明语句中移除了。此外，在消息框中显示训练心率的语句也被移除了。

