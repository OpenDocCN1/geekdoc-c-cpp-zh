
- 7. 构建并运行项目。按如下方式在文本框中输入一些数字：

![](img/41d82527c4e41cdb7e56259564306ddc_220_0.png)

Figure 8.12. 我们的增减程序

首先，当我们点击 ++ 按钮时，数字会递增 1，因为在关联的 incrementButton_Click() 方法中对它们应用了 ++ 运算符：

![](img/41d82527c4e41cdb7e56259564306ddc_220_1.png)

Figure 8.13. 应用增量运算符后的数字

现在，点击 – 按钮以应用递减运算符。此操作后，数字再次取值为 9 和 2，如图 8.14 所示。

现在，点击 += 按钮。你会看到，number2 将被加到 number1 上，number1 会被改变。然而，number2 不会被改变。这在图 8.15 中显示。

## 8.2. If-Else 语句类型

代码行在 C# 程序中从上到下执行。然而，有时需要程序根据变量或输入的状态跳过某些代码行或跳转到特定行。例如，想象一下用户需要在程序中输入用户名和密码来访问数据库。当用户输入其用户名和密码并点击登录按钮时，程序会将输入的用户名/密码与自己的记录中的进行比较。如果用户名/密码组合正确，则会向用户显示数据库。否则，程序会显示错误消息并告诉用户重试。我们使用 C# 中的两种语句类型来执行这些比较和分支操作：if-else 和 switch-case。

在本小节中，我们将学习 if-else 结构如何用于条件检查和分支。If-else 语句有三种变体：if、if-else 和 if-elseif-else。

### 8.2.1. The If Statement

if 语句用于检查条件是否满足。如果条件满足，则 if 块内的代码行将被执行：

```
if(condition)
{
    Here is the if block between the curly brackets. The code written here is executed if the condition is satisfied.
}
Code 8.14
```

让我们在一个用户将输入用户名和密码的示例中使用 if 语句。我们的程序将检查它们是否有效：

- 1. 创建一个 C# 项目。
- 2. 在窗体上添加三个 Labels、两个 TextBoxes 和一个 Button，如图 8.17 所示。
- 3. 将第一个 Label 的 Text 设置为 Login window。
- 4. 将第二个和第三个 Labels 的 Texts 设置为 Username: 和 Password:。

![](img/41d82527c4e41cdb7e56259564306ddc_223_0.png)

- 5. 将 TextBoxes 的 Name 属性分别设置为 **usernameTextBox** 和 **passwordTextBox**。
- 6. 将 Button 的 Name 和 Text 设置为 **Login** 和 **loginButton**。
- 7. 双击 Button 以像往常一样创建其 Click 事件处理程序方法。我们将在此方法中使用 if 语句。我们还没有数据库，因此让我们将用户名和密码与常量值 **csharpprogrammer** 和 **abc456** 分别进行比较。我们在 if 语句中按如下方式执行此操作：

```csharp
if (usernameTextBox.Text == "csharpprogrammer" &&
    passwordTextBox.Text == "abc456")
{
    MessageBox.Show("Login successful");
}
```

Code 8.15

> 请注意，if 结构的括号在 Visual Studio 中会在我们输入 if 然后 **按键盘上的 Tab 键两次** 时自动形成。

在第一行代码中，我们使用比较运算符检查 usernameTextBox 和 passwordTextBox 中输入的 Texts 是否具有值 **csharpprogrammer** 和 **abc456**。这里唯一的新运算符是 &&。它表示“AND”。因此，在此 if 语句中我们检查条件：**输入到 usernameTextBox 中的文本是否为 csharpprogrammer 且输入到 passwordTextBox 中的文本是否为 abc456？** 如果满足此条件，则 if 块内的代码行，即本例中的 `MessageBox.Show("Login successful");` 将被执行。请记住，我们需要将此代码插入 loginButton 的 Click 处理程序方法中：

