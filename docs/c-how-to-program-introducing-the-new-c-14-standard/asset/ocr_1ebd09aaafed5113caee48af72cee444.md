# 19.3.8 Member Function `print`

Function `print` (Fig. 19.5, lines 113–129) first determines whether the list is *empty* (line 114). If so, it prints `"The list is empty"` and returns (lines 115–116). Otherwise, it outputs the value in each node. The function initializes `currentPtr` with `firstPtr` (line 119), then prints the string `"The list is: "` (line 121). While `currentPtr` is not `nullptr` (line 123), `currentPtr->data` is printed (line 124) and `currentPtr` is assigned the value of `currentPtr->nextPtr`.

![](bbox=[0.116, 0.469, 0.824, 0.894])