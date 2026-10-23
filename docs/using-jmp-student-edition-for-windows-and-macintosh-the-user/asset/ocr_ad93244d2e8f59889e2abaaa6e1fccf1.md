+   • The control limits on a Shewhart control chart are commonly specified as 3σ limits. On a cusum chart, the limits are determined from average run length, from error probabilities, or from an economic design.

A cusum chart is more efficient for detecting small shifts in the process mean. Lucas (1976) comments that a V-mask detects a 1σ shift about four times as fast as a Shewhart control chart.

# Launch Options for Cusum Charts

When you choose Graph > Control Charts > Cusum, the Control Charts Launch dialog appears, including appropriate options and specifications as shown here.

![](bbox=[0.39, 0.28, 0.6, 0.42])

Note: The following items pertain only to cusum charts:

# Two Sided

requests a two-sided cusum scheme when checked. If it is not checked, a one-sided scheme is used and no V-mask appears. If an H value is specified, a decision interval is displayed.

# Data Units

specifies that the cumulative sums be computed without standardizing the subgroup means or individual values so that the vertical axis of the cusum chart is scaled in the same units as the data.

Note: Data Units requires that the subgroup sample size be designated as constant.

# Beta

specifies the probability of failing to discover that the specified shift occurred. Beta is the probability of a Type II error and is available only when you specify Alpha.

# H

is the vertical distance h between the origin for the V-mask and the upper or lower arm of the V-mask for a two-sided scheme. When you click H, the Beta entry box is labeled K. You also enter a value for the increase in the lower V-mask per unit change on the subgroup axis (See Figure 7.26). For a one-sided scheme, H is the decision interval. Choose H as a multiple of the standard error.

# Specify Stats

appends the panel shown here to the Control Charts Launch dialog, which lets you enter the process variable specifications.