For example in the given set of numbers:

30, 12, 16, 11, 24, 35, 56, 51, 45 35 is the pivot element which is placed as per the mentioned example. This way, the whole list is partitioned into two sub-lists, one which is less than or equal to pivot element and the other, which is greater than or equal to the pivot element.

Now each partition will have its own pivot element which will be assigned to the first element in the partition. The partitions are further divided into sub-partitions to have their own pivot elements, until each partition has either one element or null towards left or right.

Once all the portions have been successfully sorted, all the portions are united to form a sorted list. Let us consider the given list of numbers which have to be sorted using the quick sort method. 35,56,51,45,30,12,16,11,24. Now, the first element 35 is designated the pivot element. 35 is compared with the remaining list towards the right until it reaches the first element less than itself (in this case 30).

Now let us assign this position a variable x. The element at position x is 30 and it takes the position of the pivot element. All the elements from the pivot element till the element at position (x-1) are moved up the order such that the vacant space at position x is filled.

Hence, you obtain the list as follows:

30,35,56,51,45,12,16,11,24

The same process continues until all the elements toward right of the pivot element are greater than itself.

+   - Step 1: 30, 12, 35, 56, 51, 45, 16, 11, 24.
+   - Step 2: 30, 12, 16, 35, 56, 51, 45, 11, 24.
+   - Step 3: 30, 12, 16, 11, 35, 56, 51, 45, 24.
+   - Step 4: 30, 12, 16, 11, 24, 35, 56, 51, 45.

Therefore you have obtained the list that was given to you as an example in the beginning of the topic, now all the elements towards left are identified as one portion having 30 as their new pivot element. And all the elements towards right are identified to be next portion having 56 as their new pivot element.

{30, 12, 16, 11, 24} 35 {56, 51, 45}

Now each partition is independently sorted as follows.

+   - Step 1: {12, 30, 16, 11, 24} 35 {56, 51, 45}