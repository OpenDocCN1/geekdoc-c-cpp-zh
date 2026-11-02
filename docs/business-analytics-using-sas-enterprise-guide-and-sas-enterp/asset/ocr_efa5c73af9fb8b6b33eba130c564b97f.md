event-triggered peak data loads can be challenging to manage, and even more so when unstructured data is involved.

+   - **Complexity.** Today’s data comes from multiple sources, and it is still an undertaking to link, match, cleanse, and transform data across systems. However, it is necessary to connect and correlate relationships, hierarchies, and multiple data linkages, or your data can quickly spiral out of control.

New kinds of data from digitization and social media are adding to the “bigness” of data. Unstructured data appears to be the next frontier of data sources. Powerful software is now able to decipher and analyze handwritten text, audio, images, and videos. The translation of unstructured data and its integration with structured data are projected to be the primary sources of data for analysis in the future.

The first step in making the best use of any data source is to understand the nature of the data, how it is gathered, and how it is managed.

# Types of Data

Data comes in three basic types: nominal, ordinal, and continuous.

# Nominal Data

*Nominal data* is qualitative or descriptive data that has discrete values.

Variable or data columns that contain nominal data are often referred to as *class variables*, *categorical variables*, or *discrete variables*. Nominal data can be used for segmentation or classification.

When a class variable is used as an input to a particular kind of predictive model, such as a regression or neural network model, it must be converted into a numeric form. For example, you could say that the values for gender are 1 and 0, where 1 = *male* and 0 = *female*. When the values are set to 0 and 1, they are also referred to as *indicator variables*. This transformation can be accomplished automatically in modeling software such as SAS Enterprise Miner.

# Ordinal Data

*Ordinal data* is data with categories that have relative importance. The categories can be used to rank strength or severity. For example, you may be familiar with the rankings “Low, Medium, and High.” These have a relative ranking but can’t be compared mathematically.

Numeric values can also be used to denote relative ranking without a mathematic relationship. For example, a list company assigns the values 1 through 5 to denote financial risk. The value 1, characterized by no late payments, is considered low risk. The value 5, characterized by a bankruptcy, is considered high risk. The values 2 through 4 are characterized by various previous delinquencies. A prospect with a risk ranking of 5 is definitely riskier than a prospect with a ranking of 1, but he or she is not five times as risky. And the difference in their ranks, 5 − 1 = 4, has no meaning.