

由控制器处理并直接从模型获取要显示的数据。控制器处理来自视图的事件，但它也可以直接操作模型或控制器。最后，模型可以由视图或控制器直接操作，但它也可以生成事件

由视图处理。一个典型的此类事件将是状态更改事件，这将导致视图更新向用户展示的内容。

- Controller
- View
- Model

## Figure 2-2. An MVC architecture with arrows indicating communication. Solid lines indicate direct communication. Dashed lines indicate indirect communication (e.g., via eventing) [30].

正如我们对三层架构所做的那样，现在让我们检查 MVC 如何遵守一般的分解原则。首先，一个

表示层或视图仅负责接受命令，而不是解释或执行它们。强制执行这种区分可以缓解开发人员为自己创造的一个常见问题：将表示层与逻辑层混合。

(a) Three-Tiered Architecture (b) MVC Architecture

User
Interface Command Dispatcher

Command Dispatcher
Stack User Stack Interface

Figure 2-3. Calculator architecture options

## Choosing the Calculator’s Architecture

从图 2-3 可以快速看出，这两种架构将计算器划分为相同的模块。事实上，在架构层面，这两种竞争架构仅在耦合上有所不同。因此，在在这两种架构之间进行选择时，我们只需要考虑它们两种通信模式之间的设计权衡。

显然，三层架构与 MVC 架构之间的主要区别是用户界面（UI）与栈之间的通信模式。在三层架构中，UI 和栈只能通过命令调度器间接通信。这种分离的最大好处是系统耦合度的降低。UI 和栈不需要知道彼此的接口。缺点当然是，如果程序需要大量的 UI 和栈直接通信，命令调度器将被要求中介这种通信，这会降低命令调度器模块的内聚性。MVC 架构具有完全相反的权衡。也就是说，以额外的耦合为代价，UI 可以直接与栈交换消息，避免命令调度器执行与其主要目的无关的额外功能的不便。因此，架构决策归结为检查 UI 是否经常需要与栈直接连接。

在 RPN 计算器中，栈充当程序输入和输出的存储库。用户经常希望看到栈上出现的输入和输出的精确内容。这种情况有利于 MVC 架构及其视图与数据之间的直接交互。也就是说，计算器的视图不需要命令调度器在数据和用户之间转换通信，因为不需要对数据进行转换。因此，我选择了模型-视图-控制器作为 pdCalc 的架构。与三层架构相比，MVC 架构的优势对于我们的案例研究来说，坦率地说，是很小的。如果我选择使用三层架构，pdCalc 仍然会有一个完全有效的设计。

## Interfaces

虽然选择 MVC 架构后，宣布分解的第一层完成可能很诱人，但我们还不能宣布胜利。虽然我们已经定义了三个最高层的模块，但我们还必须定义它们的公共接口。然而，如果不使用某种正式方法来捕获我们问题中的所有数据流，我们很可能会遗漏接口的关键必要元素。因此，我们转向面向对象的分析技术，即用例。

用例是一种分析技术，它生成用户与系统交互的特定操作的描述。从本质上讲，用例定义了一个工作流程。重要的是，用例不指定实现。在用例生成期间，特别是当用例揭示需求中的歧义时，应咨询客户。有关用例和用例图的信息，请参阅 Booch et al [4]。

为了设计接口

上一次操作并显示新的栈。

*Exception: There is no command to redo. An error condition is displayed.*

## Use Case: User Swaps Top Stack Elements

*Scenario: The user enters the command to swap the top two elements on the stack. The system swaps the top two elements on the stack and displays the new stack.*

*Exception: The stack does not have at least two numbers. An error condition is displayed.*

## Use Case: User Drops the Top Stack Element

*Scenario: The user enters the command to drop the top element from the stack. The system drops the top element from the stack and displays the new stack.*

*Exception: The stack is empty. An error condition is displayed.*

## Use Case: User Clears the Stack

Scenario: The user enters the command to clear the stack. The system clears the stack and displays the empty stack. Exception: None. Let clear succeed even for an empty stack (by doing nothing).

## Use Case: User Duplicates the Top Stack Element

Scenario: The user enters the command to duplicate the top element on the stack. The system duplicates the top element on the stack and displays the new stack.

Exception: The stack is empty. An error condition is displayed.

## Use Case: User Negates the Top Stack Element

Scenario: The user enters the command to negate the top element on the stack. The system negates the top element on the stack

and displays the new stack.

*Exception:* The stack is empty. An error condition is displayed.

## Use Case: User Performs an Arithmetic Operation

*Scenario:* The user enters the command to add, subtract, multiply, or divide. The system performs the operation and displays the new stack. *Exception:* The stack size is insufficient to support the operation. An error condition is displayed.
*Exception:* Division by zero is detected. An error condition is displayed.

## Use Case: User Performs a Trigonometric Operation

*Scenario:* The user enters the command for sin, cos, tan, arcsin, arccos, or arctan. The system performs the operation and displays the new stack.

*Exception:* The stack size is insufficient to support the operation. An error condition is displayed.
*Exception:* The input for the operation is invalid (e.g., arctan(−50) produces an imaginary result). An error condition is displayed.

## Use Case: User Performs y^x

*Scenario:* The user enters the command for y^x. The system performs the operation and displays the new stack. *Exception:* The stack size is insufficient to support the operation. An error condition is displayed.
*Exception:* The input for the operation is invalid (e.g., −1^0.5 produces an imaginary result). An error condition is displayed.

## Use Case: User Performs □^x y

*Scenario:* The user enters the command for ^x □y. The system performs the operation and displays the new stack. *Exception:* The stack

size is insufficient to support the operation.
An error condition is displayed.
*Exception:* The input for the operation is invalid (e.g., ⁴ ■ -1 produces an imaginary result). An error condition is displayed.

## Use Case: User Loads a Plugin

*Scenario:* The user places a plugin into the plugins directory. The system loads the plugin on startup, making the plugin functionality available.

*Exception:* The plugin cannot be loaded. An error condition is

## Analysis of Use Cases

我们现在将分析用例，以便为 pdCalc 的模块开发 C++ 接口。请记住，C++ 语言并未正式定义模块概念。因此，从概念上讲，将接口视为一组类的公开面向函数签名和

