With this in mind, let's look at a high-dimensional application.

# 7.1.2 Example: production planning

This time, our company makes handwoven carpets, a product for which the demand is extremely seasonal. Our analyst has quoted demand estimates for all the next calendar year: $d_1, \hat{d}_2, \dots, \hat{d}_{12}$. As feared, they are very uneven, ranging from 440 to 920.

Here's a quick snapshot of the company. We currently have 30 employees, of whom makes 20 carpets per month and gets a monthly salary of $2,000. We have no initial status of carpets.

How can we handle the fluctuations in demand? There are three ways:

+   1. Overtime, but this is expensive since overtime is 80% more than pay. Also, workers can put in at most 30% overtime.
2. Hiring and firing, but these cost $320 and $400, respectively, per worker.
3. Storing surplus production, but this costs $8 per carpet per month. We currently have no stored carpets on hand, and we must end the year without any carpets stored.

This rather involved problem can be formulated and solved as a linear program!
A crucial first step is defining the variables.

```
$w_i = \text{number of workers during } i\text{ month}; w_0 = 30$.$\n$x_i = \text{number of carpets made during month } i$.$\n$o_i = \text{number of carpets made by overtime in month } i$.$\n$h_i, f_i = \text{number of workers hired and fired, respectively, at beginning of month } i$.$\n$s_i = \text{number of carpets stored at end of month } i; s_0 = 0$.
```

All in all, there are 72 variables (74 if you count $w_0$ and $s_0$).
We write the constraints. First, all variables must be nonnegative:

```
$w_i, x_i, o_i, h_i, s_i \geq 0, i = 1, \dots, 12$.
```

The total of carpets made per month consists of regular production plus overtime:

```
$x_i = 20w_i + o_i$.
```

(one constraint for each $i = 1, \dots, 12$). The number of workers can potentially change at the start of each month:

```
$w_i = w_{i-1} + h_i - f_i$.
```

The number of carpets stored at the end of each month is what we start with, plus the number we make, minus the demand for the month:

```
$s_i = s_{i-1} + x_i - d_i$.
```