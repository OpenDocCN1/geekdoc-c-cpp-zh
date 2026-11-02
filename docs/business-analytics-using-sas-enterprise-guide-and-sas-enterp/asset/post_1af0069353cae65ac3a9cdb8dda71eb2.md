
## Notes from the Field

In this chapter, you’ve seen how data for analysis comes in many forms and from multiple sources. Your first step in preparing the data for analysis is to understand how and from where all the data sets were extracted. When data is purchased or extracted from unfamiliar sources, you should request data dictionaries that contain a definition for every field. Be sure you know what each field means and how it is derived (if applicable). In addition, request counts, ranges, and simple statistics for each field, such as mean, median, minimum, maximum, and standard deviation.

Make friends with the people in your information technology department. They can become valuable collaborators. They can help you get the names of the people in charge of creating the data, if possible. Don’t hesitate to ask questions until you are sure you understand the data.

Data can be seductive. If you are starting a new project, you may be eager to collect as much data from as many sources as possible. However, with the amount of data available for analysis, too much of a good thing can be paralyzing.

The best approach is to work in stages. Begin with the question from Chapter 1: *What is your objective?* If you have many objectives, choose the most important two or three. Then, work with your data management team to optimize the process. If operational or pricing considerations justify the collection of a large amount of data, then focus on a few that will have the most impact. Remember that analysis is usually done in isolation, but the planning should be done in concert with the major stakeholders and end-users to ensure the optimal use of talent, time, and money.

Remember that, in the end, your analysis is only as good as your data. This fact is true for both the quality of the data and how well it aligns with the objective of your analysis.

## Chapter 3: Overview of Descriptive and Predictive Analyses

- Introduction ... 29
- Descriptive Analyses ... 30
  - Frequency Distributions ... 30
  - Cluster ... 33
  - Decision Tree ... 33
- Predictive Analyses ... 35
  - Linear Regression ... 36
  - Logistic Regression ... 39
  - Neural Networks ... 41
- Modeling Process ... 43
  - Define the Objective ... 43
  - Develop the Model ... 43
  - Implement the Model ... 48
  - Maintain the Model ... 49
- Notes from the Field ... 52

### Introduction

In this chapter, you will learn about different types of descriptive and predictive analyses that are commonly used in business today. Once your source data sets are loaded and you have all the supporting documents necessary to access and understand the data, you are ready to start your analysis.

Descriptive analysis consists of tables, charts, and graphs that unveil data patterns, trends, and relationships that can inform your strategies, decisions, and actions. Predictive analysis tools like regression, decision trees, and neural networks give you the power to prioritize and optimize a broad range of marketing, risk, and process decisions.

You will see examples of each type of analysis with guidelines to determine when to use descriptive analysis and when to use predictive analysis. The goal of this chapter is to help you see opportunities to increase your competitive advantage by interpreting both descriptive and predictive analyses and taking appropriate business actions.

### Descriptive Analyses

The purpose of descriptive analysis is to reveal the characteristics of your data. It can describe a single point in time or cover a trend over multiple time intervals. When first receiving data, you should start with a simple descriptive analysis such as a frequency for categorical variables, and a distribution analysis for continuous variables. Both sets of results can be displayed with tables and graphs.

### Frequency Distributions

A *frequency distribution* is a representation of the basic shape or distribution of a variable in a data set. The frequency distribution can be displayed in a table or a graph. The components of the table are different depending on whether you are viewing a class variable or a continuous variable.

The examples in this section are calculated on data taken from automobile research.

**Class Variables**

A frequency distribution table for a class variable typically displays counts and percentages. Table 3.1 shows a simple frequency analysis in a table that displays the frequency counts and percentages of the variable *Type (of car)*. You can easily see that 262 cars, or 61.2%, of the cars represented by this data are *sedans*.

**Table 3.1: Frequency Distribution Table for the Class Variable Type (of Car)**

| Value | Frequency Count | Total Frequency (%) |
| --- | --- | --- |
| Sedan | 262 | 61.2150 |
| SUV | 60 | 14.0187 |
| Sports | 49 | 11.4486 |
| Wagon | 30 | 7.0093 |
| Truck | 24 | 5.6075 |
| Hybrid | 3 | 0.7009 |

Figure 3.1 shows the same information in a bar chart. Although you can’t see exact percentages in the bar chart, this view can be easier for a quick comparison. You may want to use both because some people prefer tables, while others prefer visual displays of data such as charts.

**Figure 3.1: Frequency Distribution Bar Chart for the Class Variable Type (of Car)**

![](img/976d9b992e82c4ac7d195d03a30b4915_43_0.png)

**Continuous Variables**

A frequency distribution table for a continuous variable typically displays population measures, such as the values for mean, median, minimum, and maximum. Table 3.2 displays the values for the variable *miles per gallon (MPG)* on the highway. You can read the number of total observations in the data (428). No values are missing. The total of 11,489 is the sum of MPG for the whole set of cars represented here. For the variable *MPG Highway*, the total may not be meaningful. On the other hand, if it were a variable representing bank account balances, the sum would represent the total balances for the population. This value could be of interest to a financial institution. Additional values represented in the table are the mean MPG with a value of 26.84. The minimum is 12, and the maximum is 66.

**Table 3.2: Frequency Distribution for the Continuous Variable MPG (Highway)**

| Category | Measure |
|---|---|
| Number (Nonmissing) | 428.00 |
| Number Missing | 0.00 |
| Total Number | 428.00 |
| Sum | 11,489.00 |
| Minimum | 12.00 |
| Mean | 26.84 |
| Median | 26.00 |
| Maximum | 66.00 |
| Standard Mean | 0.28 |

Figure 3.2 displays the frequency distribution in a bar chart. The values are bucketed to show the underlying nature of the data. When you view the frequency distribution bar chart of a continuous variable, you learn additional information, such as the skewness of the distribution.

**Figure 3.2: Frequency Distribution Bar Chart for the Continuous Variable Miles per Gallon (Highway)**

![](img/976d9b992e82c4ac7d195d03a30b4915_44_0.png)
