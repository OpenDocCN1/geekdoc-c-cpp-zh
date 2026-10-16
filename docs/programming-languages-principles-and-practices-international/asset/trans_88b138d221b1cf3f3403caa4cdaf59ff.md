

and 是所有推导开始的符号。上下文无关文法定义了一种语言，称为 **文法的语言**。该语言是所有终端符号串的集合，对于这些串，存在一个以起始符号开始并以终端符号串结束的推导。

图 6.2 包含七个终结符（“girl,” “dog,” “sees,” “pets,” “the,” “a,” 和 “.”）、六个非终结符和六条产生式。该文法定义的语言也是有限的，这意味着该语言中只能推导出有限个句子（参见练习 6.8），但通常文法定义的语言不是有限的。

通常上下文无关文法中的产生式数量与非终结符数量相同，尽管可以通过为每个选择单独书写来消除 “|” 元符号，例如：

```
noun → girl
noun → dog
```

在这种情况下，每个非终结符对应的产生式数量与选择的数量一样多。

为什么这样的文法是 **上下文无关** 的？简单的原因是非终结符在产生式的左部单独出现。这意味着无论非终结符出现在何处，都可以用任意右部选择来替换它。换句话说，不存在 **上下文** 使得只有某些替换可以发生。例如，在刚刚讨论的文法中，只有在主语为 “girl” 时使用动词 “pets” 才有意义；这可以被视为一种上下文敏感性。我们可以通过允许上下文串出现在文法规则的左部来写出上下文敏感文法。一些作者认为上下文敏感性纯粹是句法问题。然而，我们将采用这样的观点：任何不能用上下文无关文法表达的东西都是语义问题，而不是句法问题。（即使有些可以用上下文无关文法表达的东西，通常也最好留给语义描述，因为它们涉及编写许多额外的产生式；参见练习 6.30。）

作为上下文敏感性的一个例子，回想一下，在前面的文法中，句子开头的冠词应大写。一种实现方法是重写第一条规则为：

```
sentence → beginning noun-phrase verb-phrase ‘.’
```

然后添加上下文敏感规则：

```
beginning article → The | A
```

现在推导将如下所示：

```
sentence ⇒ beginning noun-phrase verb-phrase . (new rule 1)
⇒ beginning article noun verb-phrase . (rule 2)
⇒ The noun verb-phrase . (new context-sensitive rule)
⇒ . . .
```

上下文无关文法已被形式语言理论家广泛研究，现在已被如此透彻地理解，以至于用 BNF 形式表达任何编程语言的语法变得自然。事实上，这样做使得更容易为该语言编写翻译器，因为分析阶段可以自动化，正如你在第 6.6 节中将学到的那样。

上下文无关文法在编程语言中使用的一个典型简单例子是图 6.4 中给出的简单整数算术表达式的加法和乘法描述。

```
expr → expr + expr | expr * expr | ( expr ) | number
number → number digit | digit
digit → 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

注意规则的递归性质：一个表达式可以是两个表达式的和或积，每个表达式本身可以是进一步的和或积。当然，最终这个过程必须通过选择 *number* 备选方案而停止，否则我们永远不会得到一个终端符号串。

还要注意 *number* 规则中的递归用于生成重复的数字序列。例如，数字 234 的构造如图所示 6.5。

```
number ⇒ number digit
       ⇒ number digit digit
       ⇒ digit digit digit
       ⇒ 2 digit digit
       ⇒ 23 digit
       ⇒ 234
```

这个过程实际上可以由扫描器执行，正如我们在上一节中指出的那样，因为它只处理字符序列。事实上，上述文法的终结符仅为单个字符标记，如 + 和 9，并且忽略了空白问题。我们将在第 6.7 节中回到这个问题，但为了简单起见，我们暂时忽略扫描问题。

作为 BNF 中文法的更复杂示例，图 6.6 显示了 C 语言 BNF 描述的开始。

```
translation-unit → external-declaration
                | translation-unit external-declaration

external-declaration → function-definition | declaration

function-definition → declaration-specifiers declarator
                      declaration-list compound-statement
                    | declaration-specifiers declarator compound-statement
                    | declarator declaration-list compound-statement
                    | declarator compound-statement

declaration → declaration-specifiers ‘;’
            | declaration-specifiers init-declarator-list ‘;’

init-declarator-list → init-declarator
```

```
init-declarator-list → init-declarator

init-declarator → declarator | declarator '=' initializer
declarator → pointer direct-declarator | direct-declarator

pointer → '*' type-qualifier-list pointer | '*' type-qualifier-list
        | '*' pointer | '*'

direct-declarator → ID
                  | '(' declarator ')'
                  | direct_declarator '[' ']'
                  | direct_declarator '[' constant_expression ']'
                  | direct_declarator '(' parameter_type_list ')'
                  | direct_declarator '(' identifier_list ')'
                  | direct_declarator '(' ... ')'
                  | ...
                  | ...
```

图 6.6 C 的部分 BNF（改编自 Kernighan 和 Ritchie [1988]）

解释 BNF 规则如何构造语言的字符串的另一种方法是如下。给定一个文法规则，例如：

$expr \rightarrow expr + expr \mid number$

（取自图 6.4），设 E 为表示表达式的字符串集合，N 表示表示数字的字符串集合。前述文法规则可以被视为一个 **集合方程**：

$E = E + E \cup N$

其中 E + E 是通过将 E 中所有字符串与 “+” 符号连接然后再与 E 中所有字符串连接而构造的集合，“∪” 表示集合并。假设集合 N 已构造，则这表示集合 E 的递归方程。*满足该方程的最小集合 E* 可以被视为文法规则定义的集合。直观上，这由集合组成：

$N \cup N + N \cup N \cup N + N \cup N + N + N \cup \ldots$

在练习 6.53 中，你将有机会证明这是满足给定方程的最小集合。递归方程的解在编程语言的形式描述中经常出现，并且是编程语言理论研究的主要对象。

## 6.3 语法树和抽象语法树

语法建立结构，而不是意义，但句子的意义（或程序）与其语法相关。例如，在英语中，一个句子有主语和谓语。这些是语义概念，因为主语（“执行者”）和谓语（“动作”）决定了句子的意义。主语通常出现在句子的开头，并由名词短语给出。因此，在英语句子的语法中，名词短语被放在第一位，随后与主语相关联。类似地，在表达式的文法中，当我们写：

$expr \rightarrow expr + expr$

我们期望将两个右部表达式的值相加以得到左部表达式的值。将构造的语义与其句法结构关联起来的过程称为 **语法制导语义**。因此，我们必须构造语法，使其尽可能反映我们最终将附加的语义。（语法制导语义同样可以称为语义制导语法。）

为了利用程序的句法结构来确定其语义，我们必须有一种表达由推导确定的这种结构的方法。一种标准方法是使用 **语法树**，它是推导中替换过程的图形表示。例如，句子 “the **girl** sees a dog.” 的语法树如图 6.7 所示。

![](img/062750ade02e28185b1fb8e8cf6dc89e_220_0.png)

**图 6.7：** 句子 “the **girl** sees a dog.” 的语法树

类似地，表达式文法中数字 234 的语法树如图 6.8 所示。

![](img/062750ade02e28185b1fb8e8cf6dc89e_220_1.png)

**图 6.8：** 数字 234 的语法树

语法树在内部节点（至少有一个子节点的节点）处标记为非终结符，在叶节点（没有子节点的节点）处标记为终结符。语法树的结构完全由语言的文法规则和特定终端序列的推导指定。文法规则指定

