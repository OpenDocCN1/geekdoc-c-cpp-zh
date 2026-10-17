
### 26.2.7.2 `Selector` 类：实现

`Selector` 的成员函数承担以下任务：

- `Selector`（默认）构造函数。它清空读、写、执行 `fd_set` 变量，并关闭闹钟。除 `d_max` 之外，其余的数据成员不需要初始化：

```cpp
Selector::Selector()
{
    FD_ZERO(&d_read);
    FD_ZERO(&d_write);
    FD_ZERO(&d_except);
    noAlarm();
    d_max = 0;
}
```

- `int wait()`：此方法阻塞直到闹钟时间到达，或者在 `Selector` 监控的任何文件描述符上感听到活动。当 `select` 系统本身失败时，它会抛出异常：

```cpp
int Selector::wait() {
    time t = d_alarm;
    d_ret_read = d_read;
    d_ret_write = d_write;
    d_ret_except = d_except;
    d_readidx = 0;
    d_writeidx = 0;
    d_exceptidx = 0;
    d_ret = select(d_max, &d_ret_read, &d_ret_write, &d_ret_except, t.v_sec == -1 && t.v_usec == -1 ? 0 : &t);
}
```

- `int nReady()`：此函数的返回值只有在 `wait` 返回后才有定义。如果闹钟超时而返回 0，如果 `select` 失败则返回 -1，否则返回感听到活动的文件描述符数量：

```cpp
inline int Selector::nReady() {
    return d_ret;
}
```

- `int readFd()`：此函数的返回值也只有在 `wait` 返回后才有定义。如果 `select` 失败，其返回 -1：

```cpp
int Selector::readFd() {
    return checkSet(&d_readidx, &d_read);
}
```

- `int writeFd()`：该方法在感听到活动后返回。
- `void addExceptFd(int fd)`：该方法将文件描述符添加到集合中。
- `void addReadFd(int fd)`：该方法将文件描述符添加到集合中。
- `void addWriteFd(int fd)`：该方法将文件描述符添加到集合中。
- `void noAlarm()`：关闭闹钟。
- `void rmExceptFd(int fd)`：该方法从集合中移除文件描述符。
- `void rmReadFd(int fd)`：该方法从集合中移除文件描述符。
- `void rmWriteFd(int sec, int usec = 0)`：该方法从集合中移除文件描述符。
- `int checkSet(int *index, fd_set *set)`：该方法测试文件描述符是否存在于 `fd_set` 中。
- `void addFd(fd_set *set, int fd)`：该方法将文件描述符添加到集合中：

```cpp
void Selector::addFd(fd_set *set, int fd) {
    FD_SET(fd, set);
    if (fd >= d_max)
      d_max = fd + 1;
}
```

### 26.2.7.3 `Monitor` 类：接口

程序使用一个 `Monitor` 对象完成大部分工作。`Monitor` 类的公共接口仅提供默认构造函数和一个执行任务的成员函数 `run`。所有其他成员函数都位于类的私有区域。

`Monitor` 定义了私有枚举 `Commands` 用于符号化链接各种输入命令，以及若干数据成员。成员中包括一个 `Selector` 对象和一个使用子进程指针指向 `Child` 对象（见 26.2.7 节）的 map。此外，`Monitor` 有一个静态数组成员 `s_handler[]`，存储处理用户命令的成员函数指针。

应该实现析构函数，但将其实现留给读者练习。以下是 `Monitor` 的接口，包括用于创建函数的嵌套类 `Find` 的接口：

```cpp
class Monitor
{
  enum Commands
  {
    UNKNOWN,
    START,
    EXIT,
    STOP,
    TEXT,
    sizeofCommands
  }
```

```cpp
using MapIntChild = std::map<int, std::shared_ptr<Child>>;

friend class Find;

class Find
{
  int d_nr;
  public:
    Find(int nr);
    bool operator()(MapIntChild::value_type &vt) const;
};
```

# 26.2. FORK 系统调用

