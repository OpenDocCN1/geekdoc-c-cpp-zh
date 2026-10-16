# 12.3.1 Simple Selection Sort

The basic idea of a selection sort of a list is to make a number of passes through the list or a part of the list, and on each pass select one item to be correctly positioned. For example, on each pass through a sublist, the smallest item in the sublist might be found and moved to its proper position.

As an illustration, suppose that the list 67, 33, 21, 84, 49, 50, 75 is to be sorted into ascending order:

![](bbox=[0.297, 0.203, 0.655, 0.271])

We locate the smallest item and find it in the third position:

![](bbox=[0.293, 0.253, 0.655, 0.277])

We interchange this item with the first item and thus properly position the smallest item at the beginning of the list:

![](bbox=[0.293, 0.355, 0.654, 0.402])

We now consider the sublist consisting of the items from position 2 on,

![](bbox=[0.294, 0.453, 0.655, 0.477])

to find the smallest item and exchange it with the second item (itself in this case) and thus properly position the next-to-smallest item in position 2:

![](bbox=[0.294, 0.574, 0.655, 0.631])

We continue in this manner, locating the smallest item in the sublist of items from position 3 on and interchanging it with the third item, then properly positioning the smallest item in the sublist of items from position 4 on, and so on until we eventually do this for the sublist consisting of the last two items:

![](bbox=[0.328, 0.738, 0.62, 0.776])

![](bbox=[0.328, 0.789, 0.62, 0.824])

![](bbox=[0.328, 0.842, 0.62, 0.877])

![](bbox=[0.328, 0.893, 0.62, 0.928])