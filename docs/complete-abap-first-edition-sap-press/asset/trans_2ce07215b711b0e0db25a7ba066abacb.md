

```
METHODS trigger_event.
METHODS on_double_click FOR EVENT double_click OF cl_events_demo
  IMPORTING
    column
    row
    sender.
METHODS on_right_click FOR EVENT right_click OF cl_events_demo.
ENDCLASS.
CLASS cl_events_demo IMPLEMENTATION.
  METHOD trigger_event.
    RAISE EVENT double_click
      EXPORTING
        column = 4
        row    = 5.
    RAISE EVENT right_click.
  ENDMETHOD.
  METHOD on_double_click.
    WRITE: / 'Double click event triggered at column', column,
             'and row', row.
  ENDMETHOD.
  METHOD on_right_click.
    WRITE: / 'Right click event triggered'.
  ENDMETHOD.
ENDCLASS.
DATA oref TYPE REF TO cl_events_demo.
START-OF-SELECTION.
  CREATE OBJECT oref.
  SET HANDLER oref->on_double_click FOR oref. "Instance event
  SET HANDLER oref->on_right_click. "Handler for Static event
  CALL METHOD oref->trigger_event( ).
```

**清单 8.12** 定义事件

在类的实现部分，`trigger_event` 方法使用 RAISE EVENT 语句触发 `double_click` 和 `right_click` 事件。由于 `double_click` 事件包含已定义的导出参数，此方法会将某些值导出到事件处理程序方法。`on_double_click` 方法导入由触发方法导出的值。在程序代码中，使用 SET HANDLER 语句注册事件，并且当调用 `trigger_event` 方法时，将执行事件处理程序方法中的代码。

在本节中，我们介绍了 OOP 的基础知识，包括类、方法、实例组件和静态组件以及事件。使用对象可以简化功能的实现。与过程式编程技术相比，OOP 概念具有许多优势。使用 OOP 技术开发的程序易于维护，并且如果设计良好，应该易于增强。

既然已经介绍了 OOP 的基础知识，在接下来的几节中，我们将讨论这种编程的一些特性，首先从封装过程开始。

## 8.2 封装

在过程式编程中，开发人员通常使用一种称为*功能分解*的技术来进行应用程序开发设计。在功能分解中，从功能需求中识别出应用程序需要执行的一系列步骤，并为每个步骤开发过程。换句话说，复杂的业务需求被分解为更小、易于理解的步骤。一旦所有过程都已就位，它们会被组合到主程序中，主程序按固定顺序调用这些过程，并将相关数据传递给每个过程。

例如，如果要为 ATM 机开发软件，那么需求可以分解为更小的步骤，例如读卡、验证 PIN、发放现金等。然后可以为这些步骤分别开发模块，例如一个模块用于读卡，另一个模块用于验证 PIN，还有一个模块用于验证账户余额并发放现金，等等。然后可以将这些模块组合起来形成整个应用程序。通过将需求分解为易于理解和维护的较小步骤，这种方法使开发中小型应用程序变得容易。

然而，由于过程（函数模块或子例程）没有自己的数据环境，因此每次调用过程时，它们都依赖主程序提供数据，或者必须使用程序的全局数据。这使得过程与主程序紧密耦合。随着应用程序不断扩展并变得越来越复杂，可能会导致维护上的麻烦。

例如，如果许多过程都在操作全局数据，那么如果为了未来的增强而更改过程调用顺序，我们就无法确定应用程序是否会以可预测的方式运行。由于每次调用过程时完全依赖主程序提供所需数据，接口很快就会变得杂乱，并且这会使过程限制过多，无法在其他环境中工作。过程的开发人员过于依赖外部应用程序，而开发人员对此没有控制权。开发能够为未来增强无缝工作的松耦合过程也变得困难。此外，一旦过程开发完成，开发人员就无法为了未来的增强而更改参数接口，而不破坏调用该过程的现有应用程序。

在 OOP 中，由于对象拥有自己的数据环境，因此可以使对象足够智能，能够自行做出决策，而无需过度依赖外部应用程序。

