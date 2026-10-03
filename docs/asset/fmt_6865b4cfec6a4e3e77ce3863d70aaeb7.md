
# Sith 类实现

## 构造函数

```csharp
public Sith(Being being, string name)
    : this(name, being.Race, being.Midchloridians)
{}
```

## 方法实现

### 7. AddApprentice 方法

添加一个名为 `AddApprentice` 的 public 方法，带有一个引用传递的 `Jedi` 参数和一个名为 `name` 的 `string` 参数，该参数为 Sith 主提供的新学徒。`Jedi` 参数通过引用传递是因为你希望在方法末尾使用 `Jedi` 的默认值，以象征该 Jedi 不再存在，现在是新出生的 Sith 学徒。

```csharp
public Sith AddApprentice(ref Jedi jedi, string name)
{
    Apprentice = new Sith(jedi, name);
    Apprentice.Forces.AddRange(jedi.Forces);
    jedi = default(Jedi);
    return Apprentice;
}
```

### 8. CompleteTraining 方法

添加一个名为 `CompleteTraining` 的 public 方法，带有一个 `Sith` 参数。从学徒的 `Forces` 集合中移除所有光明面（`LightSide`）值。

```csharp
Apprentice.Forces.Remove(Force.LightSide);
```

### 9. AreYouSith 方法

重写继承的方法 `AreYouSith`。按照上述描述实现它。

## Sith 类完整代码

```csharp
public class Sith : Being
{
    private Sith Apprentice { get; set; }
    internal bool IsSithLord { get; return Apprentice != null; }
}
```

# C# 入门：Sith 类成员

## 构造函数

```csharp
public Sith(string name, Races race, int midchloridians = 0) :
    base(name, race, midchloridians)
{
    AddForce(Force.DarkSide);
}
```

```csharp
public Sith(Being being, string name)
    : this(name, being.Race, being.Midchloridians)
{}
```

## 方法

```csharp
public void CompleteTraining(Sith apprentice)
{
    Apprentice.Forces.Remove(Force.LightSide);
}
```

```csharp
public Sith AddApprentice(ref Jedi jedi, string name)
{
    Apprentice = new Sith(jedi, name);
    Apprentice.Forces.AddRange(jedi.Forces);
    jedi = default(Jedi);
    return Apprentice;
}
```

```csharp
public override string AreYouSith(Being suspect)
{
    if (this is Sith && suspect is Sith)
    {
        var sith = suspect as Sith;
        if (sith.IsSithLord)
            return "I'm a Sith Lord, and my apprentice is " + sith.Apprentice.Name;
        else
            return "I'm a Sith Apprentice and my name is " + sith.Name;
    }
    return "I don't know of any Sith";
}
```

# JediSith 程序集

这是显示角色信息的主应用程序。你需要添加对其他程序集的引用，以便访问必要的类和枚举。

## PrintBeing 方法

为了显示角色信息，你必须添加一个名为 `PrintBeing` 的方法，它接收一个 `Being` 数据类型的参数，包含要显示的字符。使用 `String.Format` 方法格式化一个包含名称、种族、原力值以及该角色拥有的力量（黑暗/光明）的输出字符串，并将其打印到控制台窗口。

### 实现步骤

1. 在 `Main` 方法下方的 `Program` 类添加一个名为 `PrintBeing` 的方法，该方法有一个 `Being` 类型的参数 `being`。

```csharp
private static void PrintBeing(Being being)
{}
```

2. 添加一个名为 `forces` 的字符串变量并赋值空字符串。

3. 遍历 `being.Forces` 集合中的力量，并将存储在 `forces` 变量中的数据拼接成一个字符串。

```csharp
foreach (var force in being.Forces)
    forces += String.Format("{0}, ", force);
```

4. 如果循环后 `forces` 字符串包含任何数据，则删除字符串的最后两个字符，以避免在字符串末尾显示逗号。

