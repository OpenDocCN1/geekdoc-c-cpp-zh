

# Expressions 75

## 示例 20 继承成员优于嵌套类型的成员

C 中的调用 M() 触发了方法 B.M()，因为 C 的成员（即使是继承而来的）也优于其嵌套类的成员。如果 B.M() 是私有的，则它不会被 C 继承，而是会调用方法 E.M()。此外，如果 B.M(int) 是公开的，则 C 拥有一个可访问的方法 M(int)，此时嵌套类的成员将不再忽略，但 B.M(int) 并不适用，因此调用 M() 是非法的。

```csharp
class B {
    public static void M() { Console.WriteLine("B.M"); }
    private static void M(int i) { Console.WriteLine("B.M(int)"); }
}
class E {
    static void M() { Console.WriteLine("E.M"); }
    static void M(int i) { Console.WriteLine("E.M(int)"); }
}
class C : B {
    public static void Main(String[] args) { M(); }
}
```

## 示例 91 调用非重载、非重写的方法

此程序使用了 Apoint 类（示例 44）。静态方法 GetSize 和 GetPoint 只能通过类名 Apoint 前缀来调用。它们可以在任何 Apoint 类的对象创建之前被调用。实例方法 GetIndex 通过对象调用，即 r.GetIndex()；该方法在执行时将当前对象绑定到 r。

```csharp
Console.WriteLine("Number of points created: " + Apoint.GetSize());
Apoint p = new Apoint(12, 123), q = new Apoint(200, 10), r = new Apoint(99, 12);
Apoint s = p;
q = null;
Console.WriteLine("Number of points created: " + Apoint.GetSize());
Console.WriteLine("r is point number " + r.GetIndex());
for (int i=0; i<Apoint.GetSize(); i++)
    Console.WriteLine("Apoint number " + i + " is " + Apoint.GetPoint(i));
```

## 示例 92 调用重载方法

类 52 中四个方法的重载解析可以解释如下：调用 M(10, 20) 的签名是 M(int, double)，因此调用了签名为 M(int, double) 的方法，这是最适用的一个；同样对于 M(10.0, 20.0) 和 M(10.0, 20.0)，最适用的签名是 M(double, double)。

## 示例 93 “优”与“最佳”签名

- M(int,int) 优于 M(double, double)。M(double, double), ...
- M(long,long) 优于 M(ulong, long)。M(ulong, long)。M(float, long), ...
- M(double,int) 不优于 M(int, double)，反之亦然。
- 集合 M(double, int).M(int, int) 具有最佳签名 M(int, int)。
- 集合 M(double, int).M(int, double) 没有最佳签名。

# 表达式

### 12.17.2 方法调用：运行时按值、ref 或 out 传参

本节和下一节涵盖了当明确调用方法 M 时对方法调用 M(actual-list) 的运行时求，并侧重于传参机制。

调用通过从左到右评估实际参数列表（actual-list）来获取参数值。这些参数值随后按照出现顺序与方法形式参数列表（formal-list）中的对应参数关联。

按值传递的参数没有标记 ref 或 out。按值参数的类型必须能够隐式转换为（第 5 节）方法对应形式参数的类型。在方法调用的执行期间，转换后的值绑定到形式参数上，这类似于局部变量。对于简单类型和结构体的形式参数，这意味着如果方法更改了形式参数的值，不会影响参数表达式的值。对于引用类型参数，这意味着形式参数指向与参数相同的对象或数组，该对象或数组的更改在方法返回后是可见的（示例 94）。

ref 参数必须是一个变量、只读字段或数组访问 a[i]；它表示一个存储位置。该存储位置在调用之前必须被赋值。ref 参数表达式必须与方法的对应形式参数完全相同。在方法调用期间，作为参数的表达式会修改存储位置。

out 参数与 ref 参数非常相似。不同在于 out 参数在调用之前不需要被赋值，且方法中的每条执行路径都必须为形式参数赋值。

当参数值绑定到形式参数后，执行方法体。如果方法的返回类型非 void，则方法调用表达式的值为方法的返回值。如果方法的返回类型为 void，则方法调用没有值。方法返回时，所有的参数和局部变量都会丢弃。

