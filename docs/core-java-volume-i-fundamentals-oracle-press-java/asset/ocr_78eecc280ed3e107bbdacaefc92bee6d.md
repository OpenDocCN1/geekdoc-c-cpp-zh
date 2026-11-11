and you must cast it accordingly. Use automatic unboxing to turn it into a double:

```
```
double s = (Double) m2.invoke(harry);
```
```

How do you obtain a Method object? You can, of course, call getDeclaredMethods and search through the returned array of Method objects until you find the method you want. Or, you can call the getMethod method of the class Class. This is similar to the getField method that takes a string with the field name and returns a Field object. However, there may be several methods with the same name, so you need to be careful that you get the right one. For that reason, you must also supply the parameter types of the desired method. The signature of getMethod is

```
```
Method getMethod(String name, Class... parameterTypes)
```
```

For example, here is how you can get method pointers to the getName and raiseSalary methods of the Employee class:

```
```
Method m1 = Employee.class.getMethod("getName");
Method m2 = Employee.class.getMethod("raiseSalary",
double.class);
```
```

Use a similar approach for invoking arbitrary constructors. Supply the constructor's parameter types to the class.getConstructor method, and supply the parameter values to the Constructor.newInstance method:

```
```
Class cl = Random.class; // or any other class with a
constructor that
                // accepts a long parameter
Constructor cons = cl.getConstructor(long.class);
Object obj = cons.newInstance(42L);
```
```