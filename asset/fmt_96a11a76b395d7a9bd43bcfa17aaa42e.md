
```c
#include "DigitalStopwatch.h"
#include "SystemTime.h"

static DigitalStopWatchPtr digitalWatch;
static SystemTime currentTime;

/* 由应用程序在启动时调用。 */
void startTimeSource() {
    digitalWatch = createWatch();

     /* 代码用于设置中断处理程序或
    类似的程序，以便每毫秒从操作系统
接收通知。 */

}

/* 此函数通过与操作系统的 
交互被调用。 */
static void mTick() {
    /* 调用一个封装了时间
    表示法知识的函数。 */
    currentTime = calculateNewTime();

    /* 通知秒表又过去了一个毫秒。 */
    notifyChangedTime(digitalWatch, currentTime);
}
```

这种解决方案的吸引力在于由于其简单性。然而，如果扩展性和灵活性是该解决方案所需要的属性，那么这种权衡是不可接受的。引入的潜在问题通过该设计所违反的原则来描述最为恰当。

## 开闭原则

回顾一下开闭原则，它被总结为“软件实体（类、模块、函数等）应该对扩展开放，但对修改关闭” [Martin]。源代码清楚地违反了这一点。在它目前的形状下，它只支持一种类型的单个秒表。想象支持其他类型的秒表，例如带有模拟显示器的秒表。时间源代码由于其硬编码的通知，将在所有类型的秒表上产生全方向的依赖爆炸。

## 稳定依赖原则

在软件维护或增量开发期间，现有代码的更改通常是不可避免的；即使应用了开闭原则，设计也只是根据原始设计者的假设关闭了某些修改（对于软件实体来说，完全关闭所有类型的更改几乎是不可能的）。稳定依赖原则试图通过以下建议来隔离现有代码更改的影响，即软件实体应该“向着稳定性的方向依赖” [Martin]。

在最初的这种方法中，秒表从时间源获取方向。从稳定依赖的方向来看，这是一个更好的选择。时间源通常是一个高内聚单元且更稳定的实体；只需将其封装在合适的抽象中（隐藏系统细节），就能使其成为封装在可用的低层领域的良好候选者。

通过让时间源依赖于高层的数字秒表，我们违反了稳定依赖原则。这种违反体现在让秒表更新的代码上。

将第一种方法的依赖方向与第二种方法的通知机制相结合，将使其成为理想的设计，观察者模式提供了必要的额外独立性，以获得两种解决方案的优点，而不受任何一种的副作用。

## 观察者 (OBSERVER)

观察者模式作为使开闭原则发挥作用的工具。设计 [Gama 等] 捕捉了观察者模式的意图：“在对象之间定义一对多的依赖，当一个对象的状态改变时，它的所有依赖者都会收到通知并更新”。将观察者模式应用于我们的示例中，带有第二种类型的秒表，“依赖者”是不同的秒表。设计模式定义了 `TimeSource` 扮演的角色为“具体主题”，状态改变的对象应该触发对观察者的通知和更新，即观察者。

![](img/36484cd32ea2e3eb1b027e721e2669a9_34_0.png)

图 1：通过观察者的解耦器和接收器。

## 实现机制

为了将主体与其具体的观察者解耦并仍然使主体能够通知它们，每个观察者必须对应一个唯一的实例。一类 ADT 模式提供了实现这种目标的方法。然而，从主体来看，所有观察者必须抽象为一种共享通用接口的通用类型。在 C 语言中，由于缺乏继承的支持，通用性通常由 `\void*` 表示；任何对象的指针都可以转换为 `\void*` 并转换回其原始类型而不丢失信息。

列表 2：观察者的接口，`TimeObserver.h`

## 观察者模式 (OBSERVER Pattern)

```c
typedef void (*ChangeTimeNotification)(void* instance,
                           const SystemTime* newTime);
typedef struct
{
    void* instance;
    ChangeTimeNotification notification;
} TimeObserver;
```

该接口声明了一个函数指针，事实这是实现动态行为的一种高效技术：具体的观察者会将自身以及一个函数指针附加到主体（subject）上。当主体发生变化时，它通过绑定的函数通知观察者。

通过使用抽象，类型安全性基本上是用灵活性换得的：将观察者转换回其原始类型的责任由程序员承担。将其转换为原始类型之外的其他类型可能会导致灾难性的后果。弗兰茨·卡夫卡虽然对 C 语言编程并不熟悉，但他提供了一个行为很好的示例：“当格里戈尔·萨姆某一天早上从不安的梦中醒来时，他发现自己躺床上变成了一只巨大的害虫” [Kafka]。显然，格里戈尔·萨姆并不是类型安全的。为了防止这种错误的转换，引入了 `TimeObserver` 来维护观察者与函数指针之间的绑定。隐式类型转换被封装在观察者内部，如代码所示。

列表 5：实现为一类抽象数据类型（ADT）的具体观察者

```c
/* 头文件。 */
struct DisplayStopWatch
{
    Display watchDisplay;
    /* 其它其他属性，例如
      数字显示。 */
};

/* TimeObserver 接口所需的函数的实现。 */
static void changedTime(void* instance,
                        const SystemTime* newTime)
{
    DigitalStopWatchPtr digitalWatch = instance;
    assert(NULL != digitalWatch);

    updateDisplay(digitalWatch, newTime);
}
```

