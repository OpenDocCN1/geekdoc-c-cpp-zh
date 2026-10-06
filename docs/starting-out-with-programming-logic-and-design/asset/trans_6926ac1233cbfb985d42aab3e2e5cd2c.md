

# 图 11-6 程序 11-4 中其他模块的流程图（续）

![](img/c939132f78787c7f339c6977b3fc8c85_471_0.png)

## 11.3 使用循环重复显示菜单

**概念：** 大多数菜单驱动型程序使用循环，在执行完选定的任务后重复显示菜单。

你在本章中目前看到的程序在执行完从菜单中选择的操作后会立即结束。如果用户想从菜单中选择另一个操作，他们必须重新运行程序。为了执行多次操作而反复运行程序对用户来说可能不方便，因此大多数菜单驱动型程序使用循环，在执行完用户选定的操作后重新显示菜单。当用户准备结束程序时，他们从菜单中选择如“结束程序”之类的操作。

程序 11-5 是程序 11-4 的修改版本。它展示了我们如何在主模块中使用 `Do-While` 循环反复显示菜单，直到用户准备结束程序。选择项目 4（“结束程序”）会导致循环停止并结束程序。图 11-7 显示了主模块的流程图。

## 程序 11-5

```pascal
Module main()
  // 定义一个变量来存储
  // 用户的菜单选择。
  Integer menuSelection

  Do
    // 显示菜单并获取
    // 用户的选择。
    Call displayMenu(menuSelection)

    // 执行选择的操作。
    Select menuSelection
    Case 1:
      Call inchesToCentimeters()
    Case 2:
      Call feetToMeters()
    Case 3:
      Call milesToKilometers()
    End Select
  While menuSelection != 4
End Module

// displayModule 显示菜单并
  // 提示用户进行选择。选定的
  // 值存储在选择参数中，该参数//是通过引用传递的。
Module displayMenu(Integer ref selection)
  // 显示菜单。
  Display "1. 将英寸转换为厘米。"
  Display "2. 将英尺转换为米。"
  Display "3. 将英里转换为公里。"
  Display "4. 结束程序。"
  Display

  // 提示用户进行选择。
  Display "输入您的选择。"
  Input selection

  // 验证菜单选择。
  While selection < 1 OR selection > 4
    Display "该选择无效。"
    Display "请输入 1, 2, 3 或 4。"
    Input selection
  End While
End Module
```

```pascal
// inchesToCentimeters 模块将测量
// 从英寸转换为厘米。
Module inchesToCentimeters()
// 局部变量
Declare Real inches, centimeters

// 获取英寸数。
Display "输入英寸数。"
Input inches

// 将英寸转换为厘米。
Set centimeters = inches * 2.54

// 显示结果。
Display "等于 "
```

# 第 11 章 菜单驱动型程序

```
103 // 显示结果。
104 Display "等于 " , kilometers,
105     " 公里。"
106
107 // 显示空行。
108 Display
109 End Module
```

## 程序输出（输入部分用粗体显示）

- 1. 将英寸转换为厘米。
- 2. 将英尺转换为米。
- 3. 将英里转换为公里。
- 4. 结束程序。

输入您的选择。
1 [Enter]
输入英寸数。
10 [Enter]
等于 25.4 英寸。

- 1. 将英寸转换为厘米。
- 2. 将英尺转换为米。
- 3. 将英里转换为公里。
- 4. 结束程序。

输入您的选择。
2 [Enter]
输入英尺数。
10 [Enter]
等于 3.048 米。

- 1. 将英寸转换为厘米。
- 2. 将英尺转换为米。
- 3. 将英里转换为公里。
- 4. 结束程序。

输入您的选择。
4 [Enter]

> 提示：程序 11-5 选择了 `Do-While` 循环是因为因为它后测试循环，它至少会显示一次菜单。可以使用 `While` 循环，但请记住，`While` 循环是预测试循环。使用它需要将 `menuSelection` 变量初始化为除 4 以外的某个值。

## 图 11-7 程序 11-5 中主模块的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_475_0.png)

## 焦点关注：设计菜单驱动型程序

在第 10 章的几个*焦点关注*章节中，我们详细介绍了为 Midnight Coffee Roasters, Inc. 设计的一系列程序。这些程序用于管理公司的咖啡库存。库存中的每种咖啡在文件中都有相应的记录。每条记录都包含指示咖啡名称和库存数量的字段。

（注意：OCR 源文件中的剩余文本包含大量重复和碎片化逻辑，已过滤掉以保持可读性。）

