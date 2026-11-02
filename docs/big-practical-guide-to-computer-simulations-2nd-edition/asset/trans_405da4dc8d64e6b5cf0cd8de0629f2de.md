

| Symbol | Command | Symbol | Command |
|---|---|---|---|
| ⇌ | \rightleftharpoons | ⟺ | \iff |
| ↑ | \uparrow | ↓ | \downarrow |
| ⇈ | \Uparrow | ⇊ | \Downarrow |
| ↕ | \updownarrow | ⇅ | \Updownarrow |
| ↗ | \nearrow | ↘ | \searrow |
| ↙ | \swarrow | ↖ | \nwarrow |
| ↝ | \leadsto |  |  |

LaTeX 还包含许多其他符号：

| Symbol | Command | Symbol | Command | Symbol | Command |
|---|---|---|---|---|---|
| ∀ | \forall | ∃ | \exists | ∂ | \partial |
| ℜ | \Re | ℑ | \Im | ı | \imath |
| ℏ | \hbar | j | \jmath | ℓ | \ell |
| … | \cdots | … | \dots | : | \vdots |
| ⋱ | \ddots | ℵ | \aleph | ℘ | \wp |
| ∇ | \nabla | ∅ | \emptyset | ∞ | \infty |
| ' | , | ' | \prime | ¬ | \neg |
| △ | \triangle | ∠ | \angle | √ | \surd |
| ⊥ | \bot | ⊤ | \top | ◇ | \diamondsuit |
| ♡ | \heartsuit | ♣ | \clubsuit | ♠ | \spadesuit |
| ♭ | \flat | ♮ | \natural | ♯ | \sharp |

常用的重要元素包括分数（\frac）和根式（\sqrt）。第一个命令接受两个参数，第二个命令接受一个参数，外加一个可选的 [n] 值用于表示 n 次根。这两个命令都可以嵌套使用，如下例所示：

```
\begin{equation*}
\sqrt[3]{\frac{a+\sqrt{b+c}}{\frac{1}{x^2}+\sin(x)}}
\end{equation*}
```

结果如下：

$$\sqrt[3]{\frac{a + \sqrt{b + c}}{\frac{1}{x} + \sin(x)}}$$

二项式可以用下面这种相当非标准²的方式来使用：

```
\begin{equation*}
{ r \choose k-1}+ { r \choose k} = {r+1 \choose k}\,.
\end{equation*}
```

结果为

$$\binom{r}{k-1} + \binom{r}{k} = \binom{r+1}{k}.$$

还存在一个 \atop 命令，它的作用方式相同，但省略了括号。

在上面的分数示例中，还使用了 \sin 函数。请注意，函数名不是用斜体打印，而是用罗马字体打印。LaTeX 中预定义了一些函数，如下表所示：

| \arccos | \arcsin | \arctan | \arg | \cos | \cosh |
| \cot | \coth | \csc | \deg | \det | \dim |
| \exp | \gcd | \hom | \inf | \ker | \lg |
| \lim | \liminf | \limsup | \ln | \log | \max |
| \min | \Pr | \sec | \sin | \sinh | \sup |
| \tan | \tanh |  |  |  |  |

你可以使用以下命令声明自己的函数：

```
\DeclareMathOperator!{\verb!\operator!}{\verb!\text!}
```

该命令接受两个参数：运算符的名称和将要打印的文本。\DeclareMathOperator 只能在源文件的导言区（preamble）中使用，即 \begin{document} 之前。

复杂的公式可以使用括号和其他定界符来组织。竖箭头也可以用作定界符。除此之外，LaTeX 还支持以下括号和定界符：

请注意，大括号也可以不带分别打印在大括号上方或下方的附加部分使用。\underline 命令也允许在数学公式之外使用。

公式也可以使用不同的字体。这里特别提一下书法体（calligraphic font），例如：

```
    \begin{equation*}
    \mathcal{A,B,\ldots,y,Z}\,.
    \end{equation*}
```

将得到

$$\mathcal{A}, \mathcal{B}, \ldots, \mathcal{y}, \mathcal{Z}.$$

公式中也可以使用标准文本，例如使用罗马字体。这里可以使用 \mbox 命令，并将所需文本作为其参数。或者，也可以手动通过 \textrm 切换到罗马字体。请注意，当这些字体用作下标时，其大小会有所不同：

```
    \begin{equation*}
    x_{\textrm{critical}} \quad x_{\mbox{critical}}\,,
    \end{equation*}
```

结果为

$$x_{\textrm{critical}} \quad x_{\mbox{critical}}\,.$$

当使用 amsmath（或仅 amsfonts）宏包时，还可以使用更多字体。这里可以使用哥特体 \mathfrak。黑板体（blackboard font）非常有用，例如可以写出：

```
    \begin{equation*}
    \mathbb{C},\; \mathbb{N},\; \mathbb{R},\; \mathbb{Z}\,,
    \end{equation*}
```

