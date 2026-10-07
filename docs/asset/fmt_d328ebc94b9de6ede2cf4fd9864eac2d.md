
| Multiphone | 0.989 | 9 | 0.219-retail,service,staff,refrigerator | 18 | 193 |
| Multiphone | 0.915 | 10 | 0.219-retail,service,staff,refrigerator | 19 | 197 |
| Multiphone | 0.915 | 11 | 0.219-retail,service,staff,refrigerator | 20 | 202 |
| Multiphone | 1.002 | 12 | 0.212-retail,service,staff,refrigerator | 21 | 206 |
| Multiphone | 1.002 | 13 | 0.212-retail,service,staff,refrigerator | 22 | 211 |
| Multiphone | 0.741 | 14 | 0.211-service,retail,great,abservice | 23 | 215 |
| Multiphone | 0.858 | 15 | 0.211-service,retail,great,abservice, | 24 | 220 |
| Multiphone | 0.858 | 16 | 0.211-service,retail,great,abservice | 25 | 226 |
| Multiphone | 0.858 | 17 | 0.211-service,retail,great,abservice | 26 | 231 |
| Multiphone | 0.813 | 18 | 0.211-service,retail,great,abservice | 27 | 236 |
| Multiphone | 0.813 | 19 | 0.211-service,retail,great,abservice | 28 | 241 |
| Multiphone | 0.836 | 20 | 0.210-place,service,cafe | 29 | 246 |
| Multiphone | 0.836 | 21 | 0.210-place,service,cafe | 30 | 251 |
| Multiphone | 0.942 | 22 | 0.193-retail,staff,bathroom | 31 | 257 |
| Multiphone | 0.942 | 23 | 0.193-retail,staff,bathroom | 32 | 262 |
| Multiphone | 0.942 | 24 | 0.193-retail,staff,bathroom | 33 | 267 |
| Multiphone | 0.951 | 25 | 0.192-retail,staff,store | 34 | 273 |
| Multiphone | 0.951 | 26 | 0.188-refrigerator,retail,staff | 35 | 278 |

`Rule Builder`节点可以使用语料库中的术语来构建目标变量。例如，已知的正负文档示例用于训练和验证`Rule Builder`节点，结果（显示在 8.15）显示模型相当不错。总体分类率约为否定文档的 79.8% 和正面文档的 75.8%。

### 显示 8.15：Rule Builder 的结果

| 目标 | 结果 | 百比 | 频率计数 | 总百分比 |
| --- | --- | --- | --- | --- |
| NEGATIVE | NEGATIVE | 83.2558 | 88.6139 | 895 | 53.3055 |
| POSITIVE | NEGATIVE | 16.7442 | 26.9061 | 100 | 10.7207 |
| NEGATIVE | POSITIVE | 19.9111 | 13.3861 | 115 | 6.9889 |
| POSITIVE | POSITIVE | 80.9063 | 73.0492 | 409 | 29.1248 |

| 目标 | 结果 | 百比 | 频率计数 | 总百分比 |
| --- | --- | --- | --- | --- |
| NEGATIVE | NEGATIVE | 79.8539 | 85.0268 | 219 | 51.6588 |
| POSITIVE | NEGATIVE | 20.1461 | 14.9732 | 35 | 13.0332 |
| NEGATIVE | POSITIVE | 24.1461 | 14.7352 | 36 | 8.5308 |
| POSITIVE | POSITIVE | 71.5389 | 67.2619 | 113 | 56.7773 |

`Rule Builder`节点的布尔规则显示了可能作为 SAS Sentiment Studio get关键词、概念和特征的好候选术语。

## 显示 8.16：来自 Rule Builder 节点的布尔规则

