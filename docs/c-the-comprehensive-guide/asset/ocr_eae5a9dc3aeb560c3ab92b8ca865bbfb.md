# “std::move” Itself Does Not Move

Because you are seeing `std::move()` here for the first time, I want to give a little hint, without which you might fall into a misunderstanding. The `std::move()` function does not move itself, it only allows something to move—here, the return from the function.

Really this is just a type conversion to a temp-value reference, and some would have preferred a name like `move_cast`.

The data fields are all `unique_ptr` pointers. Simple data fields without pointers would have sufficed here. But maybe you want to extend *MyDialog* polymorphically later: for that, you need pointers. *Polymorphic* here means that you, for example, create a derived `ColorfulTextField` class from class `TextField` and then put an instance of that class into `unique_ptr<TextField> txtFirstName_`. If `txtFirstName_` were not a pointer (or a reference), the properties of `ColorfulTextField` would be lost. You can find an example of this in [Chapter 15](#).

You can apply the rules of thumb for using `unique_ptr`. Exceptions prove the rule:

+   - You can most likely use `unique_ptr` as a reference parameter. Then the parameter behaves like any other reference. In addition, you can also pass `nullptr` for “undefined state,” which is sometimes useful.
+   - A value parameter as `unique_ptr` “consumes” the parameter upon invocation. The variable that was passed to the function is empty afterward. This is useful when the object should take exactly one path. This would be the application of the *sink* (or *drain*) design pattern.
+   - A function can return `unique_ptr` by value. This is particularly suitable when you create the wrapped object with `new` within the function—essentially as a *producer function* or *factory*.
+   - You only return a reference to `unique_ptr` if the pointer already existed beforehand. So, from a free function, you return a parameter, or from a method, a data field of the class.
+   - As data fields of a class, `unique_ptr`s are well-suited because you don't have to worry about removal. Unlike a value, `unique_ptr` can have an undefined phase and store `nullptr`. It is certainly better than a raw pointer.
+   - You can put `unique_ptr` in a standard container. The container then owns all the objects it contains. If you need to reference individual container elements from another location, you can do so either by reference to `unique_ptr` or as a raw pointer to the wrapped object. The latter is useful if you don't want to reference multiple elements of the original container in another container that contains the objects.