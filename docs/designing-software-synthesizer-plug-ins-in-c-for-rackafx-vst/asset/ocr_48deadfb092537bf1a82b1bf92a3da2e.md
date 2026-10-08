previous samples and not the passing value of the current output y, and the other that depends on the input summed something that depends on the current output y. These are combined together in an equation that runs the delay-loop less an infinite number of times in a single sample period. With a part series algebra, it reduces down to a very manageable simple difference equation. The structure is synthesized by inspection of the equation or the value of u loop input.

![](bbox=[0.335, 0.45, 0.953, 0.295])

For a single loop system, the five-step process is:

+   1. Disconnect the loop by severing the input point at the node u so that the output of the summer and to the loop are open; insert 0.0 into the feed-forward path, around the feedback loop, and into the summer, forming a temporary u₀(n). This includes any processing that occurred in the loop.

+   2. This step is modified to accommodate processing in the feed-forward path. If there is nothing except a short in the feed-forward path, y₀(n) = u₀(n) and the Normal Hàrm method is used. If there is only a gain K in the forward path, y₀(n) = Ku(n). However, if there is processing that includes samples in the forward path, then you form the temporary y₀(n) = u₀(n) through the filter (or series or parallel filters). If the filters use only the linear difference equations, y(n) will have two components: y₀ is the part that depends on the only loop input u₀(n) and yS(n) is the part that depends on the past samples so y₀(n) = y₀(n) + yS(n).

+   3. Find the overall gain coefficient X by creating a delay-free structure that is the original filter structure with all delay elements removed/disconnected and apply an input of 1.0 into the loop with the filter input disconnected; the gain elements are multiplied together.

+   4. The final difference equation is found with Equation 4.39, and it reveals the modified structure by inspection; remember that each delay-loop will will be relocated to the output of one or more delay elements in the overall filter structure.

> y(n) = \frac{y_0(n)}{1-X} + y_S(n) \quad (4.39)

+   5. When implementing the filter, we would like to solve for u(n), the input loop value. We can then push that value through the processing blocks. This value will also help derive the final structure.

The best way to explain this is by example. After just a bit of practice, you will be impressed at the speed with which you can synthesize these structures. Figure 4.23 shows the first.

Step 1:

Break the feedback loop at node u and drive it with 0.0 input as shown in Figure 4.24 (a), then find the temporary value u₀. The output of the loop is S after injecting the 0.0 value through. So the temporary input u is:

Step 2:

```
u₁(n) = x(n) + S(n) \quad (4.40)
```