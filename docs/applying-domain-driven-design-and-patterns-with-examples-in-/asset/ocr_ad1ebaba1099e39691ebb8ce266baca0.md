```
}

public Employee GetDomainObject()
{
    return employee;
}
}
}
```

Note the `GetDomainObject()` method on the `ProjectWrapper` class used in the `AssignedToProject()` setter method. When you write to the `AssignedToProject` property of the PM `EmployeeWrapper` object, you pass a `ProjectWrapper` object to the setter, but we have to pass a Domain Model `Project` object to the `Project` property of the wrapped `Employee` object. Thus we need a way to get to the required `Project` object from the passed in `ProjectWrapper` object, and the `GetDomainObject()` method fills this role.

So when we implement reference properties, we suddenly have to supply a method for getting at the Domain Model object referenced internally by a PM objectsomething that might not be needed otherwise.

For completeness, and in order to be able to implement a corresponding `AssignedEmployees` property in the `ProjectWrapper` class, we have also provided a `GetdomainObject()` method on the `EmployeeWrapper` class.

But even this isn't really enough. Looking critically at the code, we can't help but notice that each time we read from the `AssignedToProject` property, a new `ProjectWrapper` object is created. Assuming the Identity Mapping in our Domain Model layer is working, each new `ProjectWrapper` object created when reading the same property over and over will wrap the same DM `Project` object, and so we shouldn't run the risk of data inconsistency and corruption, but it is hardly ideal nonetheless.

In the end, we might want a full-blown solution that could handle Identity Mapping in the PM as well, making sure that we are never two different PM instances representing the very same Domain Model instance around in a session.

The code in the `AssignedToProject` property would then have to be rewritten so that instead of creating a new instance of the `ProjectWrapper` object itself, it would ask a PM Repository with an Identity Map for the `ProjectWrapper` object.

That means that the `EmployeeWrapper` object will need a reference to the `ProjectRepository` object. Say goodbye to the comforting simplicity that has hitherto graced the Presentation Model. The end result is that the whole slew of fascinating and entertaining horrors and hardships that we remember from managing reference properties in the Domain Layer will rear their ugly heads again.

One way of "solving" these issues with reference properties is to simply avoid reference properties in your PM objects, using "flattened" objects instead that expose only primitive properties, quite possibly from referenced objects as well. See the following code listing.

```
///"Flattened" Presentation Model object, exposing only primitive
//properties
namespace  MyCompany.MyApplication.Presentation
```