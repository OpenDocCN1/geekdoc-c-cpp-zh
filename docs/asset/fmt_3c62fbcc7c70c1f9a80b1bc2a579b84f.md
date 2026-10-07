
其中 `term1`、`term2` 等是列表中的术语，`description1`、`description2` 等是与术语对应的描述。默认情况下，大多数浏览器会缩进每个术语对应的描述。很少会在术语或描述旁边显示标记。

Saja 想在一个显示某些菜单项的页面上使用描述列表。他已经开始编写 HTML 代码，但需要你通过添加描述列表的标记来完成它。

## 完成菜单页面

1. 在 HTML 编辑器中打开来自 `html01` 教程的 `menu.txt.html` 文件。在注释部分输入你的姓名和日期，并将文件保存为 `cm.html`。
2. 如果尚未打开，请在编辑器中打开 `pages.txt` 文件并复制移动菜单列出的五个菜单项。
3. 返回 HTML 编辑器中的 `code.menu.html` 文件，将复制的文本直接粘贴在 `<h1>mobile menu</h1>` 之后。
4. 将整个菜单封装在 `<dl>` 和 `</dl>` 中。
5. 使用 `<dt>` 元素标记每个菜单项的名称。使用 `<dd>` 元素标记相应的描述。缩进你的代码以便于阅读和理解。

图 1-32 显示了移动菜单描述列表的完整代码。

## HTML 52 HTML 和 CSS | 教程 1 入门 HTML

## 图 1-32 将餐厅菜单标记为描述列表

每个菜单项目的名称被标记为描述术语（term）；关于项目的信息被标记为描述（description）

```html
<article>
  <h1>Mobile Menu</h1>
  <dl>
    <dt>罗勒牛肉芝麻沙拉，顶部配有新鲜罗勒、新鲜混合沙拉、
    红卷菜、胡萝卜和番茄；配以
    芝麻油醋 ($9.95)</dt>
    <dt>路边炒饭</dt>
    <dd>洋葱、红灯椒、豌豆和
    胡萝卜炒，点缀红卷菜、黄瓜、小葱
    和炸蒜 ($6.50)；加鸡肉 ($8.50)</dd>
    <dt>黑椒猪肉</dt>
    <dd>腌制猪肉大蒜炒；
    配蒸茉莉饭、红卷菜、胡萝卜、
    黄瓜、小葱和炸蒜 ($8.50)</dd>
    <dt>泰式河</dt>
    <dd>豆芽和豆豉炒面，
    点缀红卷菜、胡萝卜、
    小葱、青柠和碎花生 ($7.50)；
    加鸡肉 ($8.50) 或虾仁 ($9.50)</dd>
    <dt>泰式红咖</dt>
    <dd>用椰奶烹制的传统红咖酱，加入
    竹笋、新鲜罗勒、青柠和泰国辣椒
    盛在蒸茉莉饭上 ($7.50)；加
    鸡肉 ($8.50) 或虾仁 ($9.50)</dd>
  </dl>
</article>
```

- 将更改保存到文件，然后在浏览器中打开 `ct_menu.html` 文件。图 1-33 显示了 Curbside Thai 的完成菜单。

Copyright 2018 Cengage Learning. 版权所有。未经许可不得复制或部分扫描或复制。WCN 02-200-203

## 教程 1 入门 HTML5 | HTML 和 CSS HTML 53

图 1-33

## 作为描述列表的路边菜单

| 术语 | 术语的描述 |
| --- | --- |
| 罗勒牛肉芝麻沙拉 | 香辣安格斯牛肉和甜罗勒配在新鲜混合沙拉、红卷菜、胡萝卜、黄瓜和番茄上；配芝麻油醋 ($9.95) |
| 路边炒饭 | 洋葱、红灯椒、豌豆和胡萝卜炒，点缀红卷菜、黄瓜、小葱和炸蒜 ($6.50)；加鸡肉 ($8.50) 或虾仁 ($5.50) |
| 黑椒猪肉 | 大蒜黑椒炒；配蒸茉莉饭、红卷菜、胡萝卜、小葱和炸蒜 ($8.50) |
| 泰式河粉 | 豆芽和韭菜炒面，点缀红卷菜、胡萝卜、小葱、青柠和碎花生 ($7.50)；加鸡肉 ($8.50) 或虾仁 ($9.50) |
| 泰式红咖 | 用椰奶烹制的传统红咖酱，加入竹笋、新鲜罗勒、青柠和泰国辣椒，盛在一盘蒸茉莉饭上 ($7.59)；加鸡肉 ($8.50) 或虾仁 ($9.50) |

