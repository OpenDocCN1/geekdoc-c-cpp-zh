![](bbox=[0.171, 0.106, 0.739, 0.454])

![](bbox=[0.129, 0.501, 0.806, 0.733])

performs up casting by extracting only the Student object from the AssistantProf object. This is very well possible because the Student object is stored at contiguous memory locations within AssistantProf object as shown in Figure 14.63. However, as seen from the figure, the two pieces of Professor object are not stored at contiguous memory locations within o1. Hence, it is practically not possible to extract the complete Professor object out of o1, which means that you cannot perform up casting to Professor type. This is clearly not acceptable; and hence this means that the design given in Figure 14.63 for an object of class AssistantProf is wrong and unacceptable.