

设计存在一些严重问题，最终才看到了经过一夜重构后最终出现的设计。也许，这里最有趣的教训是糟糕的设计确实可以导致可工作的代码，因此永远不要假设可工作的代码就是良好设计的指标。此外，如果糟糕的设计是局部的，可以对其进行重构，有时重构仅仅是为了提高清晰度而进行的。当然，重构的前提是你的项目计划包含足够的应急时间，以便定期暂停来偿还技术债务。让我们在回到更好的设计之前，先简要研究一下我的错误。

## 一个糟糕的设计

根据上面的分析，我们确定计算器应该有一个统一的 Display 类来处理输入和输出。我对显示的设计产生的根本性错误源于对“一个 Display 类”这一点的错误解读，即意味着没有为正交关注点创建额外的类。因此，我将 InputWidget 类未处理的全部功能都塞进了一个单一的 Display 类中。让我们沿着这条路走下去。然而，与我之前所做的那样完成设计和实现不同，我们将在看到第一个致命缺陷出现时就停止并重新设计该类（这正是我本应最初做的）。

在单一 Display 类设计中，Display 负责显示来自用户输入和来自计算引擎的输出。显示输出是微不足道的。Display 类观察 stackChanged() 事件（间接地，因为它不是 GUI 外部接口的一部分），并用新的栈值更新屏幕显示部件（在本例中为一个 QLabel）。从概念上讲，显示输入也是微不足道的。Display 直接接收 InputWidget 类发出的信号（例如 characterEntered()）并用当前输入更新屏幕显示部件。这种交互的简单性掩盖了该设计的基本问题，即输入并不是以原子方式输入供显示使用。相反，它是通过多次信号逐步组装的，通过独立输入多个字符并按下回车键来完成输入。这种输入的顺序构造意味着计算器必须维护一个活动输入状态，而输入状态本不应该存在于显示部件中。

那么，除了意识形态上的厌恶之外，Display 类维护输入状态有什么问题？我们不能简单地将状态视为显示输入缓冲区吗？让我们继续沿着这个设计走下去，看看它为什么有缺陷。例如，考虑退格按钮，其操作根据输入状态而重载。如果当前输入缓冲区非空，退格按钮会从该缓冲区擦除一个字符。然而，如果当前输入缓冲区为空，按下退格按钮会导致发出将栈顶数字弹出栈的命令。由于在这种设计下，Display 拥有输入状态并且是 backspacePressed() 信号的接收端，Display 必须成为发出弹出栈命令的源头。一旦 Display 开始发出命令，我们就完全放弃了内聚性，是时候找点意面酱了，因为意大利面条代码随之而来。从这里开始，我没有放弃设计，反而加倍投入，我的原始设计实际上变得更糟了。然而，与其继续沿着这条误导的道路走下去，不如直接转向研究更好的方法。

## 6.4.3 一个改进的显示设计

在讨论糟糕的显示设计早期，我指出致命的错误来自于假设统一的显示必然需要单一的类设计。然而，正如我们所见，这一假设是无效的。状态在计算器中的出现意味着至少需要两个类，一个用于视觉显示，一个用于状态。

这是否让你想起了我们已经见过的模式？GUI 需要维护内部状态（模型）。我们目前正在设计显示（视图）。我们已经为接受输入并发出命令设计了一个类，InputWidget（控制器）。显然，GUI 本身不过是熟悉模式的体现，即模型-视图-控制器（MVC）。请注意，相对于第 2 章图 2-2 中看到的 MVC 原型，GUI 可以用间接通信取代控制器和模型之间的直接通信。这种促进降低耦合的微小改动是由 Qt 的信号和槽机制实现的。

我们现在将注意力转向新引入的模型类的设计。在完成模型后，我们将返回 Display 类以完成其现在更简单的设计和接口。

模型类，我恰当地称之为 GuiModel，负责 GUI 的状态。为了正确实现这一目标，模型必须是导致系统状态发生变化的所有信号的接收端，并且必须是指示系统状态已发生变化的所有信号的源头。自然地，模型也是系统状态的存储库，并且应为 GUI 的其他组件提供查询模型状态的设施。让我们在列表 6-3 中查看 GuiModel 的接口。

### Listing 6-3. The GuiModel Interface class

```
GuiModel : public QObject {

Q_OBJECT

public:

enum class ShiftState { Unshifted, Shifted };
struct State { /* discussed below */ };

GuiModel(QObject* parent = nullptr);
~GuiModel();
void stackChanged(const vector<double>& v);

const State& getState() const;

public slots:

// called to toggle the calculator's shift state
void onShift();

// paired to InputWidget's signals
void onCharacterEntered(char c);
void onEnter();
void onBackspace();
void onPlusMinus();
void onCommandEntered(string primaryCmd, string secondaryCmd);

signals:
void modelChanged();
void commandEntered(string s);
void errorDetected(string s);

};
```

GuiModel 类中的六个槽都对应于 InputWidget 类发出的信号。GuiModel 解释这些请求，按适当方式更改内部状态，并发出一个或多个自己的信号。特别值得注意的是 commandEntered() 信号。尽管 GuiModel 的 onCommandEntered() 槽接受两个参数，即原始的主命令和

State 结构体的组成部分定义了 GUI 的整个状态。特别是，该 State 结构体包含一个保存栈顶可见数字最大数量的副本的数据结构、当前输入缓冲区、定义系统移位状态的枚举，以及定义输入缓冲区有效性的 Qt 枚举。声明如列表 6-4 所示。

### Listing 6-4. The State struct for the GuiModel

```
struct State {
    vector<double> curStack;
    string curInput;
    ShiftState shiftState;
    QValidator::State curInputValidity;
};
```

一个有趣的问题是，为什么 GuiModel 的 State 会缓冲来自栈顶的可见数字？鉴于 Stack 类是单例，Display 可以直接访问 Stack。然而，Display 仅观察 GuiModel 的变化（通过 modelChanged() 槽）。

由于与栈变化无关的状态变化在 GUI 中频繁发生（例如字符输入），Display 将被迫在每次 modelChanged() 事件上浪费地查询 Stack，因为 Display 不是 stackChanged() 事件的直接观察者。另一方面，GuiModel 是 stackChanged() 事件的观察者（通过 MainWindow 的函数调用间接）。因此，高效的解决方案是让 GuiModel 仅在计算器的栈实际发生变化时更新栈缓冲区，并让 Display 类访问该缓冲区，该缓冲区通过构造保证是最新的，以用于更新屏幕。

## 6.6 The Display Redux

我们现在准备将注意力重新转向 Display 类。将所有状态和状态交互都放在 GuiModel 类中后，Display 类可以简化为一个仅监视模型变化并显示计算器当前状态的对象

