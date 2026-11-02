

它可以实现为一个简单的记录数组，其中每条记录存储单个事件的信息；也可以采用更复杂的实现方式。例如，该包可能维护索引，以加快日期簿查询速度；也可能将事件描述打包到某种辅助数据结构中，以节省空间。对于包的用户而言，这些都无关紧要。

但是，包包含由公共子程序访问和修改的内部状态这一事实，对于流分析非常重要。例如，`Add_Event` 通过向日期簿添加新的事件记录来更新内部状态。由于新状态取决于现有状态，`Add_Event` 实际上必须读取现有状态。这意味着，在调用 `Add_Event` 之前，包的内部状态必须已经以某种方式完成初始化。

为了在 SPARK 方面描述内部状态，有必要为该内部状态指定一个名称。不必完整地声明内部状态。事实上，这样做会暴露包所隐藏的信息。包的客户端并不关心内部状态是如何组织的细节。他们只关心内部状态存在这一事实，以及公共子程序如何读取和更新它。因此，只需将内部状态抽象为一个称为状态抽象的单一名称即可。

下面的示例展示了 Datebook 规范的 SPARK 版本。这里引入了名为 `State` 的状态抽象，用于表示包的内部状态：

```ada
with Dates;
package Datebook
  with
    Abstract_State => State
is
  type Status_Type is (Success, Description_Too_Long, Insufficient_Space);

  procedure Add_Event (Description : in String;
                       Date       : in Dates.Datetime;
                       Status     : out Status_Type)
  with
    Global => (In_Out => State),
    Depends => (State =>+ (Description, Date),
                Status => (Description, State));
end Datebook;
```

本例中的名称 `State` 是程序员选择的名称，用于标识包的内部状态。由于我们希望尽可能隐藏该内部状态的性质，因此很难为它指定一个更具描述性的名称。正如第 4.3.2 节所示，有时需要将抽象状态拆分为两个或更多组成部分。在这种情况下，我们会为各组成部分指定能够清楚区分它们的名称。

我们通过描述 `Add_Event` 对包内部状态产生的影响，增强了对它的声明。注意，`State` 被视为一种全局变量。事实上，它正是全局变量。状态抽象表示包内部的全局数据。包的客户端不需要了解这些隐藏数据的细节。他们只需知道包具有状态，以及所调用的子程序会使用和/或更改该状态。

`Add_Event` 上的数据依赖契约和流依赖契约表明，状态取决于日期簿的状态以及输入的描述。日期簿已满或描述过长时，`Add_Event` 可能会失败。

如果包中唯一的公共子程序是前面示例所示的 `Add_Event`，SPARK 工具执行的流分析将报告包的内部状态没有初始化途径。过程 `Add_Event` 要求在调用前 `State` 已具有一个值。那么，`State` 如何获得其初始值呢？

一种方法是提供一个初始化过程。其声明可能如下所示：

```ada
procedure Initialize
  with
    Global => (Output => State),
    Depends => (State => null);
```

该过程不接受任何参数，因为它初始化的是包内部的全局数据。数据依赖契约和流依赖契约通过声明该过程从“无”中为状态抽象赋予一个值，表达了这一点。现在，有了这个过程，就可以先调用 `Initialize`，再正确地调用 `Add_Event`。流分析将确保这一调用顺序确实发生。

在某些情况下，包内部的全局数据无需显式调用过程即可完成初始化。正如第 3.4.1 节所述，可变包的内部状态可以通过适当的静态表达式进行初始化，也可以通过在包体展开时执行的初始化代码进行初始化。在这种情况下，包会自行完成初始化。可以修改包上的方面声明，以反映这种行为，如下例所示：

```ada
with Dates;
package Datebook
  with
    Abstract_State => State,
    Initializes    => State
is
    type Status_Type is (Success, Description_Too_Long, Insufficient_Space);

    -- No Initialize procedure needed
    procedure Add_Event (Description : in String;
                         Date        : in Dates.Datetime;
                         Status      : out Status_Type)
      with
        Global  => (In_Out => State),
        Depends => (State =>+ (Description, Date),
                    Status => (Description, State) );
end Datebook;
```

如果在程序开发过程中，内部状态变得足够复杂，以至于需要一个专门的初始化过程，则可以添加该过程，并移除 `Initializes` 方面。流分析将确保新过程在需要时得到调用。

到目前为止介绍的 `Datebook` 包，是第 3.4 节所讨论的一种可变包。它允许操作单个日期簿变量。在查看 `Datebook` 包体之前，先考虑一种作为类型包的替代实现是有帮助的，如第 3.3 节所述。下面这个名为 `Datebooks` 的版本（注意复数形式）提供了一个 `Datebook` 私有类型，并且没有内部状态。相反，私有类型的组成部分保存每个 `Datebook` 对象的状态。

```ada
with Dates;
package Datebooks is
    type Datebook is private;

    type Status_Type is (Success, Description_Too_Long, Insufficient_Space);

    procedure Add_Event (Book        : in out Datebook;
                         Description : in     String;
                         Date        : in     Dates.Datetime;
                         Status      : out    Status_Type)
      with
        Depends => (Book =>+ (Description, Date),
                    Status => (Description, Book) )
private

    -- Provide a full definition for the private type Datebook

    Maximum_Description_Length : constant := 128;
    subtype Description_Index_Type is
       Positive range 1 .. Maximum_Description_Length;
    subtype Description_Count_Type is
       Natural range 0 .. Maximum_Description_Length;
    subtype Description_Type is String(Description_Index_Type);

    -- Each Event_Record handles exactly one datebook entry.
    type Event_Record is
       record
          Description_Text : Description_Type;
          Description_Size : Description_Count_Type;
          Date             : Dates.Datetime;
          Is_Used          : Boolean;
       end record;

    subtype Event_Index_Type is
       Positive range 1 .. Maximum_Number_Of_Events;
    type Datebook is
       array (Event_Index_Type) of Event_Record;

end Datebooks;
```

在这个版本中，调用者必须创建一个 `Datebook` 对象，并将其显式传递给包中的各个子程序。因此，这些子程序（例如 `Add_Event`）现在必须接受一个额外参数。子程序不再具有数据依赖契约，但针对新参数的流依赖契约，仿照了原始包版本中针对状态抽象所使用的流依赖契约。

这个版本相比前一个版本具有一些优势。首先，它允许客户端创建和操作多个不同的 `Datebook` 对象。其次，`Datebooks` 包没有内部状态，这在多任务环境中具有优势。不过，原始版本更易于使用，因为客户端不需要自行创建日期簿。最合适的方法取决于应用程序的需求。

前面完整展示的私有部分看起来很复杂。但是，原始的 `Datebook` 包也需要在包体中进行类似的声明，以完整定义该包的内部状态。下一节将对此进行更详细的说明。

### 4.3.1 *细化*

使用状态抽象时，包体必须显式声明哪些全局变量以及嵌套包状态（如果存在）共同组成该抽象状态。