```csharp
if (!forces.Equals(String.Empty))
    forces = forces.Substring(0, forces.Length - 2);
```

5. 将所需数据单行写入控制台窗口。

### PrintBeing 完整代码

```csharp
private static void PrintBeing(Being being)
{
    string forces = String.Empty;
    foreach (var force in being.Forces)
        forces += String.Format("{0}, ", force);

    if (!forces.Equals(String.Empty))
        forces = forces.Substring(0, forces.Length - 2);
    
    Console.WriteLine(String.Format("Name: {0}, Race: {1}, Midchloridians: {2}, Forces: {3}", being.Name, being.Race, being.Midchloridians, forces));
}
```

## PrintQuestions 方法

`PrintQuestions` 方法应该有两个参数：一个 `Being` 类型的 `interrogator`，另一个 `List<Being>` 集合类型的 `suspects`。遍历 `suspects` 集合中的角色，显示询问者的名称、嫌疑人的名称以及调用 `interrogator` 实例的 `WhatAreYou` 方法的结果（将当前嫌疑人作为参数值），同时也显示询问者的名称、嫌疑人的名称以及调用 `interrogator` 实例的 `AreSith` 方法的结果（将当前嫌疑人作为参数值）。循环后向控制台添加一个空行。

### 实现步骤

- 在 `Main` 方法下方的 `Program` 中添加一个 `PrintQuestions` 方法，包含一个 `Being` 类型的参数 `interrogator` 和一个 `List<Being>` 集合类型的参数 `suspects`。

```csharp
private static void PrintQuestions(Being interrogator, List<Being> suspects) {
}
```

- 添加一个 `foreach` 循环遍历 `suspects` 集合中的内容。

- 为每个嫌疑人打印询问者的名称、嫌疑人的名称以及调用 `WhatAreYou` 方法的结果。

```csharp
Console.WriteLine(String.Format("{0} [WhatAreYou] {1}: {2}", interrogator.Name, suspect.Name, interrogator.WhatAreYou(suspect)));
```

- 现在按照上述描述的方式对 `AreSith` 方法执行相同的操作。

- 在循环后添加对 `Console.WriteLine` 方法的调用。

### PrintQuestions 完整代码

```csharp
private static void PrintQuestions(Being interrogator, List<Being> suspects) {
    foreach (var suspect in suspects) {
        Console.WriteLine(String.Format("{0} [WhatAreYou] {1}: {2}", interrogator.Name, suspect.Name, interrogator.WhatAreYou(suspect)));
        Console.WriteLine(String.Format("{0} [AreSith] {1}: {2}", interrogator.Name, suspect.Name, interrogator.AreSith(suspect)));
    }
    Console.WriteLine();
}
```

## Main 方法

这里是所有内容汇总并显示输出的地方。

### 实现步骤

1. 将角色添加到 `Main` 方法中。

```csharp
var jarJar = new Being("Jar Jar Binx", Races.Gungan, 0);
var palpatine = new Sith("Senator Palpatine", Races.Human, 10000);
var anakin = new Jedi("Anakin Skywalker", Races.Human, 50000);
var obiWan = new Jedi("Obi Wan Kenobi", Races.Human, 10000);
```

2. **输出 1**：调用 `PrintBeing` 方法并添加 `Console.ReadKey` 和 `Console.Clear` 方法的调用。

```csharp
PrintBeing(obiWan);
```

3. 通过调用 `obiWan` 实例变量的 `AddPadawan` 方法并传递 `anakin` 实例变量，将 `anakin` 作为学徒添加到 `Obi Wan Kenobi`。

```csharp
obiWan.AddPadawan(anakin);
```

4. **输出 2**：为每个角色调用 `PrintQuestions` 方法，将剩余的角色作为 `suspects` 集合的一部分传入。在 `PrintQuestions` 方法调用后添加 `Console.ReadKey` 和 `Console.Clear` 方法的调用。

```csharp
PrintQuestions(palpatine, new List<Being> { anakin, obiWan, jarJar });
```