描述列表

注意 Saja 为她的网站使用的样式在列表的每个术语和描述之间插入了分割线。描述列表可以使用任何通用列表，将一个项目与另一个提供有关第一个列表项目额外信息的列表配对。例如，Saja 有一个页面列出了 Curbside Thai 出现的时间地点。通过将内容封装在描述列表中来完成此页面，将项目标记为“items”，将地点标记为列表“descriptions”。

## 要创建时间和地点的页面

- 1. 在你的 HTML 编辑器中打开 `html01` ► `tutorial` 文件夹下的 `ct_locations.txt` 文件。在注释部分输入你的姓名和日期，并将其保存为 `ct_locations.html`。
- 2. 回到文本编辑器中的 `ct_pages.txt`，并复制 Today's 页面中的四个地点。
- 3. 回到 HTML 编辑器中的 `ct_locations.html` 文件，将复制的文本直接粘贴在 `<<h1>Today's Locations</h1>` 之后。
- 4. 使用 `dl` 元素标记时间地地点的列表。使用 `dt` 元素标记每个时间，使用 `dd` 元素标记每个地点。对代码进行缩进处理，以便于阅读和理解。
- 5. 为了将此描述列表与网站上的其他列表区分开，添加属性 `id="ct_locations"`。
- 6. Saja 有一张地图，想放在时间和地点列表的旁边。在 `article` 元素中的 `h1` 元素之后，直接插入以下图像：

```html
<img src="ct_map.png" alt="" />
```

Copyright 2018 Cengage Learning. 版权所有。未经许可不得复制或部分扫描或复制。WCN 02-200-203

## HTML 54 HTML 和 CSS | 教程 1 入门 HTML5

图 1-34 显示了 Today's Locations 页面新添加的代码。

## 图 1-34 创建描述列表

```html
<article>
  <h1>Today's Locations</h1>
  <img src="ct_map.png" alt="" />
  <dl id="ct_locations">
    <dt>11 a.m. to 2 p.m.</dt>
    <dd>205 West 3rd Street, Charlotte</dd>
    <dt>2 p.m. to 4 p.m.</dt>
    <dd>443 West 2nd Street, Charlotte</dd>
    <dt>4 p.m. to 8 p.m.</dt>
    <dd>900 South Mint Street, Charlotte</dd>
    <dt>8 p.m. to 11 a.m.</dt>
    <dd>168 North Church Street, Charlotte</dd>
  </dl>
</article>
```

描述列表
- 7. 将更改保存到文件，然后在浏览器中打开 `ct_menu.html` 文件。图 1-33 显示了 Curbside Thai 的完成菜单。

描述列表
- 11 a.m. to 2 p.m. / 205 West 3rd Street, Charlotte
- 2 p.m. to 4 p.m. / 443 West 2nd Street, Charlotte
- 4 p.m. to 8 p.m. / 900 South Mint Street, Charlotte
- 8 p.m. to 11 a.m. / 168 North Church Street, Charlotte

图 1-33 显示了 Curbside Thai 的完成菜单。

将此结构添加到 About Curbside Thai 网页中，为您在本教程中创建的六个网页中的每一个页面创建条目。

## 创建导航列表

- 1. 如果 `ct_about.html` 文件尚未打开，请在 HTML 编辑器中打开它。
- 2. 转到 body 头部部分，直接在 Curbside Thai 标志的内联图像下方，插入以下导航列表：

```html
<nav>
  <ul>
    <li>About（关于我们）</li>
    <li>Locations（门店）</li>
    <li>Menus（菜单）</li>
    <li>Reviews（评价）</li>
    <li>Catering（餐饮服务）</li>
    <li>Contact（联系我们）</li>
  </ul>
</nav>
```

