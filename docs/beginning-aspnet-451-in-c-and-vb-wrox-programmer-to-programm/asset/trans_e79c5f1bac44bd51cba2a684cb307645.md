

1. 打开 Button.skin，复制代码并将其粘贴进去以帮助现有的标记。

2. 如果 VS 添加了 ID 属性，请将其同它的值一起删除（即删除 `ID="Button1"`）。

3. 移除 CssClass 属性及其取值，将按钮的 BackColor（背景颜色）改为红色（Red），并将 ForeColor（前景色）设置为黑色（Black）。

4. 添加一个名为 RedButton 的 SkinID。你最终将得到这段代码：

```
<asp:Button CssClass="MyButton" BackColor="#509EE7" runat="server" />
<asp:Button BackColor="Red" ForeColor="Black" SkinID="RedButton" runat="server" />
```

5. 保存并关闭该 skin 文件。

6. 打开 SkinsDemo.aspx 并添加第二个按钮。将此按钮的 SkinID 设置为 RedButton。注意 IntelliSense（智能感知）如何帮助选择正确的 SkinID。现在两个按钮的代码应该看起来像：

```
<asp:Button ID="Button1" runat="server" Text="Button" />
<asp:Button runat="server" Text="Button" SkinID="RedButton" />
```

7. 在浏览器中打开 SkinsDemo.aspx。你现在应该看到两个按钮：你之前添加的那个以及新建的红底黑字按钮。如果你没有看到不同的颜色，请确保你已经在浏览器中选择了“单色（Monochrome）”主题。

# 工作原理

具名的 skin（Named skins）工作方式与普通 skin完全相同。然而，通过具名的 skin，控件可以指向 skin 文件中的某一个特定 skin。在 SkinsDemo.aspx 页面中，第一个按钮从默认的未具名 skin 中获取设置，而另一个按钮现在从 SkinID 设置为 RedButton 的 skin 中获取设置。如果你为控件分配了一个不存在的 SkinID，ASP.NET 将简单地忽略它并抛出错误。

通过具名的 skin，你拥有了一个非常灵活的解决方案。对于普通 skin，你可以更改网站中所有控件的外观。对于你希望外观与众不同的少数控件，你可以覆盖这种行为。

# 为特定控件禁用主题功能

如果由于某种原因，你不想对特定控件应用 skin，可以通过设置控件的 `EnableTheming` 属性来禁用 skin，如下所示：

```
<asp:Button ID="Button1" runat="server" EnableTheming="False" Text="Button" />
```

当 `EnableTheming` 设置为 False 时，skin 将不会应用到控件。尽管如此，主题 CSS 文件中的 CSS 设置仍然会被应用。

# 创建一致性页面的实用技巧

以下列表提供了一些关于创建一致性页面的实用技巧：

当你创建一个新网站时，始终从添加一个主页（master page）开始，并以此作为所有其他页面的基础。即使你认为网站只有几个页面，主页也能帮助你确保整个网站外观的一致性。在网站开发的后期阶段添加主页意味着要对现有页面进行大量的手动更改。

一旦你发现自己在为复杂的控件（如 TreeView 和 Menu，将在下一章讨论）或数据控件（如 GridView）添加样式，请考虑为它们创建一个 skin。事实上，你能够从单一位置控制所有控件的布局，这使得更新网站变得更加容易。如果你想覆盖少数控件的布局，可以始终使用带有 SkinID 的具名 skin，或者通过将 `EnableTheming` 设置为 False 来禁用 skin。

在创建 skin 或直接在控件上设置属性时，考虑使用 `CssClass` 属性，并将所有与样式相关的属性移动到网站或主题的 CSS 中。这可以减小页面尺寸，并使之后更改布局变得更加容易。

Visual Studio 的导出模板（Export Template）功能是一个非常实用的工具。你不仅可以用它为 ASPX 页面及其后台代码（Code Behind）创建模板，还可以用于其他文件，如类和 CSS 文件，甚至是整个完整的网站。这让你能够快速开始创建新文件。

# 工作

具名的 skin 工作方式与普通 skin完全相同。然而，通过具名的 skin，控件可以指向 skin 文件中的某一个特定 skin。在 SkinsDemo.aspx 页面中，第一个按钮从默认的未具名 skin 中获取设置，而另一个按钮现在从 SkinID 设置为 RedButton 的 skin 中获取设置。如果你为控件分配了一个不存在的 SkinID，ASP.NET 将简单地忽略它并抛出错误。

