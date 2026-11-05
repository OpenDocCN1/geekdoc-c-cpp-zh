
- 1. 在项目对话框中，我们首先需要为我们的类提供一个名称。让我们为我们的类提供名称 Tutorial.cs 为我们的类。请注意，文件名应以 .cs 结尾，以确保它被视为一个正确的类文件。
- 2. 当我们点击“添加”按钮时，该类将被添加到我们的解决方案中。

如果按照上述步骤操作，您将在 Visual Studio 中得到以下输出。

## Output

![](img/8115a2172ef67838d7fe1933fc517c4d_44_0.png)

类名 Tutorial.cs 将被添加到解决方案中。如果打开该文件，您会发现以下代码已添加到类文件中。

![](img/8115a2172ef67838d7fe1933fc517c4d_44_1.png)

## Code Explanation

- 1. 第 1 部分包含 Visual Studio 添加到任何 .Net 文件的强制性模块。这些模块始终是必需的，以确保任何 .Net 程序在 Windows 环境中运行。
- 2. 第 2 部分是添加到文件中的类。在我们的例子中，类名是‘Tutorial’。这是添加类到解决方案时指定的名称。

目前，我们的类文件没有任何作用。在以下主题中，我们将更详细地了解如何使用该类。

## Fields and methods

我们已经在之前的主题中了解了如何在类中定义字段和方法。

对于我们的 Tutorial 类，我们可以具有以下属性。

- 1. Tutorial ID – 这将用于存储代表教程的唯一数字。
- 2. Tutorial Name – 这将用于将教程名称存储为字符串。

我们的 Tutorial 类也可以具有下面提到的以下方法。

- 1. SetTutorial – 此方法将用于设置教程的 ID 和名称。
- 2. GetTutorial – 此方法将用于获取特定教程的详细信息。

现在让我们看看如何在代码中加入字段和方法。

**Step 1)** 第一步是确保 Tutorial 类具有正确的字段和方法定义。在此步骤中，我们将以下代码添加到 Tutorial.cs 文件中。

![](img/8115a2172ef67838d7fe1933fc517c4d_46_0.png)

### Code Explanation

- 1. 第一步是将 TutorialID 和 TutorialName 字段添加到类文件中。由于 TutorialID 字段将是一个数字，我们将其定义为 Integer，而 TutorialName 将定义为 string。
- 2. 接下来，我们定义 SetTutorial 方法。此方法接受 2 个参数。因此，如果 Program.cs 调用 SetTutorial 方法，则需要为这些参数提供值。这些值将用于设置 Tutorial 对象的字段。
  
  **Note:** 让我们举一个例子并假设我们的 Program.cs 文件使用参数“1”和“.Net”调用 SetTutorial。由此将执行以下步骤：
  
  - a. pID 的值将变为 1。
  - b. pName 的值将为 .Net。
  - c. 在 SetTutorial 方法中，这些值随后将被传递给 TutorialID 和 TutorialName。
  - d. 因此现在 TutorialID 的值将为 1，TutorialName 的值将为“.Net”。
- 3. 在这里我们将 Tutorial 类的字段相应地设置为参数。因此我们将 TutorialID 设置为 pID，将 TutorialName 设置为 pName。
- 4. 然后我们定义 GetTutorial 方法以返回类型为“String”的值。此方法将用于将 TutorialName 返回给调用程序。同样，您也可以使用方法 `int GetTutorial` 获取教程 ID。
- 5. 在这里我们将 TutorialName 字段的值返回给调用程序。

**Step 2)** 现在让我们向 Program.cs 添加代码，这是我们的控制台应用程序。

控制台应用程序将用于创建“Tutorial class”的对象并相应地调用 SetTutorial 和 GetTutorial 方法。

(**Note:** 对象是任何给定时间类的一个实例。类与对象之间的区别在于对象实际上包含属性的值。)

```csharp
static void Main(string[] args)
{
    Tutorial pTutor = new Tutorial();
    pTutor.SetTutorial(1, ".Net");
    Console.WriteLine(pTutor.GetTutorial());
    Console.ReadKey();
}
```

### Code Explanation

