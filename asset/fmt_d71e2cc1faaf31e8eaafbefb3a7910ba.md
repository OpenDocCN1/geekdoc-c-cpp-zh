
下面的图像显示了显示树的步骤。注意整数现在按升序排列的。

使用集合和构建泛型

12-75

![](img/3ef84844c6ac82b838cfffa6448b2346_248_0.png)

输出: -2

输出: -2, 1

输出: -2, 1, 1

输出: -2, 1, 1, 5

输出: -2, 1, 1, 5, 6

## 练习 1：定义泛型接口

在此练习中，你将为一个名为 `IBinaryTree` 的泛型二叉树定义接口。该接口将指定以下方法：

- `Add`。此方法向树中添加一个项目。
- `Remove`。此方法从树中删除具有指定值的第一个项目。
- `WalkTree`。此方法将按排序顺序显示树的内容。

该练习的主要任务如下：

1. 打开 `GenericTypes` 解决方案。
2. 定义泛型 `IBinaryTree` 接口。

### 任务 1：打开 GenericTypes 解决方案

1. 以 Student 身份使用密码 `PaSSword` 登录 `10266A-GEN-DEV` 虚拟机。
2. 打开 Visual Studio 2010。
3. 从 `E:\Labfiles\Lab 12\Lab 12\Snippets` 文件夹导入代码段。
4. 打开位于 `E:\Labfiles\Lab 12\Lab\Ex1\Starter` 文件夹中的 `GenericTypes` 解决方案。

### 任务 2：定义 IBinaryTree 接口

1. 检查任务列表。
2. 在任务列表中，找到 `TODO – Define the IBinaryTree interface` 任务，然后双击该任务。该任务位于 `IBinaryTree.cs` 文件中。
3. 在 `BinaryTree` 命名空间中，定义一个名为 `IBinaryTree` 的新泛型接口。该接口应接受一个名为 `TItem` 的类型参数。指定该类型参数必须实现泛型 `IComparable` 接口。
4. 在 `IBinaryTree` 接口中，定义以下公共方法：
   a. 一个 `Add` 方法，接受 `TItem` 作为参数且没有返回值。
   b. 一个 `Remove` 方法，接受 `TItem` 作为参数。
   c. `WalkTree` 方法，不接受参数也没有返回值。
5. 构建 `IBinaryTree` 接口。

## 练习 2：实现泛型接口

在此练习中，你将创建一个名为 `Tree` 的泛型二叉树并实现 `IBinaryTree` 接口。任务如下：

1. 打开 `GenericTypes` 解决方案。
2. 创建 `Tree` 类。

使用集合和构建泛型

12-77

### 任务 1：打开 GenericTypes 解决方案

> **注意**：如果你尚未完成此任务，请直接进入任务 2。

### 任务 2：创建 Tree 类

1. 在 `BinaryTree` 命名空间中，定义一个名为 `Tree` 的新泛型类。该类实现 `IBinaryTree` 接口。类型参数 `TItem` 必须实现 `IComparable` 接口。
2. 为 `Tree` 添加以下自动属性：
   a. `Data`
   b. `LeftTree`
   c. `RightTree`
3. 为 `Tree` 添加一个公共构造函数。构造函数接受一个名为 `newValue` 的 `TItem` 参数并初始化 `Data`，并将 `LeftTree` 和 `RightTree` 设置为 `null`。
4. 在构造函数之后，定义一个名为 `Add` 的方法。该方法接受一个名为 `newItem` 的 `TItem` 参数且没有返回值。
5. 在 `Add` 方法中，添加代码通过以下任务将 `newItem` 对象插入适当的位置：
   a. 将 `newItem` 对象与 `Data` 属性进行比较。`CompareTo` 方法在项目相同时返回零，如果 `Data` 大于 `newItem` 返回正值，如果 `Data` 小于 `newItem` 则返回负值。
   b. 如果 `newItem` 的值小于 `Data`，执行以下操作将 `newItem` 对象插入左子树：
      - 如果 `LeftTree` 为空，初始化它并将 `newItem` 传递构造函数。
      - 如果 `LeftTree` 不为空，递归调用 `LeftTree` 的 `Add` 方法并将 `newItem` 作为参数。
   c. 如果 `newItem` 的值大于或等于 `Data`，执行以下操作将 `newItem` 对象插入右子树：
      - 如果 `RightTree` 为空，初始化它并将 `newItem` 传递构造函数。
      - 如果 `RightTree` 不为空，递归调用 `RightTree` 的 `Add` 方法并将 `newItem` 作为参数。
