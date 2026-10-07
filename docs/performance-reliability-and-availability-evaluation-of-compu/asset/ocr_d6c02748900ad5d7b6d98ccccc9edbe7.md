# 730 Performance, Reliability, Availability Evaluation of Computational Systems

```
tbt = tm;
bg = Extract[[RandomVariate[ExponentialDistribution[omegal], 1],\nggt = gt + tm;
tr = 1;
datatbt = Append[datatbt, tbt];
dalag = Append[datag, {n, tr, gt, bg]];
++;
If[n > nt,
Break[];
];
Goto[st0];
Label[st2]
st = 2;
ta = Extract[RandomVariate[ExponentialDistribution[alpha], 1], 1];
tl = Extract[RandomVariate[ExponentialDistribution[lambda], 1],
1];
If[st < tl,
st2d = Append[st2d, ta];
gt = gt + ta;
Goto[st0];
st2d = Append[st2d, tl];
tbt = tl;
bg = Extract[RandomVariate[ExponentialDistribution[omega2], 1],
1];
gt = gt + tl;
tr = 2;
datatbt = Append[datatbt, tbt];
dalag = Append[datag, {n, tr, gt, bg]];
++;
If[n > nt,
Break[];
];
Goto[st3];
Label[st3]
st = 3;
ta = Extract[RandomVariate[ExponentialDistribution[alpha], 1], 1];
tl = Extract[RandomVariate[ExponentialDistribution[lambda], 1],
1];
If[st < tl,
st3d = Append[st3d, ta];
gt = gt + ta;
Goto[st0];
tbt = tl;
bg = Extract[RandomVariate[ExponentialDistribution[omega2], 1],
1];
st3d = Append[st3d, tl];
gt = gt + tl;
tr = 2;
datatbt = Append[datatbt, tbt];
dalag = Append[datag, {n, tr, gt, bg]];
++;
```