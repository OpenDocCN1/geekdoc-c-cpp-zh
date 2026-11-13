# Chapter 4

# The Visualization Pipeline

In Chapter 2, we showed the basic steps of a visualization application and also sketched a simple data representation for the function graphing problem. In Chapter 3, we described in detail how to represent discrete, sampled data. We introduced several dataset types that offer different trade-offs between representation flexibility and storage and implementation requirements. At this point, we should have a good understanding of how to represent the data we are interested in visualizing. The focus of this chapter is to present the structure of a complete visualization application, both from a conceptual and a practical perspective.

We begin our discussion with a conceptual description of the structure of visualization applications (Section 4.1), which introduces the four main ingredients of such an application: data importing, data filtering and enrichment, data mapping, and data rendering. Next, we describe several implementation considerations of this conceptual structure (Section 4.2). Section 4.3 discusses a classification of the various algorithms used in the visualization process. Finally, we conclude our analysis on the structure of visualization applications (Section 4.4).

# 4.1 Conceptual Perspective

As explained in Chapter 1, the role of visualization is to create images that convey various types of insight into a given process. The process is illustrated conceptually in Figure 1.3. The visualization process consists of the sequence of steps, or operations, that manipulate the data produced by the process under