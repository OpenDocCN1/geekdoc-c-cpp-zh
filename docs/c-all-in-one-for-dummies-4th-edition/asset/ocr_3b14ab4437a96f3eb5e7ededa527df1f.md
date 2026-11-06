This list represents nine objects interacting with each other in different ways. You could try to make all the objects communicate directly with each other. In the code, making them communicate would mean that most of the classes would have to contain references to objects of the other classes. That technique could get pretty confusing.

Figure 4-1 shows a hierarchy of the interactions between classes that demonstrates that you don’t have to have every class communication directly with every other class.

![](bbox=[0.259, 0.283, 0.656, 0.755])

**FIGURE 4-1:** A model of the hierarchy between classes.

# Outlining the car example

In the example, when there’s a hill, the road angle either increases or decreases, depending on the side of the hill you’re on (uphill or downhill). The road does not need to know about all the other car parts. Instead, it just informs the mediator of the change. The mediator then informs the necessary car parts.