### 12.17.3 方法调用：参数数组

方法、构造函数或索引器的形式参数列表可以以数组结尾：由 params 修饰符引导的形式类型数组（第 10.7 节）。假设该参数声明为 params t[]。在这种方法中，符合 t 的实际参数可以是零或多个隐式转换为 t 的按值参数。在这种情况下，会分配一个新的数组 t[]，参数表达式被求值并转换，转换后的值存储在数组中，形式参数 xs 绑定到新创建的数组。

对于重载解析，如 Max(int, int) 等显式重载优于形式参数数组的扩展 Max(params int[])。形式参数数组的扩展优于需要隐式转换的签名（示例 54 和 95）。

**示例 94 类型和数组的按值和引用传递**
调用 M(d1, ref d2, a1, ref a2) 传递了一个 double、一个持有 double 的变量 d2 的引用、一个数组以及一个持有数组的变量 a2 的引用。

```csharp
double d1 = 1.1, d2 = 2.2;
int[] a1 = new int[4], a2 = new int[4];
M(d1, ref d2, a1, ref a2);
...
static void M(double dd1, ref double dd2, int[] aa1, ref int[] aa2) {
  dd1 = 3.3; dd2 = 4.4;
  aa1[0] = 17;
  aa2[0] = 18;
  aa2 = new int[3];
}
```

实线表示方法调用前的状态，虚线由参数传递引起，点线表示方法返回后的状态。

| 在 M 中: | 在 Main 中: | 堆中: |
|---|---|---|---|
| d1 | 3.3 | | |
| d2 | 4.4 | | |
| aa1 | | 17 | 0 | 0 | 0 |
| aa2 | | 18 | |实线表示方法调用前的状态，虚线由参数传递引起，点线表示方法返回后的状态。

| 在 M 中: | 在 Main 中: | 堆中: | |
|---|---|---|---|
| d1 | 3.3 | | |
| d2 | 4.4 | | |
| aa1 | | 17 | 0 | 0 | 0 |
| aa2 | | 18 | |实线表示方法调用前的状态，虚线由参数传递引起，点线表示方法返回后的状态。

**示例 95 调用带参数数组的方法**
此示例展示了对 Max(int, int) 的调用。对于一个和四个参数，调用 params 重载是因为因为它优。对于两个参数，调用的是显式重载。

### 12.17.4 方法调用的编译时处理

所有方法都可以重载，实例方法都可以重写。虚方法的重写由运行时根据对象的运行时类处理（第 12.17.5 节）。

#### 编译时步骤 1：寻找候选方法

第一步是寻找一组候选方法。候选方法 TT.M(sig) 的概念包含了包含其名称 M 的 TT 及其签名。

如果调用的形式为 M(actual-list)，候选方法是在（声明或继承）成员 M 的嵌套类中命名的方法。或者，如果嵌套类中的成员 M 不是方法，则该调用是非法的。

如果调用的形式为 base.M(actual-list)，候选方法是当前类基类中名为 M 的非私有方法。

如果调用的形式为 C.M(actual-list)，其中 C 是类或结构体类型，候选方法是 C 中可访问的方法 M。

如果调用的形式为 o.M(actual-list)，其中表达式 o 的编译类型是类或结构体类型，候选方法是该编译类型中可访问的方法 M。

如果调用的形式为 o.M(actual-list)，该接口是接口方法调用，将在运行时特殊处理（第 12.17.5 节）。

#### 编译时步骤 2：寻找最佳适用方法

第二步是寻找适用的候选方法，然后从这些方法中找到最佳（最具体的）的一个。

候选方法是适用的，如果其形式参数列表的长度与实际参数列表相同，对应位置的参数传递方式一致（按值或 ref），对应类型相同，并且对于按值位置，从参数类型可以隐式转换为对应形式参数的类型。此外，一个形式参数列表以参数数组 t[] xs 结尾的候选方法，如果将参数数组替换为零或多个 t 类型的按值参数可以使其适用，且没有相应签名的调用，则它是适用的。

