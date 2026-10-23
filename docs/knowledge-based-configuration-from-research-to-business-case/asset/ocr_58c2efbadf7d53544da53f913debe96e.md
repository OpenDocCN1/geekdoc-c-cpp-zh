features originally developed in the expert system paradigm are still visible in these configurators. Hence, understanding expert system projects is key to understanding how and why they operate as they do.

# 27.2 Expert Systems (XPS)

The XCON system (McDermott, 1982) was deemed an expert system (XPS; see also Hotz et al., 2014a²). Its success showed that XPS can solve real business problems where classical implementations fail. At the time this grounded the fact that XPS provide a good way of dealing with configuration problems, and this in turn provided for ample funding both for corresponding research and for commercial projects in the 1980s.

The basic architecture of an XPS as depicted in Figure 27.1 is very simple. The task of implementing an application is reduced to capture and represent the knowledge of human experts. This knowledge is then stored in the knowledge base (KB) of an otherwise out-of-the-box XPS. A user may then query the XPS, which uses predefined inference techniques to answer the query using the expertise stored in the KB. The task of acquiring the expert’s knowledge and representing it adequately in the KB is termed knowledge engineering (as opposed to classical software engineering).

The XPS idea has some definite conceptual advantages. Since the XPS is to emulate the cognitive processes of the human expert, the system ideally is able to do whatever the expert would have been able to do if the KB encodes the relevant expertise and assuming the system has adequate inference techniques. Knowledge engineers are freed from worrying about the exact nature of the underlying problem. Their task is just to encode the relevant knowledge correctly. They also don’t have to worry

![](bbox=[0.15, 0.56, 0.85, 0.81])

FIGURE 27.1

General architecture of an expert system (XPS).