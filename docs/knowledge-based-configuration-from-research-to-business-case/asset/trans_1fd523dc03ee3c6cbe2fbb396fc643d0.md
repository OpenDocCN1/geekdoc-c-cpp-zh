

**图 25.3** WEEVIS：示例个人电脑配置器。用户通过回答问题的方式指定其需求。WEEVIS 确定解决方案，并在需求不一致的情况下呈现一组修复操作。

![](img/214a17cc1f5bbf0914497c7414128438_328_0.png)

作为相应 Wiki-based 应用的基础进行指定。领域本体以本体表示语言的形式定义。与 WEEVIS 相比，Baumeister 等人侧重于本体表示语言的应用，而这些语言对于非知识工程领域专家而言可访问性较差。此外，WEEVIS 的约束表示专注于配置域特定的知识表示，这使得定义相应的领域知识变得更容易。

### 配置知识表示

配置问题表示语言的开发有着悠久的历史。Mittal 和 Frayman（1989）提出了第一个基于一致性的配置问题表征方法。此后开发了不同类型的基于约束的表示，从动态约束满足问题（参见 Mittal 和 Falkenhainer，1990）到所谓的生成式约束满足问题（参见 Stumptner 等，1998）。不同类型基本配置知识表示的深入概述可在 Stumptner（1997）中找到。Felfernig（2007）介绍了一种基于统一建模语言（UML）定义配置知识库的方法，而 Felfernig 等（2003）还展示了如何基于描述逻辑概念表示此类模型。Soininen 等（1998）引入了一个通用本体，其中包含配置知识表示所需的相关概念。

### 配置环境

Felfernig 等（2006）介绍了一个用于图形化开发基于知识的推荐应用的环境。该环境与 WEEVIS 的基本功能有共同之处：产品备选方案被明确指定，然后根据给定的用户需求集进行选择和排序。Tiihonen 等（2003，2013）介绍了他们基于答案集编程的配置环境 WeCoTin，这是一个专门用于图形化定义大规模配置知识库的环境。主要配置相关约束类型可以在图形级别定义。更复杂的约束必须以专有的基于逻辑的知识表示语言定义。其他图形化开发环境见 Haselböck 和 Schenner（2014），⁴ Krebs（2014），⁵ 以及 Hotz 和 Günter（2014）。⁶

WEEVIS 与其他配置知识库开发环境之间的主要区别在于，我们可以预期更多用户能够在 Wikipedia 中处理配置器建模，而无需使用提供商特定的环境来定义知识库。然而，坦率地说，WEEVIS 的主要缺点是与更通用的知识表示形式主义相比，其表达能力有限（参见 Hotz 等，2014⁷）。此外，还必须集成图形化约束管理功能才能实现广泛使用。

### 异常管理

大多数现有配置环境都包含不同类型的异常检测（参见 Felfernig 等，2014⁸）或至少一致性管理功能。同样，WEEVIS 包含 FastDiag 诊断算法（Felfernig 等，2012）的基本实现，该算法支持用户在找不到解决方案时的情况。此外，WEEVIS 允许指定可用于回归测试目的的测试用例。将进一步的质量保证机制集成，例如 WEEVIS 知识库的自动化调试、冗余检测（Felfernig 等，2011）以及诊断区分（Shchekotykhin 等，2012）属于未来工作的范围。

### 25.5 结论

在本章中，我们介绍了 WEEVIS 环境，用于基于 Wiki 开发和维护简单的配置知识库。WEEVIS 在用户群体或社区有兴趣共同为公众或特定用户组提供配置器应用的场景中尤其有用。从技术角度来看，WEEVIS 的主要优势是在无需熟悉全新技术的情况下开发和维护配置知识库。与 WEEVIS 进一步开发相关的主要问题是集成个性化概念（Ardissono 等，2003；Tiihonen 和 Felfernig，2010），以帮助对确定的解决方案（配置）进行排序，集成额外的质量保证机制（除了 Wikipedia 的基本版本控制概念之外），以及 WEEVIS 语言本身的进一步开发，即提高可理解性并降低所提供建模概念的认知复杂性。

### 致谢

本章介绍的工作部分由奥地利研究促进机构资助（拨款编号：827587）。

⁴ 第 22 章。
⁵ 第 23 章。
⁶ 第 24 章。
⁷ 第 6 章。
⁸ 第 7 章。

- Shchekotykhin, K.M., Friedrich, G., Fleiss, P., Rodler, P., 2012. Interactive ontology debugging: two query strategies for efficient fault localization. Web Semantics: Science, Services and Agents on the World Wide Web 12–13, 88–103.
- Soininen, T., Tiihonen, J., Männistö, T., Sulonen, R., 1998. Towards a general ontology of configuration. Artificial Intelligence for Engineering Design, Analysis and Manufacturing (AI EDAM) 12 (4), 357–372.
- Stumptner, M., 1997. An overview of knowledge-based configuration. AI Communications 10 (2), 111–126.
- Stumptner, M., Friedrich, G., Haselböck, A., 1998. Generative constraint-based configuration of large technical systems. Artificial Intelligence for Engineering Design, Analysis and Manufacturing (AI EDAM) 12 (4), 307–320.
- Tiihonen, J., Felfernig, A., 2010. Towards recommending configurable offerings. International Journal of Mass Customization 3 (4), 389–406.
- Tiihonen, J., Soininen, T., Niemelä, I., Sulonen, R., 2003. A practical tool for mass-customising configurable products. In: Proceedings of the 14th International Conference on Engineering Design, Stockholm, Sweden, August 19–21, 2003, CDROM, p. 10 (Paper number: 1290).
- Tiihonen, J., Heiskala, M., Anderson, A., Soininen, T., 2013. WeCoTin – a practical logic-based sales configurator. AI Communications 26 (1), 99–131.
- Tsang, E., 1993. Foundations of Constraint Satisfaction. Academic Press, London, San Diego, New York.

## 第 26 章 VariSales

**Juha Tiihonen** 和 **Andreas Anderson**  
*Aalto University, Aalto, Finland*  
*Variantum, Espoo, Finland*

**摘要：** 本章概述了使用 VariSales 对 PC 配置知识库的建模。VariSales 基于具有明确底层语义的面向对象知识表示。VariSales 环境由半可视化 *建模工具* 和基于 Web 的 *配置工具* 组成。它应用遵循基于逻辑的答案集编程（ASP）范式的推理引擎。

### 26.1 引言

许多问题求解方法为表示配置模型、需求和配置，即配置知识提供了明确或隐式的概念模型。在我们看来，从配置器可维护性角度来看，实用的方法是提供一种配置特定的建模概念化，可用于表达配置知识。配置系统的任务是将此知识映射到能够提供支持配置任务所需推理的形式。

我们认为 Soininen 等（1998）提出的配置本体涵盖了广泛的配置问题。然而，在我们访问的许多公司中，销售配置的订单表相对简单，通常为 A4 格式的一页或两页。配置任务很直接，仅需要有限的推理。VariSales，即 WeCoTin（Tiihonen 等，2003，2013）的商业化版本，主要就是为解决这些较简单的问题而开发的。

本章其余部分组织如下。第 26.2 节概述了 VariSales 的建模概念，并展示了如何定义（表示）分类层次、属性、组合结构和约束。第 26.3 节举例说明了资源约束的建模，第 26.4 节介绍了用户界面建模以及由此产生的面向终端用户的 VariSales 界面。最后提供了简要讨论和结论。

### 26.2 工作示例的建模

Soininen 等（1998）提出的配置本体中一个显著缩减的子集为 VariSales 的建模语言提供了概念基础。该子集由

