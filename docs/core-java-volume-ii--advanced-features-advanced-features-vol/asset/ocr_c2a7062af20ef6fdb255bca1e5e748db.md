```
```java
double price = 44.95;
double tax = 7.75;
double amountDue = price * (1 + tax / 100);
var out = new PrintWriter(System.out);
/* This call will throw an exception--note the % */
Printf.format(out, "Amount due = $%.2f%n", amountDue);
out.flush();
}
}
```
```

# **Handling Java Exceptions**

+   - `jint Throw(JNIEnv *env, jthrowable obj)`
+     prepares an exception to be thrown upon exiting from the native code. Returns 0 on success, a negative value on failure.
+   - `jint ThrowNew(JNIEnv *env, jclass cl, const char msg[])`
+     prepares an exception of type cl to be thrown upon exiting from the native code. Returns 0 on success, a negative value on failure. msg is a "modified UTF-8" byte sequence denoting the String construction argument of the exception object.
+   - `jthrowable ExceptionOccurred(JNIEnv *env)`
+     returns the exception object if an exception is pending, or NULL otherwise.
+   - `jboolean ExceptionCheck(JNIEnv *env)`
+     returns true if an exception is pending.
+   - `void ExceptionClear(JNIEnv *env)`
+     clears any pending exceptions.

# ## 12.9 Using the Invocation API

Up to now, we have considered programs in the Java programming language that made a few C calls, presumably because C was faster or allowed access to functionality inaccessible from the Java platform. Suppose you are in the opposite situation. You have a C or C++ program and would like to make calls to Java code. The *invocation API* enables you to embed the Java virtual machine into a C or C++ program. Here is the minimal code that you need to initialize a virtual machine:

```
```java
JavaVMOption options[1];
JavaVMInitArgs vm_args;
JavaVM *jvm;
JNIEnv *env;

options[0].optionString = "-Djava.class.path=.";
```
```