At this point, you have all the DSP theory tools you need to understand the rest of the classical DSP filters (first-order feed back, second-order feed forward and feed back) as well as many filter design techniques. The rest of the chapter will be devoted to applying these same fundamentals to the other classical DSP filters but we will move much more quickly, applying each analysis technique to the other algorithms. For example, we will dispense with the evaluation of \(e^{j\omega}\) terms and start off directly in the \(z\) transform of the difference equations.

> The graphical interpretation method of evaluating a filter in the z-plane assumes the filter is normalized so that \(a_0 = 1.0\).

# 5.15 First-Order Feed-Back Filter Revisited

Now let's go through the same analysis technique on the first-order feed-back filter from the last chapter. We can move much more quickly now that we have the basic DSP theory down. There will be many similarities but also several key differences when dealing with feed-back designs. You already saw that the feedback topology can blow up or ring forever and that the feed-forward design cannot. We will find a way to figure out if this is going to happen and how to prevent it. Start with the original first-order feed-back filter (block diagram in Figure 5.25) and its difference equation.

The difference equation is as follows:

\(y(n) = a_0 x(n) - b_1 y(n-1)\) (5.36)

# Step 1: Take the \(z\) transform of the difference equation

This can be done by inspection, using the rules from Section 5.8 (Figure 5.26). Therefore, the \(z\) transform is shown in Equation 5.37.

\(Y(z) = a_0 X(z) - b_1 Y(z) z^{-1}\) (5.37)

![](bbox=[0.25, 0.63, 0.75, 0.76])

Figure 5.25: The first-order feed-back filter.