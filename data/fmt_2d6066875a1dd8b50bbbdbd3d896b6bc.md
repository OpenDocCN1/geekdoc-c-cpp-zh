
这使得 `ex:Country` 和 `ex:Person` 类，`ex:Student` 是 `ex:Person` 的子类，而 `ex:Canadian` 准确那些拥有 `ex:nationality` `ex:Canada` 的人。⁷

在 DL 中，属性分为对象属性（如 `ex:nationality`，将个体与其他个体关联）、数据类型属性（如 `ex:age`，将个体与数据值关联）以及注释属性（注释可用于向个体、类和属性添加非中断的信息，如版本控制）。约束可以赋予对象属性和数据类型属性，但不能赋予注释属性。

```
DatatypeProperty(ex:age domain(ex:Person)
    range(xsd:integer))
ObjectProperty(ex:nationality domain(ex:Person)
    range(ex:Country))
```

> ⁷ 关于如何使用 OWL 的更多示例，请参见 OWL 指南 [Smith et al., 2004]。

# 476 I. Horrocks, P. F. Patel-Schneider, D. L. McGinnness, and C. Welty

| 抽象语法 | DL 语法 |
|---|---|
| Class(A partial $C_1 \dots C_n$) | $A \subseteq C_1 \sqcap \dots \sqcap C_n$ |
| Class(A complete $C_1 \dots C_n$) | $A \equiv C_1 \sqcap \dots \sqcap C_n$ |
| EnumeratedClass($o_1 \dots o_n$) | $A \equiv \{o_1\} \cup \dots \cup \{o_n\}$ |
| SubClassOf($C_1$ $C_2$) | $C_1 \subseteq C_2$ |
| DisjointClasses($C_1 \dots C_n$) | $C_1 \cap \dots \cap C_n = \emptyset$ |
| DatatypeProperty($D$) | $D$ |
| ObjectProperty($R$) | $R$ |
| DatatypeProperty($U$) | $U$ |
| Individuals($o$) | $o$ |
| Data Values ($v$) | $v$ |
| inv($R$) | $R^-$ |
| Symmetric($R$) | $R = R^-$ |
| Functional($R$) | $R \le 1$ |
| InverseFunctional($R$) | $R^- \le 1$ |
| Transitive($R$) | $R \circ R \subseteq R$ |

（注：OCR 中的表格根据标准的 DL 映射进行了重建。）

# OWL: 用于语义网的基于描述逻辑的本体语言 475

OWL 对具体值的处理方式与描述逻辑中对具体值的通常处理方式有所不同 [Baader and Hansche, 1991a; Lutz, 2002]，它而是基于 [Horrocks and Sattler, 2001] 中引入的限制更强的具体数据类型。OWL 使用来自 XML Schema 的数据类型作为其具体类型，因此 `owl:integer` 是 OWL 中的一种具体类型，即整数类型。OWL 使用 RDF 语法处理这些具体值，因此 `"2^^xsd:integer"` 字面量是编写整数 2 的方式。OWL 还允许使用 RDF 字面量，它是字符串和可选语言标记的组合。这些普通字面量属于数据类型 `rdfs:Literal`。OWL 同样允许在复杂表达式中使用值集合，如 `oneOf("1^^xsd:integer", "2^^xsd:integer", "3^^xsd:integer")`。

OWL 在公理中使用这些构建描述的结构来提供关于类、属性和个体的信息，如图 14.4 所示。同样，第一列给出类似于框架的抽象语法，第二列给出标准的描述逻辑语法。符号表示与图 14.3 相同。

关于类可以说明部分或完整的信息，如下

```
Class(ex:Country partial owl:Thing)
Class(ex:Person partial owl:Thing)
Class(ex:Student partial ex:Person)
Class(ex:Canadian complete ex:Person)
    hasValue(ex:nationality ex:Canada)
```

这使得 `ex:Country` 和 `ex:Person` 类，`ex:Student` 是 `ex:Person` 的子类，而 `ex:Canadian` 准确那些拥有 `ex:nationality` `ex:Canada` 的人。⁷

在 DL 中，属性分为对象属性（如 `ex:nationality`，将个体与其他个体关联）、数据类型属性（如 `ex:age`，将个体与数据值关联）以及注释属性（注释可用于向个体、类和属性添加非中断的信息，如版本控制）。约束可以赋予对象属性和数据类型属性，但不能赋予注释属性。

```
DatatypeProperty(ex:age domain(ex:Person)
    range(xsd:integer))
ObjectProperty(ex:nationality domain(ex:Person)
    range(ex:Country))
```

> ⁷ 关于如何使用 OWL 的更多示例，请参见 OWL 指南 [Smith et al., 2004]。

# 476 I. Horrocks, P. F. Patel-Schneider, D. L. McGinnness, and C. Welty

| 抽象语法 | DL 语法 |
|---|---|
| Class(A partial $C_1 \dots C_n$) | $A \subseteq C_1 \sqcap \dots \sqcap C_n$ |
| Class(A complete $C_1 \dots C_n$) | $A \equiv C_1 \sqcap \dots \sqcap C_n$ |
| EnumeratedClass($o_1 \dots o_n$) | $A \equiv \{o_1\} \cup \dots \cup \{o_n\}$ |
| SubClassOf($C_1$ $C_2$) | $C_1 \subseteq C_2$ |
| DisjointClasses($C_1 \dots C_n$) | $C_1 \cap \dots \cap C_n = \emptyset$ |
| DatatypeProperty($D$) | $D$ |
| ObjectProperty($R$) | $R$ |
| DatatypeProperty($U$) | $U$ |
| Individuals($o$) | $o$ |
| Data Values ($v$) | $v$ |
| inv($R$) | $R^-$ |
| Symmetric($R$) | $R = R^-$ |
| Functional($R$) | $R \le 1$ |
| InverseFunctional($R$) | $R^- \le 1$ |
| Transitive($R$) | $R \circ R \subseteq R$ |

