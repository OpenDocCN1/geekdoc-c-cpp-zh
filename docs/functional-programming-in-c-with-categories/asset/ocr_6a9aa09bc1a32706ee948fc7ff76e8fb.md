![](bbox=[0.125, 0.095, 0.885, 0.36])

The domain model might seem trivial because in most implementations of the Clean architecture the domain objects are just POCO (Plain old CLR object) objects. For example:

```
public class Course
{
    public int CourseId { get; set; }
    public string Title { get; set; }
    public int Credits { get; set; }
    public int? DepartmentId { get; set; }

    public Department Department { get; set; }
    public List<Enrollment> Enrollments { get; set; }
    public List<CourseAssignment> CourseAssignments { get; set; }
}
```

Github: source

This is often seen as an anti-pattern in the Object oriented world and especially in DDD world where it has a special name: anemics domain model. Others see this as a form of proper design practice.

In small scale applications this is simply fine. What we are going to focus here is not where we are going to place the business logic but the use of the Functional Types in the Domain Model