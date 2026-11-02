![](bbox=[0.18, 0.12, 0.88, 0.68])

Fig. 8.24 Gnuplot window showing the result of plotting a shifted and rescaled Fischer-Tippett pdf with logarithmically scaled y-axis.

displays the fourth column as a function of the first, with error bars given by the 5th column. The elements behind the using are called entries. Within the using data modifier you can also perform transformations and calculations. Each entry, where some calculations should be performed have to be embraced in ( ) brackets. Inside the brackets you can refer to the different columns of the input file via $1 for the first column, $2 for the second, etc. You can generate arbitrary expressions inside the brackets, i.e. use data from different columns (also combine several columns in one entry), operators, variables, predefined and self-defined functions and so on. For example, in Sec. 8.6.2, you will see that the data from the sg_e0_L.dat file follows approximately a power law e0(L) = e∞ + a L^b with e∞ ≈ −1.788, a ≈ 2.54 and b ≈ −2.8. To visualize this, we want to show e0(L) − e∞ as a function of L^b. This is accomplished via:

```
gnuplot> einf=-1.788
gnuplot> b=-2.8
gnuplot> plot "sg_e0_L.dat" u ($1**b):($2-einf)
```

Now the gnuplot window will show the data as a straight line (not shown, but see Fig. 8.33).