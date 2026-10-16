
某些语言中变量声明中缺少显式数据类型允许代码更简洁，而大多数语言中对递归和动态数据结构的支持为程序员与机器之间提供了额外的抽象层。当然，exclusively 专注于程序员效率可能会损害其他语言原则，例如执行效率和可靠性。

事实上，可靠性本身也可以被视为一种效率问题。不可靠的程序可能带来许多额外成本——隔离或移除错误行为所需的修改、额外的测试时间，加上纠正错误行为影响所需的时间。如果程序不可靠，甚至可能导致开发和编码时间的完全浪费。这种低效率是软件工程中的资源消耗问题。从这个意义上说，程序员效率还取决于发现和纠正错误以及添加新功能的难易程度。以这种方式来看，初始编写代码的难易程度是效率中较不重要的部分。软件工程师估计他们 90% 的时间花在调试和维护上，只有 10% 花在程序的原始编码上。因此，可维护性可能最终是编程语言效率最重要的指标。

在有助于使程序可读和可维护的编程语言特性中，可能最重要的是规则性。我们将在下一节讨论这个问题。

## 2.3 规则性

规则性是一个定义不太明确的质量。一般来说，它指的是语言特性的集成程度如何。更大的规则性意味着对特定构造的使用有更少的异常限制，构造之间有更少的奇怪交互，以及语言特性行为方式上总体上更少的意外。程序员通常将语言的规则性视为理所当然，直到某个特性导致程序以令他们惊讶的方式行为。正因如此，满足规则性标准的语言被认为遵循最小惊讶原则。

通常规则性被细分为三个定义更明确的概念：通用性、正交设计和一致性。语言通过避免构造可用性或使用中的特殊情况，并将密切相关的构造组合成单一更通用的构造来实现通用性。正交是一个借自数学的术语，在数学中它指的是垂直的线。更一般地说，它有时用来指两个在独立方向上移动的事物，或

`function` in completely separate spheres. In computer science, an `orthogonal design` allows language constructs to be combined in any meaningful way, with no unexpected restrictions or behavior arising as a result of the interaction of the constructs, or the context of use. The term `uniformity` refers to a design in which similar things look similar and have similar meanings and, inversely, in which different things look different.

These dimensions of regularity are explained with examples in the following sections. As you will see, the distinctions between the three are sometimes more a matter of viewpoint than actual substance, and you can always classify a feature or construct as irregular if it lacks just one of these qualities.

### 2.3.1 Generality

A language with generality avoids special cases wherever possible. The following examples illustrate this point.

#### Procedures and functions

Function and procedure definitions can be nested in other function and procedure definitions in Pascal. They can also be passed as parameters to other functions and procedures. However, Pascal functions and procedures cannot be assigned to variables or stored in data structures. In C, one can create pointers to functions to treat them as data, but one cannot nest function definitions. By contrast, Python and most functional languages, such as Scheme and Haskell, have a completely general way of treating functions (nested functions definitions and functions as first-class data objects).

#### Operators

In C, two structures or arrays cannot be directly compared using the equality operator `==`, but must be compared element by element. Thus, the equality operator lacks generality. This restriction has been removed in Smalltalk, Ada, Python, and (partially) in C++ and Java. More generally, many languages have no facility for extending the use of predefined operators (like `==` or `+`) to new data types. Some languages, however, such as Haskell, permit overloading of existing operators and allow new operators to be created by the user. In such languages, operators can be viewed as having achieved complete generality.

#### Constants

In Pascal, the values assigned to constants may not be computed by expressions, while in Modula-2, these computing expressions may not include function calls. Ada, however, has a completely general constant declaration facility.

### 2.3.2 Orthogonality

In a language that is truly orthogonal, language constructs do not behave differently in different contexts. Thus, restrictions that are context dependent are considered nonorthogonal, while restrictions that apply regardless of context exhibit a mere lack of generality. Here are some examples of lack of orthogonality:

#### Function return types

In Pascal, functions can return only scalar or pointer types as values. In C and C++, values of all data types, except array types, can be returned from a function (indeed, arrays are treated in C and C++ differently from all other types). In Ada, Python, and most functional languages, this lack of orthogonality is removed.

#### Placement of variable declarations

In C, local variables can only be defined at the beginning of a block (compound statement),¹ while in C++ variable definitions can occur at any point inside a block (but, of course, before any uses).

#### Primitive and reference types

In Java, values of scalar types (`char`, `int`, `float`, and so forth) are not objects, but all other values are objects. Scalar types are called primitive types, whereas object types are called reference types. Primitive types use value semantics, meaning that a value is copied during assignment. Reference types use reference semantics, meaning that assignment produces two references to the same object. Also, in Java, collections of objects are treated differently from collections of primitive types. Among Java’s collections, only arrays can contain primitive values. Primitive values must be placed in special wrapper objects before insertion into other types of collections. In Smalltalk and Python, by contrast, all values are objects and all types are reference types. Thus, these languages use reference semantics only, and collections of objects are treated in an orthogonal manner.

Orthogonality was a major design goal of Algol68, and it remains the best example of a language where constructs can be combined in all meaningful ways.

### 2.3.3 Uniformity

The term uniformity refers to the consistency of appearance and behavior of language constructs. A language is uniform when similar things look similar or behave in a similar manner, but lacks uniformity when dissimilar things actually look similar or behave similarly when they should not. Here are some examples of the lack of uniformity.

#### The extra semicolon

In C++, a semicolon is necessary after a class definition, but forbidden after a function definition:

```
class A { ... } ; // semicolon required
int f() { ... } // semicolon forbidden
```

The reason the semicolon must appear after a class definition is that the programmer can include a list of variable names before the semicolon, if so desired, as is the case with struct declarations in C.

#### Using assignment to return a value

In Pascal, return statements in functions look like assignments to variables. This is a case where different things should look different, but instead look confusingly alike. For example:

```
function f : boolean;
  begin
    ...
    f := true;
  end;
```

Most other languages use a dedicated return statement for returning values from functions.

> ¹The ISO C Standard (ISO 9899 [1999]) removed this restriction.

## 2.3.4 Causes of Irregularities

Why do languages exhibit such irregularities at all? Surely the language designers did not intentionally set out to create strange restrictions, interactions, and confusions. Indeed, many irregularities are case studies in the difficulties of language design.

Take, for example, the problem with the semicolon in the C++ class declaration, noted as a lack of uniformity above. Since the designers of C++ attempted to deviate from C as little as possible, this irregularity was an essential byproduct of the need to be compatible with C. The lack of generality of functions in C and Pascal was similarly unavoidable, since both of these languages opt for a simple stack-based runtime environment (as explained in Chapter 10). Without some restriction on functions, a more general environment would have been required, and that would in turn have compromised the simplicity and efficiency of implementations. The irregularity of primitive types and reference types in Java is also the result of the designer’s concern with efficiency.

On the other hand, it is worth noting that too great a focus on a particular goal, such as generality or orthogonality, can itself be dangerous. A case in point is Algol68. While this language was largely successful in meeting the goals of generality and orthogonality, many language designers believe that these qualities led to an unnecessarily obscure and complex language.