6. 在 `Add` 方法之后，添加另一个名为 `WalkTree` 的公共方法，它不接受任何参数也没有返回值。
7. 在 `WalkTree` 方法中，通过以下任务添加按顺序访问树中的每个节点并显示每个节点保存的值：
   a. 如果 `LeftTree` 不为空，递归调用 `LeftTree` 的 `WalkTree` 方法。
   b. 使用 `Console.WriteLine` 语句将 `Data` 属性的值显示到控制台。
   c. 如果 `RightTree` 不为空，递归调用 `RightTree` 的 `WalkTree` 方法。
8. 在 `WalkTree` 方法之后，添加 `Remove` 方法从树中删除值，如下示例所示。你不需要完全理解此方法的工作原理，你可以手动输入此代码或使用 `Mod12Remove` 代码段：

```csharp
public void Remove(TItem itemToRemove)
{
    // 不能删除 null。
    if (itemToRemove == null)
    {
        return;
    }
}
```

```cs
// 检查项目是否在左树中。
if (this.NodeData.CompareTo(itemToRemove) > 0
&& this.LeftTree != null)
{
    // 检查左树 - 无法移除
    // 检查树向下 2 层
    // 'this'，仅限 LeftTree 或 RightTree 属性。
    if (this.NodeData.CompareTo(itemToRemove) == 0)
    {
        // LeftTree 属性没有子节点 -将
        // LeftTree 属性置为 null。
        if (this.LeftTree == null
        && this.LeftTree.RightTree == null)
        {
            this.LeftTree = null;
        }
        else // 移除 LeftTree。
            RemoveNodeWithChildren(this.LeftTree);
    }
}
else
{
    // 继续查找 - 递归调用 Remove 方法
    this.LeftTree.Remove(itemToRemove);
}

// 检查项目是否在右树中。
if (this.NodeData.CompareTo(itemToRemove) < 0
&& this.RightTree != null)
{
    // 检查右树。
    // 检查树向下 2 层
    // 'this'，仅限 LeftTree 或 RightTree 属性。
    if (this.NodeData.CompareTo(itemToRemove) == 0)
    {
        // RightTree 属性没有子节点 -将
        // RightTree 属性置为 null。
        if (this.RightTree.LeftTree == null
        && this.RightTree.RightTree == null)
        {
            this.RightTree = null;
        }
    }
    else // 移除 RightTree。
        RemoveNodeWithChildren(this.RightTree);
}
}
```

## 使用 Microsoft® Visual Studio® 2010 进行 C# 

```cs
} else {
    // 继续查找 - 递归调用 Remove 方法；
    this.RightTree.Remove(itemToRemove);
}

// 这仅适用于根节点。
if (this.NodeData.CompareTo(itemToRemove) == 0)
{
    // 没有子节点 - 什么都不做，树必须至少包含
    // 一个节点。
    if (this.LeftTree == null && this.RightTree == null)
    {
        return;
    }
    else // 根节点有节点。
    {
        RemoveNodeWithChildren(this);
    }
}
```

在 `Remove` 方法之后，添加 `RemoveNodeWithChildren` 方法来从树中删除包含子节点的节点，如下代码示例所示。此方法由 `Remove` 方法调用。再次，你不需要理解这段代码的工作原理，因此你可以手动输入此代码，或使用 `Mod12RemoveNodeWithChildren` 代码段。

