![](bbox=[0.106, 0.082, 0.945, 0.555])

Contextual Interpretation

Figure 15.10 In the current situation, the robot is in Room 1.

the contextual interpretation of on(a,b) is to place block a on block b in Room 1.

# 15.4 Information Extraction

We close with an application of language understanding, namely information extraction. An information extraction system takes as input a body of text, and extracts from it facts concerning pre-specified topics of interest. Figure 15.11 shows an example of how such a system proceeds. The purpose of this particular system is to extract information relative to the domain of natural disasters. The desired information is represented by a template that contains the precise attributes we want to retrieve. In this case they are as follows: Event, Date, Time, Location, Damage, Estimated Losses, and Injuries. In the example in Figure 15.11, the text consists of a paragraph that might appear