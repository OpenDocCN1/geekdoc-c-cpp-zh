

通常情况下，作为其他客户端任务服务器的任务希望维护一组可接受的条目，并在其中一个条目被调用时等待，调用后处理该条目并循环返回等待下一个条目。可选择的条目取决于若干条件（例如队列是否为空或缓冲区是否已满）。通过 select 语句来维护一组可接受的条目。select 语句的 EBNF 为：

```
select
[when condition =>] select-alternative
{or [when condition =>] select-alternative}
[else statement-sequence]
end select ;
```

其中 select-alternative 是一个 accept 语句后跟一系列语句，或一个 delay 语句（此处未描述）后跟一系列语句，或一个 terminate 语句。

select 语句的语义如下。select 语句中的所有条件都会被求值，求值为 true 的条件其对应的 select 备选方案被标记为开放。如果另一个任务已执行其条目的条目调用，则会选择一个开放的 accept 语句执行。如果有多个 accept 可用，则任意选择一个。如果没有开放的 accept 可用且存在 else 部分，则执行 else 部分的语句序列。如果没有 else 部分，则任务等待其中一个开放 accept 的条目调用。如果没有开放的 accept，则如果存在则执行 else 部分。如果没有 else 部分，则会引发异常条件（参见第 9 章）。

返回到一组 select 备选方案并不是基本 select 命令的一部分，但可以通过将 select 语句用循环包围来轻松实现。

继续之前的示例，userInput 主体可以按如下结构化，使其能够作为 keyPress 和 buttonClick 请求的服务器：

```
(1) task body userInput is
(2) begin
(3)   loop
(4)     select
(5)       when buttonClicked =>
(6)         -- respond to a button click request:
(7)             accept buttonClick (button: out ButtonID) do
(8)               -- get and return a button click
(9)               -- while the caller waits
(10)        end buttonClick; -- caller can now continue
(11)        -- do some buttonClick cleanup
(12)     or when keypressed =>
(13)       -- now respond to a keypress request:
(14)           accept keyPress (ch: out character) do
(15)             -- get a keypress while the caller waits
(16)        end keyPress; -- caller can now continue
(17)        -- do some keyPress cleanup
(18)        or terminate;
(19)        end select;
(20)    end loop;
(21) end userInput;
```

注意 select 语句中的 terminate 备选方案（第 18 行）。Ada 中任务的终止可以以两种方式发生。任务执行完毕且未创建任何仍在执行的依赖任务（即子进程），或任务在 select 语句中等待且存在开放的 terminate 备选方案，而其主程序（其在其中创建的父任务的块）已执行完毕。在这种情况下，由同一主程序创建的其他所有任务也必须已终止或正在等待 terminate 备选方案，此时它们将同时终止。这避免了在必须等待其子进程完成的父任务中编写显式同步语句（例如 join 或 wait）的必要性。

当然，取决于情况，具有上述行为的任务可能最好用 Ada 中的受保护类型编写。例如，我们可以用任务和 rendezvous 编写有界缓冲区（图 13.10）的版本，以提供互斥和同步，即使受保护类型可能更合适。代码在图 13.11 中。注意，由于任务不像受保护类型那样可以有返回值的函数，而必须通过条目中的参数返回返回值，图 13.11 中的缓冲区代码需要在图 13.10 的消费者代码中做少量修改。我们将细节留给读者（练习 13.39）。

我们提供 Ada 中任务的另外两个示例。第一个（图 13.12）是将信号量类型实现为任务类型。注意在该示例中，参数less 条目如 signal 或 wait 的 accept 中的代码块可以为空，在这种情况下可以省略 do ... end。第二个示例（图 13.13）是使用任务进行并行矩阵乘法的 Ada 包。

```
task buf is
    entry insert(ch: in character);
    entry delete(ch: out character);
    entry more (notEmpty: out boolean);
end;
task body buf is
    MaxBufferSize: constant integer := 5;
    store: array (1..MaxBufferSize) of character;
    bufferStart: integer := 1;
    bufferEnd: integer := 0;
    bufferSize: integer := 0;
begin
    loop
        select
            when bufferSize < MaxBufferSize =>
                accept insert(ch: in character) do
                    bufferEnd := bufferEnd mod MaxBufferSize + 1;
                    store(bufferEnd) := ch;
end insert;
bufferSize := bufferSize + 1;
or when bufferSize > 0 =>
    accept delete(ch: out character) do
        ch := store(bufferStart);
    end delete;
    bufferStart := bufferStart mod MaxBufferSize + 1;
    bufferSize := bufferSize - 1;
or
    accept more(notEmpty: out boolean) do
        notEmpty := bufferSize > 0;
    end more;
    or terminate;
end select;
end loop;
end buf;
```

