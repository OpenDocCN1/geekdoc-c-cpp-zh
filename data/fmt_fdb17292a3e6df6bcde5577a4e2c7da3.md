
生成器也非常适用于惰性序列，它们可以被多次调用。

基于生成器的行为（例如能够暂停和恢复执行），协程的概念在 Python 中通过原生 API 进行了迭代优化。生成器是协程的一种有限形式，因为你可以使用 `.send()` 方法向它们发送数据。

在调用者和目标之间进行双向消息传递是可能的。协程还在 `cr_origin` 属性中存储调用者。

协程最初通过装饰器可用，但此后已被弃用，取而代之的是使用 `async` 和 `await` 关键字的“原生”协程。

要标记一个函数返回协程，必须在其前面加上 `async` 关键字。

`async` 关键字显式地表明（与生成器不同）该函数返回的是协程而不是值。

要创建一个协程，请使用 `async def` 关键字定义函数。在这个示例中，使用 `asyncio.sleep()` 函数添加一个定时器并返回一个唤醒字符串：

```python
>>> asyncio

>>> async def sleepy_alarm(time):
    await asyncio.sleep(time)
    return "wake up!"

>>> alarm = sleepy_alarm(10)

>>> alarm
<coroutine object sleepy_alarm at 0x1041de340>
```

当你调用函数时，它返回一个协程对象。执行协程有很多方法。最简单的是使用 `asyncio.run(coro)`。

使用你的协程对象运行 `asyncio.run()`，10 秒后它将响铃：

```python
>>> asyncio.run(alarm)
'wake up'
```

到目前为止，与普通函数相比只有一个微小的优势。协程的优势在于你可以并发运行它们。因为协程对象是一个可以传递给函数的变量，这些对象可以相互链接并链联，或者按顺序创建。

例如，如果你想有 10 个不同间隔的闹钟并同时启动它们，这些协程对象可以转换为任务（task）。

任务 API 用于调度和执行多个协程。在任务被调度之前，必须有一个事件循环在运行。事件循环的工作是调度并发任务并将完成、取消和异常等事件与回调连接起来。当调用 `asyncio.run()` 时，`run` 函数（在 `asyncio.py` 中）为你完成了这些任务：

- 启动一个新的事件循环
- 将协程对象封装在任务中
- 在任务完成时设置回调
- 循环任务直到其完成
- 返回结果

## 相关文件

| 文件 | 用途 |
| --- | --- |
| `asyncio` | 用于 async/await 的 Python 标准库实现。 |

### 事件循环

事件循环是把异步代码结合在一起的胶水。事件循环用纯 Python 编写，要么运行一次要么永久运行。循环中的任何任务都有回调。你可以将单个定时器转换为任务：

```python
python-book-samples ▷ 33 sleepy_alarm.py

import asyncio

async def sleepy_alarm(person, time):
    await asyncio.sleep(time)
    print(f"{person} wake up!")

async def wake_up():
    tasks = [
        asyncio.create_task(sleepy_alarm("Bob", 3), name="Doris"),
        asyncio.create_task(sleepy_alarm("Sanjeet", 4), name="Sanjeet"),
        asyncio.create_task(sleepy_alarm("Doris", 2), name="Doris"),
        asyncio.create_task(sleepy_alarm("Kim", 5), name="Kim")
    ]
    await asyncio.gather(*tasks)

asyncio.run(wake_up())
```

这将打印：
Doris -- wake up!
Bob -- wake up!
Sanjeet -- wake up!
Kim -- wake up!

在事件循环中，它将遍历每个协程以检查它们是否完成。类似于 `yield` 关键字可以从同一个帧返回多个值，`await` 关键字可以返回多个状态。事件循环将反复执行 `sleepy_alarm()` 协程，直到 `asyncio.sleep()` 返回结果，并且 `print()` 函数能够执行。为了使此起作用，必须使用 `asyncio.sleep()` 而替阻塞的 `time.sleep()`。

### 示例

你可以通过以下步骤将多线程端口扫描器示例转换为 asyncio：

- 使用 `asyncio.open_connection()` 创建一个连接来修改 `check_port()` 函数
- 在定时器事件中使用 `asyncio.wait_for()` 处理 future
- 如果成功，将端口添加到结果列表中
- 添加一个新函数 `scan()`，为端口创建 `check_port()` 协程并将其加入列表
- 使用 `asyncio.gather()` 将所有任务合并为协程
- 使用 `asyncio.run()` 运行 scan

cython-book-samples ▷ 33 portscanner_async.py

```python
import time
import asyncio

timeout = 1.0

async def check_port(host: str, port: int, results: list):
    try:
        future = asyncio.open_connection(host, port=port)
        r, w = await asyncio.wait_for(future, timeout)
        results.append(port)
        w.close()
    except asyncio.TimeoutError:
        pass # 端口关闭，跳过
```

```python
async def scan(start, end, host):
    tasks = []
    results = []
    for port in range(start, end):
        tasks.append(check_port(host, port, results))
    await asyncio.gather(*tasks)
    return results

if __name__ == '__main__':
    start = time.time()
    host = "localhost" # 选择一个你拥有的主机
    results = asyncio.run(scan(80, 100, host))
    for result in results:
        print("Port {0} is open".format(result))
        print("Completed scan in {0} seconds".format(time.time() - start))
```

