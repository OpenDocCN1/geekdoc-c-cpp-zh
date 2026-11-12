37. Consider capital-loss. Identify the outliers in capital-loss using the Z-score method. How many outliers are there?

38. Construct a bar graph of Income for these outlier records.

39. Construct a bar graph of Income for the adult_ch3_training data set as a whole, without omitting the outliers.

40. Compare your bar graphs from the previous two exercises. Describe the difference between the two bar graphs. Describe the change to the character of the data set that will result if we delete these outlier records. State your conclusion regarding deleting outliers at the EDA stage.

41. Derive a flag for capital-loss, called capital-loss-flag, which equals 0 when capital-loss equals 0, and 1 otherwise. Provide a bar graph of capital-loss-flag.

42. Repeat the previous exercise for capital-gain-flag.

43. Construct a contingency table of capital-loss-flag vs Income. Include counts and column percentages. Clearly describe the effect of having any capital losses on Income.

44. Construct a contingency table of capital-gain-flag vs Income. Include counts and column percentages. Clearly describe the effect of having any capital gains on Income.

45. To prepare for further work, rename workclass as workclass-old, marital-status as marital-status-old, and occupation as occupation-old.

46. Construct a contingency table with income for the rows and workclass-old for the columns, asking for counts and column percentages.

47. Referring to the contingency table from the previous exercise, do the following:
a. Provide a one-sentence rationale for why we should combine never-worked and without-pay into no-pay.
b. Provide a one-sentence rationale for why we may combine local-gov and state-gov into state-local-gov.

48. Perform the changes mentioned in the previous exercise, along with changing "?" to "unknown". Call the new variable workclass. Construct a contingency table with Income for the rows and workclass for the columns, with counts and column percentages. Describe your table using a couple of sentences.

49. Construct a contingency table with income for the rows and marital-status-old for the columns, asking for counts and column percentages.

50. Referring to the contingency table from the previous sentence, provide two sentences of rationale for why we should combine Married-AF-spouse and Married-civ-spouse into the new category Married, and combine the other statuses into the new category Other.

51. Perform the changes mentioned in the previous exercise. Construct a contingency table with income for the rows and marital-status for the columns, with counts and column percentages. Describe your table using a couple of sentences.

52. Construct a contingency table with income for the rows and occupation-old for the columns, asking for counts and column percentages.