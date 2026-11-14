and

$H_s(S) = \frac{1}{\lambda} \sum_{k=-\lfloor s \rfloor}^{S} (g(k) - g(s)) = -K.$

Next we use the identity

$g(k+1) = g(-\lfloor -s \rfloor) + \sum_{j=-\lfloor -s \rfloor}^{k} g'(j+0).$

The second relation writes

$-K\lambda = (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1) + \sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0)(S-j).$

Using the first conditions we can write

(14.11.1) 
 $\sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0)j < K\lambda + (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1);$ 
 $\sum_{j=-\lfloor -s \rfloor}^{S} g'(j+0)j \ge K\lambda + (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1).$

To which we add

(14.11.2) 
 $\sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0) < 0;$ 
 $\sum_{j=-\lfloor -s \rfloor}^{S} g'(j+0) \ge 0.$

# 14.11.2. APPROXIMATION. If we approximate $s$ by its integer value, we get the following system

(14.11.3) 
 $\sum_{j=s}^{S-1} g'(j+0)j < K\lambda;$ 
 $\sum_{j=s}^{S} g'(j+0)j \ge K\lambda.$

(14.11.4) 
 $\sum_{j=s}^{S-1} g'(j+0) < 0;$ 
 $\sum_{j=s}^{S} g'(j+0) \ge 0.$

First we notice that if we neglect $K$, we get a base stock policy

$s = S = \bar{n}.$

Next we approximate the conditions by the equations

$\sum_{j=s}^{S} g'(j+0) = 0,$