最后，这个扫描在 1 秒多一点完成：

```bash
$ python portscanner_async.py
Port 80 is open
Completed scan in 1.0058400630950928
```

# 异步生成器

你目前学到的生成器和协程可以组合成一种类型 - 异步生成器。

如果一个函数声明了 `async` 关键字并包含 `yield` 语句，它就会转换为异步生成器对象。

与生成器一样，异步生成器必须由理解协议的实体执行。对应 `__next__()()`，异步生成器具有 `__anext__()` 方法。

普通的 `for` 循环无法理解异步生成器，因此使用了 `async for` 语句。

你可以将 `check_port()` 函数重构为一个异步生成器，它会产生下一个开放的端口，直到达到最后一个端口或找到指定数量的开放端口：

```python
async def check_ports(host: str, start: int, end: int, max=10):
    found = 0
    for port in range(start, end):
        try:
            future = asyncio.open_connection(host=host, port=port)
            r, w = await asyncio.wait_for(future, timeout=timeout)
            yield port
            found += 1
            w.close()
            if found >= max:
                return
        except asyncio.TimeoutError:
            pass # closed
```

要执行此代码，请使用 `async for` 语句：

```python
async def scan(start, end, host):
    results = []
    async for port in check_ports(host, start, end, max=1):
        results.append(port)
    return results
```

完整示例请参考 cython-book-samples ▸ 33 ▸ portscanner_async_generators.py。

### 子解释器

到目前为止，你已经涵盖了：

- 使用多进程进行并行执行
- 使用线程和异步进行并发执行

多进程的缺点是使用管道和队列的进程间通信比共享内存更慢。此外，启动新进程的开销也是相当大的。

线程和异步的开销很小，但由于 GIL 的线程安全保证，它们无法提供真正的并行执行。

第四种选择是子解释器，它的开销比多进程小，并且允许每个子解释器拥有自己的 GIL。毕竟，它是全局解释器锁（Global Interpreter Lock）。

在 CPython 运行时中，始终有 1 个解释器。解释器持有解释器状态，在一个解释器内部，你可以拥有 1 个或多个 Python 线程。解释器是评估循环的容器，解释器还管理自己的内存、引用计数和垃圾回收。CPython 提供了创建解释器的底层 API，例如 `Py_NewInterpreter()`。

| 运行时状态 | | | | | |
|---|---|---|---|---|---|
| 指令 (Python 运行时) | 文件 | 指令 (Python 运行时) | 文件 | | |
| 解释器 0 (主) | 堆 | 锁 | 解释器 n | 堆 | 锁 |
| | 解释器状态 | 隐含模块 | 接接字 | | |
| | GIL | | | | |
| 线程 @ (主) | 线程 1-n | 线程 @ (主) | 线程 1-n | | |

> 注意
subinterpreters 模块在 3.9.0b1 中仍处于实验阶段，因此 API 可能会发生变化且实现存在 Bug。

由于解释器状态包含内存分配区域以及指向 Python 对象（局部和全局）的指针集合，子解释器无法访问其他解释器的全局变量。与多进程类似，要在解释器之间共享对象，你必须对其进行序列化，或使用 `ctypes` 以及某种形式的 IPC（网络、磁盘或共享内存）。

### 相关源码

与子解释器相关的源码有：

| 文件 | 用途 |
|---|---|
| `_xxsubinterpreters.c` | 子解释器模块的 C 实现 |
| `Python pylifcycle.c` | 解释器管理 API 的 C 实现 |

### 示例

在最后的示例应用程序中，实际的代码必须封装在字符串中。在 3.9.01 中，子解释器只能通过代码字符串执行。

为了启动每个子解释器，会启动一个线程列表，并回调函数 `run()`。

该函数将：

- 创建一个通信通道
- 启动一个新的子解释器
- 向其发送要执行的代码
- 通过通信通道接收数据
- 如果端口连接成功，则将其添加到线程安全的队列中

cpython-book-samples ▸ 33 ▷ portscanner_subinterpreters.py

```python
import time
import _xxsubinterpreters as subinterpreters
from threading import Thread
import textwrap as tw
from queue import Queue

timeout = 1  # 秒..

def run(host: str, port: int, results: Queue):
    # 创建通信通道
    channel_id = subinterpreters.channel_create()
    interpid = subinterpreters.create()
    subinterpreters.run_string(
        interpid,
        tw.dedent("""\
import socket; import _xxsubinterpreters as subinterpreters
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.settimeout(timeout)
result = sock.connect_ex((host, port))
subinterpreters.channel_send(channel_id, result)
sock.close()
"""),
        shared=dict(
            channel_id=channel_id,
            host=host,
            port=port,
            timeout=timeout
        ))
    output = subinterpreters.channel_recv(channel_id)
    subinterpreters.channel_release(channel_id)
if output == 0:
    results.put(port)
if __name__ == '__main__':
    start = time.time()
    host = "127.0.0.1" # 选择一个你需要的主机
    threads = []
    results = Queue()
    for port in range(80, 100):
        t = Thread(target=run, args=(host, port, results))
```
