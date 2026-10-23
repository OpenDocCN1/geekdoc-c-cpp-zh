
(Benavides et al., 2013)。为了推广这一方面，对这两个研究领域之间潜在协同效应的系统性分析是未来研究的一个主要问题。相关研究问题的深入讨论例如可参见 Benavides et al. (2013) 和 Hubaux et al. (2012)。

## 社区化配置

通常，配置被假定为一个过程，其中一名用户与配置系统交互，目标是识别出一个解决方案（配置）。在此背景下一个主要的研究问题是如何最好地支持包含用户群体的配置过程（Felfernig et al., 2012b; Jameson, 2004）。此类场景的例子有度假行程配置、软件发布计划，以及（同样）汽车配置。在这些场景中，用户通常会合作设计其解决方案，这需要额外的配置功能，例如为用户群体提供特征（值）推荐、为用户群体提供诊断和修复推荐、为用户群体提供配置排序，等等。从这些问题我们可以推导出应回答的一般研究问题：我们必须以何种方式调整（扩展）现有的用户界面、算法和配置过程，才能支持用户群体？

## 标准化的配置知识表示

开发配置通用语言仍然是一个主要的研究问题。这种语言将有助于使配置知识在不同的配置环境之间互换，从而更好地保护企业资产免受技术变化的影响。此外，这种知识表示语言将有助于使新算法发展的实证评估更容易，因为在假设每个环境都能导入/导出标准表示的情况下，翻译现有配置知识库到特定配置环境的方言所花费的精力会更少。致力于开发此类标准化知识表示的研究集中于通用本体（Soininen et al., 1998）、UML（Felfernig, 2007; Felfernig et al., 2000），以及基于描述逻辑的表示（参见例如 Felfernig et al., 2003）。未来研究的主要问题是开发一种通用表示语言，该语言（1）考虑到配置知识的所有相关方面（例如，端口、复合和共享的层次结构部分）并且（2）也提供允许高效求解搜索的语义。基于答案集编程的配置研究显示出有前景的结果，这将为实现上述目标铺平道路（Aschinger et al., 2012; Friedrich et al., 2011; Simons et al., 2002; Tiihonen et al., 2003, 2013）。

## 配置知识获取的智能用户界面

复杂配置知识库的工程通常是一个合作过程，其中涉及产品设计师、市场和销售专家以及知识工程师等不同利益相关者。每个利益相关者仅熟悉产品域的特定方面，甚至在技术层面也有不同的专家对底层产品有不同的知识。此外，利益相关者往往对可配置产品应支持的特性存在冲突的利益。在此背景下需要回答的主要问题如下：知识库的哪些组件应成为其一部分（即提供给客户）？知识库应包含哪些约束？如何实现不同利益相关者之间的共识？在此背景下的另一个问题是知识库的可访问性：经验丰富的知识工程师在知识库中的导航行为与经验较少的工程人员不同。在此背景下一个主要的研究问题是开发智能技术以支持配置知识库的易于理解和处理（Felfernig et al., 2013）。在此背景下需要回答的问题如下：在已经检查了特定序列的约束之后，还应额外检查哪些约束？在某些维护上下文中，知识库的哪些部分不应向工程师展示？我们如何重构格式不良的知识库？在此背景下，我们必须深入了解不同约束结构和类型的认知复杂性。关于该主题的初步研究结果已在 Felfernig et al. (2010a) 中报道。

## 智能测试与调试

除了确定与配置知识库不一致的最小用户需求集合外，基于模型的诊断（MBD；Reiter, 1987）的概念也可以应用于配置知识库的测试和调试（参见 Felfernig et al., 2004）。如果配置知识库与测试套件的某些（或全部）测试用例不一致，我们感兴趣的是以知识库中必须删除或调整的最小约束集合为最小解释，以便能够恢复知识库相对于测试套件的一致性。知识库测试和调试背景下需要回答的研究问题如下：我们如何自动生成测试套件？软件工程中的测试用例生成技术如何应用于或扩展到基于知识的配置场景？我们如何个性化诊断的确定，例如基于提供知识库某些部分质量指标的复杂性度量？我们如何提高调试算法的效率？

## 非侵入式偏好 elicitation

与推荐系统类似，用户偏好估计的质量是成功确定用户感兴趣的配置的一个主要因素（在假设个性化技术已集成到配置环境中的前提下）。在许多配置器（以及推荐应用）中，偏好 elicitation 基于直接询问用户或从先前用户交互的交互日志中推断偏好的概念（参见例如 Felfernig et al., 2009, 2010b）。从用户交互中推导偏好的替代方式例如是（在线）解释眼动追踪数据或基于语音处理推导需求和偏好。这些是未来研究的问题。

## 智能系统开发流程

知识型技术的广泛应用引发了对支持以结构化方式进行应用开发的方法论的需求。相关研究问题是标准软件工程方法在多大程度上适用，或者敏捷方法是否提供更好的方法支持。例如，Knublauch 和 Rose (2003) 中讨论了在知识型系统开发背景下应用敏捷方法。

## 参考文献

Ardissono, L., Felfernig, A., Friedrich, G., Goy, A., Jannach, D., Petrone, G., Schäfer, R., Zanker, M., 2003. A framework for the development of personalized, distributed web-based configuration systems. AI Magazine 24 (3), 93–108.

Aschinger, M., Drescher, C., Vollmer, H., 2012. LoCo – a logic for configuration problems. In: 20th European Conference on Artificial Intelligence (ECAI2012). IOS Press, Montpellier, France, pp. 73–78.

Asikainen, T., Soininen, T., Männistö, T., 2003. Towards managing variability using software product family architecture models and product configurators. In: Proceedings of the Software Variability Management Workshop, Groningen, The Netherlands, pp. 84–93.

Asikainen, T., Männistö, T., Soininen, T., August 2004. Representing feature models of software product families using a configuration ontology. In: 16th European Conference on Artificial Intelligence (ECAI-2004), Configuration Workshop, Valencia, Spain.