图 1-36 高亮显示了导航列表的结构。

![](img/bf90ebf56b5f948b05e7a26851204c31_73_0.png)

- 3. 保存对文件的更改，然后在浏览器中重新打开 `ct_about.html` 文件。

# 教程 1 入门 HTML5 | HTML 和 CSS HTML 57

图 1-37 显示了导航列表的外观。

## 图 1-37

## Curbside Thai 网站的导航列表

![](img/bf90ebf56b5f948b05e7a26851204c31_74_0.png)

Curbside Thai 将泰国风味带到了北罗来纳州。
Saja Adams 主厨在 House of Asia 拥有超过 35 年的经验，他利用这些专业知识，通过我们的现代移动食品餐车将美食带到了夏洛特的街头。
这可不是包装在油腻纸盒里的平淡摊位食品！欢迎在周一至周四上午 11 点到下午 2 点，以及周五和周六的上午 11 点，在我们各的移动地点品尝备受誉目的料理。如果您无法离开办公桌，也可以尝试一下。Curbside Thai 将为您送达。
© 2016 Cengage Learning: Xenon/Shutterstock.com

注意，`ct_about.html` 文件中导航列表的外观是基于 Saja 的样式表的。导航列表可以根据采用的样式以多种方式显示，同一个导航列表在桌面设备上以一种方式排列，而在移动设备上以另一种方式排列。您将在教程 5 中学习更多内容。

现在您已经创建了导航列表的结构，可以将列表中的项目标记为超链接。

## 处理超文本链接

超文本通过将内容包含在一对起始和结束 `<a>` 标签中创建，格式如下：

```html
<a href="url">content</a>
```

其中 `url` 是统一资源定位符 (URL)，它是一种用于识别资源位置的标准格式，包括文档、电子邮件地址、电话号码和短信，而 `content` 是标记为链接的文档文本。当链接到同一文件夹中的另一个 HTML 文件时，URL 仅为文件名。例如，指向 `ct_menu.html` 文件的超链接将标记为：

```html
<a href="ct_menu.html">Menu</a>
```

当您点击或触摸“Menu”一词时，浏览器将在浏览器中加载 `ct_menu.html` 文件。注意，某些 Web 服务器对文件名是敏感的，它们会区分命名为 `ct_menu.html` 和 `Ct_Menu.html` 的文件名。所有文件名的标准是使用小写，并避免特殊字符和空格。

默认样式是为链接添加下划线，如果用户之前访问过该页面，则为超链接显示不同的文本颜色。然而，页面设计师可以根据自己的样式将超链接与其他区分来。我们将在教程 2 中探索这种技术。

- 提示：保持链接简短且具有描述性，这样用户在访问您的网站时不容易输入错误。

## 标记超文本链接

- 要标记内容为超文本链接，请使用 `<a href="url">content</a>`

其中 `url` 是链接文档的地址，`content` 是被标记为链接的内容。

标记导航列表中的六个条目，使每个条目指向相应的 Curbside Thai 页面。

## 创建超链接

- 1. 返回 HTML 编辑器中的 `ct_about.html` 文件。
- 2. 通过将项目更改为 `<a href="ct_about.html">About</a>`，将第一个条目标记为指向 `ct_about.html` 的超文本链接。
- 3. 将第二个列表项的代码更改为 `<a href="ct_locations.html">Locations</a>`。
- 4. 此此类，将 Menu 条目更改为指向 `ct_menu.html` 文件的链接，将 Reviews 条目更改为指向 `ct_reviews.html` 文件的链接，将 Catering 条目更改为指向 `ct_catering.html` 文件的链接，并将 Contact 条目更改为指向 `ct_contact.html` 文件的链接。

图 1-38 高亮显示了更改所有项目的新添加代码。

标记链接

```html
<nav>
  <ul>
    <li><a href="ct_about.html">About</a></li>
    <li><a href="ct_locations.html">Locations</a></li>
    <li><a href="ct_menu.html">Menu</a></li>
    <li><a href="ct_reviews.html">Reviews</a></li>
    <li><a href="ct_catering.html">Catering</a></li>
    <li><a href="ct_contact.html">Contact</a></li>
  </ul>
</nav>
```

