In Section 7.3, you defined several categories that classified each observation as either "standard," "sweet," "too big," or "too small" based on their x and y values. Using those same classification rules, let's define a factor to correspond to x and y.

```
R ptype <- rep(NA,length(x=x))
R ptype[y>=5] <- "too_big"
R ptype[y<=-5] <- "too_small"
R ptype[(x>=5&x<15)&(y>--5&y<5)] <- "sweet"
R ptype[(x<5|x>=15)&(y>--5&y<5)] <- "standard"
R ptype <- factor(x=ptype)
R ptype
```

+   [1] standard standard standard sweet sweet too_big
[8] too_big sweet too_small too_small too_big
[15] too standard too_small too_small standard too_big
Levels: standard sweet too_big too_small

Now you have a factor with 20 values sorted into four levels. You'll use this factor to ggplot how to map your aesthetics. Here's a simple way to do that:

```
R ggplot(x,y,color=ptype,shape=ptype)
```

This single line of code produces the left plot in Figure 7-11, which separates the four categories by color and point character and provides a legend. This was all done by the aesthetic mapping in the call to ggplot, where you set color and shape to be mapped to the ptype variable.

![](bbox=[0.238, 0.585, 0.878, 0.773])

Figure 7-11: Demonstration of aesthetic mapping using aplot and geoms in ggplot2. Left: The initial call to aplot, which maps point character and color using ptype. Right: Augmenting the left plot using various geoms to override the default mappings.