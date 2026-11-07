As shown in Figure 18–24, the next element of the list that needs to be moved into a sublist is indicated by `index`. Because `list[index] < pivot`, we need to move the element `list[index]` into the lower sublist. To do so, we first advance `smallIndex` to the next array position and then swap `list[smallIndex]` with `list[index]`. The resulting list is as shown in Figure 18–25. (Notice that 11 is swapped with 9.6.)

![](bbox=[0.198, 0.234, 0.897, 0.374])

**FIGURE 18-25**  List after moving 11 into the lower sublist

Now consider the list in Figure 18–26.

![](bbox=[0.198, 0.465, 0.897, 0.604])

**FIGURE 18-26**  List before moving 58 into a sublist

For the list in Figure 18–26, `list[index]` is 58, which is greater than pivot. Therefore, `list[index]` is to be moved into the upper sublist. This is accomplished by leaving 58 at its position and increasing the size of the upper sublist by one, to the next array position. After moving 58 into the upper sublist, the list is as shown in Figure 18–27.

![](bbox=[0.198, 0.766, 0.897, 0.905])

**FIGURE 18-27**  List after moving 58 into the upper sublist