```cpp
);
Selector    d_selector;
int         d_nr;
MapInt      d_child;
static void (Monitor::*s_handler[])(int, std::string const &);
static int s_initialize();

public:
    enum Done
    {};

    Monitor();
    void run();

private:
    static void killChild(MapInt::value_type it);
    static int initialize();
    Commands next(int *value, std::string *line);
    void    processInput();
    void    processChild(int fd);
    void createNewChild(int, std::string const &);
    void exiting(int = 0, std::string const &msg = std::string());
    void sendChild(int value, std::string const &line);
    void stopChild(int value, std::string const &);
    void unknown(int, std::string const &);
;
```

由于只有一个类数据成员，该类的构造函数是一个非常简单的函数，可以实现实现：

```cpp
inline Monitor::Monitor()
: d_nr(0)
{}
```

### 26.2.7.4 类 `Monitor`: `s_handler`

数组 `s_handler` 存储了也将被初始化的函数指针。这可以通过几种方式完成：

- 由于 `Commands` 枚举 `Monitor::s_handler()` 仅指定了一组相当有限的命令，可以考虑编译时初始化：

```cpp
void (Monitor::*s_handler[])(int, string const &) = =
{
    &Monitor::unknown, // 遵循 enum Command 的顺序
    &Monitor::createNewChild, // 元素
    &Monitor::exiting,
    &Monitor::stopChild,
    &Monitor::sendChild,
}
```

# 第 26 章，具体示例

这种方法的优点是它简单，不需要任何运行时开销。缺点无疑是维护起来相对复杂。如果由于某种原因修改了 `Commands`，那么 `s_handler` 也必须随之进行修改。在这些情况下，编译时初始化是自找麻烦。不过，有一个简单的替代方案。

- 观察 `Monitor` 的接口，我们看到一个静态成员 `s_initialize` 和一个静态成员函数 `initialize`。静态成员函数处理 `s_handler` 数组元素的初始化，而枚举 `Commands` 值的顺序的任何修改都会通过重新编译自动处理：

```cpp
void (Monitor::Monitor::s_handler(sizeofCommands))(int, string const &);
int initialize()
{
    s_handler[UNKNOWN] = &Monitor::unknown;
    s_handler[START] = &Monitor::createNewChild;
    s_handler[EXIT] = &Monitor::exiting;
    s_handler[STOP] = &Monitor::stopChild;
    s_handler[TEXT] = &Monitor::sendChild;
    return 0;
}
```

成员 `initialize` 是一个静态成员，因此它可以用来初始化 `s_initialize`（一个静态 int 变量）。初始化通过将初始化语句放在已知会执行的函数源文件中强制执行。它可以是 `main` 函数，但如果我们是 `Monitor` 且只能控制包含 `Monitor` 代码的库，那么这就不是一个选项。在这些情况下，包含析构函数的源文件是一个非常好的候选。如果一个类只有一个构造函数且没有定义，那么该构造函数的源文件也是一个很好的候选。在 `Monitor` 的当前实现中，初始化语句被放在 `run` 的源文件中，理由是 `s_handler` 只有在使用 `run` 时才需要。

## 26.2.7 类 `Monitor`: 成员 `run`

`Monitor` 的核心活动由 `run` 执行。它执行以下任务：

- 最初，`Monitor` 对象监控其标准输入。`d_select` 监听的输入文件描述符集合 `STDIN_FILENO`。然后，在循环中调用 `d_select'wait'` 函数。如果 `cin` 上有输入，则由 `processInput` 处理。否则，输入来自子进程，由 `processChild` 处理。为了防止僵尸进程，子进程必须捕获终止信号。这将在下文中讨论。正如 Simons 指出的，`Monitor` 必须捕获终止信号（产生子进程的过程负责其子进程；子进程反过来负责它自己）。正如所述，`run` 的源文件定义并初始化了 `s_initialize`，以确保 `s_handler` 数组的正确初始化。

## 26.2 `FORK` 系统调用

以下是 `run` 的实现和 `s_initialize` 的定义：

