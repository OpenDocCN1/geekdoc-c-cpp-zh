To move a scroll bar, the user can click on and drag the box, called the knob, in the scroll bar that indicates its current location (in that dimension: up/down or right/left). Alternatively, the user can click in the bar to the right or left of the knob, or on the arrows at either end of the scroll bar, to adjust the location. The programmer can determine how much each of these actions changes the viewing area.

Note that no event listeners need to be set up to use a scroll pane in this manner. A scroll pane responds automatically to the adjustments of its scroll bars.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 11.27 Describe the use of scroll bars on a scroll pane.

+   SR 11.28 What happens if you change the first parameter passed to the Dimension constructor within the TransitMap program to 1000? Explain.

# 11.10 Split Panes

A split pane is a container that displays two components separated by a moveable divider bar. Depending on how the split pane is set up, the two components are displayed either side by side or one on top of the other, as shown in Figure 11.3. In Java, we can create a split pane using the JSplitPane class.

![](bbox=[0.24, 0.68, 0.88, 0.88])

FIGURE 11.3 The configurations of a split pane