- 1. 第一步是为 Tutorial 类创建对象。请注意，这是通过使用关键字‘new’完成的。‘new’关键字用于在 C# 中从类创建对象。然后对象被分配给 pTutor 变量。
- 2. 然后调用 SetTutorial 方法。参数 1 和“.Net”被传递给 SetTutorial 方法。然后这些参数将用于相应地设置类的“TutorialID”和“TutorialName”字段。
- 3. 然后我们使用 Tutorial 类的 GetTutorial 方法获取 TutorialName。然后通过 Console.WriteLine 方法将其显示到控制台。

如果正确输入上述代码并运行程序，将显示以下输出。

## Output

![](img/8115a2172ef67838d7fe1933fc517c4d_48_0.png)

从输出中，您可以清楚地看到字符串“.Net”是由 GetTutorial 方法返回的。

## Access Modifiers

访问修饰符用于定义类属性或方法的可见性。有时您可能不希望其他程序看到类的属性或方法。在这种情况下，C# 提供了在类属性和方法上放置修饰符的能力。类修饰符能够限制访问，以使其他程序无法看到类的属性或方法。

通常有 3 种类型的访问修饰符。它们在下面进行解释。

- 1. **Private** – 当此访问修饰符附加到属性或方法时，表示这些成员无法从任何外部程序访问。
  
  让我们举一个例子，看看使用 private 访问修饰符时会发生什么。
  
  让我们修改 Tutorial.cs 文件中的当前代码。在 SetTutorial 方法中，让我们将 public 关键字更改为 private。
  
  ![](img/8115a2172ef67838d7fe1933fc517c4d_49_0.png)
  
  现在让我们切换到 Program.cs 文件。您会注意到 SetTutorial 方法下方有一条红色波浪线。
  
  由于我们现在已在 Tutorial 类中将 SetTutorial 方法声明为 private，Visual Studio 已检测到这一点。它通过突出显示告诉用户，现在此方法将无法从 Program.cs 文件中使用。
  
  ```csharp
  {
      static void Main(string[] args)
      {
          Tutorial pTutor = new Tutorial();
          pTutor.SetTutorial(1, ".Net");
          Console.WriteLine(pTutor.GetTutorial());
          Console.ReadKey();
      }
  }
  ```
- 2. **Public** – 当此访问修饰符附加到属性或方法时，表示这些成员可以从任何外部程序访问。我们在之前的示例中已经看到过这一点。
  
  ```csharp
  int TutorialID;
  string TutorialName;
  
  public void SetTutorial(int pID , String pName) {
      TutorialID=pID;
      TutorialName=pName;
  }
  public String GetTutorial()
  {
  ```
  
  由于我们在 Tutorial 类中将方法定义为 public，因此它们可以从 Program.cs 文件中访问。
- 3. **Protected** – 当此访问修饰符附加到属性或方法时，表示这些成员只能由从当前类继承的类访问。这将在继承类中更详细地解释。

## C# Constructor

构造函数用于在创建相应对象时初始化类字段的值。构造函数是一个与类同名的方法。如果在类中定义了构造函数，那么它将在创建对象时被调用的第一个方法。假设我们有一个名为 Employee 的类。构造函数方法也将命名为 Employee()。

关于构造函数方法需要注意以下关键事项：

- 1. 构造函数的访问修饰符需要设为 public。
- 2. 构造函数方法不应有返回类型。

现在让我们看看如何在代码中加入构造函数的用法。我们将使用构造函数在创建对象时将 TutorialID 和 TutorialName 字段初始化为一些默认值。

**Step 1)** 第一步是为我们的 Tutorial 类创建构造函数。在此步骤中，我们将以下代码添加到 Tutorial.cs 文件中。

```csharp
namespace DemoApplication
{
    public class Tutorial
    {
        int TutorialID;
        string TutorialName;
        public Tutorial() {
            TutorialID = 0;
            TutorialName = "Default";
        }
        public void SetTutorial(int pID , String pName) {
            TutorialID=pID;
            TutorialName=pName;
        }
    }
}
```

### Code Explanation

- 1. 我们首先添加一个与类同名的新方法。因为它与类同名，所以 C# 将其视为构造函数方法。因此，现在每当调用方法创建此类的对象时，此方法将默认被调用。