```cpp
#include "monitor.ih"

int Monitor::s_initialize = Monitor::initialize();

void Monitor::run() {
    d_selector.addReadFd(STDIN_FILENO);
    while (true) {
        cout << "?" << flush;
        try {
            d_selector.wait();
            int fd;
            while ((fd = d_selector.readFd()) != -1) {
                if (fd == STDIN_FILENO)
                    processInput();
                else
                    processChild(fd);
            }
            cout << "NEXT ..\n";
        } catch (char const *msg) {
            exiting(1, msg);
        }
    }
}
```

成员函数 `processInput` 使用程序的标准输入读取用户命令。成员 `next` 更简单，它获取用户输入的下一个命令，然后调用 `s_handler[]` 数组中匹配的函数。这里是成员 `processInput` 和 `next`：

```cpp
void Monitor::processInput() {
    string line;
    int value;
    Commands cmd = next(&value, &line);
    this->s_handler[cmd](value, line);
}
```

```cpp
Monitor::Commands Monitor::next(int *value, string *line) {
    if (!getline(cin, *line))
        exiting(1, "Monitor::next(): reading failed");
    if (*line == "start")
        return START;
}
```

```cpp
if (*line == "exit" || *line == "quit")
{
  *value = 0;
  return EXIT;
}
```

```cpp
if (line->find("stop") == 0)
{
  istream instr(line->substr(4));
  instr >> *value;
  return !instr ? UNKNOWN : STOP;
}
```

```cpp
istream instr(line->c_str());
instr >> *value;
if (instr)
{
  getline(instr, *line);
  return TEXT;
}
return UNKNOWN;
```

`d_select` 的所有其他输入由子进程创建。由于 `d_select->readFd()` 返回相应的输入描述符，该描述符可以传递给 `processChild`。使用 `IFdambuf`，从输入流读取其信息。对于子进程的每一行输入，这里使用的通信协议通过发送一行文本回复。该行由 `processChild` 读取：

```cpp
void Monitor::processChild(int fd)
{
  IFdambuf ifbuf(fd);
  istream instr(&ifbuf);
  string line;
  getline(instr, line);
  cout << d_child[fd]->pid() << " " << line << '\n';
}
```

上述 `d_child[fd]->pid()` 的构造值得特别关注。`Monitor` 定义了数据成员 `map<int, shared_ptr<Child>> d_child`。该 map 将子进程序号作为键，指向 `Child` 的智能指针作为值。这里使用智能指针而不是 `Child` 对象，是因为我们想使用 map 提供的功能，但不想再次拷贝 `Child` 对象。

## 26.2.7 类 `Monitor`:示例

现在已经涵盖了 `run` 的实现，我们将集中于各种输入命令：

- 当发布 `start` 命令时，会启动一个新的子进程。成员 `createChild` 向 `d_child` 添加一个新元素。接下来，`Child` 对象应该开始其活动，但 `Monitor` 对象不能等待子进程完成其活动，而且短期内没有定义的终点，用户希望能够输入更多命令。因此，子进程必须作为守护进程运行。所以被 `fork` 的进程会终止，但它自己的进程继续运行（在后台）。因此，`createNew` 调用了子进程的 `fork` 成员。虽然调用的是子进程的 `fork` 函数，但是调用函数时的状态。因此，监控被 `fork` 中断。执行随后继续：

- 在其父进程中的父进程中；
- 在其父进程中的子进程中

由于 `ParentProcess` 是一个空函数并立即返回，子进程实际上会从 `createNew` 的 `cp->fork()` 状态立即继续。当子进程返回（见 26.7.7），子进程永远不会执行 `cp->fork()` 下方的代码。这是正确的。
在父进程中，`createNew` 的剩余代码只需将用于读取子进程信息的文件描述符添加到 `d_select` 的描述符集合中，并使用 `d_child` 建立该描述符与 `Child` 地址之间的关联：

```cpp
void Monitor::createNew(int, string const &)
{
    Child *cp = new Child(++d_nr);
    cp->fork();
```
