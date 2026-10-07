
在书中所有的设计模式中，策略模式（`STRATEGY`）是我使用最频繁的一种。这种模式是基础性的。它是思维的自由转变。应用策略将算法的焦点从“如何做”转移到“做什么”。与其试图控制函数如何执行其任务，我们不如通过一个封装了“做什么”的高层行为来对其参数化。

在软件设计中，过度耦合是程序受害最大的属性之一。最糟糕的耦合形式是控制耦合。在控制耦合的退化情况下，客户端向某些对象传递一个标志位（`flag`）来控制其行为。这是一种常见的编码风格，会导致条件逻辑。过多的条件逻辑本身就引入了复杂性。但情况会糟。

正如我在原文中讨论的那样，控制耦合破坏了封装。突然，函数被拆解，模块融合在一起。这种代码难以扩展。它就像是 Bug 的邀请。我发现的最难的 Bug 是当不同功能之间相互作用时。这正是使用控制耦合方法的情况。相反，良好的设计将功能和变化分离。它让它们独立地变化（功能通常有不同的变化率），而无需参数。

策略模式并不是一种面向对象的模式。我对《四人行模式》一书的主要问题之一是它大量使用了类图。打开书中的任何一个模式，我们看到的第一样就是类图。通常，一个类似的图会在“结构”部分重复出现。这导致许多开发者将图表与实际模式混淆。它并不是最好的，它只是在特定语言中实现该模式的一种方法。仅此如此。一个模式是一个动态的、生成性的实体。根据上下文的不同，模式的应用每次看起来都可能截然不同。我坚信，如果《四人行》能排除结构部分，对设计模式运动造成的很多伤害本是可以避免的。

## 实现策略模式

识别并利用共性是软件设计的基石。通过封装和重用公共功能，设计的质量将超越代码重复和令人恐惧的“复制-粘贴”等反模式。在本章中，我们将使用策略模式来实现一个奖金系统。

策略模式允许我们根据客户的类型改变客户的行为。例如，我们有三种客户：

- 铜级客户：获得 2% 折扣。
- 银级客户：获得 5% 折扣。
- 金级客户：获得 10% 折扣。

通过使用策略模式，我们可以将每种客户的折扣逻辑封装在单独的类中，使代码更容易扩展和维护。

### 策略模式

```cpp
enum CustomerCategory {
    bronze,
    silver,
    gold
};

class CustomerStrategy {
public:
    virtual ~CustomerStrategy() {}
    virtual double calculatePrice(double totalAmount) = 0;
};

class BronzeStrategy : public CustomerStrategy {
public:
    double calculatePrice(double totalAmount) override {
        return totalAmount * 0.98;
    }
};

class SilverStrategy : public CustomerStrategy {
public:
    double calculatePrice(double totalAmount) override {
        return totalAmount * 0.95;
    }
};

class GoldStrategy : public CustomerStrategy {
public:
    double calculatePrice(double totalAmount) override {
        return totalAmount * 0.90;
    }
};

class Customer {
private:
    CustomerStrategy* strategy;
public:
    Customer(CustomerStrategy* s) : strategy(s) {}
    void setStrategy(CustomerStrategy* s) {
        strategy = s;
    }
    double getPrice(double totalAmount) {
        if (strategy) {
            return strategy->calculatePrice(totalAmount);
        }
        throw std::runtime_error("Strategy not set");
    }
};

double calculatePrice(CustomerCategory category, double totalAmount) {
    switch (category) {
        case bronze:
            return BronzeStrategy().calculatePrice(totalAmount);
        case silver:
            return SilverStrategy().calculatePrice(totalAmount);
        case gold:
            return GoldStrategy().calculatePrice(totalAmount);
        default:
            throw std::invalid_argument("Unsupported category");
    }
}
```

上面的代码使用了 `switch` 语句，如果增加了更多类别，这并不理想。通过使用策略模式，我们可以避免 `switch` 语句并使代码更具扩展性。

### 实现机制

在 C 语言中实现 `STRATEGY` 模式时，由于缺乏对多态和继承的支持，必须找到一种面向对象特征的替代方案来实现抽象。这个问题与在 C 中实现 `STATE` 模式时面临的问题几乎相同，这表明可以使用相同的机制，即函数指针。通过指针指定具体的操作被证明是实现动态行为的一种高效技术。

在 C 语言实现中，图中的基本结构仍然保留，但接口被表示为函数指针的声明。

#### 列表 2：`CustomerStrategy.h` 中的策略接口

```c
typedef double (*CustomerPriceStrategy)(double amount,
                                            double shipping);
```

不同的策略通过遵循接口指定的签名来实现。每个客户类别的权限（即上下文）各异，这些差异被封装在各自具体的策略中。根据具体策略的复杂性和内聚性，源代码可以组织为每个客户一个策略，也可以将所有支持的策略聚集在一个单一编译单元中。对于本示例中使用的策略，选择了后者方法。

