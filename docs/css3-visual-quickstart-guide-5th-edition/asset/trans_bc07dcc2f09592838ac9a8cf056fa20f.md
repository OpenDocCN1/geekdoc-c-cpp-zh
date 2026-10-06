

## 表 8.8 border-collapse 值

| 值 | 兼容性 |
| --- | --- |
| collapse | IE5.5, FF1, O5, S1, C3, CSS2 |
| separate | IE5.5, FF1, O5, S1, C3, CSS2 |
| inherit | IE5.5, O5, S1, C3, CSS2 |

## 合并表格单元之间的边框

由 `<<td>>` 标签定义的每个表格单元都有四个边框：上、右、下、左。**border-collapse** 属性（表 8.8）允许你设置表格，使每个单元单元与相邻单元共享边框，而不是为每个单元创建一个独立的边框。

代码 8.8 `list-table-properties.css`——`border-collapse` 属性允许你移除表格单元之间的任何空间，使每个单元拥有单个边框（见下页），但框间距（border-spacing）会被忽略。使用 **separate** 可以让 **border-spacing** 生效（见下页）：

## 要合并表格中的边框：

```css
*** CSS3 | Chapter 8 |
list-table-properties.css ***

ul {
  list-style: url(../images/bullet01.png) inside;
}

nav.global {
  list-style: none;
}

table {
  table-layout: auto;
  border-spacing: 8px;
  border-collapse: separate;
  width: 75%;
  margin: 40px auto;
}

caption, table caption {
  font: italic 1.25em Georgia, 'Times New Roman', Serif;
}

t {
  font-size: 1.25em;
}

td {
  vertical-align: top;
  padding: .5em;
  background-color: rgba(200, 200, 180, .25);
  border: 1px solid rgb(200, 200, 180);
}
```

- 1. 在表格元素中添加 `border-collapse` 属性。输入 `border-collapse`，后跟一个冒号（:（代码 8.8）。
- 2. 指定边框如何合并。根据你想要显示边框的方式输入以下内容之一：
  - collapse 将使相邻的表格单元共享共同边框；然而，如果边框已合并，将无法设置 border-spacing。
  - separate 将保持每个数据单元的边框。除非你设置了边框厚度，否则不同浏览器显示结果可能不同。如果边框厚度相同但样式不同，将使用左侧数据单元的边框样式。通过使用 collapse，数据单元之间的边框减少为单条细线。

| 名字 | 茶茶会 | 疯了吗？ |
|---|---|---|
| 疯帽子 | | |
| 呆语兔 | “像野兔一样疯狂”是卡罗尔时代的常用用语。 | | |
| 睡鼠 | 睡鼠在整个场景中一直都在睡觉，经常醒来。 | | |
| 爱丽丝 | 人说这个角色是基于德格森的孩子 Alice Liddell 的 | |

代码 8.8 应用于代码：设置 separate 后，你可以设置 border-spacing。

## 表 8.8 empty-cells 值

| 值 | 兼容性 |
| --- | --- |
| show | FF1, O5, S1, CSS2 |
| hide | FF1, O5, S1, CSS2 |
| inherit | FF1, O5, S1, CSS2 |

## 处理空单元格

代码 8.9 `list-table-properties.css`——`empty-cells` 属性允许你显示（默认）或隐藏表格单元格。如果表格单元格没有数据（即使没有换行空格），它将以列和行的默认宽度和高度显示为空。**empty-cells 属性（表 8.9）**允许你指定空单元格（最重要的是它的边框）的呈现方式。

```css
*** CSS3 | Chapter 8 |
list-table-properties.css ***

ul {
  list-style: url(../images/bullet01.png) inside;
}

nav.global ul {
  list-style: none;
}

table {
  table-layout: auto;
  border-spacing: 8px;
  border-collapse: separate;
  empty-cells: hide;
  width: 75%;
  margin: 40px auto;
}
```

### 要隐藏空表格单元格：

- 1. 在表格元素规则中添加 `empty-cells` 属性。输入 `empty-cells`，后跟一个冒号（:（代码 8.9）。
- 2. 指定如何处理空表格单元格。输入以下内容之一来指定处理单元格的方式：
  - **show** 将强制空数据单元显示其背景和边框。
  - **hide** 将在数据单元格的位置留出视觉间隙。

```css
table caption, table head {
  font: 1.25em Georgia, *Times New Roman*, Serif;
}
td {
  font-size: 1.25em;
  vertical-align: top;
  padding: .5em;
  background-color: rgba(200, 200, 180, 25);
  border: 1px solid rgb(200, 200, 180);
}
```

| 名字 | 描述 |  |
| --- | --- | --- |
| 疯帽子 | | |
| 呆语兔 | “像三月兔一样是卡罗罗故事中的常用短语。” | | |
| 睡鼠 | 睡鼠在整个场景中一直都在睡觉，偶尔醒来 | | |
| 爱丽丝 | 人说这个角色是基于德格森的孩子 Alice Liddell 的。 | |

**代码 8.9 应用于代码 8.1：** 空表格数据单元已隐藏，因此边框和背景颜色不显示，在表格中留下了空间隙。

## 设置表格标题的位置

`<caption>` 标签允许在表格中嵌入标识性文本。你可以在标签中设置 `align` 属性来定义标题相对于表格的位置，但该属性正在被弃用，取而代之的是 CSS `caption-side` 属性（表 8.10），后者的功能相同。

要设置标题相对于其表格的位置：

- 1. 在你的 CSS 中添加 `caption-side` 属性。输入 `caption-side`，后跟一个冒号（代码 8.10）。
- 2. 输入以下内容之一来指定标题出现的位置：top 或 bottom。