```
P_type=positive {
  AND, (OR, "bad", "badly")
  AND, (NOT, (OR, "value", "cheap", "great", (OR, "friendly", "friendly")))
  AND, (OR, "good", "great", (OR, "excellent", "excellent"))
  AND, (OR, "service")
  AND, (OR, "customer", "customer")
  AND, (OR, "outstanding", "outstanding")
  AND, (OR, "quality", "quality", (OR, "great", "great"))
  AND, (OR, "expensive", "expensive")
  AND, (OR, "efficient", "efficient")
  AND, (OR, "value", "value")
  AND, (OR, "last", "last", (NOT, (OR, "unreliable", "reliable")))
  AND, (OR, "fast", "fast", "fast")
  AND, (OR, "price", "price")
  AND, ("affordable", "affordable")
  AND, (OR, "cheap", "cheap", "cheap")
  AND, (OR, "useful", "useful")
  AND, (OR, "best", "best", "best")
  AND, (OR, "quick", "quick", "quick")
  AND, (OR, "value", "value", "waited")
  AND, (OR, "money", "money")
  AND, (OR, "show", "show", "show", (NOT, (OR, "clean", "clean", "dirty")))
  AND, (OR, "good", "good", "good")
  AND, (OR, "rule", "rule")
}
```

## 总结

情感分析在理解客户对产品或服务的体验方面起着重要作用。在本章中，你学习了如何使用 SAS Sentiment Analysis Studio 构建复杂的模型，以将消费者对实体或实体属性的意见或反馈分类为正面、否定或中性。通过使用已知情感类别的示例，可以通过构建统计模型对数据进行快速的情感分析。通过创建不同类型的规则（`CLASSIFIER`、`CONCEPT`、`C_CONCEPT`、`CONCEPT_RULE`、`PREDICATE_RULE` 和 `REGEX`），可以构建使用先进语言技术的基于规则的模型。基于规则的模型提供了在更细粒度上提取情感的增强，例如句子或产品特征。通过将统计模型的结果整合到基于规则的模型中，可以创建一个混合模型，这在许多情况下可以获得更好的结果。同样，利用 SAS Text Miner Text Rule Builder 节点的结果，也可以构建更好的情感分析模型。`Rule Builder`节点的布尔规则可以作为开发用于 SAS Sentiment Studio 的情感关键词、概念和特征的良好起点。案例研究 3 和案例研究 6 详细讨论了如何结合 SAS Sentiment Analysis Studio 和 SAS Text Miner 构建更好的情感分析模型。

## 参考文献

Castellanos, M. Dayal, U., Hsu, M., Ghosh, R., Dekhil, M., Lu, Y., Zhang, L., and Schreiman, M. 2011. “LCI: A Social Channel Analysis Platform for Live Customer Intelligence”. Proceedings of the 2011 ACM SIGMOD International Conference on Management of Data, 1049-1058.

Duraidhayalu, H. Garla, S., and Chakraborty, G. 2012. “Analyzing Sentiments in Tweets about Wal-Mart’s Gender Discrimination Verdict Using SAS* Text Miner”. Proceedings of the SAS Global Forum 2012 Conference, 306.

Grover, S., Jacob, J., and Chakraborty, G. 2013. “Analysis of Change in Sentiments towards Chick-fil-A after Dan Cathy’s Statement about sex Marriage Using SAS* Text Miner and SAS* Sentiment Analysis Studio”. Proceedings of the SAS Global Forum 2013 Conference, 251.

Joshi, M. Das, D., Gimpel, K., and Smith, N. 2010. “Movie Reviews and Revenues: An Experiment in Text Regression”, Human Language Technologies: Proceedings of the 2010 Annual Conference of the North American Chapter of the ACL, 293-296.

Liu, B. 2012. Sentiment Analysis and Opinion Mining (Lectures on Human Language Technologies), Morgan & Pool.

Liu, J., Sarkar, M., and Chakraborty, G. 2013. “Feature-Based Sentiment Analysis on Android App Reviews Using SAS* Text Miner and SAS* Sentiment Analysis Studio”. Proceedings of the SAS Global Forum 2013 Conference, 250.

Meng, Yanyan. 2012. “Sentiment Analysis: A Study on Product Features”, University of Nebraska – Lincoln.

http://digitalcommons.unl.edu/cgi/viewcontent.cgi?article=1031&context=businessdiss

Nagarajan, D., Harasudhan, H., and Chakraborty, G. 2013. “Investigating the Impact of Amazon Kindle Fire 7” on Amazon Consumers Using SAS* Text Miner and SAS* Sentiment Analysis”. Proceedings of the SAS Global Forum 2013 Conference, 261.

Pang, B., and Lee, L. 2008. “Using Very Simple Statistics for Review Search: An Exploration”. COLING 2008: Companion Volume – Posters and Demonstrations, 75–78.

