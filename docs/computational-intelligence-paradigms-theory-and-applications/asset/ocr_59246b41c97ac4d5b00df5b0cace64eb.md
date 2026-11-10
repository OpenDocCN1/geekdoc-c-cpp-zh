![](bbox=[0.111, 0.09, 0.868, 0.379])

**FIGURE 6.15:** Illustration of 'mf2mf' Function

```
```
outParams = mf2mf (inParams, inType, outType)
```
```

where inParams - the parameters of the membership function to be transformed inType - a string name for the type of membership function to be transformed outType - a string name for the new membership function The following code translates the polynomial Z curve membership function into triangular membership function.

```
```
x=0:0.1:5;
mfp1 = [1 2 3];
mfp2 = mf2mf(mfp1,'zmf','trimf');
plot(x,zmf(x,mfp1),x,trimf(x,mfp2))
```
```

The resultant plot is shown in Figure 6.15.

# ## 6.7 Singletons

Strictly speaking, a fuzzy set D is a collection of ordered pairs

A={(x,μ(x))} (6.11)

Item x belongs to the universe and μ (x) is its grade of membership in A. A single pair (x,μ (x)) is called a fuzzy singleton; therefore the