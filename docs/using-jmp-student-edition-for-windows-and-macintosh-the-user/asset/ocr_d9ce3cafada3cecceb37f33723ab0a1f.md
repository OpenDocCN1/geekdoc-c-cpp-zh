# Excluded, Hidden, and Deleted Samples

The following table summarizes the effects of various conditions on samples and subgroups:

# Table 7.3 Excluded, Hidden, and Deleted Samples

| | |
|---|---|
| Sample is excluded before creating the chart. | Sample is not included in the calculation of the limits, but it appears on the graph. |
| Sample is excluded after creating the chart. | Sample is included in the calculation of the limits, and it appears in the graph. Nothing will change on the output by excluding a sample with the graph open. |
| Sample is hidden before creating the chart. | Sample is included in the calculation of the limits, but does not appear on the graph. |
| Sample is hidden after creating the chart. | Sample is included in the calculation of the limits, but does not appear on the graph. The sample marker will disappear from the graph, the sample label will still appear on the axis, but limits remain the same. |
| Sample is both excluded and hidden before creating the chart. | Sample is not included in the calculation of the limits, and it does not appear on the graph. |
| Sample is both excluded and hidden after creating the chart. | Sample is included in the calculation of the limits, but does not appear on the graph. The sample marker will disappear from the graph, the sample label will still appear on the axis, but limits remain the same. |
| Data set is subsetted with Sample deleted before creating chart. | Sample is not included in the calculation of the limits, the axis will not include a value for the sample, and the sample marker does not appear on the graph. |
| Data set is subsetted with Sample deleted after creating chart. | Sample is not included in the calculation of the limits, and does not appear on the graph. The sample marker will disappear from the graph, the sample label will still be removed from the axis, the graph will shift, and the limits will change. |

Some additional notes:

+   1. Exclude and Hide operate only on the row state of the first observation in the sample. For example, if the second observation in the sample is hidden, while the first observation is not hidden, the sample will still appear on the chart.
+   2. An exception to the exclude/hide rule: Tests for Special Causes can flag if a sample is excluded, but will not flag if a sample is hidden.

# Shewhart Control Charts

Shewhart control charts are broadly classified into control charts for variables and control charts for attributes. Moving average charts are special kinds of control charts for variables.

The Control Chart platform in JMP-SE implements a variety of control charts: