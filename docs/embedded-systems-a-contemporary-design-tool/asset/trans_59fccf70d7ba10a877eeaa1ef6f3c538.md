

![](img/679b8d2d47f1bf86e17aca48f596f5cc_665_0.png)

系统的行为首先在图 12.28 的状态图中捕获。请注意，对于生产者任务 T0，从空闲到写入状态的转换由缓冲区的非满条件保护。同样，进入读取状态的转换由消费者图中的非空条件保护。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_665_1.png)

然后用伪代码表达该问题（参见图 12.29）。

```
Task T0 - Producer
while(1)
If not full
  add item
  increment count
else
  wait for space
end while
|
Task T1 - Consumer
while(1)
If not empty
  get item
  decrement count
else
  wait for item
end while
```

![](img/679b8d2d47f1bf86e17aca48f596f5cc_665_2.png)

C 代码片段如图 12.30 所示。

与同时访问桥梁的尝试类似，同时访问 count 也存在潜在问题。变量 count 的值取决于哪个任务访问它以及访问顺序。由于两个任务异步运行，该变量在任一时刻可能具有三个不同值中的任何一个。与桥梁一样，count 表示两个进程 T0 和 T1 之间共享的关键数据或临界区。

通常，临界区是多个任务可能共享的资源，例如 I/O 端口或他们在其中读写公共变量的内存段。

```
Task T0 - Producer
int in = 0;
while(1)
{
   // produce an item nextT0
   // wait for room
   while (count == MAXSIZE);
   B0[in] = nextT0;
   in = (in + 1) % MAXSIZE;
   count++;
}

Task T1 - Consumer
int out = 0;
while(1)
{
   while (count == 0); // wait for item
   nextT1 = B0[out];
   out = (out + 1) % MAXSIZE;
   count--;
   // consume an item nextT1
}
```

图 12.30 模拟生产者-消费者信息交换的 C 代码片段。

- 互斥同步
- 互斥
- 同步
- 条件同步

此类变量可能简单到仅为一个位，也可能复杂到一个文件或表格。如同穿越苏格兰桥梁的目标一样，当任务在临界区中处理一段数据或其他资源时，我们希望阻止所有其他进程的访问。也就是说，我们希望确保互斥访问。

控制对共享资源或公共数据的访问的需求产生了一种称为互斥同步的进程或处理器同步形式。第二种同步形式称为条件同步。对于互斥同步，目标是确保两个进程不会同时处于各自的临界区中。另一方面，条件同步要求进程延迟或阻塞，直到指定条件为真（或假）。

只有当多个任务或处理器希望同时使用不可共享资源或修改公共数据时，才存在共享和协调访问的需求。这是一个关键点。如果资源是可共享的，或者任务正在执行只读操作，则不会出现问题。

如同我们通过简单的桥梁管理方案所期望实现的那样，临界区问题的解决方案需要一种控制算法或协议来调节对共享区域的访问。从高层次来看，协议应当使得希望访问临界区的任务检查是否有其他任务正在使用该变量；如果没有，则向所有其他任务宣布它即将使用该变量，完成工作，然后在完成时通知所有人。

带有临界区的任务结构的抽象模型可以如图 12.31 所示。

```
while(1)
noncritical code

entry section
critical section
exit section

noncritical code
end while
```

图 12.31 临界区的抽象模型。

与临界区相关的代码包含在图中所示的三个矩形内。顶部矩形（入口区）充当守门人，控制对临界区域的访问。底部矩形（退出区）用于告知世界，之前正在使用关键变量的任务现已完成。

临界区问题的任何解决方案都必须满足以下要求。

- 它必须确保临界区域中的互斥。如果一个任务在临界区中，则不允许其他任务进入。
- 它必须防止死锁。如果两个或多个任务试图进入临界区，则必须有一个成功。
- 它必须确保通过临界区的进度。如果没有任务在临界区中且其他某个任务希望进入，则只有不在退出区矩形中的任务才能影响下一个进入临界区的任务。此外，希望进入的任务不能无限期地被禁止这样做。
- 解决方案必须确保有限等待。

一旦低优先级任务提出进入请求，必须对其被高优先级任务阻塞的次数设置上限。

让我们来审视几种可能的临界区问题解决方案。我们将从基于标志的方法开始。不过，在此之前，我们先将 atomic 一词作为操作的修饰语来介绍。

```
Atomic Operation
One that is guaranteed to terminate and is indivisible when applied to either examining a program variable or modifying the state of such a variable.
```

不可分割简单意味着，一旦开始，操作就会不间断地运行至完成。从粗粒度角度看，操作表现为单个语句；从细粒度角度看，操作实际上可能包含多个步骤。必须保证完整的步骤序列完成且不中断。

### 12.8.2 标志

为了保护临界区，首要目标是确保互斥访问。这种排他性可以通过在原子操作中嵌入标志来实现。该方法使用两个标志和两个进程进行说明。扩展到更多数量的进程在逻辑上是顺理成章的。

定义两个进程 T0 和 T1。让它们共享一个临界区。定义两个布尔标志 T0flag 和 T1flag，用于标记哪个进程在临界区中。最后，定义原子操作 await，其伪代码如图 12.32 所示。

```
await( condition )
{
statements
}
```

图 12.32 await 语句伪代码模型。

条件是一个布尔表达式，任务、线程或处理器会等待该表达式直到其求值为真。语句包含在条件求值为真时要执行的一组操作。如果条件求值为真，执行将通过 await 构造体主体中的语句继续。这里的一个重要假设是，当进程正在等待条件时，其他进程有机会运行。否则会发生死锁。

使用 await 操作，现在可以重新审视先前的共享缓冲区问题。await 语句针对每个任务表达如下：

```
await (!T0flag) {T0flag = true;}
await (!T1flag) {T1flag = true;}
```

接下来，使用 await 语句来控制对临界区（变量 count）的访问。首先，我们来看生产者（参见图 12.33a）。

```
Task T0 - Producer
int in = 0;
while(1)
{
// produce an item nextT0
while (count == n);
// wait for room
B0[in] = nextT0;
in = (in + 1) % n;
await (!T1flag ) (T0flag = true); // entry section
count++; // critical section
T0flag = false; // exit section
}
```

图 12.33a 使用 await 语句管理临界区。生产者端。

然后我们来看消费者（图 12.33b）。

```
Task T1 - Consumer
int out = 0;
while(1)
{
while (count == 0);
// wait for item
nextT1 = B0[out];
out = (out + 1) % n;
await (!T0flag ) (T1flag = true); // entry section
count--; // critical section
T1flag = false; // exit section
// consume an item nextT1
}
```

图 12.33b 使用 await 语句管理临界区。消费者端。

