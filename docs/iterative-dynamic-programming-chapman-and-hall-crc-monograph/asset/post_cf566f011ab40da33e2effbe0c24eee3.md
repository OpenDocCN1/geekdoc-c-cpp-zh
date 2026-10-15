
for the other 9 sets and the table is completed, showing the minimum costs for three jobs.

## Table 3.2: Order and minimum cost for 3 jobs

| Ordered Jobs | Minimum cost |
|---|---|
| $J_2 J_1 J_3$ | $c_2(\tau_2) + c_1(\tau_2 + \tau_1) + c_3(\tau_1 + \tau_2 + \tau_3)$ |
| $J_3 J_1 J_4$ | $c_3(\tau_3) + c_1(\tau_3 + \tau_1) + c_4(\tau_1 + \tau_3 + \tau_4)$ |
| $J_1 J_4 J_2$ | $c_1(\tau_1) + c_4(\tau_4 + \tau_1) + c_2(\tau_1 + \tau_4 + \tau_2)$ |
| $J_1 J_5 J_3$ | $c_1(\tau_1) + c_5(\tau_5 + \tau_1) + c_3(\tau_1 + \tau_5 + \tau_3)$ |
| $J_2 J_3 J_4$ | $c_2(\tau_2) + c_3(\tau_2 + \tau_3) + c_4(\tau_2 + \tau_3 + \tau_4)$ |
| $J_4 J_2 J_5$ | $c_4(\tau_4) + c_2(\tau_4 + \tau_2) + c_5(\tau_4 + \tau_2 + \tau_5)$ |
| $J_2 J_5 J_1$ | $c_2(\tau_2) + c_5(\tau_2 + \tau_5) + c_1(\tau_2 + \tau_5 + \tau_1)$ |
| $J_4 J_3 J_5$ | $c_4(\tau_4) + c_3(\tau_4 + \tau_3) + c_5(\tau_4 + \tau_3 + \tau_5)$ |
| $J_3 J_5 J_2$ | $c_3(\tau_3) + c_5(\tau_3 + \tau_5) + c_2(\tau_3 + \tau_5 + \tau_2)$ |
| $J_5 J_4 J_1$ | $c_5(\tau_5) + c_4(\tau_5 + \tau_4) + c_1(\tau_5 + \tau_4 + \tau_1)$ |

Now we proceed to stage 2 where 4 jobs are to be considered. There are 5 possible sets of 4 jobs that can be chosen from 5 jobs. Let us choose the set consisting of jobs $J_1$, $J_2$, $J_3$, and $J_5$. We use the information in Table 3.2 to determine the order and the minimum cost for the first three jobs, and we simply add the cost of doing the last job. If $J_1$ is done last, then we know the order in which jobs $J_2$, $J_3$ and $J_5$ are to be done and the cost associated with these three jobs from Table 3.2. All that is necessary is to add the additional cost $c_1(\tau_2 + \tau_3 + \tau_5 + \tau_1)$. We proceed for the other three cases, where $J_2$, $J_3$, or $J_5$ is done last as before and compare the 4 cost values to give the arrangement yielding the smallest cost. Repeating the procedure with the other 4 sets provides the information that can be displayed in Table 3.3.

## Table 3.3: Order and minimum cost for 4 jobs

| Ordered Jobs | Minimum cost |
|---|---|
| $J_1 J_4 J_2 J_3$ | $c_1(\tau_1) + c_4(\tau_4 + \tau_1) + c_2(\tau_1 + \tau_4 + \tau_2) + c_3(\tau_1 + \tau_4 + \tau_2 + \tau_3)$ |
| $J_1 J_5 J_3 J_4$ | $c_1(\tau_1) + c_5(\tau_5 + \tau_1) + c_3(\tau_1 + \tau_5 + \tau_3) + c_4(\tau_1 + \tau_5 + \tau_3 + \tau_4)$ |
| $J_4 J_2 J_5 J_1$ | $c_4(\tau_4) + c_2(\tau_4 + \tau_2) + c_5(\tau_4 + \tau_2 + \tau_5) + c_1(\tau_4 + \tau_2 + \tau_5 + \tau_1)$ |
| $J_4 J_3 J_5 J_2$ | $c_4(\tau_4) + c_3(\tau_4 + \tau_3) + c_5(\tau_4 + \tau_3 + \tau_5) + c_2(\tau_4 + \tau_3 + \tau_5 + \tau_2)$ |
| $J_3 J_5 J_2 J_1$ | $c_3(\tau_3) + c_5(\tau_3 + \tau_5) + c_2(\tau_3 + \tau_5 + \tau_2) + c_1(\tau_3 + \tau_5 + \tau_2 + \tau_1)$ |

Let us now proceed to stage 1 where 5 jobs are to be considered. There is only one set to consider. We ask ourselves which job is to be done last. If $J_4$ is done last, then the minimum cost of doing the other 4 jobs is obtained from the last line of Table 3.3 and we simply add the cost of doing $J_4$, namely, $c_4(\tau_1+\tau_2+\tau_3+\tau_4+\tau_5)$. Similarly, we find from the second line of Table 3.3 the order and the minimum cost of doing the first four jobs if $J_2$ is done last and simply add the cost $c_2(\tau_1+\tau_2+\tau_3+\tau_4+\tau_5)$. We continue the process for when $J_3$ is done last, when $J_4$ is done last, and when $J_1$ is done last. These 5 values of cost are compared and the minimum of these gives us the order of the 5 jobs such that the cost is minimized.

