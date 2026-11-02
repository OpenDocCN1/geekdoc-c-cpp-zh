
代码放在包的 begin 和 end 之间。下面是我们可能如何使用包初始化代码为 Next_Number 赋予初始值：

```ada
package body Serial_Numbers2 is

   Next_Number : Serial_Number;

   procedure Get_Next (Number : out Serial_Number) is
   begin
      Number := Next_Number;
      Next_Number := Next_Number + 1;
   end Get_Next;

begin -- package initialization code
   Next_Number := Serial_Number'First;
end Serial_Numbers2;
```

对于包初始化代码中可以包含什么内容，并没有限制。我们可以调用在那里或任何包中定义的子程序。不过，明智的做法是保持这段初始化代码简单，以尽量减少引发异常的可能性。尽管包初始化代码主要用于初始化变量包的状态（通过初始化其全局变量），但并没有规则禁止在任何具有包体的包中使用它。

精化何时发生？每次调用子程序时，其所有局部声明都会在 begin 之后的代码执行之前完成精化。在这种情况下，局部变量的存储空间在栈上分配，并赋予所有初始值。

程序加载后，每个包规范和包体都会精化一次。包的精化顺序必须遵循一条基本规则：一个单元必须先精化，另一个单元才能使用其中的资源。对于大多数项目，Ada 编译器可以确定合法的精化顺序。然而，使用具有相互依赖关系的包可能会使编译器难以或无法确定精化顺序。Ada 提供了编译指示（pragmas），我们可以用它们向编译器提示正确的顺序。但在某些情况下，可能有必要通过重构程序的设计来消除相互依赖关系。第3.6节提供了关于精化的更多讨论和示例。

## 3.5 子包

Ada 为库单元提供了一种分层命名方案。名为 Apple 的包可以有一个名为 Apple.McIntosh 的子包。Apple 是 McIntosh 的父包。这种命名方案克服了名称唯一性问题，就像分层文件系统允许我们通过将两个同名文件放在不同目录中来区分它们一样。我们已经在 Ada 库中见过这种包名层次结构的示例。Ada 是库中所有预定义单元的父包。Text.IO 是 Ada 的子包，包含用于文本输入和输出的资源。

除了提供用于组织名称的层次结构之外，子单元还提供了重要的信息隐藏特性。我们已经看到私有类型如何用于隐藏抽象数据类型的细节。在我们有界队列类型包的示例中，定义实现的记录和数组对于使用我们队列类型的程序单元是不可访问的。这些客户端必须使用我们在包规范的公有部分中定义的操作（例如 Enqueue）来操作队列对象。然而，私有类型的细节在实现这些操作的包体中是可用的。这些私有细节也可供子包的私有部分和包体使用。这种访问允许一组单元共享私有信息，同时使该信息对外部客户端保持隐藏。<sup>2</sup>

这种共享使我们能够轻松扩展抽象数据类型。事实上，子包是继承和动态分派等面向对象编程特性的关键构造，这些内容超出了本书的范围。让我们看一个示例。下面是一个简单栈类型包的规范：

```ada
package Stacks is
   -- Implements a simple stack of integers (with no safety features)
   type Stack_Type (Max_Size : Positive) is private;

   procedure Clear (Stack : out Stack_Type);
   function Empty (Stack : in Stack_Type) return Boolean;
   procedure Push (Item : in Integer;
                   Stack : in out Stack_Type);
   procedure Pop (Item : out Integer;
                  Stack : in out Stack_Type);
private
   type Stack_Array is array (Positive range <>) of Integer;
   type Stack_Type (Max_Size : Positive) is
      record
         Top : Natural := 0; -- Initialize all stacks to empty
         Items : Stack_Array (1 .. Max_Size);
      end record;
end Stacks;
```

下面是一个子包规范，其中为我们的栈类型新增了一个操作：

```ada
package Stacks.More is
    function Peek (Stack : in Stack_Type) return Integer ;
    -- Returns a copy of the top element on the Stack
end Stacks.More;
```

我们当然可以将函数 Peek 添加到原来的栈包中。然而，对原包进行该更改将要求我们重新编译所有使用它的客户端。当然，我们还想演示子包的一种用法。为此，下面是我们的子包的包体：

```ada
package body Stacks.More is
    function Peek (Stack : in Stack_Type) return Integer is
    begin
        return Stack.Items (Stack.Top);
    end Peek;
end Stacks.More;
```

可以看到，这个包体使用了栈包规范私有部分中给出的栈类型细节。

### 3.5.1 私有子包

包 Stacks.More 是*公有子包*的一个示例。公有子包允许扩展其私有类型并继续保持其私有性，从而为客户端提供额外资源。

在开发子系统时，有时我们希望将其分解为若干部分，同时又不让该子系统的客户端直接访问这些部分。Ada 的私有子包提供了隐藏这些部分的机制。使用私有子包中的资源仅限于以其父包为根的分层包结构。

为了说明私有子包的这一作用，考虑一个飞行管理系统（FMS）。FMS 是驾驶舱软件的一个组件，可自动执行各种飞行中的任务。FMS 的一项主要功能是对飞行计划进行飞行中管理。下面是一个包的大纲，该包向客户端提供对飞行计划的操作：

```ada
package FMS is
    type Flight_Plan is private;
    . . .
    -- Many operations on flight plans
    . . .
```

```ada
private
   -- Hidden details of the flight plan type
   type Flight_Plan is ...
end FMS;
```

导航数据库和位置确定是构成 FMS 的众多组件中的两个。我们飞行管理子系统的客户端无需直接访问这两个组件。它们由客户端调用的 FMS 中的操作来访问。因此，我们将这两个子系统放入私有子包中。下面是这两个私有子包的大纲：

```ada
private package FMS.Navigation_Database is
   ...
end FMS.Navigation_Database;
```

```ada
private package FMS.Positioning is
   ...
end FMS.Positioning;
```

包 FMS 的包体将与这些私有包协同工作，以使用它们的资源。客户端单元不能使用这些包。

让我们再看一层这个 FMS 设计。位置信息通过多个子系统获得，包括全球定位系统、惯性参考系统（IRS）和甚高频全向无线电信标（VOR）。由于这三个子系统是定位系统的组件，我们将它们作为该系统的私有子包。

```ada
private package FMS.Positioning.GPS is
   ...
end FMS.Positioning.GPS;
```

```ada
private package FMS.Positioning.IRS is
   ...
end FMS.Positioning.IRS;
```

```ada
private package FMS.Positioning.VOR is
   ...
end FMS.Positioning.VOR;
```

在本书中，我们在开发分层状态抽象（第4.3.3节和第7.3.3节）、将非 SPARK 代码与遗留 Ada 软件隔离（第8.2节）以及划分未经验证的 SPARK 代码（第9.3.5节）时，使用了私有子包。