在观察者获取任何通知之前，它必须对其进行注册。列表 4 声明了观察者所需的接口。

列表 4：主体的接口，`Subject.h`

```c
#include "TimeObserver.h"
void attach(const TimeObserver* observer);
void detach(const TimeObserver* observer);
```

这些接口由具体主体 `TimeSource` 实现，它必须跟踪所有附加的观察者。下面的示例使用链表来完成该任务。附加观察者对应于将给定的 `TimeObserver` 表示的副本添加到列表中。同样，在调用 `detach` 时，应从列表中移除与给定 `TimeObserver` 对应的节点，该观察者将不再接收来自主体的任何通知。下面的代码段阐述了这种机制。

列表 5：主体的实现，`TimeSubject.c`

```c
#include "TimeSubject.h"
struct ListNode {
  TimeObserver item;
  struct ListNode* next;
};
static ListNode* observers;
static SystemTime currentTime;

/* 管理链表的局部辅助函数
   （省略实现部分） */
static void appendToList(const TimeObserver* observer) {
  /* 将观察者的副本添加到链表尾。 */
}
static void removeList(const TimeObserver* observer) {
  /* 在链表中找到该观察者并
   移除该节点。 */
}

/* TimeSubject 接口的实现。 */
void attach(const TimeObserver* observer) {
  assert(NULL != observer);
  appendToList(observer);
}
void detach(const TimeObserver* observer) {
  assert(NULL != observer);
  removeList(observer);
}
```

```c
/* TimeSource 原始职责的实现（省略了初始化等代码）。 */
static void msTick()
{
    struct ListNode* node = observers.next;


    /* 调用封装了关于时间表示
       知识的函数。 */
    currentTime = calculateNewTime();

    /* 遍历链表并通知每个
       观察者又一个毫秒过去了。 */
    while(NULL != node)
    {
        TimeObserver* observer = &node->item;
        observer->notification(observer->instance,
                               currentTime);

        node = node->next;
    }
}
```

上面的代码解决了我们的问题；可以在不修改 `TimeSource` 的情况下添加新类型的计时表，这些计时表（我们的观察者）以高效的方式得到更新，而无需承担昂贵的轮询代价。

## 观察者注册 (Observer Registration)

将观察者模式实现为一类抽象数据类型（ADT）的额外好处是松散耦合与信息隐藏的结合。客户端既不知道也不依赖于主体。事实上，客户端甚至不知道 `DigitalStopWatch` 充当了观察者，因为创建和销毁 ADT 的函数封装了注册处理。下面的代码扩展了：

```c
static void changedTime(void* instance,
                                     const SystemTime* newTime)
{
    /* 按照之前的实现（列表 3）。 */
}

DigitalStopWatchPtr createDigitalWatch(void)
{

    DigitalStopWatchPtr watch = malloc(sizeof *watch);
    if(NULL != watch) {
        /* 创建成功 -> 附加到
           主体。 */
        TimeObserver observer = {0};
```

列表 6：注册处理的封装

```c
observer.instance = watch;
observer.notification = changedTime;

    attach(&observer);
}
    return watch;
}

void destroyDigitalWatch(DigitalStopWatchPtr watch)
{
    /* 在删除实例之前，我们必须从
     观察者中分离。 */
    TimeObserver observer = {0};
observer.instance = watch;
observer.notification = changedTime;

    detach(&observer);
    free(watch);
}
```

## 主体与观察者依赖关系 (Subject - Observer Dependencies)

观察者模式的引入导致了主体与观察者之间的松散依赖。客户端既不知道也不依赖主体。事实上，客户端甚至不知道 `DigitalStopWatch` 充当了观察者，因为创建和销毁 ADT 的函数封装了注册处理。为了防止这种错误的转换，引入了 `TimeObserver` 来维护观察者与函数指针之间的绑定。隐式类型转换被封装在观察者内部，如代码所示。

列表 5：实现为一类抽象数据类型（ADT）的具体观察者

（注：此处原文列表编号可能与上下文有冲突，遵循翻译逻辑保留）

（注：原文处标记为 Listing 5，但前文已出现过 Listing 5，保持原样）

*纠正：由于原文中存在两次 Listing 5，此处翻译严格遵循原文编号。*

列表 5：实现为**第一类抽象数据类型（FIRST-CLASS ADT）**的观察者

（此处对应代码代码片段）

```c
        TimeObserver* observer = &node->item;
        observer->notification(observer->instance,
                               currentTime);

        node = node->next;
    }
```

列表 7：从以下中提取的：

```

观察者模式的引入导致了主体与观察者之间的松散依赖。无论这种关系如何松散，都无法忽视：在通知期间允许主体变化。解决方案通过在通知期间禁止主体变化来确保其正常工作。此外，可以使用断言在运行时检查约束。
列表 8：使用断言检查主体约束

```c

static int isNotifying = 0;

void attach(const TimeObserver* observer) {

    assert(0 == isNotifying);

    /* 之前的代码。 */

}

void detach(const TimeObserver* observer) {

    assert(0 == isNotifying);

    /* 之前的代码。 */

}

static void msTick()

{

    struct ListNode* node = observers.next;

    /* 确保通知期间不对主体更改。 */

    isNotifying = 1;

    while(NULL != node)

    {

        /* 之前的观察者遍历。 */

    }

    /* 所有观察者已通知，再次允许更改。 */

    isNotifying = 0;

}
```
