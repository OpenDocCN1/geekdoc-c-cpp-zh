*euc lid-distance/Program.cs (lines 4-12)*

```
var p1 = new SPoint(10, -10);
var p2 = new SPoint(10, 20);
var p3 = new SPoint(0, 40);
Console.WriteLine($"p0 = {p0}; p1 = {p1}; p2 = {p2}; p3 = {p3}");

Console.WriteLine($"{(p0 == p2 ? "p0 == p2" : "p0 != p2")}");
10
11 TestPointType(p0, p1, p2, p3);
12 Console.WriteLine();
```

*euc lid-distance/Program.cs (lines 16-24)*

```
16 var q1 = new RPoint(10, -10);
17 var q2 = new RPoint(10, 20);
18 var q3 = new RPoint(0, 40);
19 Console.WriteLine($"q0 = {q0}; q1 = {q1}; q2 = {q2}; q3 = {q3}");
20
21 Console.WriteLine($"{(q0 == q2 ? "q0 == q2" : "q0 != q2")}");
22
23 TestPointType(q0, q1, q2, q3);
```