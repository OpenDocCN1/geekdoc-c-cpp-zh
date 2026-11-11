
知道它将从哪个任务接收消息的名称。这种不对称性与被称为 CSP（即通信顺序进程，Hoare，1978）的语言设计形成对比。在 CSP 中，也使用消息传递并发模型，任务仅接受来自显式命名任务的消息。其缺点是，无法构建供通用使用的任务库。

描述任务 A 向任务 B 发送消息所导致的会合的常用图形方法如图 13.5 所示。

**图 13.5**

由任务 A 向任务 B 发送消息引起的会合的图形表示

![](img/e22931b583977bc24a4263ee43d0f0bb_592_0.png)

任务在包、子程序或块的声明部分中声明。静态创建的任务与附加该声明部分的代码中的语句同时开始执行。例如，在主程序中声明的任务与主程序代码体中的第一条语句同时开始执行。任务终止是一个复杂问题，将在本节后面讨论。

任务可以有任意数量的入口。相关联的 **accept** 子句在任务中出现的顺序决定了可接受消息的顺序。如果一个任务有多个入口点，并且要求它们能够以任意顺序接收消息，则该任务使用 **select** 语句将这些入口包围起来。例如，假设一个任务模拟银行出纳员的活动，该出纳员必须在银行内的步行服务台服务客户，并且还必须在驾车窗口服务[^2]客户。下面这个骨架式出纳员任务说明了 select 结构：

```ada
task body Teller is
begin
  loop
    select
      accept Drive_Up (formal parameters) do
        ...
      end Drive_Up;
      ...
    or
      accept Walk_Up (formal parameters) do
        ...
      end Walk_Up;
      ...
    end select;
  end loop;
end Teller;
```

在这个任务中，有两个 accept 子句：Walk_Up 和 Drive_Up，每个子句都有一个关联队列。select 执行时的动作是检查与这两个 accept 子句关联的队列。如果其中一个队列为空，而另一个队列至少包含一条等待消息（客户），则与这条或这些等待消息相关联的 accept 子句将与发送所接收第一条消息的任务进行会合。如果两个 accept 子句的队列都为空，则 select 等待直到其中一个入口被调用。如果两个 accept 子句的队列都非空，则不确定地选择其中一个 accept 子句与其某个调用者进行会合。循环强制 select 语句反复执行，永不停息。

accept 子句的结束标记着对 accept 子句形式参数进行赋值或引用的代码的结束。一个 accept 子句与下一个 or（如果该 accept 子句是 select 中的最后一个，则为 end select）之间的代码（如果有）称为扩展 accept 子句。扩展 accept 子句仅在其关联的（紧接其前的）accept 子句执行之后才执行。扩展 accept 子句的这种执行不属于会合的一部分，并且可以与调用任务的执行并发进行。发送方在会合期间被挂起，但当到达 accept 子句末尾时，它会被放回就绪队列。如果一个 accept 子句没有形式参数，则不需要 do-end，并且该 accept 子句可以完全由扩展 accept 子句组成。这种 accept 子句将专门用于同步。扩展 accept 子句在第 13.6.3 节的 `Buf_Task` 任务中说明。

[^2]: 任务也可以动态创建，但此处不讨论此类任务。

若一个任务有嵌套任务，则该嵌套任务也可以访问共享结构，这可能会破坏数据的完整性。因此，用于控制对共享数据结构访问的任务不应定义任务。

下面是一个 Ada 任务示例，它实现了一个用于缓冲区的监视器。该缓冲区的行为与第 13.3 节中的缓冲区非常相似，后者使用信号量控制同步。

```ada
task Buf_Task is
    entry Deposit(Item : in Integer);
    entry Fetch(Item : out Integer);
end Buf_Task;

task body Buf_Task is
    Bufsize : constant Integer := 100;
    Buf     : array (1..Bufsize) of Integer;
    Filled  : Integer range 0..Bufsize := 0;
    Next_In,
    Next_Out : Integer range 1..Bufsize := 1;
begin
    loop
        select
            when Filled < Bufsize =>
                accept Deposit(Item : in Integer) do
                    Buf(Next_In) := Item;
                end Deposit;
                Next_In := (Next_In mod Bufsize) + 1;
                Filled := Filled + 1;
        or
            when Filled > 0 =>
                accept Fetch(Item : out Integer) do
                    Item := Buf(Next_Out);
                end Fetch;
                Next_Out := (Next_Out mod Bufsize) + 1;
                Filled := Filled - 1;
        end select;
    end loop;
end Buf_Task;
```