通过具名的 skin，你拥有了一个非常灵活的解决方案。对于普通 skin，你可以更改网站中所有控件的外观。对于你希望外观与众不同的少数控件，你可以覆盖这种行为。

# 为特定控件禁用主题功能

如果由于某种原因，你不想对特定控件应用 skin，可以通过设置控件的 `EnableTheming` 属性来禁用 skin，如下所示：

```
<asp:Button ID="Button1" runat="server" EnableTheming="False" Text="Button" />
```

当 `EnableTheming` 设置为 False 时，skin 将不会应用到控件。尽管如此，主题 CSS 文件中的 CSS 设置仍然会被应用。

# 创建一致性页面的实用技巧

以下列表提供了一些关于创建一致性页面的实用技巧：

当你创建一个新网站时，始终从添加一个主页（master page）开始，并以此作为所有其他页面的基础。即使你认为网站只有几个页面，主页也能帮助你确保整个网站外观的一致性。在网站开发的后期阶段添加主页意味着要对现有页面进行大量的手动更改。

一旦你发现自己在为复杂的控件（如 TreeView 和 Menu，将在下一章讨论）或数据控件（如 GridView）添加样式，请考虑为它们创建一个 skin。事实上，你能够从单一位置控制所有控件的布局，这使得更新网站变得更加容易。如果你想覆盖少数控件的布局，可以始终使用带有 SkinID 的具名 skin，或者通过将 `EnableTheming` 设置为 False 来禁用 skin。

在创建 skin 或直接在控件上设置属性时，考虑使用 `CssClass` 属性，并将所有与样式相关的属性移动到网站或主题的 CSS 中。这可以减小页面尺寸，并使之后更改布局变得更加容易。

Visual Studio 的导出模板（Export Template）功能是一个非常实用的工具。你不仅可以用它为 ASPX 页面及其后台代码（Code Behind）创建模板，还可以用于其他文件，如类和 CSS 文件，甚至是整个完整的网站。这让你能够快速开始创建新文件。

# 工作

具名的 skin 工作方式与普通 skin完全相同。然而，通过具名的 skin，控件可以指向 skin 文件中的某一个特定 skin。在 SkinsDemo.aspx 页面中，第一个按钮从默认的未具名 skin 中获取设置，而另一个按钮现在从 SkinID 设置为 RedButton 的 skin 中获取设置。如果你为控件分配了一个不存在的 SkinID，ASP.NET 将简单地忽略它并抛出错误。

通过具名的 skin，你拥有了一个非常灵活的解决方案。对于普通 skin，你可以更改网站中所有控件的外观。对于你希望外观与众不同的少数控件，你可以覆盖这种行为。

# 为特定控件禁用主题功能

如果由于某种原因，你不想对特定控件应用 skin，可以通过设置控件的 `EnableTheming` 属性来禁用 skin，如下所示：

```
<asp:Button ID="Button1" runat="server" EnableTheming="False" Text="Button" />
```

当 `EnableTheming` 设置为 False 时，skin 将不会应用到控件。尽管如此，主题 CSS 文件中的 CSS 设置仍然会被应用。

# 总结

网站外观的一致性非常重要。通过使用具名 skin 等技术，你可以创建整个网站的外观。由于主页和内容页可以帮助你。

[/content]

## 以下是需要翻译的文本 

[content]

1. 打开 Button.skin，复制代码并将其粘贴进去以帮助现有的标记。

2. 如果 VS 添加了 ID 属性，请将其同它的值一起删除（即删除 `ID="Button1"`）。

3. 移除 CssClass 属性及其取值，将按钮的 BackColor（背景颜色）改为红色（Red），并将 ForeColor（前景色）设置为黑色（Black）。

4. 添加一个名为 RedButton 的 SkinID。你最终将得到这段代码：

```
<asp:Button CssClass="MyButton" BackColor="#509EE7" runat="server" />
<asp:Button BackColor="Red" ForeColor="Black" SkinID="RedButton" runat="server" />
```

5. 保存并关闭该 skin 文件。