We see in this example that the calculations proceed in a systematic way, so that at each stage the optimization involves only the addition of a single job to those that have been already optimally calculated. The procedure is ideally suited for the use of a digital computer where the same calculational procedure is used repeatedly numerous times. Instead of simply providing a numerical approach to optimization problems, dynamic programming also provides functional relationships as can be seen in the next example.

## 3.2.3 The stone problem

Let us illustrate the use of dynamic programming in solving the problem of how high a stone rises when tossed upwards with a velocity of $v_0$. Let us assume that air resistance cannot be ignored, so the equation of motion for the stone can be written as

$$\frac{dv}{dt}=-g-kv^2 \tag{3.2}$$

with the initial condition $v=v_0$ at $t=0$. It is clear that the height is a function of the initial velocity. Let us break the trajectory into two parts: the first part is the short distance the stone travels in a short time $\Delta t$ and the second part is the remainder of the trajectory

$$h(v_0)=v_0\Delta t+h\left(v_0+\frac{dv}{dt}\Delta t\right)+O(\Delta t^2). \tag{3.3}$$

Now let us expand the second term on the right hand side by Taylor series, retaining only the first two terms, and using Eq. (3.2) to give

$$h(v_0)=v_0\Delta t+h(v_0)-[(g+kv_0^2)\Delta t]\frac{dh(v_0)}{dv_0}+O(\Delta t^2). \tag{3.4}$$

When we rearrange Eq. (3.4) and divide by $\Delta t$, we get

$$\frac{dh(v_0)}{dv_0}=\frac{v_0}{g+kv_0^2}+O(\Delta t). \tag{3.5}$$

Now we let Δt → 0 to yield a first order ordinary differential equation

$$\frac{dh(v_0)}{dv_0}=\frac{v_0}{g+k v_0^2},\qquad (3.6)$$

which can be immediately integrated with the given initial condition to give

$$h(v_0)=\frac{1}{2k}\ln\left(1+\frac{k v_0^2}{g}\right).\qquad (3.7)$$

When $k$ is negligibly small then we see that $h(v_0)\to v_0^2/2g$, a result which can be obtained by equating the kinetic energy at the initial time and the potential energy at the maximum height.

## 3.2.4 Simple optimal control problem

Let us consider a rather simple optimal control problem where a linear discrete scalar system is given in the form

$$x(k+1)=a x(k)+b u(k),\qquad k=0,1,2,\cdots,P-1,\qquad (3.8)$$

where the initial state $x(0)$ is given, and the final state $x(P)=0$. We assume there are no constraints placed on the control $u(k)$. The optimal control problem is to choose $u(k),k=0,1,2,\cdots,P-1$ so that the performance index

$$I[x(0),P]=\sum_{k=1}^{P}[x^2(k)+u^2(k-1)]\qquad (3.9)$$

is minimized. Here we have shown the explicit dependence of the performance index on the initial state and the number of steps $P$. Naturally the performance index is also a function of the control policy which has to be chosen for minimization. To solve this problem by dynamic programming we first consider a single stage problem and then progressively increase the number of stages until the posed problem is solved.

$P = 1$

When we have a single stage problem, the performance index is

$$I[x(0),1]=x^2(1)+u^2(0)\qquad (3.10)$$

and no minimization is possible, since the specification of the final condition requires that we use

$$u(0)=\frac{x(1)-a x(0)}{b}=-\frac{a}{b}x(0).\qquad (3.11)$$

The value of the performance index is

$$I[x(0),1]=\frac{a^2}{b^2}x^2(0).\qquad (3.12)$$

Next we consider $P = 2$ stages.

### $P = 2$

With two stages we start at $x(0)$ proceed to $x(1)$ and then go to $x(2)=0$. The performance index to be minimized is

$$I[x(0),2]=x^2(1)+u^2(0)+x^2(2)+u^2(1)=x^2(1)+u^2(0)+u^2(1). \tag{3.13}$$

Once we get to $x(1)$, we already know how to get to $x(2)=0$, because that is a 1-stage problem that was solved above. We therefore have

$$u(1)=-\frac{a}{b}x(1). \tag{3.14}$$

The performance index becomes

$$I[x(0),2]=\left(1+\frac{a^2}{b^2}\right)x^2(1)+u^2(0). \tag{3.15}$$

By using Eq. (3.8) with $k=0$, we can rewrite the performance index as an explicit function of $u(0)$ only, namely,

$$I[x(0),2]=\left(1+\frac{a^2}{b^2}\right)[ax(0)+bu(0)]^2+u^2(0). \tag{3.16}$$

Differentiating Eq. (3.16) with respect to $u(0)$ gives

$$\frac{dI[x(0),2]}{du(0)}=2b\left(1+\frac{a^2}{b^2}\right)[ax(0)+bu(0)]+2u(0). \tag{3.17}$$

Since the second derivative of the performance index is positive, the choice of $u(0)$ to minimize the performance index is obtained from the stationary condition that yields

$$u(0)=-\left(\frac{ab+(a^3/b)}{1+a^2+b^2}\right)x(0). \tag{3.18}$$

We are now ready to consider $P=3$ stages.

### $P = 3$

The pattern for calculations becomes clear with the addition of one more stage. With $P=3$, the performance index is

$$I[x(0),3]=x^2(1)+u^2(0)+x^2(2)+u^2(1)+u^2(2), \tag{3.19}$$

since $x(3)=0$. Here we know that the optimal choices for $u(2)$ and $u(1)$, as determined before, are

$$u(2)=-\frac{a}{b}x(2). \tag{3.20}$$