图 13.11 作为 Ada 任务的有界缓冲区（续）

```
task type Semaphore is
    entry initSem (n: in integer);
    entry wait; -- use wait instead of delay, which is reserved in Ada
    entry wait;
end;
task body Semaphore is
    count : integer;
begin
    accept initSem (n: in integer) do
        count := n;
    end initSem;
    loop
        select
            when count > 0 =>
                accept wait;
                count := count - 1 ;
            or
                accept signal;
                count := count + 1;
            or
                terminate;
        end select;
    end loop;
end Semaphore;
```

图 13.12 Ada 中的信号量任务类型

```
generic Size: INTEGER;
package IntMatrices is
    type IntMatrix is array (1..Size,1..Size) OF INTEGER;
    function ParMult(a,b: in IntMatrix) return IntMatrix;
end;

package body IntMatrices is
    function ParMult(a,b: in IntMatrix) return IntMatrix is
        c:IntMatrix;

        task type Mult is
            entry DoRow (i: in INTEGER);
        end;
        task body Mult is
            iloc: INTEGER;
        begin

            accept DoRow (i: in INTEGER) do
                iloc := i;
            end;
            for j in 1..Size loop
                c(iloc,j) := 0;
                for k in 1.. Size loop
                    c(iloc,j) := c(iloc,j) + a(iloc,k) * b(k,j);
                end loop;
            end loop;
        end Mult;

        begin -- ParMult
            declare m: array (1..Size) of Mult;
            begin
                for i in 1..Size loop
                    m(i).DoRow(i);
                end loop;
            end;
            return c;
        end ParMult;
    end IntMatrices;
```

图 13.13 Ada 包中的并行矩阵乘法

## 13.7 非命令式语言中的并行性

尽管自 1980 年代中期以来已有大量工作，但使用函数式或逻辑编程语言的并行处理仍处于实验和研究阶段。尽管如此，仍存在一些研究提案的良好实现。在本节中，我们在简要介绍该领域后讨论其中几种，包括 MultiLisp、QLisp、Parlog 和 FGHC。最后，我们探讨了使用 Erlang 进行并行编程，Erlang 是一种支持消息传递风格的非命令式语言。读者应查阅本章末尾的参考文献以获取更多信息。

在前面的章节中，我们提到 Lisp 和 Prolog 等非命令式语言为翻译器提供了比命令式语言更多的自动并行化机会。此类语言中并行执行的机会可分为两个基本类别：and-并行性和 or-并行性。我们先考虑 and-并行性。

### 13.7.1 And-并行性

在 and-并行性中，多个值可由子进程并行计算，而父进程等待子进程完成并返回其值。这种类型的并行性可在函数式语言中用于函数调用的参数计算中。例如，在 Lisp 中，如果一个进程执行函数调用

```
(f a b c d e)
```

它可以创建六个并行进程来计算值 f、a、...、e。然后它暂停自己的执行，直到所有值都被计算出来，然后用 a 到 e 的返回值为参数调用 f 的（函数）值。类似地，在 let 绑定中：

```
(let ((a e1) (b e2) (c e3)) (...))
```

e1、e2 和 e3 的值可以并行计算。在 Prolog 中，执行子句时也存在类似的 and-并行机会

```
q :- p1, p2,..., pn.
```

p1 到 pn 可以并行执行，并且当所有 pi 都成功时 q 成功。隐含在此描述中的是，并行执行的计算不会相互干扰。在纯函数式语言中，参数和 let-绑定的求值不会产生副作用，因此非干扰性得到保证。然而，大多数函数式语言并非纯粹的，副作用或状态变化要求 and-并行性必须同步。在 Prolog 中，变量的实例化是一个典型的且必要的副作用，它会影响 and-并行性的行为。例如，在子句中

```
process(N,Data) :-
        M is N - 1,
        Data = [X|Data1],
        process(M,Data1).
```

右侧的三个目标通常不能并行执行，因为前两个对最后一个做出了实例化贡献。因此，这里也需要同步。

