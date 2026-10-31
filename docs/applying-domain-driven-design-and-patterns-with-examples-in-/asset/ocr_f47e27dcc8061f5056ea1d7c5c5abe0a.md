```
mockUser.Expect("Validate");
mockUserDao.Expect("Insert", user);
mockUserDao.ExpectNoCall("Update", typeof(IUserInfo));

// (3 - Execute) Executing method under test
UserBC bcUser = new UserBC(daoUser);
// Unexpected calls on the mocks will fail here
// (e.g. calling Validate twice)
bcUser.SaveUser(user);

// (4 - Verify) Checks that all expectations have been met
mockUser.Verify();
mockUserDao.Verify(); // Note: No need for assertions
}
```

# Note

NMock either produces a class that implements an interface or generates a subclass of a real class. In both cases, we then use polymorphism to replace the real class with an instance of the generated class. Although really powerful, this approach presents some notable limitations. For example, it is not possible to create mocks of sealed classes, and mocked methods must be marked as virtual.

An interesting alternative to NMock is a commercial framework called POCMock [POCMock] from Pretty Objects. In this case, mocks are created by replacing collaborators statically.

As you can see, there is no need for assertions in our test because they are located inside the mock objects and are designed to ensure that the mocks are called as expected by the code under test. For example, calling Validate() twice would immediately throw an exception even before the call to Verify() is made.

This example leads us to the following observation: As mock objects verify whether they are used correctly, they allow us to obtain a finer understanding of how the object under test interacts with the collaborating objects.

# Design Implications

When I first learned about mock objects, I thought that it was particularly tricky to come up with an easy mechanism to replace my collaborators. The fundamental problem was that my code was coupled with the concrete implementation of those collaborators rather than their interfaces. The "aha!" moment came when I discovered two key mechanisms called Dependency Injection and Service Locator.

The first principle, Dependency Injection, suggests that a class explicitly declares the interfaces of its collaborators (for example, in the constructor or as parameters in a method) but leaves the