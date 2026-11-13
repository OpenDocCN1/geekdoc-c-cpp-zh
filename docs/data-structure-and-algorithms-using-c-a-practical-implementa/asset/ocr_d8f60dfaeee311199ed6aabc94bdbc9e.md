FOR TYPE1 :
P = 5*2 + 8*2 + 10*2 + 6*2= 10 + 16 + 20 + 12 = 58

FOR TYPE2 :
P = 10*1 + 5*2 + 8*3 + 6*3 = 10 + 10 + 24 + 18 = 62

FOR TYPE3:
P = 6*1 + 10*2 + 8*3 + 5*3 = 6+20+24+15 = 65

FOR TYPE4:
P = 8*2 + 10*1 + 5*3 + 6*3 = 16+10+15+18 = 59

From the above we observe that different trees have different path lengths even if same type of trees. So problem arises to find the minimum weighted path length. This type of extended binary tree can be obtained by the Huffman algorithm.

# HUFFMAN ALGORITHM

+   STEP1 : Lets Consider there are N numbers of weights as W1,W2,.....,WN

+   STEP2 : Take two minimum weights and create a sub tree. Suppose W1 and W2 are first two minimum weights then sub tree will be of the form

![](bbox=[0.35, 0.52, 0.65, 0.62])

+   STEP3 : Now the remaining weights will be W1 + W2 , W3,.....,WN

+   STEP4 : Create all subtrees at the last weight

# Example

Create a Huffman Tree by considering the numbers as

+   15, 18, 25, 7, 8, 11, 5

+   STEP1: Taking Two nodes with minimum weights as 5 and 7

![](bbox=[0.35, 0.84, 0.65, 0.94])