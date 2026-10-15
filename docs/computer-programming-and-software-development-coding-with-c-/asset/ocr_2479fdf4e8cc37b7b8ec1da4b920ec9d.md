# Chapter 18 How to Add Properties

We're now going to extend our class properties, and by doing so, we are going to apply, well, a better design. Let's see what they are really. At this point, our class looks a bit like this. I have my fields, and they're public.

```
public class Employee
{
    public string firstName;
    public int age;
    public Employee(string name, int ageValue)
    {
        firstName = name;
        age = ageValue;
    }
}
```

The data of our class is stored in public fields. Now, because these fields are public, we can, once we have created an object, change the values of the fields as we have done before from pretty much everywhere. So definitely from outside the class, as we can see here. I have an object of type Employee, somewhere in my application, and I'm setting the firstName. We've done this before. But while this, , works, it's not a great design choice. Having publicly accessible