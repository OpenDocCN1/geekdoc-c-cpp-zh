```
```csharp
Tuple<int, string, bool, int?>
CreateBranchOffice(Tuple<int, string, bool, int?> company){
    var branch = Tuple.Create(1, company.Item2, company.Item3, null);
    Console.WriteLine(company);
    branch = Tuple.Create(10*company.Item1+1, company.Item2 +
                          " Office", true, company.Item1);
    Console.WriteLine(t);
    var office = new { ID = branch.Item1,
        Name = branch.Item2,
        IsOffice = branch.Item3,
        ParentID = company.Item4 };
    return branch;
}
```
```

In this example, the function agrees on the company and creates a branch office. Both company and branch offices are represented as tuples with four items. Also, in this code, an anonymous object office with properties ID, Name, IsOffice, and ParentID is added, which is equivalent to tuple (this object is just created but not used anywhere). In this statement, you can see how easy it is to convert tuples to actual objects. The office object is an anonymous object; its class is not known by name outside of the function body. Therefore, you cannot define the return type of the function. If you want to return some dynamic structure instead of tuple, you would have to start a separate class instead of an anonymous class, or you will need to set the return type as dynamic, but in that case, you will lose information about the structure of the returned object.