5. 通过 `palpatine` 实例变量调用 `AddApprentice` 方法传递 `anakin` 实例以及名称 `"Darth Vader"`，并将结果存储在名为 `darthVader` 的变量中。

```csharp
var darthVader = palpatine.AddApprentice(ref anakin, "Darth Vader");
```

6. 调用 `PrintBeing` 方法传入 `darthVader` 实例。通过调用 `darthVader` 实例的 `CompleteTraining` 方法让 Vader 完成训练。

7. **输出 3**：调用 `PrintBeing` 方法传入 `darthVader` 实例，注意 Darth Vader 力量的变化。在 `PrintBeing` 方法调用后添加 `Console.ReadKey` 和 `Console.Clear` 方法的调用。

8. 通过调用 `obiWan` 实例变量的 `RemovePadawan` 方法将 `anakin` 从 `obiWan` 的学徒移除。

9. **输出 4**：调用 `PrintQuestions` 方法，让 Palpatine 询问 Darth Vader 和 Obi Wan，让 Darth Vader 询问 Palpatine 和 Obi Wan，让 Obi 询问 Darth Vader。

10. 添加对 `Console.ReadKey` 方法的调用。

### Main 方法完整代码

```csharp
static void Main(string[] args)
{
    var jarJar = new Being("Jar Jar Binx", Races.Gungan, 0);
    var palpatine = new Sith("Senator Palpatine", Races.Human, 10000);
    var anakin = new Jedi("Anakin Skywalker", Races.Human, 50000);
    var obiWan = new Jedi("Obi Wan Kenobi", Races.Human, 10000);

    #region Output 1
    PrintBeing(obiWan);
    PrintBeing(anakin);
    PrintBeing(palpatine);
    PrintBeing(jarJar);
    Console.ReadKey();
    Console.Clear();
    #endregion

    obiWan.AddPadawan(anakin);

    #region Output 2
    PrintQuestions(palpatine, new List<Being> { anakin, obiWan, jarJar });
    Console.ReadKey();
    Console.Clear();
    #endregion

    var darthVader = palpatine.AddApprentice(ref anakin, "Darth Vader");

    #region Output 3
    PrintBeing(darthVader);
    darthVader.CompleteTraining();
    PrintBeing(darthVader);
    Console.ReadKey();
    Console.Clear();
    #endregion

    obiWan.RemovePadawan();

    #region Output 4
    PrintQuestions(palpatine, new List<Being> { darthVader, obiWan });
    PrintQuestions(darthVader, new List<Being> { palpatine, obiWan });
    PrintQuestions(obiWan, new List<Being> { darthVader });
    Console.ReadKey();
    #endregion
}
```

# 程序运行输出示例

```text
Obi Wan Kenobi [AreYouSith] Anakin Skywalker: 我是一个学徒，我的名字叫安金·天行者。
Obi Wan Kenobi [WhatAreYou] Senator Palpatine: 我既不是西斯也不是绝地。
Obi Wan Kenobi [AreYouSith] Senator Palpatine: 我不知道任何西斯。
Obi Wan Kenobi [WhatAreYou] Jar Jar Binx: 我既不是西斯也不是绝地。
Obi Wan Kenobi [AreYouSith] Jar Jar Binx: 我不知道任何西斯。

Jar Jar Binx [WhatAreYou] Anakin Skywalker: 我是一个绝地武士。
Jar Jar Binx [AreYouSith] Anakin Skywalker: 我不是西斯。
Jar Jar Binx [WhatAreYou] Obi Wan Kenobi: 我是一个绝地武士。
Jar Jar Binx [AreYouSith] Obi Wan Kenobi: 我不是西斯。
Jar Jar Binx [WhatAreYou] Senator Palpatine: 我既不是西斯也不是绝地。
Jar Jar Binx [AreYouSith] Senator Palpatine: 我不知道任何西斯。
```
