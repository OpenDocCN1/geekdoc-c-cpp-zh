

![](img/214a17cc1f5bbf0914497c7414128438_300_0.png)

**图 23.2**
工具景观的整体视图。

配置模型在源系统中出现主数据的新版本时无需更改。

### 23.5 数据集成

应用程序可以连接到目录以获取产品数据的访问权限。例如，一个不需要推理引擎的选取器可以直接通过实现 API 或使用网络服务对目录数据进行操作。K-Build 提供了使用目录中的产品组作为“分支点”的功能。分支点被视为一种组件类型，同时是指向目录中特定产品组的指针。这意味着在运行时，属于该产品组的产品被视为可能的子组件类型。

- Mittal, S., Frayman, F., 1989. Towards a generic model of configuration tasks. 11th International Joint Conference on Artificial Intelligence (IJCAI-89), Detroit, MI, vol. 2, pp. 1395–1401.
- Ranze, K., Scholz, T., Wagner, T., Günter, A., Herzog, O., Hollmann, O., Schlieder, C., Arlt, V., 2002. A structure-based configuration tool: Drive Solution Designer – DSD. In: 14th Conference on Innovative Applications of AI (IAAI-02), Edmonton, Alberta, Canada, pp. 845–852.
- Reiter, R., 1978. On closed world databases. In: Gallaire, H., Minker, J. (Eds.), Logic and Databases. Plenum Press, New York, pp. 55–76.
- Russell, S., Norvig, P., 2003. Artificial Intelligence – A Modern Approach, second ed. Prentice Hall, Upper Saddle River, NJ.
- Stumptner, M., 1997. An overview of knowledge-based configuration. AI Communications 10 (2), 111–126.

## 第24章 KONWERK

Lothar Hotz and Andreas Günter
HITeC e.V., University of Hamburg, Hamburg, Germany

**摘要：** 本章介绍了领域无关的配置工具 KONWERK。KONWERK 提供了在所谓的 basic modules 中实现的混合配置表示设施。Enhancement modules 提供诸如复杂需求建模或创建空间配置等方面。这些模块可用于开发多样化的应用。

### 24.1 概述

KONWERK¹ 是在汉堡大学开发的领域无关混合配置工具（Günter, 1995; Hotz et al., 2006）。该工具为知识表示和推理提供了 basic modules，涉及四种不同类型的知识：（1）概念知识，（2）约束知识，（3）任务知识（以下称为任务描述），以及（4）过程知识（参见 Günter and Cunis, 1992）。概念知识以本体形式表示。可使用分类（isA）和组合（hasParts）关系。知识库元素之间的限制通过约束定义。任务描述通过提供配置目标来表示用户需求。基于过程知识，可以定义配置决策的默认顺序。配置过程可以划分为多个子任务以指导用户。可以实现不同的交互风格；例如，按顺序呈现决策的配置向导，或更灵活的过程，其中用户会得到关于下一步应采取哪些配置步骤的指导。使用 KONWERK 进行配置的结果是对所有组件及其属性值的详细描述。

KONWERK 的 basic modules 部分作为商业配置工具 EngCon（参见 Krebs, 2014）² 和 Hollmann et al. (2000)³ 的蓝本。研究活动通过 enhancement modules 扩展了这些模块，以支持配置任务的额外方面，如基于资源的配置、模糊计算和空间推理。

本章的其余部分组织如下。第 24.2 节提供了 KONWERK 支持的知识表示和推理的概述。第 24.3 节介绍了 KONWERK 的 enhancement modules。第 24.4 节提供了工具实现的见解。第 24.5 节概述了使用该工具构建的一些配置器。

¹ KONWERK（Konfigurierungs-Werkzeug，配置工具）是在德国政府资助的研究项目 Prokon 中开发的。

² 第 23 章。

³ KONWERK 本身是 PLAKON 的继任者；参见 Hotz et al.（2014a，第 2 章）和 Neumann（1988）。

### 24.2 工作示例的建模

