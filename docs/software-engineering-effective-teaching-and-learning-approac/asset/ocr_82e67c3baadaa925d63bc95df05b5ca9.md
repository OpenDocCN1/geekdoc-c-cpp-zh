bibliography. There are a few recommendations on the topic; even frameworks like JUnit provide helper tools. However, we have observed a lack of an in-deep analysis in which students can rely to successfully proceed in most of the possible scenarios.

When testing exceptions, students use to consider them as an if-else block of code, where the if corresponds to the try sentence and the else corresponds to the catch sentence. This way, the testing procedure would consist in defining two test cases, one for each possible execution path. Nevertheless, there are a fair number of non trivial questions that arise among students when taking this procedure to practice. Should all the exceptions be tested following the same procedure? Should all the potentially thrown exceptions be tested? If not, what is the criteria to decide which of them should not? In the rest of this section we will try to shed some light on these questions.

The goal is to verify that exceptions are generated only when it’s due, following this consideration it makes sense to classify them as expected or unexpected. Note that this classification does not attend to the exception itself but to the nature of the test cases designed for testing it.

# Expected Exceptions

Expected exceptions refer to test cases in which the method-under-test execution context is set-up so an exception must be thrown. Testing them consists of invoking the throwing method with “exceptional” data and checking that the exception is actually thrown via an assertion. Testing this kind of exceptions can be done in JUnit 4.x using the annotation @Test(expected=ExpectedException.class) when defining the test method. However, it presents a clear shortcoming, checking that the right exception has been produced is up to the framework and no extra verifications over the exception object itself can be done since it is not available in the

test method. For simplicity and generality the procedure shown in the Source code listing 4 has been proposed to students:

```
public void testSomeMethod () {
    try{
        instanceToTest.
methodToTest(params);
        fail("An exception was expected");
    } catch (ExpectedException e){
        // Execution control must reach here
    }
}
```

# Source Code Listing 4

With these code sentences we ensure that a failure will occur if the exception ExpectedException is not raised when invoking the method to test with the adequate parameters. We have observed among students a common misconception of expected exceptions. Sometimes, they include some test cases in which the concept of expected exceptions is extended to “testing the Java platform”. For example, test cases are written which result in a method invoked over a non initialized object that produces a NullPointerException raised by the JVM. This kind of test cases doesn’t make any sense because testing the JVM is obviously out of the scope of the test plan.

# Unexpected Exceptions

Unexpected exceptions correspond to those unpredicted situations for which the system can not suggest any solution. This kind of exceptions is easy to test since JUnit automatically catches exceptions thrown by test methods and report them as errors (note the non trivial distinction between errors and failures in JUnit). While for unchecked exceptions (those who inherit from RuntimeException) nothing needs to be done, checked exceptions have to be declared in