
IComboBox 的基接口是 IControl、ITextBox 和 IListBox。换句话说，上述 IComboBox 接口继承了成员 SetText 和 SetItems 以及 Paint。结束示例]

从构造的泛型类型继承的成员在类型替换后继承。也就是说，成员中的任何构成类型都将基类声明的类型参数替换为类基规范中使用的相应类型参数。[示例：以下代码中

```
interface IBase<T>
{
    T[] Combine(T a, T b);
}
interface IDerived : IBase<string[,]>
{
    // Inherited: string[,] Combine(string[,] a, string[,] b);
}
```

接口 IDerived 在类型参数 T 被替换为 string[,] 后继承 Combine 方法。结束示例]

实现接口的类或结构也隐式地实现了该接口的所有基接口。

部分接口声明 (§15.2.7) 中接口在多个部分上的处理在 §15.2.4.3 中进一步讨论。

接口的每个基接口都应是输出安全的 (§18.2.3.2)。

## 18.3 接口体

接口的 interface-body 定义了接口的成员。

```
interface-body:
    { interface-member-declarationsopt }
```

## 18.4 接口成员

### 18.4.1 通用

接口的成员是继承自基接口的成员以及接口本身声明的成员。

```
interface-member-declarations:
    interface-member-declaration
    interface-member-declarations interface-member-declaration

interface-member-declaration:
    interface-method-declaration
    interface-property-declaration
    interface-event-declaration
    interface-indexer-declaration
```

接口声明声明零个或多个成员。接口的成员应为方法、属性、事件或索引器。接口不能包含常量、字段、运算符、实例构造函数、终结器或类型，也不能包含任何种类的静态成员。

所有接口成员隐式具有公共访问。接口成员声明包含任何修饰符是编译时错误。

interface-declaration 创建一个新的声明空间 (§8.3)，并且 interface-declaration 直接包含的类型参数和 interface-member-declarations 在此声明空间中引入新成员。以下规则适用于 interface-member-declarations：

-   接口声明的类型参数列表中的类型参数的名称应与同一类型参数列表中的所有其他类型参数的名称不同，并且应与接口的所有成员的名称不同。
-   方法的名称应与同一接口中声明的所有属性和事件的名称不同。此外，方法的签名 (§8.6) 应与同一接口中声明的所有其他方法的签名不同，并且同一接口中声明的两个方法不得仅因 ref 和 out 而签名不同。
-   属性或事件的名称应与同一接口中声明的所有其他成员的名称不同。
-   索引器的签名应与同一接口中声明的所有其他索引器的签名不同。

接口的继承成员明确不属于接口的声明空间的一部分。因此，接口允许声明与继承成员具有相同名称或签名的成员。当这种情况发生时，派生接口成员被认为隐藏了基接口成员。隐藏继承成员不被视为错误，但会导致编译器发出警告。为了抑制警告，派生接口成员的声明应包含 new 修饰符以指示派生成员旨在隐藏基成员。此主题在 §8.7.2.3 中进一步讨论。

如果在不隐藏继承成员的声明中包含 new 修饰符，则会发出相应警告。通过移除 new 修饰符可抑制此警告。

[注意：严格来说，class object 中的成员不是任何接口的成员 (§18.4)。然而，class object 中的成员可通过任何接口类型的成员查找 (§12.5) 获得。结束注意]

在多个部分 (§15.2.7) 中声明的接口的成员集合是各部分中声明的成员的并集。接口声明的所有部分的主体共享相同的声明空间 (§8.3)，并且每个成员的范围 (§8.7) 扩展到所有部分的主体。

### 18.4.2 接口方法

接口方法使用 interface-method-declarations 声明：

```
interface-method-declaration:
    attributesopt newopt return-type identifier type-parameter-listopt
        ( formal-parameter-listopt ) type-parameter-constraints-clausesopt ;
```

接口方法声明的属性、return-type、identifier 和 formal-parameter-list 与类 (§15.6) 中的方法声明具有相同的含义。接口方法声明不允许指定方法体，因此声明始终以分号结束。interface-method-declaration 除非同时具有 type-parameter-list，否则不得具有 type-parameter-constraints-clauses。

接口方法的每个形式参数类型应为输入安全 (§18.2.3.2)，并且返回类型应为 void 或输出安全。此外，任何 out 或 ref 形式参数类型也应为输出安全。[注意：即使是 out 参数也要求为输入安全，这是由于常见的实现限制。结束注意]此外，方法任何类型参数上的每个类类型约束、接口类型约束和类型参数约束都应为输入安全。

这些规则确保接口的任何协变或逆变使用仍然是类型安全的。[示例：

```
interface I<out T> { void M<U>() where U : T; }
```

是格式错误的，因为 T 作为 U 的类型参数约束上的使用不是输入安全的。

如果没有此限制，就可能以以下方式违反类型安全：

```
class B {}
class D : B {}
class E : B {}
class C : I<D> { public void M<U>() {...} }
... I<B> b = new C();
b.M<E>();
```

这实际上是对 C.M<E> 的调用。但该调用要求 E 派生自 D，因此这里的类型安全将被违反。结束示例]

### 18.4.3 接口属性

接口属性使用 interface-property-declarations 声明：

```
interface-property-declaration:
    attributesopt newopt type identifier { interface-accessors }
interface-accessors:
    attributesopt get ;
    attributesopt set ;
    attributesopt get ; attributesopt set ;
    attributesopt set ; attributesopt get ;
```

接口属性声明的属性、type 和 identifier 与类 (§15.7) 中的属性声明具有相同的含义。

接口属性声明的访问器对应于类属性声明 (§15.7.3) 的访问器，只是访问器体始终为分号。因此，访问器仅指示属性是读写、只读还是只写。

如果接口属性具有 get 访问器，则其类型应为输出安全；如果具有 set 访问器，则其类型应为输入安全。

### 18.4.4 接口事件

接口事件使用 interface-event-declarations 声明：

```
interface-event-declaration:
    attributesopt newopt event type identifier ;
```

接口事件声明的属性、type 和 identifier 与类 (§15.8) 中的事件声明具有相同的含义。

接口事件的类型应为输入安全。

### 18.4.5 接口索引器

接口索引器使用 interface-indexer-declarations 声明：

```
interface-indexer-declaration:
    attributesopt newopt type this [ formal-parameter-list ] { interface-accessors }
```

接口索引器声明的属性、type 和 formal-parameter-list 与类 (§15.9) 中的索引器声明具有相同的含义。

接口索引器声明的访问器对应于类索引器声明 (§15.9) 的访问器，只是访问器体始终为分号。因此，访问器仅指示索引器是读写、只读还是只写。

接口索引器的所有形式参数类型都应为输入安全。此外，任何 out 或 ref 形式参数类型也应为输出安全。[注意：即使是 out 参数也要求为输入安全，这是由于常见的实现限制。结束注意]

