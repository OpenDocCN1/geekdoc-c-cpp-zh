
-   在创建皮肤或直接在控件上设置样式属性时，请考虑改用 `CssClass` 属性，然后将所有与样式相关的属性移至站点或主题的 CSS 中。这可以减小页面的大小，并且在之后更改布局时更容易。
-   Visual Studio 的导出模板功能非常节省时间。你不仅可以用它为 ASPX 页面及其代码隐藏创建模板，还可用于类和 CSS 文件等其他文件，甚至完整的网站。这可以让你快速开始创建新文件，避免反复输入相同的内容。

## Summary

保持网站所有页面的一致外观和感觉对于让网站看起来专业且有吸引力非常重要。这反过来有助于访客在网站中找到正确的信息，增加他们再次访问网站的可能性。ASP.NET 4.5 提供了许多优秀的工具来帮助你创建外观一致的网站。

ASP.NET 主页和内容页可帮助你创建在基于该主页的每个页面中重复使用的布局。

而主页定义了集中的外观和感觉，你使用基页来集中行为，例如检查页面是否具有无效标题。

主题用于更改网站中页面及其包含的控件的外观和感觉。由于主题可以包含 CSS 文件、图像和皮肤，因此只需应用主题即可更改颜色、字体、定位和图像。通过很好地使用命名皮肤和 `EnableTheming` 属性等技术，你可以创建适用于整个网站的设计，同时保持按控件逐个覆盖设计的灵活性。

Planet Wrox 网站现在开始增长。这意味着你和访客找到正确页面变得更加困难。下一章将向你展示用户浏览网站的多种不同方式，以便他们不会在查找所需页面时遇到任何问题。

## Exercises

1.  `ContentPlaceHolder` 和 `Content` 控件有什么区别？在什么类型的页面中使用哪一个？
2.  如何将内容页中的 `Content` 控件连接到主页中的 `ContentPlaceHolder`？
3.  假设你创建了一个皮肤，该皮肤会应用于网站中的所有按钮，皮肤定义如下：

    ```
    <asp:Button runat="server" CssClass="MyButton" />
    ```

    假设的 CSS 类 `MyButton` 将按钮的背景色设置为黑色，前景色设置为白色。为了引起对页面中某个特定按钮的注意，你决定将其背景改为红色。你有哪些选项可以控制这个单个按钮的外观？
4.  解释为页面设置 `Theme` 属性和 `StyleSheetTheme` 属性之间的区别。
5.  命名为页面设置 `Theme` 属性的三种不同方法并解释这些选项之间的区别。
6.  在网站中实现基页的主要原因是什么？

可在附录 A 中找到这些练习的答案。

## Relative URLs

在之前的示例中，你看到了一个相对 URL，它指向相对于 URL 使用位置的另一个资源。这意味着包含 `<a>` 元素的页面和 Login.aspx 页面都应放置在网站的同一文件夹中。要引用其他文件夹中的资源，你可以使用以下 URL。所有示例均基于图 7-1 所示的站点结构。

从根目录中的 Login.aspx 链接到 Management 文件夹中的 Default.aspx，可以使用此 URL：

```
<a href="Management/Default.aspx">Management</a>
```

要从 Management 文件夹中的 Default.aspx 引用图像 Header.jpg，可以使用此 URL：

```
<img src="./../Images/Header.jpg" />
```

这两个前导句点“导航”到根目录上一级文件夹，然后路径进入 Images 文件夹指向 Header.jpg。

对于更深的文件夹层次结构，你可以使用多个双句点，每个句点对应你希望在站点层次结构中向上移动的一个文件夹，如以下 `<img>` 元素所示。你可以将其用于从位于 Management 文件夹下的 Reviews 文件夹中的页面引用同一图像：

```
<img src="./../../Images/Header.jpg" />
```

![](img/eadab2ccd79b253c01a3fdff2321202d_300_0.png)

相对 URL 的一个好处是，你可以将一组文件移动到同一级别的另一个目录，而不会破坏其内部链接。然而，同时，它们使将文件移动到站点层次结构中的不同级别变得更加困难。例如，如果你将 Login.aspx 页面移动到 Members 等单独文件夹，指向 Management 文件夹的链接就会失效。新的 Members 文件夹没有 Management 作为其子文件夹，因此 Management/Default.aspx 不再是有效的链接。

为克服此问题，你可以使用基于根的相对 URL。

## Root-Based Relative URLs

基于根的相对 URL 总是以前导正斜杠开头，表示站点的根目录。如果再次使用指向 Management 文件夹的链接，其基于根的版本如下所示：

```
<a href="/Management/Default.aspx">Management</a>
```

注意 Management 文件夹前的前导正斜杠，表示网站的根目录。此链接是明确的。它始终指向根目录中 Management 文件夹里的 Default.aspx 文件。使用此链接，将 Login.aspx 页面移动到子文件夹不会破坏它；它仍然指向完全相同的文件。

resources within your own site—but that's not the case. The extra protocol and domain information adds to the size of the page in the browser, making it unnecessarily slower to download. But more important, it creates difficulties if you're changing your domain name, or if you want to reuse some functionality in a different website. For example, if you previously had your site running on www.mydomain.com but you're moving it to www.someotherdomain.com, you will need to update all the absolute URLs in the entire website.

在开发期间使用绝对 URL 也会遇到问题。经常，你会在诸如 http://localhost 之类的 URL 上测试网站。如果你将所有图像都指向该 URL，一旦将网站部署到 www.PlanetWrox.com 等生产域名上，它们都会失效。

简而言之，请谨慎使用绝对 URL。当引用网站外部的资源时，你总是需要它们，但在自己的项目内部应尽可能优先使用相对 URL。

## Understanding Default Documents

在 URL 的上下文中，你还应该了解 *default documents*。当你浏览到像 www.domainname.com 这样的站点时，页面会神奇地出现。 这是如何工作的？每个 Web 服务器都有所谓的默认文档，即当未提供显式文档名称时可提供给浏览器的文档名称列表。因此，当你浏览到 www.domainname.com 时，Web 服务器会扫描请求的目录（本例中为根文件夹），并处理其在磁盘上找到的默认文档列表中的第一个文件。在大多数 ASP.NET 场景中，Web 服务器设置为使用 Default.aspx 作为默认文档。因此，当你在 ASP.NET Web 服务器上浏览 www.domainname.com 时，实际提供给你的页面是 www.domainname.com/Default.aspx。

在你创建的链接中，通常应在使用时省略 Default.aspx。它可以减小页面大小，但更重要的是，它使用户输入地址变得更容易。

现在你已经了解如何使用 URL 指向文档和其他文件，是时候查看一些使用这些 URL 的更高级别控件了：ASP.NET 导航控件。

## Using the Navigation Controls

ASP.NET 4.5 提供了三种有用的导航工具：SiteMapPath、TreeView 和 Menu。图 7-2 显示了三种导航控件的基本示例，未应用任何样式。

左侧的 SiteMapPath 向用户显示当前页面的路径。这有助于用户在站点层次结构中向上移动一层或多层。它也有助于他们了解自己的位置。TreeView 可以显示网站的结构，并允许你展开和折叠不同的节点；在图 7-2 中，整个树都已展开。右侧的 Menu 控件最初仅显示 Home 菜单项。然而，一旦将鼠标移至菜单项上，就会出现子菜单。在图 7-2 中，这些子元素之一是 Reviews 项，其本身也有子元素。

