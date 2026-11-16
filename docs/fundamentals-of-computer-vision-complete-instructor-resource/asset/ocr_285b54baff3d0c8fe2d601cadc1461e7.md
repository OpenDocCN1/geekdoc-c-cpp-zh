Assignment 7.4: Prove that dilation is increasing.

Assignment 7.5: Let C be the class of binary images that have only **one** dark pixel. For a particular image, let that pixel be located at $(i_0, j_0)$.

Using erosion and dilation by kernels that have $(0, 0)$ as an element, devise an operator, that is, a set of erosions and dilations, and structuring elements (you may need only one s.e. or you may need more than one), which when applied to an element of C, would output an image with the dark pixel shifted to $(i_0 + 2, j_0 + 1)$. Disregard boundaries.

Assignment 7.6: Which of the following statements is correct? (You should be able to reason through this, without doing a proof.)

+   1) $(A \ominus B) \ominus C = A \ominus (B \ominus C)$
+   2) $(A \ominus B) \ominus C = A \ominus (B \oplus C)$ (7.32)

Assignment 7.7: Use the thresholded images you created in Assignment 5.4 or (it's up to the instructor) Assignment 5.5. Choose a suitable structuring element, and apply opening to remove the noise.

Assignment 7.8: In section 7.4, a mask (Figure 7.16) is given and it is stated that application of this mask produces a distance transform that is "not a bad approximation" to the Euclidean distance from the interior point to the nearest edge point. How bad is it? Apply the algorithm to the following image:

```
∞ ∞ ∞ ∞
∞ ∞ ∞ ∞
∞ ∞ 0 ∞
∞ ∞ 0 ∞
∞ 0 0 ∞
∞ 0 0 ∞
```

Your instructor may ask you to do this by hand. Show the output after each pass through the program, or your instructor may ask you to write a program.

> CAUTION: If you do this manually, it can be tedious and time-consuming, as you will need to compute by hand a number of steps (something like fifteen). Or, if you write a program: That can be time-consuming too. Be sure you allocate sufficient time.

Assignment 7.9: Consider a region with an area of 500 pixels of which 120 pixels are on the boundary. You need to find the distance transform from each pixel in the interior to the boundary, using the Euclidean distance. (Note: Pixels on the boundary are not considered in the region – at least in this problem). What is the computational complexity? (Note: You may come up with some algorithm more clever than that used to produce any of the answers below, so if your algorithm does not produce one of these answers, explain it.)

+   a) 60,000
+   b) 120,000
+   c) 45,600
+   d) 91,200