- 5. 保存对文件的更改，然后在浏览器中重新打开 `ct_about.html` 文件。
- 6. 在浏览器中点击导航列表并刷新 `ct_about.html` 文件。

# 教程 1 入门 HTML5 | HTML 和 CSS HTML 59

问题？如果链接不起作用，请确保 `ct_about.html` 的拼写正确。

您注意到当鼠标指针悬停在导航列表上时，链接的外观发生了变化。这是一种悬停效果，我们将在教程 5 中学习如何创建这种效果。

## 悬停效果

Saja 希望能够从网站的任何页面跳转到 Curbside Thai 文档。

将图像转换为链接

内联图像也可以通过将其放在起始和结束的 `<a>` 标签中来转换为链接。

> 将图像转换为链接：
> 1. 返回 HTML 编辑器中的 `ct_about.html` 文件。
> 2. 将图像包裹在：`<a href="start.html"><img src="logo2.png" alt="Curbside Thai"></a>`。

图 1-39 显示了将图像转换为链接的代码。

| 图 1-39 | 标记内联图像链接 |
|---|---|
| 链接 | `<body><header><a href="start.html"><img src="logo2.png" alt="Curbside Thai"></a></header></body>` |

- 3. 保存对文件的更改，然后在浏览器中重新打开 `ct_about.html` 文件。
- 4. 点击 Curbside Thai 标志并验证浏览器打开了启动页面。

# 教程 1 HTML5 入门 | HTML 和 CSS HTML 61

要在文件夹中的文件之间创建链接，你必须提供被链接文件的路径。HTML 支持两种路径：绝对路径和相对路径。

## 绝对路径

绝对路径是从根目录开始，并处理由以下表达式描述的整个文件夹结构的路径：

```
/folder1/folder2/folder3/file
```

其中 `folder1` 是根目录，随后是子文件夹 `folder2`、`folder3` 等，最后是被链接的文件。例如，根据之前图 1-40 所示的结构，指向 `ct_catering.html` 文件的绝对路径表达式为：

```
/thai/docs/catering/ct_catering.html
```

如果文件位于不同的驱动器以及不同的文件夹中，你必须在路径中包含驱动器号，表达式如下：

```
/drive/folder1/folder2/folder3/file
```

其中 `drive` 是分配给驱动器的字母。注意，驱动器字母后面必须紧跟一个字符。如果 `ct_catering.html` 文件位于 E 驱动器，则该驱动器的绝对路径表达式为：

```
/E/thai/docs/catering/ct_catering.html
```

注意，如果链接文档与当前文件位于同一个驱动器，则不需要包含驱动器号。

## 相对路径

当涉及许多文件夹和子文件夹时，绝对路径表达式会迅速变得繁琐且难以处理。大多数网页设计师倾向于使用相对路径，即路径相对于当前文档的位置。如果当前文档和链接文件位于同一个文件夹中，则没有路径，你只需要包含文件名。如果链接文件位于当前文档的子文件夹中，路径将包含从当前页面位置开始的所有子文件夹名称，表达式如下：

```
folder1/folder2/folder3/file
```

其中 `folder1`、`folder2`、`folder3` 等是当前文档的文件夹。例如，从 `index.html` 文件到 `ct_about.html` 文件的相对路径是：

```
docs/general/ct_about.html
```

注意，相对路径是以（家族关系，如父级、后级、兄弟等）来表示的，以指示结构的层级性质。相对路径还可以通过包含符号 `..` 向上层级到达父级文件夹，该符号意味着“向上一级”。从 `general` 文件夹中的 `ct_about.html` 向上移动两级到达 `index` 文件，你需要如下表达式：

```
../../index.html
```

最后，要通过进入不同文件夹但在同一层级的文件在文件夹结构中进行横向移动，你需要回到父文件夹再向下进入另一个不同的文件夹。例如，从 `general` 文件夹中的 `ct_about.html` 文件到 `mobile` 文件夹中的 `ct_locations.html` 文件，你将使用相对表达式：

```
../mobile/ct_locations.html
```