6. 打开 SkinsDemo.aspx 并添加第二个按钮。将此按钮的 SkinID 设置为 RedButton。注意 IntelliSense（智能感知）如何帮助选择正确的 SkinID。现在两个按钮的代码应该看起来像：

```
<asp:Button ID="Button1" runat="server" Text="Button" />
<asp:Button runat="server" Text="Button" SkinID="RedButton" />
```

7. 在浏览器中打开 SkinsDemo.aspx。你现在应该看到两个按钮：你之前添加的那个以及新建的红底黑字按钮。如果你没有看到不同的颜色，请确保你已经在浏览器中选择了“单色（Monochrome）”主题。

# 工作原理

具名的 skin（Named skins）工作方式与普通 skin完全相同。然而，通过具名的 skin，控件可以指向 skin 文件中的某一个特定 skin。在 SkinsDemo.aspx 页面中，第一个按钮从默认的未具名 skin 中获取设置，而另一个按钮现在从 SkinID 设置为 RedButton 的 skin 中获取设置。如果你为控件分配了一个不存在的 SkinID，ASP.NET 将简单地忽略它并抛出错误。

通过具名的 skin，你拥有了一个非常灵活的解决方案。对于普通 skin，你可以更改网站中所有控件的外观。对于你希望外观与众不同的少数控件，你可以覆盖这种行为。

# 为特定控件禁用主题功能

如果由于某种原因，你不想对特定控件应用 skin，可以通过设置控件的 `EnableTheming` 属性来禁用 skin，如下所示：

```
<asp:Button ID="Button1" runat="server" EnableTheming="False" Text="Button" />
```

当 `EnableTheming` 设置为 False 时，skin 将不会应用到控件。尽管如此，主题 CSS 文件中的 CSS 设置仍然会被应用。

# 创建一致性页面的实用技巧

以下列表提供了一些关于创建一致性页面的实用技巧：

当你创建一个新网站时，始终从添加一个主页（master page）开始，并以此作为所有其他页面的基础。即使你认为网站只有几个页面，主页也能帮助你确保整个网站外观的一致性。在网站开发的后期阶段添加主页意味着要对现有页面进行大量的手动更改。

一旦你发现自己在为复杂的控件（如 TreeView 和 Menu，将在下一章讨论）或数据控件（如 GridView）添加样式，请考虑为它们创建一个 skin。事实上，你能够从单一位置控制所有控件的布局，这使得更新网站变得更加容易。如果你想覆盖少数控件的布局，可以始终使用带有 SkinID 的具名 skin，或者通过将 `EnableTheming` 设置为 False 来禁用 skin。

在创建 skin 或直接在控件上设置属性时，考虑使用 `CssClass` 属性，并将所有与样式相关的属性移动到网站或主题的 CSS 中。这可以减小页面尺寸，并使之后更改布局变得更加容易。

Visual Studio 的导出模板（Export Template）功能是一个非常实用的工具。你不仅可以用它为 ASPX 页面及其后台代码（Code Behind）创建模板，还可以用于其他文件，如类和 CSS 文件，甚至是整个完整的网站。这让你能够快速开始创建新文件。

# 工作

具名的 skin 工作方式与普通 skin完全相同。然而，通过具名的 skin，控件可以指向 skin 文件中的某一个特定 skin。在 SkinsDemo.aspx 页面中，第一个按钮从默认的未具名 skin 中获取设置，而另一个按钮现在从 SkinID 设置为 RedButton 的 skin 中获取设置。如果你为控件分配了一个不存在的 SkinID，ASP.NET 将简单地忽略它并抛出错误。

通过具名的 skin，你拥有了一个非常灵活的解决方案。对于普通 skin，你可以更改网站中所有控件的外观。对于你希望外观与众不同的少数控件，你可以覆盖这种行为。

# 为特定控件禁用主题功能

如果由于某种原因，你不想对特定控件应用 skin，可以通过设置控件的 `EnableTheming` 属性来禁用 skin，如下所示：

```
<asp:Button ID="Button1" runat="server" EnableTheming="False" Text="Button" />
```

当 `EnableTheming` 设置为 False 时，skin 将不会应用到控件。尽管如此，主题 CSS 文件中的 CSS 设置仍然会被应用。

# 总结

网站外观的一致性非常重要。通过使用具名 skin 等技术，你可以创建整个网站的外观。由于主页和内容页可以帮助你。