#### 列表 3：`CustomerCategories.c` 中指向具体类别的接口

```c
double bronzePriceStrategy(double amount, double shipping);
double silverPriceStrategy(double amount, double shipping);
double goldPriceStrategy(double amount, double shipping);
```

#### 列表 4：`CustomerCategories.c` 中具体客户策略的实现

```c
/* 在生产环境中，所有输入都应该在进入每个函数时
进行验证，并确保计算的安全。 */
double bronzePriceStrategy(double amount, double shipping)
{
    return amount * 0.98 + shipping;
}

double silverPriceStrategy(double amount, double shipping)
{
    return amount * 0.95 + shipping;
}
double goldPriceStrategy(double amount, double shipping)
{
    /* 黄金客户免运费。 */
    return amount * 0.90;
}
```

使用这些策略，上下文代码现在将计算委托给与客户相关的策略。

#### 列表 5：委托给策略，`Customer.c`

```c
#include "CustomerStrategy.h"
/* 省略其他包含文件... */
struct Customer {
    const char* name;
    Address address;
    List orders;
    /* 将策略绑定到 Customer: */
    CustomerStrategy priceStrategy;
}
void placeOrder(struct Customer* customer, const Order* order) {
    double totalAmount = customer->priceStrategy(order->shipping);
    /* 更多处理订单的代码... */
}
```

上述代码选择了设计算法。由于客户现在只依赖于策略接口，可以添加或删除类别，而无需更改客户代码，且不会有向现有策略中引入 Bug 的风险。实现中剩余的开放问题是指定如何将特定策略绑定到客户。

### 绑定策略

策略可以由客户的客户端提供并在创建客户期间绑定到客户，或者由客户本身选择一个初始策略。前者的方案显然更灵活，因为它避免了客户依赖于具体策略。以下代码说明了这种方法，使用了作为一类抽象数据类型（`FIRST-CLASS ADT`）实现的客户。

#### 列表 6：创建时绑定策略，`Customer.c`

```c
CustomerPtr createCustomer(const char* name,
    const Address* address,
    CustomerPriceStrategy priceStrategy)
{
    CustomerPtr customer = malloc(sizeof(*customer));
    if(NULL != customer)
    {
        /* 绑定客户端提供的
        初始策略。 */
        customer->priceStrategy = priceStrategy;
        /* 在这里初始化
        客户的其他属性。 */
    }
    return customer;
}
```

#### 列表 7：指定绑定的客户端代码

### STRATEGY 模式

```c
#include "Customer.h"
#include "CustomerCategories.h"
static CustomerPtr createBronzeCustomer(const char* name, 
    const Address* address)
{
    return createCustomer(name, address, bronzePriceStrategy);
}
```

根据当前的问题，它可以被重新绑定到策略。例如，当客户升级为银牌级时，客户应该与 `silverPriceStrategy` 关联。使用函数指针技术，运行策略策略意味着指向另一个函数。

#### 列表 8：重新绑定策略，`Customer.c`

```c
void createPriceCategory(CustomerPtr customer, 
    CustomerStrategy newPriceStrategy)
{
    assert(NULL == customer);
    customer->priceStrategy = newPriceStrategy;
}
```

另一种方案是避免绑定，让客户端在每次函数调用时将不同的策略传递给上下文。如果上下文没有任何状态内存，这种替代方案可能适用。例如，在这个使用了一类对象的例子中，情况恰恰相反，自然的抽象是如上所示将客户与价格策略关联。

### STRATEGY 与 STATE 的比较

在讨论 `STRATEGY` 模式时，它与《设计模式》[`Gama, et al`] 书中前一个模式的关系值得特别提及。`STATE` 和 `STRATEGY` 设计模式密切相关。`Robert C. Martin` 这样说道：“State 模式的所有实例都是 Strategy 模式的实例，但并非所有 Strategy 模式的实例都是 State 模式实例” [`Martin`]。

这一观察让我们想起了《设计模式》合作者 `John Vlissides` 的一段话：“让模式的意图来引导它们的差异，而不是实现它们的类” [`Vlissides`]。事实上，尽管 `STATE` 和 `STRATEGY` 具有相似的结构，但它们的意图是不同的。

与上述示例有关，如果类别是基于转换的，那么 `STATE` 将是更好的选择。然而，如果结果是类别的成员身份，`STRATEGY` 是一个更好的抽象。虽然这不能被视为普遍真理，但另一个观察涉及到这些模式的用法：`STATE` 倾向于是上下文的内部关注。与 `STRATEGY` 相比，客户端通常将策略绑定到其上下文。

### 后果

应用 `STRATEGY` 模式的主要后果是：

