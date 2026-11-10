

```
*Logic to check number of messages goes here and the parameter
*Boolean is set to abap_true or abap_false accordingly.
  ENDMETHOD.
  METHOD check_status.
*Logic to check user personal setting goes here and the parameter
*Boolean is set to abap_true or abap_false accordingly.
  ENDMETHOD.
ENDCLASS.
*Code in the calling program.
DATA notify TYPE REF TO cl_notification_api.
CREATE OBJECT notify.
notify->set_message( im_message = 'My App notification' ).
notify->display_notification( ).
```

### 清单 8.16 实现隐藏

清单 8.16 中的代码现在将消息属性移到了私有部分，这样它就无法在类外部访问，也就意味着其实现对外部世界是隐藏的。此外，在私有部分中还定义了三个新方法，用于在消息显示给用户之前对其进行各种检查；例如，如果用户关闭了应用的通知，程序可以通过 check_status 方法检查该信息，如果 check_status 方法返回布尔值 abap_false，则不显示消息。类似地，如果用户设置了限制，规定某个应用每天显示的通知不得超过五条，则 check_count 方法可以处理该校验。私有部分中使用的这些校验方法可以在不必担心依赖关系的情况下进行增强或更改。

外部开发人员无需了解为了显示通知而执行的那些复杂校验。他们只需要知道如何设置消息以及如何调用通知 API。借助清单 8.16 中的实现，你可以完全控制所显示的通知，并且任何校验都无法被绕过。这也使该实现具有面向未来的能力，因为你可以根据需要添加任意数量的额外校验，而外部开发人员无需在应用程序中更改调用 API 的方式。

如果使用得当，实现隐藏能让软件开发更不容易出错，也更容易增强或维护。

现在我们已经了解了封装的主要特征，在下一节中，我们将转向另一个 OOP 概念：继承。

## 8.3 继承

*继承*是 OOP 中一个重要的概念，它帮助我们避免重复代码，并充分利用现有的代码库。在第 8.1 节中，我们描述了继承如何在不重写现有代码的情况下轻松扩展功能。使用过程式编程技术，能做到的最接近继承的方式，要么是编辑现有代码以扩展功能，要么是复制现有代码并添加额外功能。这两种方法都不可取，因为编辑现有代码可能会破坏原有功能，而且需要大量测试来验证原有功能和新功能都能正常运作；每次功能增强时，这本身都是一个耗时的过程。如果我们复制现有代码，那么不仅代码会冗余，还会导致维护噩梦，因为每次对原始代码进行更新，都需要在所有副本中重复同样的修改。

继承允许你在复用已有开发成果的同时，扩展类以满足更具体的要求，而无需重复现有代码。例如，假设在开发的初始阶段，你定义了一个用于处理学生信息的类。因为当时的需求并未区分学生类型，所以你开发了一个通用的学生类。

然而，在开发过程的后期，需求得到了增强，需要将学生分为不同类别——商科学生、IT 学生、理科学生等——并且每个学生类别都需要执行特定的任务。随着需求变得越来越具体，你只需继承原来的学生类，就能为每个学生类别添加更具体的功能，如清单 8.17 所示。这样，你就可以从通用功能转向特定功能，同时复用原先开发已经投入的精力，而不会破坏现有实现。

```
CLASS cl_student DEFINITION.
  PUBLIC SECTION.
  METHODS tuition_fee.
ENDCLASS.
CLASS cl_commerce_student DEFINITION INHERITING FROM cl_student.
  PUBLIC SECTION.
  METHODS tuition_fee REDEFINITION.
  METHODS subject. "New method for additional functionality
ENDCLASS.
CLASS cl_commerce_student IMPLEMENTATION.
  METHOD tuition_fee.
    " Logic to calculate tuition fee for commerce students goes here
  ENDMETHOD.
  METHOD subject.
  ENDMETHOD.
ENDCLASS.
```

### 清单 8.17 继承

在清单 8.17 中，新的 `cl_commerce_student` 类是原始学生超类 `cl_student` 的子类，并从中继承。

在本节中，我们将了解继承概念的各个组成部分。然后，在讨论组合关系之前，我们还会了解抽象类和最终类，以及抽象方法和最终方法。在最后一小节中，我们将了解如何在类构建器中使用重构助手在继承树中移动类组件。

### 8.3.1 继承组件

在清单 8.16 中，我们只关心类内部和外部可以访问什么。公共部分允许外部应用程序访问，而私有部分则将访问权限限制在类内部的组件。

继承为实现隐藏带来了新的维度。通过受保护部分，你可以限制外部应用程序对这些组件的访问，但允许子类访问。因此，对于外部程序来说，受保护部分中定义的组件与私有部分中的组件类似。这使你可以向子类提供访问权限，同时又不对外公开父类的组件。

清单 8.18 提供了一些示例代码来演示继承。在这个示例中，我们演示了父类的所有组件是如何被子类继承的。

```
CLASS cl_parent DEFINITION.
  PUBLIC SECTION.
    METHODS set_value IMPORTING value TYPE string.
  PROTECTED SECTION.
    DATA value TYPE string.
    METHODS check_value.
  PRIVATE SECTION.
    METHODS reset_value.
ENDCLASS.
CLASS cl_parent IMPLEMENTATION.
  METHOD set_value.
  ENDMETHOD.
  METHOD check_value.
  ENDMETHOD.
  METHOD reset_value.
  ENDMETHOD.
ENDCLASS.
CLASS cl_child DEFINITION INHERITING FROM cl_parent.
ENDCLASS.
CLASS cl_child IMPLEMENTATION.
ENDCLASS.
DATA child TYPE REF TO cl_child.
START-OF-SELECTION.
  CREATE OBJECT child.
  child->set_value( value = 'child' ).
```

### 清单 8.18 继承示例

在清单 8.18 中，`cl_child` 类被定义为 `cl_parent` 的子类。这里，`cl_parent` 是超类，它在公共部分实现了 `set_value` 方法，在受保护部分实现了 `check_value` 方法和 `value` 属性，并在私有部分实现了 `reset_value` 方法。

`cl_child` 类通过类定义语句中的 INHERITING FROM 附加项从 `cl_parent` 继承。这就在两个类之间建立了父子关系。`cl_child` 类自身没有列出任何组件。`cl_parent` 超类的公共部分和受保护部分中的所有组件在默认情况下都可供 `cl_child` 子类使用。这一点在 `start-of-selection` 下的程序代码中可以看到（见清单 8.18）：定义了一个引用对象 child，它指向 `cl_child`，然后使用这个子类引用通过语句 `child->set_value( value = 'child' ).` 访问 `cl_parent` 的 `set_value` 方法。

请记住关于继承的以下要点：

- 子类可以访问超类中在公共和受保护可见性部分下定义的组件。
- 你不能在子类中定义与超类公共或受保护部分中的组件同名的组件。
- 由于超类的私有部分对子类不可见，因此你可以在子类中定义与超类中组件同名的组件。

