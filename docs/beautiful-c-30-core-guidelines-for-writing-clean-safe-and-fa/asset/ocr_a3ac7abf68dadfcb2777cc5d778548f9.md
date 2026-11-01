```
template <typename T>
concept payroll_queryable =
requires (T p) { p.query_payroll(); };

void current_salary(payroll_queryable auto employee);
```