

为了便于标识符的处理，Parser 类定义了另外两个新方法，enterId 和 findId。这些方法现在在语法规则的所有地方被调用，在这些地方解析器期望消费标识符。每个方法首先检查 token 的 code 以确定它确实是一个标识符，如果不是，则注册一个致命错误（这与第 6 章的原始语法分析器没有变化）。否则，该方法将在符号表中进入或查找标识符，然后消费该 token。以下是这两个 Parser 方法的代码：

```
private SymbolEntry enterId(){
    SymbolEntry entry = null;
    if (token.code == Token.ID)
        entry = table.enterSymbol(token.string);
    else
        fatalError("identifier expected");
    token = scanner.nextToken();
    return entry;
}

private SymbolEntry findId(){
    SymbolEntry entry = null;
    if (token.code == Token.ID)
        entry = table.findSymbol(token.string);
    else
        fatalError("identifier expected");
    token = scanner.nextToken();
    return entry;
}
```

我们用每个新的作用域分析方法的一些使用示例来结束本小节。Parser 方法 subprogramBody 和 subprogramSpecification 协同处理 TinyAda 过程声明。在 subprogramBody 的末尾，解析器必须退出 TinyAda 过程的局部作用域。解析器也可能在此短语末尾遇到一个可选的过程标识符，因此该标识符必须在刚刚恢复的外层作用域中查找。以下是 subprogramBody 的修订代码：

```
/*
subprogramBody =
    subprogramSpecification "is"
    declarativePart
    "begin" sequenceOfStatements
    "end" [ <procedure>identifier ] ";"
*/
private void subprogramBody(){
    subprogramSpecification();
    accept(Token.IS, "'is' expected");
    declarativePart();
    accept(Token.BEGIN, "'begin' expected");
    sequenceOfStatements();
    accept(Token.END, "'end' expected");
    table.exitScope();                         // The nested scope ends here
    if (token.code == Token.ID)                // Look up procedure's ID
        findId();
    accept(Token.SEMI, "semicolon expected");
}
```

我们最后一个示例方法 subprogramSpecification 处理 TinyAda 过程头。该方法应看到过程名称的声明，该名称被进入当前作用域。该方法也可能看到形式参数声明，因此它进入一个新的作用域，如下定义所示。

```
/*
   subprogramSpecification = "procedure" identifier [ formalPart ]
*/
private void subprogramSpecification(){
    accept(Token.PROC, "'procedure' expected");
    enterId();
    table.enterScope();                    // Nested scope begins here
    if (token.code == Token.L_PAR)
        formalPart();
}
```

在调用 formalPart 之前进入的作用域在过程声明中更下方其他局部声明中仍然有效。对解析方法的剩余修改留给读者作为练习。

请注意，在示例中对 enterId 和 findId 方法的使用丢弃了这些方法返回的 SymbolEntry 对象。解析器对于作用域分析并不真正需要此对象。然而，我们将在下一节和后面的章节中展示如何使用它来执行进一步的语义检查。

## 7.8.2 标识符角色分析

在大多数高级语言中，一个标识符命名某个实体，例如变量、常量或整个数据类型。我们称标识符的此属性为其角色。你不应将标识符的角色与其值或其数据类型混淆，后两者也是额外的属性。事实上，TinyAda 标识符的角色出现在第 6.8 节 EBNF 语法中的语义限定符（在尖括号中）中。标识符的角色对其使用施加了某些限制。例如，只有变量或参数标识符可以出现在赋值语句的左侧，而只有类型标识符可以作为数组的元素类型。如果在这些位置发现具有其他角色的标识符，则应将其标记为语义错误。

标识符如何获得角色呢？它在声明中获得角色，在那里解析器有足够的上下文信息来确定它。但随后解析器如何在标识符使用时很久之后检查此角色呢？标识符的角色与其一起保存在符号表中，在需要时可以访问它。就像作用域分析一样，角色分析使用符号表在否则独立的解析方法之间共享关于标识符的上下文信息。²³

