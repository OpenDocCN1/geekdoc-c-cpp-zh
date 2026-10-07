

## 使用 Visual C#.NET 进行数据选择查询

![](img/d59a47501d0a20fc0460a49c469c6fb7_235_0.png)

图 5.39 TableAdapter 配置向导的结果。

在我们开始编码之前，需要将数据绑定到登录表（Login form）上的控件，以设置表单上每个控件与数据源上每个数据列之间的连接。

## 5.6 将数据绑定到登录表单中的关联控件

打开解决方案资源管理器（Solution explorer）窗口并从中选择登录表（Login Form），然后点击查看设计器（View Designer）打开其 GUI 界面。现在我们想要使用 `BindingSource` 将登录表单中的控件（特别是用户名和密码文本框）绑定到数据源中 Login 表的关联数据字段。

点击用户名（User Name）文本框，然后进入窗口顶部部分的 `DataBindings` 属性。展开该属性以显示各个项目，然后选择 `Text` 项。点击下拉列表展开以下项目：

- 其他数据源（Other Data Sources）
- 项目数据源（Project Data Sources）
    - CSE DEPTDDataSet
    - LogIn
    - user_name

展开结果如图 5.40 所示。

## 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_236_0.png)

**图 5.40** `DataBindings` 属性。

我们通过点击选择 **user_name** 列。通过这种方式，我们完成了数据绑定，并建立了登录表单上的 **User Name**（用户名）文本框与 LogIn 数据中 **user_name** 列之间的连接。

完成此绑定后，你会发现三个对象：**cse_DEPTDataSet**、**logBindingSource** 和 **logTableAdapter** 已添加到项目中，并显示在窗口底部。

好了，这容易吗？是的的。对 **Pass Word**（密码）文本框执行类似的操作，以将其绑定到 LogIn 数据中的 **pass_word** 列。但你你需要注意的一点是：当我们对 **User Name** 文本框进行数据绑定时，没有可用的预建或默认 **BindingSource** 对象，因为我们还没有执行任何数据绑定，而且 **User Name** 是你想要绑定的第一个控件。然而，在你完成第一次绑定后，一个新的 **BindingSource** 对象 **logBindingSource** 就被创建了。你需要使用这个 **BindingSource** 对象来处理登录表单上所有控件的所有其他数据绑定。

> 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。

现在让我们为 **Pass Word** 文本框执行数据绑定。

点击该 **Pass Word** 文本框以选择它，然后转到属性窗口展开 `DataBindings` 属性，选择 `Text` 项并点击下拉列表。你会发现显示了一个新的 `BindingSource` 对象 **logBindingSource**（图 5.41）。展开这个新对象，并通过点击它选择 Log 表中的 **pass_word** 列。**Pass Word** 文本框的数据绑定完成了。

一些读者可能已经注意到，当我们构建 **FillUsernamePassword** 方法时，使用了 Login 表中的四列——user_name、pass、faculty 和 student_id。事实上，我们只填充了表单上的两个文本控件 **txtName** 和 **txtPassword**，对应于 Login 表中的两个关联列：**user_name** 和 **pass**。因为我们只需要知道如何从 Login 中找到用户输入的匹配的用户名和密码。如果两者

## 使用 Visual C#.NET 进行数据选择查询

![](img/d59a47501d0a20fc0460a49c469c6fb7_237_0.png)

**图 5.41** 新的 BindingSource 对象。

可以从 LogIn 表中找到匹配的项，这意味着登录成功，我们可以继续进行下一步。表单上的两个绑定控件 **txtUserName** 和 **txtPassword** 将被填充存储在 Login 表中的相同值。这看起来似乎不合逻辑。事实上，我们并不想从 Login 表中检索任何列；相反，我们只想从 LogIn 表中找到用户名和密码的匹配条目。如果我们能找到匹配的用户名和密码，我们就不在乎 *faculty_id* 和 *student_id*。如果找不到匹配的项，这意味着登录失败，应该显示一条警告消息。

![](img/d59a47501d0a20fc0460a49c469c6fb7_237_1.png)

为了检查用户从数据源输入的用户名和密码，可以为 Login 返回一个*数据单值查询（Single Value Query for Data）*。但在这里，为了简化此检查，我们使用 `Fill()` 方法来填充 DataSet 中映射数据表中的四列。然后我们可以检查此 `Fill` 是否成功。如果是，则找到了匹配的数据项。否则，则未找到匹配的项。

在我们继续编码之前，我们需要指出文本框控件 **txtPassword** 中的密码。通常，我们需要设置 **txtPassword** 的 `PasswordChar`。

- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。
- 当你执行第一次数据绑定时，没有可用的 BindingSource 对象，因为你还没有执行任何绑定。你可以浏览到所需的数据列并选择它以完成此绑定。或者，会创建一个新的 BindingSource 对象，随后的所有数据绑定都应该使用我们创建的 BindingSource 来执行所有数据绑定。

## 5.7 使用 Fill() 方法开发查询

从解决方案资源管理器选择 Login.cs 并点击查看设计器打开其图形界面。双击登录按钮打开其 Click 方法。

首先我们需要移除 Login_Load() 方法内部的内容，因为该方法执行 Fill() 来填充我们 DataSet 中的整个表，但我们不需要这个函数。因此，高亮整个主体（不包含括号），右键点击此部分并选择剪切项以移除这些代码。然后我们需要创建一个本地对象 self，它是 SelectionForm 的实例，并将图 5.42 所示的代码放入此处。

让我们来看看这段代码，看看它是如何工作的。

一个新的命名空间是由 Visual C# 创建的，命名空间的名称等于我们的项目名称 SelectWizard Project。通过使用命名空间技术，可以更容易区分具有相同但位置不同的的变量、方法和事件。

