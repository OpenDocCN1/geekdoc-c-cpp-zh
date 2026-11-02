
状态。这样的实体被称为状态抽象的构成要素，而将状态抽象分解为其构成要素的过程称为细化。在简单情况下，状态抽象可能被细化为单个包全局变量，从而只有一个构成要素。在更复杂的情况下，状态抽象将被细化为多个包全局变量。

例如，假设 Datebook 包是通过记录数组实现的，其中每个记录包含一个事件的信息，类似于 Datebook 包的工作方式。于是该数组就成为状态抽象的唯一构成要素。包体可能部分如下所示：

```ada
package body Datebook
  with
    Refined_State => (State => Event_Array)
is
  -- Provide an appropriate type definition.
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
  type Event_Array_Type is
    array(Event_Index_Type) of Event_Record;

  Event_Array : Event_Array_Type;

  -- Body of add event operation
  procedure Add_Event ...
end Datebook;
```

包体上的 Refined_State 方面指定了包内部哪些全局变量构成先前声明的抽象状态的构成要素。在我们的示例中，抽象状态 State 被细化为单个全局变量 Event_Array。在包规范中存在抽象状态而在包体中未对其进行细化是错误的。

此外，包规范中的数据和流依赖契约必须在包体中进行细化，以明确指定这些子程序对细化状态的影响。这些细化后的契约出现在包体内部，因为它们引用的是包内部的信息。过程 Add_Event 的主体可能是

```ada
procedure Add_Event (Description : in  String;
                     Date        : in  Dates.Datetime;
                     Status      : out Status_Type)
  with
    Refined_Global  => (In_Out => Event_Array),
    Refined_Depends => (Event_Array =>+ (Description, Date),
                        Status      => (Description, Event_Array))
is
  Found     : Boolean; -- Is there an available slot?
  Available : Event_Index_Type := Event_Index_Type'First; -- Location
begin
  -- If the given description won't fit there is no point continuing.
  if Description'Length > Maximum_Description_Length then
    Status := Description_Too_Long;
  else
    -- Search for a free slot in the event array.
    Found := False;
    for Index in Event_Index_Type loop
      if not Event_Array(Index).Is_Used then
        Available := Index;
        Found := True;
        exit; -- We found an available slot in the array
      end if;
    end loop;

    if not Found then
      -- If there is no free slot return an error.
      Status := Insufficient_Space;
    else
      -- Otherwise fill in the free slot with the incoming information.
      -- Need to pad the description with blanks.
      Event_Array(Available).Description_Text := Description &
        (1 .. Maximum_Description_Length - Description'Length => ' ');
      Event_Array(Available).Description_Size := Description'Length;
      Event_Array(Available).Date := Date;
      Event_Array(Available).Is_Used := True;
      Status := Success;
    end if;
  end if;
end Add_Event;
```

请注意，Refined_Global 和 Refined_Depends 方面是根据实际的包全局变量表达的，而不是像在包规范中所做的那样根据状态抽象表达的。

到目前为止的示例显示了状态抽象与单个构成变量之间的一一对应关系。Datebook 包的更复杂的实现可能包含一个索引，允许根据常用字段快速查找事件。在这种情况下，状态抽象可能被细化为两个包全局变量，如下所示：

```ada
package body Datebook
  with
    Refined_State => (State => (Event_Array, Event_Index))
is
  type Event_Array_Type is ...;
  type Event_Index_Type is ...;

  Event_Array : Event_Array_Type;
  Event_Index : Event_Index_Type;
end Datebook;
```

同样，子程序上的细化数据和流依赖契约必须更新，以描述这些子程序对各个构成要素的影响。Add_Event 很可能会同时修改日记本本身及其索引。例如，

```ada
package body Datebook
  with
    Refined_State => (State => (Event_Array, Event_Index))
is
  ...

  procedure Add_Event (Description : in  String;
                       Date        : in  Dates.Datetime;
                       Status      : out Status_Type)
    with
      Refined_Global  => (In_Out => (Event_Array, Event_Index)),
      Refined_Depends => (Event_Array =>+ (Description, Date),
                          Event_Index =>+ (Description, Date),
                          Status      => (Description, Event_Array))
  is
    -- Local variables of Add_Event omitted
  begin
    -- Body of Add_Event omitted
  end Add_Event;

end Datebook;
```

请注意，在这种情况下 Status 不依赖于 Event_Index。推测，Add_Event 的成功或失败不受索引影响。在包规范中，Status 依赖于整体状态抽象 State，因为它依赖于该抽象的一个构成要素，即 Event_Array。

重要的是，新版本的 Datebook 包在不改变包规范的情况下改变了日记本的内部组织。不仅该包的客户端无需重新编译，而且这些客户端的流分析也无需重新进行。当然，包 Datebook 主体的分析确实需要重新进行，导致 SPARK 工具在实施变更的背景下考虑新的细化契约。

### 4.3.2 多个状态抽象

在迄今为止的 Datebook 包的表述中，单个状态抽象用于抽象两个构成要素：日记本本身及其索引。这最大化了从包客户端隐藏的信息量。假设现在想要添加一个用于压缩索引的公共子程序。规范必须更改以包含此子程序并声明它如何与包提供的状态抽象交互。我们将此包命名为 Indexed_Datebook，以告知其用户它与先前描述的 Datebook 包相比具有不同的性质。由于索引现在是公共信息，因此在包的名称中反映该信息是合适的：

```ada
with Dates;
package Indexed_Datebook
  with
    SPARK_Mode  => On,
    Abstract_State => State
is
  type Status_Type is (Success, Description_Too_Long, Insufficient_Space);

  procedure Initialize
    with
      Global  => (Output => State),
      Depends => (State => null);

  procedure Compact_Index
    with
      Global  => (In_Out => State),
      Depends => (State =>+ null);

  procedure Add_Event (Description : in  String;
                       Date        : in  Dates.Datetime;
                       Status      : out Status_Type)
    with
      Global  => (In_Out => State),
      Depends => (State  =>+ (Description, Date),
                  Status => (Description, State));

end Indexed_Datebook;
```

因为 Compact_Index 只更新内部状态，所以它不需要参数。流依赖契约显示新状态仅依赖于旧状态。由于数据依赖契约声明状态的模式为 In_Out，流分析将要求在可以使用 Compact_Index 之前调用包的初始化过程。

然而，使用单个状态抽象有时会在包的子程序之间造成不必要且不期望的耦合。例如，假设事件索引可以直接由包初始化，而不需要初始化过程的帮助。在这种情况下，应该可以在不先调用 Initialize 的情况下调用 Compact_Index。也许某些程序会发现这样做很方便。

这些思想可以通过使用多个状态抽象来表达。下面的规范版本展示了这一点。名称 State 已被放弃，改用两个更具描述性的名称。

```ada
with Dates;
package Indexed_Datebook_V2
  with
    SPARK_Mode  => On,
    Abstract_State => (Book, Index),
    Initializes   => Index
```
