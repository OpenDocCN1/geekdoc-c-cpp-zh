Tuples fit perfect the linear model of functional programming because we can easily adjust the inputs and outputs of consecutive function pipelines.

![](bbox=[0.135, 0.17, 0.435, 0.205])

For example, we can trail along the pipeline some state data without the need to access the outside scope and thus maintaining the purity of the functions:

```
Func<(Order, double discount), (Order updatedOrder,double totalPrice)> updateOrder = state => { ... };
```

```
Func<(Order, double totalPrice), (double totalPrice, string errors)> validate = state => { ... };
```

```
Func<(Order, double discount), (double totalPrice, string errors)> proccess = order => validate(updateOrder(order));
```

here for example, we transfer the updated Order across the pipeline.

![](bbox=[0.125, 0.48, 0.83, 0.53])

Sometimes if you must pass too much data across, it might be an indication that you should break down even more the functions, or even use Object oriented instead of Functional design.

There are functional patterns like the State monad that facilitate this kind of composition. We are not going to see state monad in this book since C# is not purely functional and there is no need to introduce complexity when not needed.

# 1.9 Extension Methods

we are going to use Extension methods a lot. Extension methods might diverge from the traditional Object-oriented model of programming but allow us to provide custom functionality to .NET native types or extend our classes in ways that are not possible (or very difficult) through the standard language capabilities.