![](bbox=[0.247, 0.098, 0.733, 0.238])

# **FIGURE 6.9:** Gaussian Membership Function

```
```matlab
% Gaussian membership function
x=0:0.1:10;
y=gaussmf(x,[1 6]);
plot(x,y)
xlabel('gaussmf, P=[1 6]')
title('Gaussian Membership Function');
```
```

# Output

The Gaussian Membership Function plotted from the above code is shown in Figure 6.9.

# Generalized Bell Shaped Membership Function

# Syntax

```
```matlab
Y = gbellmf(x,params)
```
```

The Generalized bell function depends on three parameters a, b, and c as given by

$$f(x;a,b,c)=\frac{1}{1+\left|\frac{x-c}{a}\right|^{2b}}$$

where the parameter b is usually positive. The parameter c locates the center of the curve. The parameter vector params, the second argument for gbellmf, is the vector whose entries are a, b, and c, respectively.

# Code

```
```matlab
% Generalized Bell Shaped membership function
x=0:0.1:10;
y=gbellmf(x,[1 3 7]);
plot(x,y)
xlabel('gbellmf, P=[1 3 7]')
```
```