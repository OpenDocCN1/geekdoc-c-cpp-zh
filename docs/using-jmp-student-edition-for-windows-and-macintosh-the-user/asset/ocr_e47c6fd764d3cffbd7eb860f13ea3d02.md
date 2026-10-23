# Control Charts

Control charts are a graphical and analytic tool for deciding whether a process is in a state of statistical control and for monitoring an in-control process. This monitoring process is often called *quality control* or QC.

# Introduction

Control charts have the following characteristics:

+   - Each point represents a summary statistic computed from a subgroup sample of measurements of a quality characteristic.
+   - The vertical axis of a control chart is scaled in the same units as the summary statistic.
+   - The horizontal axis of a control chart identifies the subgroup samples.
+   - The center line on a Shewhart control chart indicates the average (expected) value of the summary statistic when the process is in statistical control.
+   - The upper and lower control limits, labeled UCL and LCL, give the range of variation to be expected in the summary statistic when the process is in statistical control.
+   - A point outside the control limits signals the presence of a special cause of variation.
+   - Graph > Control Chart subcommands create control charts that can be updated dynamically as samples are received and recorded or added to the data table.

![](bbox=[0.22, 0.62, 0.78, 0.78])

The following example uses the Coating.jmp data in the Quality Control sample data folder (taken from the ASTM Manual on Presentation of Data and Control Chart Analysis). The quality characteristic of interest is the Weight column. A subgroup sample of four is chosen. An X̄-chart and an R-chart for the process are shown in Figure 7.1.

To replicate this example,

Choose the Graph > Control Chart > XBar command.