# 22.2. Code Review - Total Salary Calculator

salary-calculation/Organizations.cs (lines 23-34)

```
`3 public sealed class Management : Organization {\n  public Management(string name) : base(name) { }\n\n  protected override Manager? GetEmployeeByName(string name) {\n27 foreach (var w in this) {\n  if (w.Name == name) {\n29 return w as Manager;\n  0 }\n31 }\n  return null;\n}\n- }`
```

salary-calculation/Organizations.cs (lines 36-47)

```
`36 public sealed class RankAndFile : Organization {\n  public RankAndFile(string name) : base(name) { }\n\n39 protected override Worker? GetEmployeeByName(string name) {\n  0 foreach (var w in this) {\n  if (w.Name == name) {\n\n  return w as Worker;\n\n  }\n}\nreturn null;\n}`
```

The TotalExpense of the Corporation is the sum of the salaries of all Employees.