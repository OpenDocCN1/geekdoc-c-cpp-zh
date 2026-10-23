object, or objects themselves. They could also be enums, a topic discussed in appendix B. This could also appear in code using if expressions.

```
val monthlyPay = if(employeeType == Wage) ...
  else if(employeeType == Salary) ...
  else ...
}
```

The key to this being a smell is that the pattern above is repeated in multiple locations. If a new category or employee were added, all of those would need to be modified. Missing one or more occurrences will lead to difficult to track errors.

There are two refactoring methods that can be employed to remove this smell. They are “Replace Conditional with Polymorphism” and “Replace Type Code with Subclasses”. This would appear in the code as an abstract supertype that has methods for each of the different types of actions/calculations that are required. That might look like the following.

```
trait EmployeeType {
  def monthlyPay(hours:Int, wage:Int):Int
  def logBenefits(employee:Employee, hours:Int):Unit
  def leaveTime(hours:Int):Double
}
```

Using this, the match or if constructs shown above would be replaced by this simple line.

```
val monthlyPay = employeeType.monthlyPay(hours,wage)
```

This works because the employeeType will be a reference to an appropriate subtype of EmployeeType. That subtype will have the appropriate code in it for that type. The code might look like the following with proper implementations of all the methods. Then the parts of the code that give a value to employeeType would provide the appropriate subtype.

```
class WageEmployee extends EmployeeType {
  def monthlyPay(hours:Int, wage:Int):Int = ...
  def logBenefits(employee:Employee, hours:Int):Unit = ...
  def leaveTime(hours:Int):Double = ...
}
```

```
class SalaryEmployee extends EmployeeType {
  def monthlyPay(hours:Int, wage:Int):Int = ...
  def logBenefits(employee:Employee, hours:Int):Unit = ...
  def leaveTime(hours:Int):Double = ...
}
```

```
class TempEmployee extends EmployeeType {
  def monthlyPay(hours:Int, wage:Int):Int = ...
  def logBenefits(employee:Employee, hours:Int):Unit = ...
  def leaveTime(hours:Int):Double = ...
}
```

Note that if each of these had no state, fields that differ between different instances, they could be declared as objects instead of classes.

There are two main benefits to this change that improve upon the switch statement smell. The first is that this new structure makes it significantly easier to add new types of employees. If it is decided that any of these categories needs to be resolved into different