# 4.3 R as a Calculator

# 4.3.1 Mathematical Operations Using R

To learn to do statistical analysis and computations, one may start by considering the R programming language as a simple calculator.

Start from here: just enter an arithmetic expression, press the <Enter> key, and the answer from the machine is found in the next line

```
> 
> 2 + 3
[1] 5
>
```

OK! What about other calculations? Such as: 13 - 7, 3 x 5, 12 /4, 7^2, √2, e^3, e^x, ln 5 = loge5, (4 + √3)(4 - √3), (4 + i√3)(4 - i√3), ... and so on. Just try:

```
> 
> 13 - 7
[1] 6
> 3*5
[1] 15
> 12/4
[1] 3
> 7^2
[1] 49
> sqrt(2)
[1] 1.414214
> 
> exp(3)
[1] 20.08554
> 
> exp(1i*pi)  [i is used for the complex number i = √-1.]
[1] -1-0i  [This is just the famous Euler’s Identity equation: e^{iπ}+1 = 0.]
> log(5)
[1] 1.609438
> (4 + sqrt(3))*(4 - sqrt(3))
[1] 13
[Checking: (4+√3)(4-√3)=42-(√3)2=16-3=13 (Checked!)]
> (4+1i*sqrt(3))*(4-1i*sqrt(3))
[1] 19+0i [Checking: (4+1i√3)(4-1i√3)=42-(i√3)2=16-(-3)=19 (Checked!)]
```