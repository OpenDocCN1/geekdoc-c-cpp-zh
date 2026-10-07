# Object Oriented Programming using C#

The figure below shows the results from the tests....

| Result | Test Name |
|---|---|
| Passed | DecreaseCreditRemove5UnitsOfCredit_CreditShouldBe5 |
| Passed | AddClient_TestAddTwice_ShouldGenerateException |
| Passed | GetClient_TestGettingClient_AttributesShouldNotChange |
| Passed | GetClient_TestGettingClient_ShouldNotGenerateException |
| Passed | AddClient_TestAddTwice_AlternativeVersion |
| Passed | IncreaseCredit_TestAddUnitsOfCredit_CreditShouldBe5 |
| Passed | GetClient_TestDeleteClient_ShouldNotGenerateException |
| Passed | GetClient_TestGettingUnknownClient_ShouldGenerateException |
| Passed | GetClient_TestDeleteUnknownClient_ShouldGenerateException |
| Passed | AddClient_TestAddingClient_ShouldNotGenerateException |

By creating test fixtures to all classes and all methods we can run these tests every time the system is adapted to meet the clients changing needs.

# 11.13 Generating the Documentation

Documentation is essential and can be generated automatically (as described in Chapter 8 - C# Development Tools) assuming appropriate comments have been placed in the code.

XML comments have been placed in the code to describe all classes, all constructors and all methods. All parameters, return values and exception thrown have also been described.