角色分析需要对 SymbolEntry 类和 Parser 类进行修改。SymbolEntry 对象现在除了 name 字段外还包括一个 role 字段。角色的可能值在此类中定义为常量。它们包括 CONST、VAR、TYPE、PROC 和 PARAM，具有明显的含义。除了这个新属性及其可能的值之外，SymbolEntry 类还定义了两个新方法，setRole 和 append。我们稍后会看到它们如何使用。

解析器在标识符被声明时设置 SymbolEntry 对象的适当角色。例如，方法 typeDeclaration 在 TinyAda 程序中引入一个新的类型名。因此，在名称进入符号表后，角色 TYPE 被进入该名称的 SymbolEntry 中，如下所示：

```
/*
typeDeclaration = "type" identifier "is" typeDefinition ";"
*/
private void typeDeclaration(){
    accept(Token.TYPE, "'type' expected");
    SymbolEntry entry = enterId();
    entry.setRole(SymbolEntry.TYPE);    // Establish the ID's role as TYPE
    accept(Token.IS, "'is' expected");
    typeDefinition();
    accept(Token.SEMI, "semicolon expected");
}
```

TinyAda 程序中的其他类型名包括内置数据类型，它们在表创建时进入符号表。

为了访问和检查标识符的角色，解析器只需在符号表中查找标识符后查看其 SymbolEntry。如果找到的角色与预期角色不匹配，解析器打印错误消息并继续处理。有时，一个短语可以允许具有不同角色的标识符。例如，变量、参数和常量可以出现在表达式中，但类型名或过程名不可以。

实用方法 acceptRole 接受一个 SymbolEntry、一个错误消息以及一个角色或一组角色作为参数，执行所需的角色检查。以下是此方法及其在解析方法 index 中的使用的代码。请注意，acceptRole 方法对单个角色和一组角色进行了重载。

```
private void acceptRole(SymbolEntry s, int expected, String errorMessage){
    if (s.role != SymbolEntry.NONE && s.role != expected)
        chario.putError(errorMessage);
}

private void acceptRole(SymbolEntry s, Set<Integer> expected,
                        String errorMessage){
    if (s.role != SymbolEntry.NONE && ! (expected.contains(s.role)))
        chario.putError(errorMessage);
}

/*
index = range | <type>name
*/
private void index(){
    if (token.code == Token.RANGE)
        range();
    else if (token.code == Token.ID){
        SymbolEntry entry = findId();
        acceptRole(entry, SymbolEntry.TYPE, "must be a type name");
    }
    else
        fatalError("error in index type");
}
```

acceptRole 方法测试 entry 的角色是否为值 SymbolEntry.NONE。如果标识符甚至未在符号表中找到，这将是其角色。因此，在这种情况下不应报告角色错误。

一些 TinyAda 声明，例如 index，引入单个标识符，而另一些，例如 parameterSpecification 和 enumerationTypeDefinition，引入标识符列表。为了简化属性的输入，所有这些属性对于标识符列表都是相同的，SymbolEntry 类现在包括一个 next 字段，可作为指向列表中下一个标识符条目的链接的用途。为了构建此列表，解析器获取列表中第一个标识符的条目并运行 SymbolEntry 方法 append，将每个剩余标识符的条目附加到列表中。SymbolEntry 方法 setRole 然后可以在条目列表中设置相同的角色。解析方法 enumerationTypeDefinition 和 identifierList 展示了此机制的工作方式。identifierList 方法现在返回一个 SymbolEntry 对象，它实际上是 SymbolEntry 对象的列表的头。enumerationTypeDefinition 方法接收此对象并设置其角色，就像它代表单个标识符一样。以下是这两个解析方法的代码：

> ²³ 请注意，像 Ada 这样的实际语言的解析器通常不依赖符号表来执行超出作用域分析的静态语义分析。相反，它们在语法分析期间生成解析树，然后遍历该树以安装和访问语义信息以供进一步处理。这种类型的策略是编译器构造课程的主题。