OOP 中的*封装*允许你定义边界并向外部世界隐藏实现。术语*封装*意味着属性（数据）和操作数据的方法（函数）被封闭在一个胶囊（对象）中。这意味着我们可以在对象内部可访问的内容与外部世界可访问的内容之间设置边界。这个边界有助于解决前面提到的许多与过程相关的问题。

在本节中，我们将讨论 OOP 中封装的一些特性。我们将探讨组件可见性、不同的可见性区域、类之间的友元关系以及实现隐藏。

### 8.2.1 组件可见性

如前面的清单 8.7 所示，对象的组件可以从*外部程序*、*子类*或类内部访问。对类组件的访问限制定义了其可见性。换句话说，我们可以决定类组件是只能从类或其子类内部访问，还是可以从外部程序访问。

回到清单 8.10，我们定义了用于声明组件的区域（PUBLIC SECTION、PRIVATE SECTION）。这些区域称为*可见性区域*。共有三个可见性区域：*公有、受保护*和*私有*。

可见性区域标识类组件的访问方式。以下列表定义了不同的可见性区域：

- **公有部分**
  *公有部分*中的组件可以从类内部和类外部访问。这些组件构成类的公有接口。
- **受保护部分**
  *受保护部分*中的组件只能从类及其子类（子类）内部访问。这些组件不能从外部程序访问。
- **私有部分**
  *私有部分*中的组件只能从类及其友元类内部访问（我们将在第 8.2.2 节讨论友元类）。

清单 8.13 显示了可见性区域的示例。

```text
CLASS cl_encapsulation_demo DEFINITION.
  PUBLIC SECTION.
    METHODS print.
    METHODS set_copies IMPORTING copies TYPE i.
    METHODS get_counter EXPORTING counter TYPE i.
  PROTECTED SECTION.
    METHODS reset_counter.
  PRIVATE SECTION.
    DATA copies TYPE i.
    DATA counter TYPE i.
    METHODS reset_copies.
ENDCLASS.
CLASS cl_encapsulation_demo IMPLEMENTATION.
  METHOD print.
    "Business logic goes here
  ENDMETHOD.
  METHOD set_copies.
    "Business logic goes here
    me->copies = copies.
  ENDMETHOD.
  METHOD get_counter.
    "Business logic goes here
    counter = me->counter.
  ENDMETHOD.
  METHOD reset_counter.
    "Business logic goes here
    CLEAR counter.
  ENDMETHOD.
  METHOD reset_copies.
    "Business logic goes here
    CLEAR copies.
  ENDMETHOD.
ENDCLASS.
CLASS cl_encapsulation_sub_demo DEFINITION INHERITING FROM cl_encapsulation_demo.
  PROTECTED SECTION.
    METHODS reset_counter REDEFINITION.
ENDCLASS.
CLASS cl_encapsulation_sub_demo IMPLEMENTATION.
  METHOD reset_counter.
    super->reset_counter( ).
*   super->reset_copies( ). "gives syntax error
  ENDMETHOD.
ENDCLASS.
```

**清单 8.13** 实现可见性区域

清单 8.13 中的代码实现了 `cl_encapsulation_demo` 类，并将 `cl_encapsulation_sub_demo` 类定义为 `cl_encapsulation_demo` 的子类。该代码展示了实现可见性区域的语法。请注意可见性区域的实现顺序：首先定义公有组件，然后定义受保护组件，最后定义私有组件。此声明顺序不能更改。

在清单 8.13 中，子类 `cl_encapsulation_sub_demo` 只能访问其超类 `cl_encapsulation_demo` 的公有和受保护组件。如果 `cl_encapsulation_sub_demo` 类尝试访问其超类的私有组件，该尝试将导致语法错误。请注意，在子类中重定义超类的方法时，不能更改该方法的可见性区域。例如，如果该方法定义在超类的受保护部分中，则应在子类的受保护部分中重定义该方法。

图 8.1 显示了全局类在类构建器中设置的可见性。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_327_0.png)

**图 8.1** 使用类构建器的可见性

通过可见性区域，可以定义清晰的边界，使得只有对象所需的组件暴露给外部世界。这种安排

