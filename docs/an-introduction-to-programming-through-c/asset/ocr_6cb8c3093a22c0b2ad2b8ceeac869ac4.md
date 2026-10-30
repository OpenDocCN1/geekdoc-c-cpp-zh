# 22.1.5  Drawing the formula: overview

The input to the drawing step is a formula, and an indication of where it is to be drawn on the canvas. It is natural that the formula is presented to us as a node f, which is the root of the tree representing the formula that is to be drawn. We will abuse terms and let f denote the formula as well. As to where to draw it, presumably the user will tell us something like “Draw the formula below and to the right of some point (x, y).” The values x, y will be given by the user. Then our goal is to draw the given formula f such that the top left corner of its bounding box is at the point (x, y) on the canvas.

How do we perform our task? It would seem natural to consider recursion. Presumably primitive formulae are the base case, and clearly we can write out the required text wherever required. So let us consider a non primitive formula f / g. Perhaps we should recursively draw f then draw the horizontal bar denoting the division, and then recursively draw g. However, in order to draw f we need to know the width of g, so that we can center them with respect to the horizontal bar (Section 22.1.2). To draw g we need to know the width of f, and also the height of f.

So it is natural to have a calculation phase before we draw anything. In this phase we calculate the width and height of the layouts of the different subformulae in our formula. We also determine the operator level. More specifically we determine for each subformula a parameter called descent, which is the distance of the operator level from the bottom of the formula. Likewise we define the ascent to be the distance of the operator level from the top of the formula. Once we know the width, height, ascent and descent, we start the actual drawing. Note that the height is just the sum of the ascent and the descent, so we ignore the height in what follows. If f is a formula, we will use w_f, a_f, d_f to denote the width, ascent and the descent of the layout of f.

Our algorithm to determine these parameters will be recursive. Suppose f is some identifier x. Then the width of x can be determined using the call textWidth(x). The height of x does not depend upon x, and can be determined by calling textHeight(). We will assume that the + symbol must align with the center of x. Thus we will have ascent and descent to be both textWidth(x)/2.

So next consider formulae of the form (f+g). This is shown in Figure 22.3(a). The dashed line is the operator level, for f, g and also f + g. From the picture we have:

$$a_{f+g}=\max(a_f,a_g)$$

$$d_{f+g}=\max(d_f,d_g)$$

$$w_{f+g}=w_f+w_\circ+w_g$$

where w_\circ is the width of the + symbol. In the figure we have also marked the top left corners of the layouts f, g, f + g. This will be used in Section ??.

In Figure 22.3(b) we consider formulae of the form f/g. We first note that

$$w_{f/g}=\max(w_f,w_g)$$

We remarked earlier that the operator level of f / g is at the position of the horizontal bar. Above the bar we have the entire formula f and half the height needed to accommodate the horizontal bar. Similarly below we have the formula g and half the height required for the