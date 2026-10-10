
```
<ColumnDefinition Width="146" />
```

变为 XAML 框架中的这行代码：

```
<ColumnDefinition Width="Auto" />
```

有些人喜欢代码。有些人喜欢设计器。有些人（像我们）更喜欢两者的奇混合。你决定如何使用这些工具。

## Windows Forms

Windows Forms 设计器与 WPF 设计器之间的主要区别是 Windows Forms 缺少代码面板。虽然有（某种）代码支持 Windows Forms，但你无法编辑它。所以它是。

Windows Forms 主题没有在这个活动开发平台上介绍，我做出了改为介绍它的决定。它执行与 Windows Forms 相同的编程职责，但是是更新的技术。Windows Forms 设计器如图 2-2 所示。

![](img/6df7bb8e9302e98442acc19cfbd7fc_545_png)

> 图 2-2：Windows Forms 设计器。

事实上，关于 Windows Forms 设计器话并不不多。单个控件有一些很棒的功能，但设计器本身没做什么。

## Web Forms

Web 编程比像 Windows Forms 更像 WPF，但它是 Web Forms。设计器在图 2-3 中所示。在使用 HTML 设计器很容易。我想指出 HTML 设计器中的两个功能：

- 视图切换按钮，即 Source 和 Design：Source 只显示 HTML。Design 显示视觉设计器。Split 显示两者。 文档树显示光标所在的位置以及与其他的关系。

![](img/6df7bb8e9302e98442acc19cfbd7fc_546_png)

图 2-3：
Web 项目的代码。

## 类设计器

你可以从任何项目创建类设计器，但我的示例使用了类库项目，如图 2-4 所示。

![](img/6df7bb8e9302e98442acc19cfbd7fc_547_png)

```
1 @Page Title="Home Page"
2 <asp:Content runat="server">
3 <asp:Content ID="ContentPlace1">
4  <section class="garden">
5    <div class="row">
6      <p>
7        To the page
8        If you has
9        <a href="#">
10       </a>
11     </p>
12    </div
13  </section>
14 </asp:Content>
15 <asp:Content ID="ContentPlace2"
16   runat="server">
17  <asp:Button Text="submit the form"
18    class="..." />
19 </asp:Content>
20 %>
```
