# 528 Appendix B Solutions to Exercises

6. Figure B-17 shows the process of adding the value 56 to the B-tree on the top. To add the new value, you must split the bucket containing the values 52, 54, 55, and 58. You add the value 56 to those, make two buckets, and send the middle value 55 up to the parent node. The parent node doesn't have room for another value, so you must split it too. Its values (including the new one) are 21, 35, 49, 55, and 60. You put 21 and 35 in new buckets and move the middle value 49 up to its parent. This is the root of the tree, so the tree grows one level taller.

![](bbox=[0.135, 0.226, 0.804, 0.683])

Figure B-17: Sometimes bucket splits cascade to the root of a B-tree, and the tree grows taller.