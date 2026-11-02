
一般规则是，如果精化方面（refined aspects）可见，就会使用它们。这包括第 4.3.1 节中提到的 Refined_Global 和 Refined_Depends 方面。

当然，包的客户端不能使用精化后置条件来帮助证明调用上下文中的验证条件。这是一项必要的限制，因为精化后置条件是用客户端无法访问的私有术语编写的。实际上，公共后置条件对精化后置条件进行了净化，使其适合客户端。如果私有信息发生变化，精化后置条件可能必须更新，但公共后置条件捕获了关键设计信息，不需要（也不应该）更改。

如果不使用精化后置条件，则公共后置条件取而代之，并代表关于子程序效果的唯一已知信息，即使对内部调用者也是如此。如果不使用公共后置条件，则将其视为真，这很容易从可能存在的任何精化后置条件中证明。

在 Make_Circle 的早期实现中，SPARK 工具无法证明公共后置条件可由精化后置条件推出。这是因为公共后置条件是用函数 In_Bounds 来编写的，而 SPARK 工具不知道 In_Bounds 对 Circle 的私有组件有什么影响。我们需要给 In_Bounds 添加一个精化后置条件：

```ada
function In_Bounds (C : in Circle) return Boolean
  with
    Refined_Post => In_Bounds'Result =
      (C.Center_X + C.Radius in Coordinate_Type and
       C.Center_X - C.Radius in Coordinate_Type and
       C.Center_Y + C.Radius in Coordinate_Type and
       C.Center_Y - C.Radius in Coordinate_Type)
  is
  begin
    return
      (C.Center_X + C.Radius in Coordinate_Type and
       C.Center_X - C.Radius in Coordinate_Type and
       C.Center_Y + C.Radius in Coordinate_Type and
       C.Center_Y - C.Radius in Coordinate_Type);
  end In_Bounds;
```

精化后置条件断言 In_Bounds 返回的值与其实现给出的值相同。当然，这非常冗余。SPARK 有一条特殊规则，可以在这种情况下提供帮助。当使用表达式函数时（见第 2.2.2 节），表达式函数的函数体自动充当其后置条件。实际上，一个后置条件

```ada
Radius : Radius_Type;
end record;

function In_Bounds (C : Circle) return Boolean is
  (C.Center_X + C.Radius in Coordinate_Type and
   C.Center_X - C.Radius in Coordinate_Type and
   C.Center_Y + C.Radius in Coordinate_Type and
   C.Center_Y - C.Radius in Coordinate_Type);
end Shapes3;
```

现在 SPARK 工具可以证明 Make_Circle 满足其公共后置条件，因为它“知道” In_Bounds 做了什么。此外，在这种情况下，Make_Circle 上不再需要精化后置条件，因为 In_Bounds 以同样可用于内部子程序的方式捕获了所有必要信息。因此，我们绕了一圈又回到了原点，也可以移除 Make_Circle 上的 Refined_Post 方面。

这个故事的寓意是，尽量将公共断言中使用的函数实现为包规范的私有部分或包体中的表达式函数。

我们通过指出私有信息还可能包括包的内部状态（例如包包含的任何全局数据）来结束本节。前面的许多讨论同样适用于公共断言需要访问此类内部状态的情况。然而，在这种情况下，断言中使用的任何函数的实现都需要放在包体中，因为在那里可以访问包的内部状态；仅仅放在规范的私有部分是不够的。

### 6.2.4 *类型不变量*

到目前为止，我们讨论的是附加到子程序上的断言，它们描述与调用子程序相关的条件或与子程序返回值相关的条件。然而，Ada 还允许将断言附加到类型本身。此类断言描述这些类型的所有对象的属性。在本节中，我们描述类型不变量，并给出一些关于 SPARK 未来可能如何支持它们的提示。

在上一节的包 Shapes3 中，使用了一个前置条件来确保在将 Circle 对象传递给函数 Inside_Circle 之前它们是合理的。如果该包提供了许多子程序，那么每个子程序大概都需要为所有 Circle 参数提供类似的前置条件。