在 KONWERK 中，配置模型由概念和约束组成。它以组件为导向的方式表示配置知识。类似本体的表示法能够定义概念以及参数、分类和结构关系等关系。参数描述概念与原始数据类型（如数字、字符串、区间或这些数据类型的集合）之间的关系。分类关系描述两个概念之间的子集关系。结构关系是概念之间的关系（在 GCSP 中称为连接，在描述逻辑中称为角色）。结构关系的一个例子是组合关系（如 hasParts）。约束表示增强了这种本体知识，用于定义 n 元关系和代数表达式。尤其是概念与约束的紧密集成，使得能够结合使用描述逻辑服务（Baader et al., 2003）和基于约束的推理（Mackworth, 1977; Rossi et al., 2006; Tsang, 1993）；另见 Hotz et al.（2014b）⁴。

⁴ 有关替代配置知识表示的详细讨论，请参见 Hotz et al.（2014b，第 6 章）。

PC 域中使用的概念示例（参见 Hotz et al., 2014b⁶）以 KONWERK 的 Component Description Language 表示（Hotz, 2009）为：⁷

```
(define-concept :name PC
:super-concept Domain-Object
:parameters ((usage {internet scientific multimedia})
(efficiency {A B C})
(price [0 inf]))
(maxprice [0 inf])
:hasParts
((:type PC-Part :min 5 :max inf) :=     ; (*)
(:type InternetConn :min 0 :max 1)   ; (**)
(:type HDUnit :min 1 :max 2)
(:type MB :min 1 :max 1)
(:type Screen :min 1 :max 2)
(:type OS :min 1 :max 1)
(:type Application :min 1 :max inf))
```

概念（组件类型）PC 表示个人计算机。术语 :super-concept Domain-Object 将概念集成到 specialization hierarchy 中。PC 概念的参数表示个人计算机的属性，如 usage 或 efficiency。这些参数具有符号集合作为值（例如，{A B C}）。参数 price 和 maxprice 最初具有正无限范围 [0 inf]。结构关系 hasParts 模拟 PC 与其部件的组合关系，例如与 HDUnit。集合描述符使用所有部件的超概念 PC-Part 和基数 (*) 以及部件描述列表定义整个部件集合。概念和基数定义每个部件（**）。

概念约束。每个概念约束 cc ∈ CC 由（1）描述结构情况的条件和（2）一组约束调用组成。结构情况描述了概念的关联结构，其实例将由约束调用限制。每个约束调用由实现特定限制的约束关系指定。

包含相关概念的概念约束示例如下：

```
(define-conceptual-constraint :name prc1
:structural-situation
((?hdu :name HDUnit)                 ; (*)
(?hup :all :name HDUnit-Part        ; (**)
:partOf ?hdu))
:constraint-calls
((totalsum (?hdu price) (?hup price))) ; (3*)

(define-concept :name HDUnit-Part
:super-concept Domain-Object
:parameter ((price [0 inf]))
:partOf HDUnit)

(define-concept :name HDController
:super-concept HDUnit-Part
:parameter ((price [0 500]))
:hasParts ((:type DiskPort :min 1 :max 4)))

(define-concept :name HDisk                ; HDisk inherits parameter price from
:super-concept HDUnit-Part                 ; HDUnit-Part
:parameter ((capacity [0 inf])))
```

该模型片段定义了工作示例的价格约束 prc1。该约束通过将磁盘（HDisk）和控制器（HDController）的价格相加来计算硬盘单元（HDUnit）的价格。由于两者都被建模为硬盘单元的部件，因此我们可以在概念约束的结构情况中指定 HDUnit-Part。该情况描述了约束关系成立的条件。通过“?”表示的变量可以在其他条件或约束调用中引用在结构情况中识别的特定概念实例。因此，只有当存在一个 HDUnit (*) 及其某些 HDUnit-Parts (**) 时，才需要计算指定的约束调用 totalsum (3*)。在此，使用了特定的 :all 约束（参见（**）），其对数量具有灵活性

