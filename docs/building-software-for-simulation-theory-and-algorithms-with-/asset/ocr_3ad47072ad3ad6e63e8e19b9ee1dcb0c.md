```
~~~text
1  procedure route(parent,d,y^b)
2  foreach d' ∈ E_d do
3      d' is an atomic component of parent
4      if d' is atomic then
5          x_{d'}^b ← x_{d'}^b ∪ z_{d,d'}(y^b)
6      d' is a network component of parent
7      else if d' ≠ parent then
8          route(d',d,z_{d,d'}(y^b))
9      Else if this is an output from parent
10     else if d' = parent and PARENT(d') exists then
11         route(PARENT(d'),d',z_{d,d'}(y^b))
12     end
13 end
~~~
```

**Algorithm 3.6** Procedure to route input and output within a network model. The set E_d of influencees and coupling functions z_{d,d'} belong to the network parent.

The other two parts of the routing problem—putting input into a network model and observing output from a network model—are conveniently solved by Algorithm 3.6. An input x^b is injected into a network N by calling route with N for the first and second arguments (i.e., parent = d = N) and x^b for the third argument. A network model produces an output whenever the third condition is true (i.e., the “output from parent” condition), and EventListeners registered with the Simulator are notified when this occurs.

Algorithm 3.7 describes the complete simulation procedure. It applies an input trajectory x < t_0, t_n > to a network N with a set of atomic components A_N. For each component d ∈ A_N there is a bag x^b_d of input and its state s_d. Notifications for EventListeners have been omitted even though they will appear in the implementation.

```
~~~text
1  for t_k ∈ < t_0, t_n > do
2      Clear the bags of input
3      foreach d ∈ A_N do
4          x_{d}^b ← ∅
5      end
6      Route the input to N
7      route(N,N,x(t_k))
8      Compute and route output from the components
9      foreach d ∈ A_N do
10         route(PARENT(d),d,z_{d,d}(s_d))
11     end
12     Change the state of the components
13     foreach d ∈ A_N do
14         s_d ← δ_d(s_d, x_d^b)
15     end
16 end
~~~
```

**Algorithm 3.7** Bottom-up simulation algorithm for a discrete-time model.