另一种方法是，在所有子程序上应用后置条件，以检查它们返回的 Circle 对象是否合理。Make_Circle 函数就是这样做的。由于 Circle 类型是私有的，因此不必同时做这两件事。Circle 只能由包中的子程序更改。如果所有返回圆的子程序都只返回有效的圆，那么接受圆的子程序就可以直接假定它们是有效的。

无论如何，我们试图应用的断言——即所有圆都完全位于工作区内——实际上是对类型 Circle 的限制，而不是与操作圆的那些过程相关的限制。Ada 提供了一种使用类型不变量更直接地表达这一想法的方法。下面的包 Shapes4 规范说明了这种方法：

```ada
pragma SPARK_Mode(On);
package Shapes4 is
   subtype Coordinate_Type is Integer range -100 .. +100;
   subtype Radius_Type is Coordinate_Type range 0 .. 10;
   type Circle is private
     with
       Type_Invariant => In_Bounds (Circle);

   -- Create a circle object.
   function Make_Circle (X, Y : in Coordinate_Type;
                         Radius : in Radius_Type) return Circle;

   -- Return True if X, Y are inside circle C.
   function Inside_Circle (X, Y : in Coordinate_Type;
                           C : in Circle) return Boolean;

   -- Return True if C is entirely in the workspace.
   function In_Bounds (C : in Circle) return Boolean
     with Inline;

private
   type Circle is
     record
       Center_X : Coordinate_Type;
       Center_Y : Coordinate_Type;
       Radius   : Radius_Type;
     end record;

   function In_Bounds (C : in Circle) return Boolean is
     (C.Center_X + C.Radius in Coordinate_Type and
      C.Center_X - C.Radius in Coordinate_Type and
      C.Center_Y + C.Radius in Coordinate_Type and
      C.Center_Y - C.Radius in Coordinate_Type);
end Shapes4;
```

相对于先前的 Shapes3 包，唯一的更改是：关于圆位于工作区内的条件，已从 Inside_Circle 的前置条件和 Make_Circle 的后置条件，移到了 Circle 私有类型的不变量。请注意，在用于类型不变量的表达式中，类型本身的名称 Circle 被用作正在检查的该类型对象的替身。

类型不变量只能应用于私有类型。它们所断言的条件只在实现该类型的包的“边界”处强制执行。在该包内部，对象可能经历不变量暂时为假的中间状态。然而，每当公共子程序返回时都会检查该不变量，以确保包的客户端看到的对象始终处于适当状态。在这方面，类型不变量有点类似于自动应用于所有公共子程序的后置条件。由于 SPARK 目前不支持类型不变量，因此它们的效果在很大程度上可以通过繁琐地定义适当的后置条件来模拟。

当前定义的包 Shapes4 没有为 Circle 对象提供默认初始化。仅仅声明一个 Circle 就可能导致类型不变量失败，因为默认初始化之后也会检查类型不变量，而 Circle 各组成部分的初始值是不确定的。

可以通过简单地向定义 Circle 的记录的各组成部分添加适当的初始化器，来指定合理的默认初始化：

```ada
type Circle is
   record
      Center_X : Coordinate_Type := 0;
      Center_Y : Coordinate_Type := 0;
      Radius   : Radius_Type     := 0;
   end record;
```

现在，一个默认初始化的 Circle 将遵守其不变量。

一旦 SPARK 支持类型不变量，它将在每个需要检查不变量的地方生成验证条件；如果这些条件得到证明，就表明该检查不会失败。

### 6.2.5 子类型谓词

除类型不变量之外，Ada 还允许以子类型谓词的形式将断言应用于非私有类型。在某些方面，子类型谓词类似于约束（例如范围约束），这些约束限制子类型允许的取值。它们在类似的位置接受检查。然而，将子类型谓词描述为断言是很自然的，因为与其他
