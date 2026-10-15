In the above example, the new property explores the existing property values to calculate its own value. The advantage is that there is no change of structure and no extra operations to achieve the desired result.

![](bbox=[0.19, 0.17, 0.81, 0.39])

The following unit tests operate on the new property and display the result having IsAboveEighteen as true.

```
[TestMethod()]
public void IsAboveEighteenTest()
{
    IList<Member> list = new List<Member>()
    {
        new Member() { Name = "N1", DateOfBirth= new DateTime(2000, 1, 1) },
        new Member() { Name = "N2", DateOfBirth= new DateTime(2000, 1, 1) },
        new Member() { Name = "N3", DateOfBirth= new DateTime(1990, 1, 1) },
        new Member() { Name = "N4", DateOfBirth= new DateTime(1980, 1, 1) }
    };

    var selectedList = list.Where(m => m.IsAboveEighteen);
    foreach (Member member in selectedList)
        Console.WriteLine(member.Name);

    Assert.AreEqual(2, selectedList.Count());
}
```

On running the test we can see the following output.