- 开闭原则原则的好处。`STRATEGY` 设计模式提供了极大的灵活性，允许客户端通过实现他们自己的具体策略来更改和控制现有模块的行为。因此，通过添加新代码而不是修改代码来支持功能。
- 减少复杂性和条件逻辑。复杂的交互可能导致充斥着条件逻辑单体模块，可能以控制耦合的形式存在。此类代码往往难以维护和扩展。通过将条件分支的每个分支封装在策略中，`STRATEGY` 模式消除了条件逻辑。
- 允许相同算法的不同版本。模块的非功能性需求可能根据其用法而异。速度与内存使用之间的典型权衡是经典的。使用 Strategy 模式，权衡的选择可以委托给用户（策略可以提供相同行为的不同实现）(`Gamma, et al.`)。
- 额外的间接层。这种后果产生的主要问题是，策略需要从上下获取数据。由于所有作为策略的函数必须遵循相同的签名，简单地添加参数会降低内聚性。将上下文实现为一类数据类型（`ADT`）可能会解决这个问题，因为它将参数减少到单个句柄。通过一类 ADT 方法，关于感兴趣的数据的知识封装在每个策略中，并通过对一类 ADT 的句柄获取。仔细的设计应努力保持实现为一类 ADT 的模块具有高内聚性，避免其退化为不同策略所需的无关数据的仓库（这种设计通常表明选择了错误的抽象）。

### 使用示例

`STRATEGY` 在框架设计中指定策略时可能非常有用。使用 `STRATEGY`，客户端可以参数化实现。

例如，错误处理通常委托给应用程序。这种设计可以通过让客户端提供一个在发生错误时调用的策略来实现。通过这种方式，可以以应用程序特定的方式处理错误，其范围从简单的忽略错误到记录日志甚至重启系统。

## 观察者模式 (`OBSERVER`)

### 对观察者模式的反思

在我编写最初关于模式的文章时，我是基于几段生产代码的实际经验编写实现的。在过去的几年里，我收集了一些常用模式的笔记和示例实现。我最初的计划是发布五篇文章，从更通用的模式开始。这导致我必须在这些模式之间进行选择和排序。前三个（一类 ADT、状态模式 `STATE` 和策略模式 `STRATEGY`）都已给出。我知道我想通过对反应器模式 `REACTOR` 的讨论来结束全文。显然，某些模式必须被选出来。

我最终选择了观察者模式（`OBSERVER`）。回想起来，其他模式可能是更好的候选者。例如，门面模式 `FACADE`（`Gamma` 等人）在 C 语言中既直接又自然。最后，我选择观察者模式是出于：准备工作和通用性。

首先，我在观察者模式中使用的实现机制与我倾向于用于反应器模式的机制相似。观察者模式的实现可以作为引入更复杂的架构——反应器模式的入门。

其次，事件通知是许多应用程序的一部分。解耦事件通知的发送者和接收者是核心。今天，许多编程语言已经包含了对观察者模式的原生支持。例如，`C#` 通过其事件机制提供了一个通用版本。当然，`Common Lisp` 通过之前和之后的方法方法拥有它，这使得观察者模式的实现既简单又具有表现力。在 C 语言中，我们必须面对更多挑战才能获得合适的实现。如果做得好，观察者仍然是一个可行的解决方案。

### 实现观察者模式

管理系统中实体之间的依赖关系对于健壮的设计至关重要。在上一章中，我们查看了开闭原则的核心。现在，我们将转向另一个依赖管理原则，并说明如何使用观察者模式来实现这两种原则。

### 依赖的产生

回到用于状态模式的示例中，它们描述了实现简单秒表行为的技术。实现此类秒表通常涉及从某种时间源获取时间的任务。由于时间源可能与操作系统的交互绑定，因此将其封装在一个抽象中以隐藏系统特定的部分，是一个好主意，以便于测试和可移植性。同样，数字秒表的内部结构也应该封装在它自己的模块中。由于数字秒表负责从时间源获取时间（为了显示在它的数字显示屏上），显然秒表和时间源之间存在依赖关系。这种依赖的方向有两个显而易见的选择。

### 将秒视为视为

将秒表视为时间源的客户端似乎相当自然。也就是说……遗憾的是，在这个方向上实现依赖引入了一个显而易见的问题：秒表如何知道时间变化了？快速回答是：它不知道。至少，除非它对时间源引入了某种轮询机制。正如避免过早优化同样重要，人们也努力避免过早悲观化：

### 观察者模式

即使依赖的方向看起来是正确的，这种解决方案也很可能消耗大量的 CPU。如果应用程序需要执行除更新显示之外的更多操作，那么该问题就需要另一个解决方案。

### 让时间源更新秒表

通过反转依赖关系，可以很容易避免上述的潜在问题。时间源可以在时间发生变化时只需通知秒表。这种方法引入了从时间源到秒表的依赖。

#### 列表 1：时间源代码