这将生成

$$\mathbb{C}, \mathbb{N}, \mathbb{R}, \mathbb{Z}.$$

到目前为止所讨论的公式都只包含一行。跨越多行的公式可以使用 \begin{eqnarray} ... \end{eqnarray} 环境来生成，也可以使用对应的不带公式编号的 * 版本。每一行由三个部分组成，各部分之间用 & 符号分隔。一行以 \\ 结束。第一部分右对齐，第二部分居中对齐，第三部分左对齐。例如，第 290 页显示的公式就是使用以下代码生成的：

```
\begin{eqnarray}
\sigma^2_1 & = & \frac{ns^2}{\chi^2(1-\alpha/2, n-1)} \nonumber \\
\sigma^2_u & = & \frac{ns^2}{\chi^2(\alpha/2, n-1)}.,
\end{eqnarray}
```

请注意，\nonumber 可以防止在公式的相应行中打印公式编号。最后需要强调的是，美国数学会的 LaTeX 扩展包 amsmath 还提供了多种额外的多行公式环境。

## 9.3.1.6 迷你页、表格和数组

通过水平细分段落，可以创建更多的结构。为此，可以使用 minipage（迷你页）环境。在 minipage 内部，几乎可以放入任何能放到普通页面上的内容，也可以嵌套使用 minipage。从外部来看，minipage 被当作单个符号处理，只不过可能是一个很大的符号。作为示例，我们展示第 15 页列表中某一项的源代码，其中一个小段落和一个小表格并排显示：

```
\begin{minipage}[t]{0.65\textwidth}
Calculates a bitwise OR of the two operands, defined as shown in the table on the right: The result is 1 if $a$ OR $b$ are 1. Hence, for the numbers 201 and 158 one will obtain the result 223 (binary \verb|11011111|).
\end{minipage}
\hfill
\begin{minipage}[t]{0.2\textwidth}
\vspace*{-.1mm}
\begin{tabular}{(cc|c)}
$a$ & $b$ & $a$\verb! & ! $b$\verb! !\\
\hline
0 & 0 & 0\\
0 & 1 & 1\\
1 & 0 & 1\\
1 & 1 & 1
\end{tabular}
\end{minipage}
```

minipage 环境总是接收一个参数，即它的宽度。你可以相对于一些预定义的长度来指定宽度，例如本例中的 \textwidth。另一个重要的长度是 \columnwidth，对于双栏格式（这在科学期刊中相当常见），它大约是 textwidth 的一半。或者，你也可以使用实际单位来指定长度，例如 3cm、30mm 或 15pt，其中 pt 是一个点（point）的大小。

在这里，minipage 使用了可选参数 [t]，表示 minipage 按顶部对齐。其他可选值还有 [b] 和 [c]，分别表示底部对齐和居中对齐。

在第二个 minipage 中使用了一个表格，这也是一个广泛使用的 LaTeX 元素。请注意，整个表格通过 \vspace*{-1mm} 向上移动了。还使用了 \hfill 命令，参见第 9.3.1.2 节。表格使用 tabular 环境定义。它需要将表格的格式作为参数。表格的每一列都必须指定一个格式。在本例中，有两列内容居中（用字母 'c' 表示），接着是一条竖线（'|'），然后是另一列居中内容。其他格式还有左对齐（'l'）和右对齐（'r'）的列。如果某一列总是呈现相同的外观，可以通过 @{ content } 来指定，其中 content 需要替换为实际内容。这也可以是一个空格，例如 @{\hspace*{5mm}}。如果你希望表格周围有边框，还应该在格式行的开头和结尾加上竖线。与 minipage 类似，可以为表格指定 [t]、[b] 或 [c] 选项，分别表示顶部、底部或居中对齐。这样的选项通常可以写在 tabular 和 {...} 参数之间。

接下来是表格的实际条目。每一行不同列的条目之间用 '&' 符号分隔。这里我们有三个列，因此每行需要两个 & 符号。一行以 \\ 结束。如果希望在某一行的下方画一条水平线，可以使用 \hline。对于上面提到的表格边框，你需要在第一行之前和最后一行之后各画一条水平线。请注意，c、r 或 l 格式的每个表格行在打印页面上都限制为一行。要解决这个问题，你可以在条目中放入一个 minipage，正如上面提到的，LaTeX 会将其视为单个符号。由于这有点麻烦，tabular 环境提供了另一种选择：段落列格式。这种格式用格式字母 p 表示，列宽需要作为参数指定，例如 p{0.2\textwidth}。条目将根据给定的宽度进行格式化，可能会跨越多行。此外，还可以创建跨越多列的条目。为此，可以使用 \multicolumn 条目，它接受三个参数：列数、列的格式（与整个表格的格式相同，例如 |c|）以及条目的实际内容。下面的示例表格（本书中未出现）提供了段落格式和多栏格式的使用示例。