Patangi, A., Mandati, S., Savuri, S., and Chakraborty, G. 2013. “Feature Extraction and Rating of a Smartphone Photosharing Application Using SAS* Sentiment Studio”. Proceedings of the SAS Global Forum 2013 Conference, 241.

Sarkar, Mantosh, Kumar, and Chakraborty, G. 2013. “Opinion Mining and Geo-Positioning of Textual Feedback from Professional Drivers,” Proceedings of the SAS Global Forum 2013 Conference, 500.

## 案例研究

通过书中的章节，你到目前已经学习了文本分析的概念，并阅读了使用 SAS Text Analytics 套件对这些概念的应用。引用本杰明·富兰克林（Benjamin Franklin）的名言：“告诉我，我会忘记；教导我，我会记住；让我参与，我会学会。”尽管通过阅读章节来概念和理论非常重要，但从学习的角度来看，具有详细工具应用的真实案例研究可能更为重要。本书的核心目标之一是为你（读者）提供一个机会，尝试书中讨论的大多数概念的实际应用。

本书包含九个案例研究。每个案例都包含了如何使用不同 SAS 工具进行文本分析的逐步说明。我们为你提供了七个案例的数据。案例 8 是一个新的基于 Web 的应用程序演示，它将 SAS* Text Miner 和 SAS* Content Categorization 的功能整合到一个名为 SAS* Contextual Analysis 的界面中。该案例的数据目前可用。

下表列出了每个案例中使用的 SAS Text Analytics 工具。

| 案例 | 标题 | 工具 |
| --- | --- | --- |
| 1 | 文本挖掘 SUGI/SAS 论坛论文摘要以揭示趋势 | SAS* Text Miner |
| 2 | SAS 会议论文摘要提交的章节成员自动检测 | SAS* Text Miner |
| 3 | 基于特征的客户评论情感分析 | SAS* Enterprise Content Categorization, SAS* Text Miner, SAS* Sentiment Analysis Studio, SAS* Enterprise Content Categorization |
| 4 | 探索伤害数据以进行根因和关联分析 | SAS* Text Miner, SAS* Enterprise Content Categorization |
| 5 | 使用文本数据增强预测模型 | SAS* Text Miner |
| 6 | 专业驱动员反馈的意见挖掘 | SAS* Text Miner |
| 7 | 安恩邮件的信息组织与访问以协助调查 | SAS® Sentiment Analysis Studio, SAS® Information Retrieval Studio, SAS® Text Miner, SAS® Enterprise Content Categorization |
| 8 | 利用统一文本分析的力量分类呼叫中心数据 | SAS® Contextual Analysis |
| 9 | 使用文本响应评估医疗提供者的服务性能 | SAS® Text Miner, SAS® Sentiment Analysis Studio |

## 案例研究 1 文本挖掘 SUGI/SAS 论坛论文摘要以揭示趋势

Zubair Shaik

Satish Garla

Goutam Chakraborty

- 引言
- 数据
- 结果
- 趋势
- 总结
- 访问案例研究项目的说明

## 引言

文本挖掘主要用于信息检索和文本分类。随着社交媒体的发展，文本挖掘作为一种发现主题趋势的技术，其普及程度极大提高。给定一组带有时间戳的文档，可以使用文本挖掘来识别文本中存在的不同主题以及它们如何随时间变化。在这个案例研究中，我们的目的是演示文本挖掘在理解会议论文趋势方面的应用。

全球每年都会举办许多专业会议或论坛。每年在所有会议上发表的论文总数可能达几十万。虽然有些会议只专注于一个特定领域，但也有许多会议作为不同领域的平台。与高度索引且可搜索的学术期刊不同，大多数会议论文并没有得到妥善的索引。此外，许多学术机构和咨询公司每年都会发表论文，但这些论文也没有被索引。使用结构化查询可能获取索引期刊/会议中发布的关于特定主题的论文列表，但要获取某一段时间内展示或发表的数百个主题的广泛知识，几乎是不可能的。

## 数据

本案例研究中使用的数据是 1976 年至 2011 年每年在 Global Forum 上发表的所有 SAS 论文的摘要。起初，我们考虑了三种类型的文本数据进行文本挖掘：

- 论文标题
- 论文摘要
- 论文正文