```cs
private void RemoveNodeWithChildren(Tree<TItem> node)
{
    // 检查节点是否具有子节点。
    if (node.LeftTree == null && node.RightTree == null)
    {
        throw new ArgumentException("Node has no children");
    }

    // 树只有一个子节点 - 用其子节点
    // 替换树节点。
    if (node.LeftTree == null ^ node.RightTree == null)
    {
        if (node.LeftTree == null)
        {
            node.CopyNodeToThis(node.RightTree);
        }
        else
        {
            node.CopyNodeToThis(node.LeftTree);
        }
    }
    else
    {
        // 树节点有两个子节点 - 用其“中序后继”节点的值
        // 替换树节点的值并移除
        // 中序后继节点。
        {
            // 寻找中序后继 - 即其 RightTree
            // 最左的后代。
            Tree<TItem> successor = GetLeftDescendant(node.RightTree);

            // 从中序后继拷贝节点值。
            node.NodeData = successor.NodeData;

            // 移除中序后继节点。
            if (node.RightTree.RightTree == null &&
              node.RightTree.LeftTree == null) // 后继节点没有
                // 子节点。
            {
            }
            else
            {
                node.RightTree.Remove(successor.NodeData);
            }
        }
    }
}
```

1. 在 `RemoveNodeWithChildren` 方法之后，添加 `CopyNodeToThis` 方法，用于将另一个节点的属性拷贝到当前节点。`RemoveNodeWithChildren` 方法调用此方法。你可以手动拷贝此类型，或使用 `Mod12CopyNodeToThis` 代码段。

```cs
private void CopyNodeToThis(Tree<TItem> node) {
  this.NodeData = node.NodeData;
  this.LeftTree = node.LeftTree;
  this.RightTree = node.RightTree;
}
```

2. 在 `CopyNodeToThis` 方法之后，添加 `GetLeftDescendant` 方法，如下代码所示。`RemoveNodeWithChildren` 方法也调用此方法来获取树节点的最左侧后代。你可以手动输入此代码或使用 `Mod12GetLeftDescendant` 代码段。

```cs
private Tree<TItem> GetLeftDescendant(Tree<TItem> node)
{
    while (node.LeftTree != null)
    {
        node = node.LeftTree;
    }
    return node;
}
```

3. 解决方案并修正任何错误。

## 练习 3：为 BinaryTree 实现测试程序

在此练习中，你将修改测试程序以使用 BinaryTree。该练习的主要任务如下：

- 1. 打开 `GenericTypes` 解决方案。
- 2. 导入 `TestHarness` 项目。
- 3. 完成测试程序。
- 4. 测试 `BinaryTree` 项目。

### 任务 1：打开 GenericTypes 解决方案

> **注意**：如果你还没有完成练习 2，请执行此任务。如果你已成功定义 `BinaryTree` 接口并构建了 `Tree` 类，请直接跳转到任务 3：完成测试程序。

- 打开 `E:\Labfiles\Lab 12\Lab B\Ex3\Starter` 中的 `GenericTypes` 解决方案。

### 任务 2：导入 TestHarness 项目

> **注意**：只有在你成功完成练习 2 后，才执行此任务。

1. 将 `E:\Labfiles\Lab 12\Lab B\Ex3\TestHarness` 文件夹中的 `TestHarness` 项目导入 `GenericTypes` 解决方案。
2. 在 `TestHarness` 项目中，更新对 `BinaryTree` 项目的引用。
3. 将 `TestHarness` 项目设为启动项目。

### 任务 3：完成测试程序

1. 打开 `Program.cs` 文件。
2. 在 `Main` 方法中，添加代码来实例化名为 `tree` 的新 `BinaryTree` 对象，使用 `int` 作为类型。通过值 `5` 初始化新的 `Tree` 对象。
3. 在 `Main` 方法中，向树添加以下值：
   a. `1`
   b. `4`
   c. `7`
   d. `3`
   e. `4`
4. 在 `Main` 方法中，执行以下操作：
   a. 向控制台打印“Current Tree:”并调用树的 `WalkTree` 方法。
   b. 向控制台打印“Add 15”，向树中添加 `15`。
   c. 向控制台打印“Current Tree:”并调用树的 `WalkTree` 方法。
   d. 向控制台打印“Remove 5”，从树中移除 `5`。
   e. 向控制台打印“Current Tree:”并调用树的 `WalkTree` 方法。
5. 解决方案并修正任何错误。

### 任务 4：测试 BinaryTree 项目

1. 运行应用程序。
2. 验证控制台中的输出类似于以下。注意二叉树中的数据是排序的。

```
Current Tree:
1
3
4
7

Add 15

Current Tree:
1
3
4
7
15

Remove 5

Current Tree:
1
3
4
7
```
