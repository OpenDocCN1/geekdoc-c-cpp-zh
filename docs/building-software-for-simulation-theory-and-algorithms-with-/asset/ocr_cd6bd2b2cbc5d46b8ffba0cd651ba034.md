segments that either (1) have exactly one event, which starts the trajectory, or (2) contain no events. Specifically, a trajectory $x[t_{\alpha},t_{\beta})$ with events at times $t_1,\ldots,t_n$ is broken into the pieces $x_{\alpha},x_1,\ldots,x_n$ such that the initial segment $x_{\alpha}$ is defined over the interval $[t_{\alpha},t_1)$, the intermediate $x_k$, with $1\leq k<n$, which are defined over $[t_k,t_{k+1})$, and the terminal segment $x_n$ is defined over $[t_n,t_{\beta})$. The segments $x_1, x_2,\ldots,x_n$ are equal to $\Phi$ everywhere except at their beginning. The exception is $x_{\alpha}$, which contains only $\Phi$ if $t_{\alpha}<t_1$ or has an empty domain with $\ell(x_{\alpha})=0$ otherwise. If $x_{\alpha}$ has no events or contains only a single event at its beginning, then it is already primitive.

The function $\delta$ takes an initial total state and a primitive segment $x[t_0,t_f)$ and returns the total state at the end of that segment. This is the discrete-event analog of the single-step transition function of a discrete-time system, but $\delta$ is complicated by the ability of the discrete-event system to take autonomous action. To traverse $x$, several small steps may be required by the time advance function and, consequently, $\delta$ is defined recursively. The recursion has five cases: input at the start of the trajectory, input and autonomous action that occur simultaneously, intermediate autonomous action, no action, nonaction while advancing to intermediate events, and termination at the end of the trajectory.

Definitive action by the system is required in the first three cases, and for each a function is defined to describe the system’s response. The effect of autonomous action is given by the internal transition function; it has the form

$$\delta_{\mathrm{int}}: S\to S$$

and takes the system from its state at the time of the autonomous event to a subsequent state. The effect of an input is given by the external transition function. It gives the next state as a function of the total state $(s,e)$ at the time of the input and the input itself; it has the form

$$\delta_{\mathrm{ext}}: Q\times X\to S$$

where $Q$ is the total set of states defined by Equation 4.6. It is possible for an autonomous action and an input to occur at the same time, and this case is the province of the confluent transition function. This is really a special case of the external transition function where $e=t_a(s)$; it has the form

$$\delta_{\mathrm{con}}: S\times X\to S$$

From an initial state $(s,e)\in Q$, $\delta$ gives the response of the system to a primitive trajectory $x[t_0,t_f)$ as

$$\delta((s,e),x[t_0,t_f))=\tag{4.7}$$

+   1. Input event at the beginning: $\delta((\delta_{\mathrm{ext}}(s,e,x(t_0)),0),x[t_0,t_f))$ if $x(t_0)\neq\Phi\land e<t_a(s)$