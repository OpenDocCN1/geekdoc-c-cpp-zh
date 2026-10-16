

以下是 wait 和 release 的简洁伪代码描述：

```
wait(aSemaphore)
if aSemaphore's counter > 0 then
  decrement aSemaphore's counter
else
  put the caller in aSemaphore's queue
  attempt to transfer control to some ready task
  (if the task-ready queue is empty, deadlock occurs)
end if
```

```
release(aSemaphore)
if aSemaphore's queue is empty (no task is waiting) then
  increment aSemaphore's counter
else
  put the calling task in the task-ready queue
  transfer control to a task from aSemaphore's queue
end
```

我们现在可以给出一个实现共享缓冲区合作同步的示例程序。在此例中，共享缓冲区存储整数值并且是一个逻辑上的循环结构。它设计用于可能由多个生产者和消费者任务使用。

下面的伪代码展示了生产者和消费者任务的定义。使用了两个信号量来防止缓冲区下溢或溢出，从而提供合作同步。假设缓冲区长度为 BUFLEN，并且实际操作它的例程已作为 FETCH 和 DEPOSIT 存在。对信号量计数器的访问使用点号表示。例如，如果 fullspots 是一个信号量，其计数器通过 fullspots.count 引用。

```
semaphore fullspots, emptyspots;
fullspots.count = 0;
emptyspots.count = BUFLEN;
task producer;
  loop
    -- produce VALUE --
    wait(emptyspots);      { wait for a space }
    DEPOSIT(VALUE);
    release(fullspots);    { increase filled spaces }
  end loop;
end producer;
```

```
task consumer;
  loop
    wait(fullspots);       { make sure it is not empty }
```

```
FETCH (VALUE);
release(emptyspots); { increase empty spaces }
-- consume VALUE --
end loop
end consumer;
```

信号量 fullspots 会使消费者任务排队等待缓冲区条目，如果缓冲区当前为空。信号量 emptyspots 会使生产者任务排队等待缓冲区中的空闲空间，如果缓冲区当前已满。

## 13.3.3 竞争同步

我们的缓冲区示例未提供竞争同步。可以通过额外的信号量来控制对结构的访问。该信号量无需计数，只需用其计数器指示缓冲区当前是否正在被使用即可。wait 语句仅在信号量的计数器值为 1 时才允许访问，这表示共享缓冲区当前未被访问。如果信号量的计数器值为 0，则表示正在进行当前访问，任务将被放入信号量的队列中。

请注意，信号量的计数器必须初始化为 1。信号量的队列在使用队列之前必须始终初始化为空。

一个仅需要二值计数器的信号量，如以下示例中用于提供竞争同步的信号量，被称为二进制信号量。

下面的示例伪代码说明了使用信号量为并发访问的共享缓冲区同时提供竞争和合作同步。访问信号量用于确保对缓冲区的互斥访问。请记住，可能存在多个生产者和多个消费者。

```
semaphore access, fullspots, emptyspots;
access.count = 1;
fullspots.count = 0;
emptyspots.count = BUFLEN;
task producer;
loop
-- produce VALUE --
wait(emptyspots); { wait for a space }
wait(access); { wait for access }
DEPOSIT(VALUE);
release(access); { relinquish access }
release(fullspots); { increase filled spaces }
end loop
end producer;
```

```
task consumer;
  loop
    wait(fullspots);      { make sure it is not empty }
    wait(access);         { wait for access }
    FETCH(VALUE);
    release(access);      { relinquish access }
    release(emptyspots); { increase empty spaces }
    -- consume VALUE --
  end loop
end consumer;
```

对这个示例稍作审视可能会让人认为存在问题。具体来说，假设在消费者中 wait(access) 调用时有一个任务正在等待，另一个任务取走了共享缓冲区中的最后一个值。幸运的是，这不可能发生，因为 wait(fullspots) 通过递减 fullspots 计数器为调用它的任务保留了缓冲区中的一个值。

到目前为止，尚未讨论信号量一个至关重要的方面。回顾前面关于竞争同步问题的描述：对共享数据的操作不得重叠。如果在早期操作仍在进行时开始第二个操作，共享数据可能会被损坏。信号量本身就是一个共享数据对象，因此对信号量的操作也容易受到同样的问题。因此，信号量操作必须是不可中断的。许多计算机都有专门为信号量操作设计的不可中断指令。如果没有此类指令，那么使用信号量来提供竞争同步就是一个严重的问题，没有简单的解决方案。

## 13.3.4 评价

使用信号量提供合作同步会产生不安全的编程环境。无法静态检查其使用的正确性，这取决于它们出现的程序的语义。在缓冲区示例中，如果省略生产者任务的 wait(emptyspots) 语句，将导致缓冲区溢出。如果省略消费者任务的 wait(fullspots) 语句，将导致缓冲区下溢。省略任一 release 将导致死锁。这些是合作同步失败。

信号量在提供合作同步时造成的可靠性问题在使用它们进行竞争同步时也会出现。如果在任一任务中省略 wait(access) 语句，可能导致对缓冲区的非安全访问。如果在任一任务中省略 release(access) 语句，将导致死锁。这些是竞争同步失败。注意到使用信号量的危险，Per Brinch Hansen（1973）写道：“信号量是为从不犯错的理想程序员准备的一种优雅的同步工具。” 不幸的是，理想的程序员很少见。

## 13.4 监视器

在并发环境中，解决信号量的一些问题的方案之一是将共享数据结构与其操作封装在一起并隐藏其表示形式——即使共享数据结构成为具有某些特殊限制的抽象数据类型。该方案可以通过将同步责任转移给运行时系统来在没有信号量的情况下提供竞争同步。

### 13.4.1 引言

当数据抽象的概念正在形成时，参与该工作的研究人员将相同的概念应用于并发编程环境中的共享数据，从而产生了监视器。根据 Per Brinch Hansen（Brinch Hansen, 1977, p. xvi）的说法，Edsger Dijkstra 于 1971 年建议将对共享数据的所有同步操作集中到单个程序单元中。Brinch Hansen（1973）在操作系统环境中形式化了这一概念。第二年，Hoare（1974）将这些结构命名为监视器。

第一个将监视器纳入的编程语言是 Concurrent Pascal（Brinch Hansen, 1975）。Modula（Wirth, 1977）、CSP/k（Holt et al., 1978）和 Mesa（Mitchell et al., 1979）也提供了监视器。在当代语言中，Ada、Java 和 C# 都支持监视器，这些语言将在本章后面讨论。

### 13.4.2 竞争同步

监视器最重要的特性之一是共享数据驻留在监视器中，而不是任何客户端单元中。程序员不通过使用信号量或其他机制来同步对共享数据的互斥访问。由于访问机制是监视器的一部分，监视器的实现可以保证同步访问，即一次只允许一个访问。对监视器过程的调用如果在调用时监视器正忙，则会被隐式阻塞并存储在队列中。

### 13.4.3 合作同步

尽管监视器固有地提供对共享数据的互斥访问，但进程之间的合作仍然是程序员的任务。特别是，程序员必须保证共享缓冲区不会发生下溢或溢出。不同的语言提供不同的合作同步编程方式，所有这些都与信号量相关。

一个包含四个任务和一个监视器的程序，该监视器提供对并发共享缓冲区的同步访问，如图 13.3 所示。在此图中，

