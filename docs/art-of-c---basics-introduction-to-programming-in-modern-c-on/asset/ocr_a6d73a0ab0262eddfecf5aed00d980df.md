async method. For example, the task might be the result of a call to `System.Threading.Tasks.Task.WhenAll`. When you await such a task, only one of the exceptions is caught, and you can't predict which exception will be caught.

# **Two catch blocks example**

In the following example, two catch blocks are used, and the most specific exception, which comes first, is caught.

To catch the least specific exception, you can replace the throw statement in `ProcessString` with the following statement: `throw new Exception();`.

If you place the least-specific catch block first in the example, the following error message appears: `A previous catch clause already catches all exceptions of this or a super type ('System.Exception').`

# **Using Directive (using, using static)**

The using directive has three uses:

+   * To allow the use of types in a namespace so that you do not have to qualify the use of a type in that namespace:

```
```
using System.Text;
```
```

+   * To allow you to access static members and nested types of a type without having to qualify the access with the type name.

```
```
using static System.Math;
```
```

+   * To create an alias for a namespace or a type. This is called a *using alias directive*.