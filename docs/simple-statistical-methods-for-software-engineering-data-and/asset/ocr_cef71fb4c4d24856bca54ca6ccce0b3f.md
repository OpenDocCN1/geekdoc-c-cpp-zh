Deciding on the test cases to be automated is a critical decision. Not every test case could be automated. Some defects could be found only by slow manual testing. Although speed is an advantage, only some test cases should be automated.

# Automation Progress

To track the automation project, we can measure automation progress by setting up the following metric:

```
Automation progress = \frac{Number of test cases actually automated}{Test cases selected for automation} \times 100
```

# Case Study: Defect Age Data

Defect age is a very well-known metric in the industry, but only a limited number of organizations collect this metric. The time defect spends in the product, from injection till resolution, is defect age. This can be calculated from the defect data in the bug tracker if appropriate fields have been set and populated. The fields required are phase injected and phase detected. It is now evident that the defect database is maintained throughout the project life cycle. Moreover, the information in the column phase injected is only obtained by reasoning during causal analysis and not from the log book. The term data in testing includes even reasoned, intuitive judgments.

```
Defect age = 1 + phase detected – phase injected
```

Some people use the formula without the “1”; they just recognize the incremental difference and choose to keep the base value at 0. If a defect is detected in the same phase where it was injected, defect age is 1. If discovery happens in the next phase, defect age is 2. If a defect is injected during the requirement phase but discovered in the test phase, defect age is 4.

This case study is about a testing project with a defect database with 32 fields and quite rich in raw data. However, no one derived the metric defect age although the possibility was there.

Much after the release, data mining by a QA analyst revealed the defect age metric. Motivation for this metric creation from available data had come from an unexpected direction. Managers asked for a model for defect economics, and one of the factors driving cost was obviously defect age. Supporting metrics in this model building were the cost of finding defects and the cost of fixing defects. Both could be calculated from the data available in the database. The cost of finding defects was labeled as part of the cost of appraisal, and the cost of fixing