```
var usCompanies = addresses
.Where(addr =>
    String.Equals(addr.Country,"United States"))
.Select(usComp => usComp.CompanyName);
```