（注：OCR 中的表格根据标准的 DL 映射进行了重建。）

# OWL: 用于语义网的基于描述逻辑的本体语言 475

OWL 对具体值的处理方式与描述逻辑中对具体值的通常处理方式有所不同 [Baader and Hansche, 1991a; Lutz, 2002]，它而是基于 [Horrocks and Sattler, 2001] 中引入的限制更强的具体数据类型。OWL 使用来自 XML Schema 的数据类型作为其具体类型，因此 `owl:integer` 是 OWL 中的一种具体类型，即整数类型。OWL 使用 RDF 语法处理这些具体值，因此 `"2^^xsd:integer"` 字面量是编写整数 2 的方式。OWL 还允许使用 RDF 字面量，它是字符串和可选语言标记的组合。这些普通字面量属于数据类型 `rdfs:Literal`。OWL 同样允许在复杂表达式中使用值集合，如 `oneOf("1^^xsd:integer", "2^^xsd:integer", "3^^xsd:integer")`。

# 478 I. Horrocks, P. F. Patel-Schneider, D. L. McGuinness, and C. Welty

针对描述逻辑的 TBox，而不是 TBox 和 ABox 的组合。

本体（Ontologies）可以像类、属性和个体一样被赋予注释（annotations）。本体可以拥有本体属性作为注释。大多数本体属性的作用类似于注释属性（即提供未解释的解释），但有一个特殊的属性 `owl:imports` 可用于“导入”其他本体。导入本体实际上是将网页的内容视为当前本体的一部分，如下所示：

```
Ontology(Simple
Annotation(rdf:comment "A simple ontology for nationality")
Annotation(owl:imports http://www.foo.ex/simpler.owl)
```

...

上述导入语句的含义是：`Simple` 本体中的公理集被认为包含了 `simpler.owl` 本体中的公理集。

## 14.3.4 OWL DL 的语义

对于这种使用 OWL 的风格，提供了一种形式化语义，这与描述逻辑提供的语义非常相似（见第 2.2.1 节）。关于该模型理论的完整细节可以在《OWL 语义与抽象语法》[Patel-Schneider et al., 2004] 中找到。

由于 OWL 包含了数据类型（datatypes），因此 OWL 的语义与同样包含数据类型的描述逻辑非常相似，特别是 SHOQ(D)。然而，OWL 中使用的特定数据类型来自 RDF 和 XML Schema 数据类型 [Binon and Malhotra, 2001]。诸如 `"44^^xsd:integer"` 等数据值的含义与其作为 XML 数据值的含义相同。

OWL DL 的语义包含了一些从描述逻辑角度来看可能是不寻常的方面。注释在这里被赋予简单的独立含义，可以以与 RDF 语义兼容的方式与类、属性和个体关联。本体也存在于语义之中，并可以赋予注释信息。最后，`owl:imports` 提供的含义涉及寻找引用的本体（如果可能），并为当前本体的含义增加含义。但在其他方面，OWL 本体的含义应当完全等于根据图 14.3 和 14.4 所示对应关系导出的描述逻辑知识库的含义。

# OWL：一种基于描述逻辑的语义网本体语言 479

因此，使 OWL DL（以及 OWL Lite）成为语义网语言的并不是它的语义（语义对于描述逻辑来说是相当标准的），而是使用 URI 引用作为名称、使用 XML Schema 数据类型作为数据值，以及连接到全球网文档的能力。

## 14.3.5 OWL Lite 和 OWL Full

正如我们所见，OWL DL 与 SHOIN(D) 相关，这是一种表达能力很强的描述逻辑。这种描述逻辑向初级用户展示有些困难，因为可以使用并集（union）和补集（complement）等操作构建复杂的布尔描述。SHOIN(D) 的推理也很困难，因为推理问题具有 NExp 复杂度，而且复杂描述的潜力使得构建编辑器之类的工具变得有些困难。

由于某些原因，人们识别出 OWL DL 的一个子集，该子集在所有指标上都应该更容易处理；这个子集就是 OWL Lite。OWL Lite 禁止并集，将交集限制在类框架类公理的隐式交集中，将所有限制描述限制为类名，不允许个体出现在描述或类公理中，并将基数（cardinalities）限制为 0 或 1。

这些限制使得 OWL Lite 明确等同于 SHIF(D)。在 SHIF(D) 中，OWL Lite 中的关键推理可以在最坏情况指数时间（ExpTime）内计算，并且已经有针对与 OWL Lite 等效逻辑的几种优化推理（见第 14.3.7 节）。这种可行性的提高是以表达能力的相对损失为代价的，尽管 OWL 语法受限制更多，但通过引入新的类名并利用 `allValuesFrom` 和 `someValuesFrom` 限制之间的对偶性，仍然可以表达复杂的描述 (Horrocks and Patel-Schuster, 2003)。例如，OWL Lite 公理：

```
Class(C complete A B)
ObjectProperty(p)
Class(C complete restriction(p allValuesFrom(Nothing)))
Class(D complete restriction(p someValuesFrom(Thing)))
```
