```
> `pointplot(pts, title = “Mumps Infections”);`
```

![](bbox=[0.277, 0.132, 0.716, 0.407])

By 21 days, essentially all the students are infected. Let’s look at the weekly counts.

```
> `seq(round(Mumps(k)), k in [7, 14, 21, 28])`  
`33, 413, 977, 1000`
```

**Interpretation.**  
The results show that essentially all the students will be infected by 3 weeks. Since only about 3% will be infected within one week, every effort must be made to get the vaccine to the school and to vaccinate the students within one week.  

We can model the effect of the vaccine on the spread of mumps by reducing *k* in the model and using *Mumps*(7) as the initial value of the new curve.

# Exercises

Iterate and graph the following DDSs. Explain their long-term behavior. For each DDS, find a realistic scenario that it might explain/model.

+   1. Consider the model \(a(n+1)=r\cdot a(n)(1-a(n))\). Let \(a(0)=0.2\). Determine the numerical and graphical solutions for the following values of \(r\). Find the pattern in the solutions.
+   
+      (a) \(r=2\)
+   
+      (b) \(r=3\)