在这个示例中，两个 **accept** 子句都是扩展的。这些扩展子句可以与调用相关联的 **accept** 子句的任务并发执行。

可以使用 `Buf_Task` 的生产者任务和消费者任务具有以下形式：

```ada
task Producer;
task Consumer;
task body Producer is
    New_Value : Integer;
begin
    loop
        -- produce New_Value --
        Buf_Task.Deposit(New_Value);
    end loop;
end Producer;

task body Consumer is
    Stored_Value : Integer;
begin
    loop
        Buf_Task.Fetch(Stored_Value);
        -- consume Stored_Value --
    end loop;
end Consumer;
```

### 13.6.4 受保护对象

正如我们所见，可以通过将数据封装在任务中并仅允许通过任务入口访问来控制对共享数据的访问，任务入口隐式提供竞争同步。这种方法的一个问题是难以高效实现会合机制。Ada 95 的受保护对象提供了一种无需涉及会合机制即可提供竞争同步的替代方法。

受保护对象不是任务；它更像第 13.4 节所述的监视器。受保护对象可以通过受保护子程序访问，也可以通过语法上类似于任务中 accept 子句的入口访问。[^3] 受保护子程序可以是受保护过程，它对受保护对象的数据提供互斥的读写访问；也可以是受保护函数，它对该数据提供并发只读访问。入口与受保护子程序的区别在于入口可以带有卫式。

在受保护过程的主体中，封闭受保护单元的当前实例被定义为变量；在受保护函数的主体中，封闭受保护单元的当前实例被定义为常量，这允许并发只读访问。

对受保护对象的入口调用提供与使用同一受保护对象的一个或多个任务的同步通信。这些入口调用提供的访问类似于对封装在任务中的数据提供的访问。

上一小节中用任务解决的缓冲区问题，可以用受保护对象更简单地解决。注意，此示例不包括受保护子程序。

```ada
protected Buffer is
    entry Deposit(Item : in Integer);
    entry Fetch(Item : out Integer);
private
    BufSize : constant Integer := 100;
    Buf     : array (1..BufSize) of Integer;
    Filled  : Integer range 0..BufSize := 0;
    Next_In,
    Next_Out : Integer range 1..BufSize := 1;
end Buffer;

protected body Buffer is
    entry Deposit(Item : in Integer)
        when Filled < BufSize is
    begin
        Buf(Next_In) := Item;
        Next_In := (Next_In mod BufSize) + 1;
        Filled := Filled + 1;
    end Deposit;
    entry Fetch(Item : out Integer) when Filled > 0 is
    begin Item := Buf(Next_Out);
        Next_Out := (Next_Out mod BufSize) + 1;
        Filled := Filled - 1;
    end Fetch;
end Buffer;
```

[^3]: 受保护对象主体中的入口使用保留字 *entry*，而不是任务主体中使用的 *accept*。

### 13.6.5 评价

使用通用的消息传递并发模型来构造监视器，就像使用 Ada 包来支持抽象数据类型一样——两者都是比实际需要更通用的工具。受保护对象是提供对共享数据同步访问的更好方法。

在没有具有独立存储器的分布式处理器的情况下，在并发环境中，作为实现共享数据同步访问的手段，在监视器和采用消息传递的任务之间进行选择，在某种程度上是个人偏好问题。然而，在 Ada 的情况下，受保护对象在支持对共享数据的并发访问方面显然优于任务。不仅代码更简单，而且效率也高得多。

对于分布式系统，消息传递是更好的并发模型，因为它自然支持在独立处理器上并行执行的独立进程这一概念。

### 13.7 Java 线程

Java 中的并发单元是名为 run 的方法，其代码可以与其他此类方法（属于其他对象）以及 main 方法并发执行。执行 run 方法的进程称为线程。Java 的线程是轻量级任务，这意味着它们都在同一地址空间中运行。这与 Ada 任务不同，Ada 任务是重量级线程。