```csharp
private void loginButton_Click(object sender, EventArgs e)
{
    if (usernameTextBox.Text == "csharpprogrammer" &&
        passwordTextBox.Text == "abc456")
    {
        MessageBox.Show("Login successful");
    }
}
```

Code 8.16

- 8. 构建并运行项目，登录窗口将如下所示出现：

![](img/41d82527c4e41cdb7e56259564306ddc_224_0.png)

Figure 8.18. 登录程序

如果我们在 TextBoxes 中输入随机的用户名和密码值并点击登录按钮，什么都不会发生，因为语句中的 if 条件不会得到满足。然而，如果我们输入正确的用户名和密码然后点击登录按钮，则程序将显示相应的消息框：

![](img/41d82527c4e41cdb7e56259564306ddc_224_1.png)

Figure 8.19. 使用正确的用户名和密码成功登录

类似于用于逻辑 AND 的 &&，我们可以使用字符串 ||（通过按键盘上的 Alt+< 键输入）来实现 if 语句中的逻辑 OR。

顺便说一下，我们可以隐藏密码字符，因为这是登录窗口的惯例。我们通过将 passwordTextBox 控件的 PasswordChar 属性设置为我们选择的任何字符来实现这一点。我已将其设置为 * 字符，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_225_0.png)

Figure 8.20. 为密码输入设置 PasswordChar

设置 PasswordChar 后，密码在 TextBox 中输入的内容将被隐藏：

![](img/41d82527c4e41cdb7e56259564306ddc_225_1.png)

Figure 8.21. 登录窗口中隐藏的密码

### 8.2.2. The If-Else Statement

If-else 语句的工作方式与 if 语句相同。然而它们具有 else 块，当条件不满足时执行。if-else 语句的模板如下所示：

```
if(condition)
{
    Here is the if block between the curly brackets. The code written here is executed if the condition is satisfied.
}
else
{
    Here is the else block between the curly brackets. The code written here is executed if the condition is NOT satisfied.
}
```

Code 8.17

让我们通过添加 else 块按如下方式修改之前的 if 示例（请记住，您可以复制粘贴整个项目文件夹以创建用于修改的新项目）：

```csharp
if (usernameTextBox.Text == "csharpprogrammer" && passwordTextBox.Text == "abc456")
{
    MessageBox.Show("Login successful");
}
else
{
    MessageBox.Show("Username/password incorrect");
    usernameTextBox.Clear();
    passwordTextBox.Clear();
}
```

Code 8.18

当用户输入错误的用户名/密码组合时，if 语句的条件将为 true。在这种情况下，else 块将被执行。它将显示消息 Username/password incorrect，然后使用 Clear() 方法清除用户名和密码 TextBoxes，如图 8.22 所示

> 请注意，else 块没有单独的条件。它也依赖于 if 语句的条件。

让我们创建一个新示例，我们将在其中检查学生的考试分数并以字母形式显示相应的等级。我们可以遵循下表中显示的规则：

| Exam point | Grade |
|---|---|
| [90, 100] | A |
| [75, 89] | B |
| [60, 74] | C |
| [45, 59] | D |
| [0, 44] | E |

Table 8.4. 等级与考试分数

- 1. 创建一个新的 C# 项目。
- 2. 在窗体上添加两个 Labels、一个 TextBox 和一个 Button，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_228_0.png)

Figure 8.24. 窗体的布局

- 3. 将顶部 Label 的 Text 设置为 Grade Mapper。
- 4. 将中间 Label 的 Text 设置为 Enter the exam point:。
- 5. 将 TextBox 的 Name 设置为 pointsTextBox。
- 6. 将 Button 的 Name 和 Text 分别设置为 gradeButton 和 Show grade。
- 7. 将底部 Label 的 Text 和 Name 设置为 Grade appears here... 和 gradeLabel。
- 8. 双击按钮以创建其默认事件处理程序名为 gradeButton_Click()。我们将在此事件处理程序中插入我们的代码。
- 9. 首先，获取 TextBox 的 Text 并将其转换为名为 points 的整数变量，如下所示：

