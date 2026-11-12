
更令人兴奋的是，你已经有了一个主页！在下一个项目中，你将让主页完全按照你想要的样子呈现。但在那之前，你需要创建其他页面。

## 向你的网站添加更多页面

既然你已经有了一个基本主页，你可以添加在项目2的站点地图中规划的其他页面。本书中的站点地图示例有三个新页面：恐龙类型、恐龙名称和恐龙时间线。

- **1.** **回到** [http://drive.google.com](http://drive.google.com) **并双击你的项目文件夹。**
- **2.** **右键单击 index.html，然后单击** **创建副本。**

![](img/b129720fc9ac9e14546b8756740d362a_90_0.png)

- **5.** 重复此操作，直到创建出你需要的所有页面。此示例还需要两个页面：names.html 和 timeline.html。

![](img/b129720fc9ac9e14546b8756740d362a_92_0.png)

- **6.** 单击 index.html 上方和左侧，然后拖动鼠标选中所有 HTML 文件和图片，以高亮显示它们。

![](img/b129720fc9ac9e14546b8756740d362a_92_1.png)

- **7.** 右键单击 `index.html`，然后单击 **共享**。

![](img/b129720fc9ac9e14546b8756740d362a_93_0.png)

- **8.** 就像处理第一张图片时那样，单击 **高级**。然后单击 **更改**，并将其改为 **在网络上公开**。

![](img/b129720fc9ac9e14546b8756740d362a_93_1.png)

- **9.** 当你单击 **保存** 时，你应该会看到四个文件都是公开的。单击 **完成**。

![](img/b129720fc9ac9e14546b8756740d362a_94_0.png)

- **10.** 右键单击你的某个新页面，例如 types.html，然后单击“打开方式”，再单击“HTML 查看器”。

![](img/b129720fc9ac9e14546b8756740d362a_94_1.png)

## 项目5 让你的设计栩栩如生

- **11.** 你应该会看到与主页（index.html）相同的内容，因为你还没有更改新页面的外观——你只是复制了主页。目前这样没问题。

![](img/b129720fc9ac9e14546b8756740d362a_95_0.png)

- **12.** 在地址栏中，单击并高亮显示 URL，然后在 Windows 上按 Ctrl+C，或在 Mac 上按 ⌘-C 来复制它。
- **13.** 回到你的 index.html 文件。如果你关闭了它，可以右键单击 index.html，然后单击“打开方式”，再单击“HTML 编辑器”来重新打开它。
- **14.** 找到你的页眉，并输入链接的 HTML 代码：`<a href=YOUR_URL_HERE> </a>`。（不要输入句号。）

```html
31-  <header>
32-    <iframe src="https://drive.google.com/file/d/0B87t6P68R_Xt2d5Dv-fZGZ0pWT0lk/
      preview" width="280" height="140"></iframe>
33-    <a href="YOUR_URL_HERE">Types of Dinosaurs</a>
34-  </header>
```

- **15.** 用你在步骤12中复制的 URL 替换 YOUR_URL_HERE。在 Windows 上按 Ctrl+V，或在 Mac 上按 ⌘-V 来完成此操作。

```html
31-  <header>
32-    <iframe src="https://drive.google.com/file/d/0B87t6P68R_Xt2d5Dv-fZGZ0pWT0lk/
      preview" width="280" height="140"></iframe>
33-    <a href="https://drive.google.com/viewerng/viewer?url=https://api.stripe.com/v1/
      checkout/sessions?cs_live_b1GK7g9yzALsnR8796211dAnG2
      %2Buz1er1oQZ %2t2211463355j79D9B3g8f21aDBc2N0">Types of Dinosaurs</a>
34-  </header>
```

这就是你链接所有页面的方式。你应该从主页链接到你的所有页面，就像你为添加的第一个新页面创建链接一样。

- **16.** 将 **页眉背景颜色** 改为橙色，以便你能看到链接。

```css
header {
    background-color: #ff8000;
}
```

![](img/b129720fc9ac9e14546b8756740d362a_96_0.png)

- **17.** 在你的另外三个页面中分别添加一个返回主页的链接。操作方式与你为每个页面添加链接时相同。

> **警告**
>
> *请确保也把这些页面的页眉颜色改为橙色！否则很难看清链接。*

你可以访问 [https://thewecanzone/website-building](https://thewecanzone/website-building) 并单击 MyDinoSite 项目5，查看可运行版本。

> **警告**
>
> *有时当你从新的浏览器窗口打开你的网站时，它会要求你再次授权。只需单击 **授权** 即可。*

![](img/b129720fc9ac9e14546b8756740d362a_96_1.png)

选择你的账户，然后单击“允许”。

![](img/b129720fc9ac9e14546b8756740d362a_97_0.png)

恭喜！你现在有了一个可运行并能跳转到其他页面的网站！在下一个项目中，你将学习如何让这个网站与你的线框图和样式指南相匹配。

## 项目6 让你的网站看起来更棒

![](img/b129720fc9ac9e14546b8756740d362a_98_0.png)

如果你一直按照本书中的每个项目进行操作，你已经拥有一个可运行的网站，随时可以与全世界分享。但还有一些部分仍然缺失。你制作了站点地图、线框图、样式指南和一个基本网站。

### 将你的 Google Drive 文件夹设为公开

因为你将向 Google Drive 文件夹添加新文件，所以最好将整个文件夹设为公开，以便分享整个网站。

> 将这个文件夹设为公开后，世界上的每个人都能看到其中的内容。非常重要的一点是，不要在这个文件夹中放入任何个人信息。确保把你计划放到互联网上的所有内容都展示给一位成年人看，并征得许可后再这样做。

- **1.** 前往 [http://drive.google.com](http://drive.google.com) 并登录你的 Google 账户。
- **2.** 右键单击你的项目文件夹，然后单击 **共享**。

![](img/b129720fc9ac9e14546b8756740d362a_100_0.png)

- **3.** 单击 **高级**，然后单击 **更改**。选择 **在网络上公开**，并单击 **保存**。现在你的整个文件夹应该都是 **公开** 的。

![](img/b129720fc9ac9e14546b8756740d362a_101_0.png)

现在，每当你向此文件夹添加新文件时，**Google 都会提示** 你该文件将变为公开。只需单击 **确定**。

![](img/b129720fc9ac9e14546b8756740d362a_101_1.png)

### 将 CSS Editey 应用添加到 Google Drive

正如你在上一个项目中可能已经注意到的，必须把为主页编写的代码复制粘贴到其他每个页面中，这确实很令人沮丧。因此，与其这样做，你将把所有样式代码移到一个新文件中。然后，你将从 HTML 代码中引用该文件。下一节将对此做进一步说明。

现在，先将 CSS Editey 应用添加到 Google Drive。

- **1.** 前往 [http://drive.google.com](http://drive.google.com)，如果你尚未登录，请登录你的 Google 账户。
- **2.** 双击你的项目文件夹以打开它。
- **3.** 单击“新建”，再单击“更多”，然后单击“关联更多应用”。

![](img/b129720fc9ac9e14546b8756740d362a_102_0.png)

- **4.** 搜索“CSS”并按 Enter。单击 CSS Editey 旁边的“连接”。

![](img/b129720fc9ac9e14546b8756740d362a_102_1.png)

- **5.** 当 Google 询问是否应使用 CSS Editey 打开 CSS 文件时，单击 **确定**。

![](img/b129720fc9ac9e14546b8756740d362a_103_0.png)

现在你的编码环境已经准备好了！

### 创建用于样式的 CSS 文件

在本节中，你将把所有样式代码从 HTML 文件移到一个 CSS 文件中。CSS 是另一种编程语言，代表层叠样式表。你甚至已经在不知不觉中编写了 CSS 代码！HTML 文件 head 部分中 **style 标签** 之间的所有代码就是 CSS 代码。

```html
<!doctype html>
<html>
<head>
  <title>
    <style>
      body {
        font-family: 'Open Sans', sans-serif;
        background-color: #f0f0f0;
      }
      header {
        background-color: #ff0000;
      }
      footer {
        background-color: #0000ff;
      }
      div {
        background-color: #ff0000;
      }
      .left {
        width: 75%;
        float: left;
        background-color: #ffffff;
      }
      .right {
        width: 25%;
        float: left;
        background-color: #000000;
        color: #ffffff;
      }
    </style>
```

### 创建 CSS 文件

首先，你需要一个文件来容纳所有要移入的 CSS 代码。

- **1.** 前往 http://drive.google.com，并双击你的项目文件夹以打开它。
- **2.** 单击“新建”，再单击“更多”，然后单击“CSS 编辑器”。

![](img/b129720fc9ac9e14546b8756740d362a_104_0.png)

- **3.** Google 可能会提示你，你的文件将具有与文件夹相同的权限。这意味着你的新文件将变为公开，这很好。单击 **确定**。
- **4.** 单击新文件左上角的 Untitled.css。

![](img/b129720fc9ac9e14546b8756740d362a_104_1.png)
