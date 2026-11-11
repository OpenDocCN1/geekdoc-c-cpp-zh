characters e, E, f, g, or G, then we simply do not format the number. We’ll show
you later how to make a native method throw an exception.

# 12.4 Accessing Fields

All the native methods you saw so far were static methods with number and
string parameters. We’ll now consider native methods that operate on objects.
As an exercise, we will reimplement as native a method of the Employee class that
was introduced in Volume I, Chapter 4. Again, this is not something you would
normally want to do, but it does illustrate how to access fields from a native
method when you need to do so.

# 12.4.1 Accessing Instance Fields

To see how to access instance fields from a native method, we will reimplement
the raiseSalary method. Here is the code in Java:

```
```java
public void raiseSalary(double byPercent)
{
    salary *= 1 + byPercent / 100;
}
```
```

Let us rewrite this as a native method. Unlike the previous examples of native
methods, this is not a static method. Running javac gives the following prototype:

```
```c
JNIEXPORT void JNICALL Java_Employee_raiseSalary(JNIEnv *, jobject, jdouble);
```
```

Note the second argument. It is no longer of type jclass but of type jobject. In fact,
it is an equivalent of the this reference. Static methods obtain a reference to the
class, whereas nonstatic methods obtain a reference to the implicit this argument
object.

Now we access the salary field of the implicit argument. In the “raw” Java-to-C
binding of Java 1.0, this was easy—a programmer could directly access object
data fields. However, direct access requires all virtual machines to expose their
internal data layout. For that reason, the JNI requires programmers to get and
set the values of data fields by calling special JNI functions.

In our case, we need to use the GetDoubleField and SetDoubleField functions because
the type of salary is double. There are other functions—GetIntField/SetIntField,
GetObjectField/SetObjectField, and so on for other field types. The general syntax is:

```
```c
x = (*env)->GetXxxField(env, this_obj, fieldID);
(*env)->SetXxxField(env, this_obj, fieldID, x);
```
```