
例如，假设一个父类有两个方法 `meth1` 和 `meth2`，而子类有一个额外的方法 `meth3`，该方法未在父类中定义。执行类型转换操作后，你只能通过父对象引用来访问子类的 `meth1` 和 `meth2` 方法。如果你尝试访问 `meth3` 方法，将会导致语法错误，如代码清单 8.26 所示。不过，你可以使用子对象引用来访问 `meth3` 方法，因为它仍然存在于程序中，并且没有被截断。

```
Parent = child. *Assigns child reference to parent.
Parent->meth1( ). *Calls the method meth1 in child if redefined.
Parent->meth2( ). *Calls the method meth2 in child if redefined.
Parent->meth3( ). *Results in syntax error.
Child->meth3( ). *Works as expected.
```

**代码清单 8.26** 窄化类型转换

窄化类型转换也可以在实例化期间通过向 `CREATE OBJECT` 语句添加 `TYPE` 来执行，如下所示：

```
DATA parent TYPE REF TO cl_parent.
CREATE OBJECT parent TYPE cl_child.
```

## 拓宽类型转换

当目标引用对象的静态类型比源引用对象的静态类型更具体时，就会发生拓宽类型转换。由于这违反了类型转换规则——该规则规定目标对象应始终比源对象更通用——如果你尝试使用 `=` 运算符分配对象或使用 `MOVE` 语句，语法检查器将报错，指出源对象无法转换为目标对象。为了绕过这一限制并告诉编译器我们知道自己在做什么，我们使用 `?=` 运算符进行拓宽类型转换，如下所示：

```
Child ?= parent.
```

使用 `?=` 运算符只会在编译时静态地绕过检查，并将其推迟到运行时。如果目标对象不比源对象更通用，则会抛出运行时错误。

例如，**代码清单 8.27** 中的代码将通过语法检查器（静态检查），但会导致运行时错误，因为子对象比父对象更具体。

```
CLASS cl_parent DEFINITION.
  PUBLIC SECTION.
  METHODS meth1.
  METHODS meth2.
ENDCLASS.
CLASS cl_parent IMPLEMENTATION.
  METHOD meth1.
    WRITE 'In method1 of parent'.
  ENDMETHOD.
  METHOD meth2.
    WRITE 'In method2 of parent'.
  ENDMETHOD.
ENDCLASS.
CLASS cl_child DEFINITION INHERITING FROM cl_parent.
  PUBLIC SECTION.
  METHODS meth2 REDEFINITION.
  METHODS meth3.
ENDCLASS.
CLASS cl_child IMPLEMENTATION.
  METHOD meth2.
    WRITE 'In method2 of child'.
  ENDMETHOD.
  METHOD meth3.
    WRITE 'In method3 of child'.
  ENDMETHOD.
ENDCLASS.
DATA parent TYPE REF TO cl_parent.
DATA child TYPE REF TO cl_child.
START-OF-SELECTION.
CREATE OBJECT parent.
CREATE OBJECT child.
Child ?= parent. "Results in runtime error
```

**代码清单 8.27** 导致运行时错误的拓宽类型转换

只有当目标对象的动态类型比源对象更通用时，才应使用拓宽类型转换。这实际上意味着，在执行拓宽类型转换之前，必须先执行窄化类型转换，如代码清单 8.28 所示。拓宽类型转换可能令人困惑且危险，因此应谨慎使用。

```
CLASS cl_parent DEFINITION.
  PUBLIC SECTION.
  METHODS meth1.
  METHODS meth2.
ENDCLASS.
CLASS cl_parent IMPLEMENTATION.
  METHOD meth1.
    WRITE 'In method1 of parent'.
  ENDMETHOD.
  METHOD meth2.
    WRITE 'In method2 of parent'.
  ENDMETHOD.
ENDCLASS.
CLASS cl_child1 DEFINITION INHERITING FROM cl_parent.
  PUBLIC SECTION.
  METHODS meth2 REDEFINITION.
  METHODS meth3.
ENDCLASS.
CLASS cl_child1 IMPLEMENTATION.
  METHOD meth2.
    WRITE 'In method2 of child1'.
  ENDMETHOD.
  METHOD meth3.
    WRITE 'In method3 of child1'.
  ENDMETHOD.
ENDCLASS.
CLASS cl_child2 DEFINITION INHERITING FROM cl_child1.
  PUBLIC SECTION.
  METHODS meth2 REDEFINITION.
  METHODS meth3 REDEFINITION.
  METHODS meth4.
ENDCLASS.
CLASS cl_child2 IMPLEMENTATION.
  METHOD meth2.
    WRITE 'In method2 of child2'.
  ENDMETHOD.
  METHOD meth3.
    WRITE 'In method3 of child2'.
  ENDMETHOD.
  METHOD meth4.
    WRITE 'In method4 of child2'.
  ENDMETHOD.
ENDCLASS.
DATA parent TYPE REF TO cl_parent.
DATA child1 TYPE REF TO cl_child1.
DATA child2 TYPE REF TO cl_child2.
START-OF-SELECTION.
CREATE OBJECT parent.
CREATE OBJECT child1.
CREATE OBJECT child2.
parent = child2.
child1 ?= parent.

child1->meth2( ).
```

