![](bbox=[0.244, 0.094, 0.765, 0.346])

**FIGURE 4.5:** Contribution by ranging error when using three beacon nodes

$$\sqrt{r_1'^2-d_1'^2}=\sqrt{(r_1\pm\delta)^2-(d_1\pm2\delta)^2}$$

$$=\sqrt{r_1^2-d_1^2\pm2\delta r_1\mp4\delta d_1}\qquad\text{(neglecting }O(\delta^2)\text{ terms).}$$

Thus, the error along the y-axis (along line $TS$ in Figure 4.2) is

$$\left|\sqrt{r_1'^2-d_1'^2}-\sqrt{r_1^2-d_1^2}\right|\leq\frac{2\delta(r_1+2d_1)}{\sqrt{r_1^2-d_1^2}}. \tag{4.9}$$

Thus, from Equations (4.8) and (4.9), the magnitude of the error in the coordinate value of $u$ along the line $B_1B_2$ joining the two beacon nodes is upper bounded by $2\delta$, for a maximum error of $\pm\delta$ in each measured range. However, the error in the coordinate value normal to the line $B_1B_2$ caused by $\pm\delta$ error in each measured range is a function of the distances between the beacon nodes and between $u$ and the beacon nodes and hence cannot be bounded.