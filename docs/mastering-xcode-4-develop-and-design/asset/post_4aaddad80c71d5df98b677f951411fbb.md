
## Unit Testing in Xcode

**Figure 18.1** The default tests in the Scheme Editor

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_290_0.png)

As you saw in Chapter 14, Xcode provides a specific Build action called Test (which you can initiate by pressing Command+U or by choosing Product > Test from the main menu). You can see the tests that are to be run for the active scheme in the scheme’s Test action (Figure 18.1). These tests are automatically detected based on their formatting, which you’ll learn later in this chapter.

Recall that you chose to include unit tests when you created the familiar TestApp project. Because of this, the TestAppTests target was created for you automatically and was added to the scheme. Contrast this with the TestAppSharedFramework scheme, where no unit tests were added (Figure 18.2).

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_291_0.png)

**Figure 18.2** No tests defined for the TestAppSharedFramework scheme

In Figure 18.1, the TestAppTests target is expanded, showing another node called TestAppTests. This corresponds to the only file that belongs to the TestAppTests target: TestAppTests.m. The TestAppTests class defined in its .m file defines the individual tests available (in the form of methods). Were there any test methods defined in that class, those method names would show up under the class name in the scheme’s Test action automatically. The Test column lets you toggle individual tests on or off.

> **Note:** The TestAppTests.m file is located in the TestAppTests group in the Project navigator. This is automatically created for you when you include unit tests when creating a new project. The file itself is a generic place to run tests, but best practice is to create a matching test class for each class in your code base.

In their current state, the template-supplied tests aren’t particularly helpful. When you test TestApp now, the last line of the results (found in the Log navigator) shows zero unexpected failures—a clean test. Obviously it’s only a clean test because nothing was really tested. You’ll explore the test result logs in more detail later in this chapter.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_291_1.png)

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_292_0.png)

### Powered by OCUnit

It’s important to know that Xcode uses OCUnit, part of the SenTestingKit framework. OCUnit provides the test management and interface code, the Cocoa Unit Testing Bundle target template, and the Objective-C test case class template.

### Test Targets and Classes

The target links against `SenTestingKit.framework`. In its Compile Sources build phase, it contains not only the `.m` files of its test classes but those of the classes they test (since they must be compiled and linked so the test classes can use them).

The test classes, as mentioned above, can be created using the Objective-C test case class template (accessed from the Add Files panel or by dragging the template file into the project from the File Template library, as in **Figure 18.3**).

Again, it’s important to note that the test case classes and the classes they test against must be added to the unit test target. The test case classes are subclasses of the SenTestCase class provided by `SenTestingKit.framework`. The test case class template provides basic stub methods for setup and tear-down of the testing environment. Beyond that, it’s up to you to add individual tests in the form of methods. Test case classes are created for each class in your code base.

> **Tip:** You can learn more about OCUnit by visiting www.sente.ch/software/ocunit.

### Asserting Yourself

Tests ultimately pass or fail an assertion. Depending on what you’re testing, you will assert that a condition must be satisfied. For example, you may assert equality with an expected value, or that an exception must or must not be raised, or that a return value must or must not be nil. Following are some of the assertions provided by OCUnit with descriptions and basic example code for each.

`STAssertEqualObjects()` generates a failure if the two objects passed to it are not equal.

```objc
STAssertEqualObjects(objectA, objectB, @"One of these objects is not like the other.");
```

`STAssertEquals()` generates a failure if the two scalars, structs, or unions passed to it are not equal.

```objc
STAssertEquals(myValue, kSomeConstant, @"myValue should be %f but it's %f. My world view is shattered.", myValue, kSomeConstant);
```

`STAssertEqualsWithAccuracy()` generates a failure if two scalars are not equal to within some accuracy. In other words, if the accuracy is .1, the values 0.9 and 1.0 would be considered equal. The primary use is for float or double scalars but works for others.

```objc
STAssertEqualsWithAccuracy(piCloseEnough, M_PI, 0.005, @"piCloseEnough (%f) isn't close enough to pi for our tastes. Mmm. Tasty pi.", piCloseEnough);
```

`STFail()` generates an unconditional failure. It’s useful for those edge cases the other assertions do not cover, as well as for cases where a certain block of code should never be reached (the line after a while loop that’s not intended to be broken, for example).

```objc
STFail(@"Error: Hamster should not float; Q has changed the gravitational constant of the universe.");
```

`STAssertNil()` generates a failure if the passed object is not nil.

```objc
STAssertNil(someNilObject, @"How exactly do you get something from nothing?");
```

`STAssertNotNil()` generates a failure if the passed object is nil.

```objc
STAssertNotNil(aValidObject, @"I visited this method and all I got was this lousy nil.");
```

`STAssertTrue()` generates a failure if the passed Boolean (BOOL) expression evaluates to false.

```objc
STAssertTrue((M_PI == 3.0f), @"Professor Frink says pi is exactly three!");
```

`STAssertFalse()` generates a failure if the passed Boolean (BOOL) expression evaluates to true.

```objc
STAssertFalse((1 == 1), @"We don't BELIEVE in equality 'round THESE parts, stranger!");
```

`STAssertNoThrow()` generates a failure if the expression throws an Objective-C exception.

```objc
STAssertNoThrow([someCalculatorObject addOneToThree], @"The answer is 4, you dolt. What went wrong?");
```

`STAssertThrows()` generates a failure if the expression does not throw an Objective-C exception.

```objc
STAssertThrows([someCalculatorObject divideByZero], @"Wait, what? What result did YOU get?!");
```

Each test should contain at least one assertion. Some argue that each test should include only one assertion so that the test’s name (the method signature) is precisely descriptive of what is being tested, making the precise failure easier to identify should it arise.

### Test Results Log

As mentioned previously, the test result output shows up in the Log navigator. Following is the output from the first run of the TestApp scheme’s Test action.

```text
GNU gdb 6.3.50-20050815 (Apple version gdb-1518) (Sat Feb 12 02:52:12 UTC 2011)

Copyright 2004 Free Software Foundation, Inc.

GDB is free software, covered by the GNU General Public License, and you are welcome to change it and/or distribute copies of it under certain conditions.

Type "show copying" to see the conditions.

There is absolutely no warranty for GDB. Type "show warranty" for details.

This GDB was configured as "x86_64-apple-darwin".
tty /dev/ttys000
sharedlibrary apply-load-rules all

[Switching to process 12421 thread 0x0]
objc[12421]: GC: forcing GC OFF because OBJC_DISABLE_GC is set

Test Suite 'All tests' started at 2011-04-13 20:02:20 -0400

Test Suite '/Developer/Library/Frameworks/SenTestingKit.framework(Tests)' started at 2011-04-13 20:02:20 -0400

Test Suite 'SenInterfaceTestCase' started at 2011-04-13 20:02:20 -0400

Test Suite 'SenInterfaceTestCase' finished at 2011-04-13 20:02:20 -0400.

Executed 0 tests, with 0 failures (0 unexpected) in 0.000 (0.000) seconds

Test Suite '/Developer/Library/Frameworks/SenTestingKit.framework(Tests)' finished at 2011-04-13 20:02:20 -0400.

Executed 0 tests, with 0 failures (0 unexpected) in 0.000 (0.001) seconds
```
