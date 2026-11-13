+   (C,G) 5
+   (G,E) 5
+   (A,G) 6
+   (F,E) 6
+   (E,D) 7
+   (A,F) 8
+   (B,G) 9

Now connect and every edge from the beginning of the above list and if a closed path is found then discard that edge.

+   (B,C)
+   
+   B ---1--- C

+   (G,D)
+   
+   B ---1--- C
+   
+   G ---2--- D

+   (C,D)
+   
+   B ---1--- C ---3--- D
+   
+   G ---2--- D

+   (F,G)
+   
+   B ---1--- C ---3--- D
+   
+   G ---2--- D
+   
+   F ---4--- G