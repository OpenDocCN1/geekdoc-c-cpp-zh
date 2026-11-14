# 7.1.2.4 Visualize test results

The result of the tests can be seen in “Test Explorer” window, a green check mark indicating the test is valid and a red cross indicating the test has failed as shown below.

![](bbox=[0.01, 0.25, 0.95, 0.42])

MSTest offers a good solution for the implementation of Unit Testing in your project, as native inside Visual Studio the tool Integrates itself perfectly with the IDE of Microsoft. It is very well documented by the Microsoft team. References and tutorials can be found by following the link in reference.

![](bbox=[0.01, 0.64, 0.95, 0.73])

# 7.1.3 Mock concept

The issue for the definition of pertinent Unit Testing is the developer context: many objects are not yet been defined or the database is not yet available when the unit tests project is written. That could be an issue because the developer has to test the method with the larger panel of input data as possible, covering every case possible (in theory).