Notice that in the first diagram of Figure 18-7, `list[0] > list[1]`. Therefore, `list[0]` and `list[1]` are swapped. In the second diagram, `list[1]` and `list[2]` are compared. Because `list[1] < list[2]`, they do not get swapped. The third diagram of Figure 18-7 compares `list[2]` with `list[3]`; because `list[2] > list[3]`, `list[2]` is swapped with `list[3]`. Then in the fourth diagram, we compare `list[3]` with `list[4]`. Because `list[3] > list[4]`, `list[3]` and `list[4]` are swapped.

After the first iteration, the largest element is at the last position. Therefore, in the next iteration, we consider the `list[0...3]`.

# **Iteration 2:** Sort `list[0...3]`. Figure 18-8 shows how the elements of list get rearranged in the second iteration.

![](bbox=[0.309, 0.386, 0.769, 0.514])

Figure 18-8. Elements of `list` during the second iteration

The elements are compared and swapped as in the first iteration. Here, only the list elements `list[0]` through `list[3]` are considered. After the second iteration, the last two elements are in the right place. Therefore, in the next iteration, we consider `list[0...2]`.

# **Iteration 3:** Sort `list[0...2]`. Figure 18-9 shows how the elements of list get rearranged in the third iteration.

![](bbox=[0.373, 0.766, 0.754, 0.887])

Figure 18-9. Elements of `list` during the third iteration