# 120 Non-Linear Differential Equations and Dynamical Systems

The proof of (4.125a–c) [4.126a, b]) follows from the vanishing of the coefficients of cosines (4.128a) [sines (4.128b)] of lowest order in (4.116):

```
0=[a-2q\cos(2\theta)] A_0+[(a-1)\cos\theta-2q\sin\theta\cos(2\theta)] A_1
+[(a-4)\cos(2\theta)-2q\cos^2(2\theta)] A_2
+[(a-9)\cos(30\theta)-2q\cos(30\theta)\cos(2\theta)] A_3
+[(a-16)\cos(40\theta)-2q\cos(40\theta)] A_4+...
a= a A_0-2q A_0\cos(2\theta)+(a-1)A_1\cos\theta-qA_1[\cos\theta+\cos(30\theta)]
+(a-4)A_2\cos(2\theta)-qA_2[1+\cos(40\theta)]+(a-9)A_3\cos(30\theta)]
-q A_3[\cos\theta+\cos(50\theta)]+(a-16)A_4\cos(40\theta)-qA_4[\cos(20\theta)+\cos(60\theta)]+...
= a A_0-q A_2+(a-1)A_1-q(A_1+A_3)]\cos\theta
```

```
+[(a-4)A_2-q(2A_0+A_4)]\cos(2\theta)+... (4.128a)
```

```
0=[(a-1)\sin\theta-2q\sin\theta\cos(2\theta)] B_1
+[(a-4)\sin(2\theta)-2q\sin(2\theta)] B_2
+[(a-9)\sin(30\theta)-2q\sin(30\theta)\cos(2\theta)] B_3
+[(a-16)\sin(40\theta)-2q\sin(40\theta)] B_4
= (a-1)B_1\sin\theta-qB_1[\sin(30\theta)-\sin\theta]+(a-4)B_2\sin(2\theta)
-q B_2\sin(40\theta)+(a-9)B_3\sin(30\theta)-qB_3[\sin(50\theta)+\sin\theta]
+(a-16)B_4\sin(40\theta)-qB_4[\sin(60\theta)+\sin(2\theta)]+....
=[(a-1)B_1+q(B_1-B_3)]\sin\theta+(a-4)B_2-qB_2
```

```
(4.128b)
```

The differential equation (4.119a)/(4.120a)/(4.121a)/(4.122a) satisfy the Mathieu equation (4.89) by the recurrence of formulas for the coefficients respectively (4.119b, c; 4.125a, c; 4.125b)/(4.121b, c; 4.126b)/(4.122b, c; 4.126a). For the series to converge the Cauchy (Cauchy) I.2.9.1) necessary condition (1.296a) must be met, that the coefficients to zero for large order:

```
0 = \lim_{r\to\infty} A_{2r} = \lim_{r\to\infty} B_{2r+1}. (4.128c-f)
```