

## 第 8 章：Objective-C 编程基础

# 195

![](img/322e107ddf8f5cd963a6efafdcd86f38_202_0.png)

列表 8–21。点击时选择书籍。

```
146      (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath { * (NSIndexPath **)indexPath
147      {
148          Book *selectedBook = [self.myBookStore bookAtIndex:indexPath.row];

150          if (!self.detailViewController) {
151              self.detailViewController = [[DetailViewController alloc]
152                                            initWithNibName:"DetailViewController"
153                                            bundle:nil];
154                                         }
155          self.detailViewController.detailItem = selectedBook;
156          [self.navigationController pushViewController:self.detailViewController
157                                            animated:YES];
158}
```

如果第 #148 行看起来与列表 8–20中的第 #104 行非常相似，那它们基本上是同一个东西。根据 `indexPath.row`，我们从 `Bookstore` 对象中选择了特定的书籍，并将其保存到名为 `selectedBook` 的变量中。

在第 #155 行，我们将 `selectedBook` 存储到属性 `detailItem` 中，该属性已经是 `DetailViewController` 类的一部分。这就是我们在 `MasterViewController` 中需要做的所有工作。我们基本上将书籍传递给了 `DetailViewController`。我们快完成了。现在，我们需要对 `DetailViewController` 进行一些小修改，使其能够正确显示 `Book`。

### 修改 DetailViewController

在本章的开头，我们修改了 `DetailViewController` 以显示有关书籍的某些详细信息。在刚刚完成的代码中，我们修改了 `MasterViewController`，将选定的书籍传递给 `DetailViewController`。现在剩下的是将信息从 `DetailViewController` 中的 `Book` 对象移动到屏幕上相应的字段上。这一切都在一个方法中完成——`configureView`。

列表 8-22。将 `Book` 对象数据移动到你的详情视图。

```
33  (void)configureView
34  {
35      // 更新详细项的用户界面。
36 
37      if (self.detailItem) {
38          Book *theBook = (Book *)self.detailItem;
39          self.titleLabel.text = theBook.title;
40          self.authorLabel.text = theBook.author;
41          self.descriptionTextView.text = theBook.description;
42      }
43 }
```

`configureView` 方法是 Xcode 模板包含的许多便利方法之一，每当 `DetailViewController` 初始化时就会调用。这就是我们将选定的 `Book` 对象的信息移动到视图字段的地方。

DetailViewController.m 文件中的第 #38–41 行是将信息从对象移动到对象的地方。如果你还记得，列表 8–21 中的第 #155 行将选定的书籍设置为 `DetailViewController` 中名为 `detailItem` 的属性。第 #38 行将该项提取出来一个名为 `theBook` 的 `Book` 对象。

第 #39–41 行只需将 `Book` 对象的每个属性移动到我们在章节早些时候构建的视图控件中。这就是我们在这个类中需要做的所有。如果你构建并运行项目并点击其中一本书，你应该能看到类似图 8–16 的内容。

不要忘记如列表 8–23 的第 #10 行所示导入 "Book.h" 文件。

列表 8-23。导入 Book.h 头文件。

```
1  //
2  // DetailViewController.m
3  // MyBookstore
4  //
5  // Created by M.R. Fisher on 8/28/11.
6  // Copyright (c) 2011 www.committed-code.com. All rights reserved.
7  //
```

8

9 #import "DetailViewController.h"

10 #import "Book.h"

![](img/322e107ddf8f5cd963a6efafdcd86f38_204_0.png)

图 8–16。查看详情。

### 总结

我们终于到达这一章的结尾！以下是我们涵盖内容的总结：

- 理解集合（Collection）：集合类非常强大。
 使用 使用实例变量（instance variables）：实例变量用于存储信息。
- 使用属性（properties）：属性允许获取器（getter）和设置器（setter）。
- 使用 for... 循环：这允许我们遍历列表。
- 构建主-详情界面（Master-Detail）：我们使用了主-详情界面。
- 使用简单数据：我们使用了事实上的显示信息。

### 练习题

- 修改 `DetailViewController` 以显示（...）。
- 在 `Bookstore` 中添加一个属性。
- 修改 `DetailViewController` 以便（...）。
- 使用接口的属性。
- 排序视图中的数据。
- 比较变量的类型。

## 第 9 章：数字比较

### 回顾布尔逻辑（Boolean Logic）

在之前的之前的章节中，我们引入了布尔逻辑。由于其普及性，我们将详细复习这个主题。布尔逻辑通常以 `if` 语句的形式出现。这里有一些布尔问题的很好的例子：

- 5 比 3 大吗？
- "now" 的字母更多吗？
- 6 比今天晚吗？

注意，只有 2 种可能的答案：是（yes）和否（no）。如果你问的问题可能有超过 2 个答案，它的表述方式会有不同。每个 `if` 语句都需要一个关系运算符。例如，如果 5 大于 3，则打印一条消息。

为了在程序中使用这类问题，你首先需要熟悉 Objective-C 中可用的关系运算符。之后，我们将查看不同变量如何表现。

### 使用关系运算符

Objective-C 使用 6 个关系运算符。这些是标准的代数运算符，只有一个变化：在 Objective-C 语言中，与大多数其他编程语言一样，相等运算符由两个等号 (=）组成。在第 4 章表 4-7 中，我们描述了不同的运算符。

> 注意：单个等号 (=) 用于给变量赋值。双等号 (==) 用于比较两个值。例如 `if(x=9)` 将 9 赋值给变量，如果 9 成功赋值给 x，则返回“是”，这在大多数甚至所有情况下都是如此。`if(x==9)` 则将实际比较检查 x 是否等于 9。

### 比较数字

开发者过去面临的困难之一是在比较中处理不同的数据类型。在本书的早些时候，我们讨论了不同变量的类型。你可能记得 1 是一个整数。如果你想将整数与浮点数如 1.2 进行比较，这可能会产生问题。坦率地说，Objective-C 帮助我们解决了这个问题。