**代码清单 8.28** 拓宽类型转换示例

在代码清单 8.28 中，定义了三个类：`cl_parent`、`cl_child1` 和 `cl_child2`。`cl_child1` 继承自 `cl_parent`，而 `cl_child2` 继承自 `cl_child1`。

首先通过将 `child2` 对象分配给父对象来执行窄化类型转换，然后通过将 `parent` 对象分配给 `child1` 来执行拓宽类型转换。在拓宽类型转换之后，使用 `child1` 对象引用调用 `meth2` 方法时，它将执行 `cl_child2` 类的 `meth2` 方法中的代码。

## 8.4.3 使用 CALL 方法的动态绑定

当对象作为参数传递给方法时，系统会自动动态绑定该对象。这使我们能够设计易于扩展的对象。

为了理解使用 `CALL` 方法的动态绑定，让我们看一下代码清单 8.29 中的代码片段。这里，我们将 `cl_student` 定义为一个抽象类，其中 `tuition_fee` 和 `get_fee` 是公有可见性的抽象方法。在受保护部分中定义了一个 `fee_paid` 属性，如果学生已支付费用，则可以设置该属性。

`cl_commerce_student` 和 `cl_science_student` 这两个类继承 `cl_student` 类，并维护它们自己对 `tuition_fee` 和 `get_fee` 抽象方法的实现。在 `tuition_fee` 方法中，如果学生已支付费用，则将私有 `fee_paid` 属性设置为 `abap_true`。`get_fee` 方法返回私有 `fee_paid` 属性的值。

我们定义了一个 `cl_admission` 类，可用于将学生注册到课程中。该类有两个方法 `set_student` 和 `enroll`，可用于完成学生在课程中的录取。由于这个 `cl_admission` 类应能够录取任何学生类别（理科学生、商科学生等）的任何学生，我们需要设计该类以导入任何学生类别的信息。

`cl_admission` 类的 `set_student` 方法定义了一个导入参数，用于导入 `student` 对象。如果我们将此导入参数的静态类型保持为 `cl_commerce_student`，则它只能导入商科学生对象，我们的类也只能处理商科学生的录取。同样，如果我们将导入参数的静态类型保持为 `cl_science_student`，则它只能导入理科学生对象，我们的类也只能处理理科学生的录取。为了使其适用于任何学生类别，我们将该方法的导入参数保持为 `cl_student` 抽象类的静态类型，而 `cl_science_student` 和 `cl_commerce_student` 类均继承自该类。

```
CLASS cl_student DEFINITION ABSTRACT.
  PUBLIC SECTION.
  METHODS tuition_fee ABSTRACT.
  METHODS get_fee ABSTRACT RETURNING VALUE(fee_paid) TYPE boolean.
  PROTECTED SECTION.
  DATA fee_paid TYPE boolean.
ENDCLASS.
CLASS cl_commerce_student DEFINITION INHERITING FROM cl_student.
  PUBLIC SECTION.
  METHODS tuition_fee REDEFINITION.
  METHODS get_fee REDEFINITION.
ENDCLASS.
CLASS cl_commerce_student IMPLEMENTATION.
  METHOD tuition_fee.
  "logic to calculate tuition fee for commerce students goes here
  "IF fee_paid.
      fee_paid = abap_true.
  ENDMETHOD.
  METHOD get_fee.
      fee_paid = me->fee_paid.
  ENDMETHOD.
ENDCLASS.
CLASS cl_science_student DEFINITION INHERITING FROM cl_student.
  PUBLIC SECTION.
  METHODS tuition_fee REDEFINITION.
  METHODS get_fee REDEFINITION.
ENDCLASS.
CLASS cl_science_student IMPLEMENTATION.
  METHOD tuition_fee.
  "logic to calculate tuition fee for science students goes here
  "IF fee_paid.
      fee_paid = abap_true.
  ENDMETHOD.
  METHOD get_fee.
      fee_paid = me->fee_paid.
  ENDMETHOD.
ENDCLASS.
CLASS cl_admission DEFINITION.
  PUBLIC SECTION.
  METHODS set_student IMPORTING im_student TYPE REF TO cl_student.
  METHODS enroll.
  PRIVATE SECTION.
  DATA admit TYPE boolean.
ENDCLASS.
```
