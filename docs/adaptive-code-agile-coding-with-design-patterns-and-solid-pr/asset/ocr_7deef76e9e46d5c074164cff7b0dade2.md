```
{
    var person = new Person();
    if(person.GetName().Equals("N/A"))
    {
        // exceptional case when name not available.
    }
}
```

# Algorithm

Connascence of algorithm requires both the client and the service to agree on the steps used in an algorithm.

This type of connascence can creep into test code when the test replicates the algorithm in the production code. Listing 13-5 shows this kind of connascence of algorithm. Imagine that an extra field is added to the Person class, or a different prime number is chosen by which to multiply the hash. Either of these changes would cause a change to the GetHashCode() method, and the test would fail because it would also have to be updated.

LISTING 13-5 The test method repeats the algorithm for generating a hash code.

```
//Person.cs
public class Person
{
    public int GetHashCode()
    {
        unchecked
        {
            var hash = 17;
            hash = hash * 23 + _name.GetHashCode();
            hash = hash * 23 + _age.GetHashCode();
            return hash;
        }
    }
}

//PersonTests.cs
[TestFixture]
public class PersonTests
{
    [Test]
    public void HashCodeMatchTests()
    {
        var name = "My Name";
        var age = 33;
        var person = new Person(name, age);
```