# THE BENEFITS

Unit testing gives developers several clear advantages. The following are usually found at the top of the list.

# DESIGN

When software design is test-driven, the tests themselves are designed first and provide the goals for the software to meet. That is, if you design the tests to specify how the software should behave and then write the software with the intention of passing the tests, the developer knows that the design goals are met only when the code passes all the defined tests.

# CHANGE MANAGEMENT

Part of maintaining an application’s code base involves refactoring the existing code. With proper unit tests, a developer can make these changes confidently, re-running the tests after each change to verify that the code still meets the requirements the tests have set. The developer will know immediately whether their “new way of doing things” broke things when the test fails. Even better, well-designed unit tests tell the developer exactly where and why the new code failed.

# SIMPLIFIED INTEGRATION TESTING

Integration testing is the testing of the various software components when brought together as a whole. For example, integration testing is done on the entire application to make sure all its parts work together properly. For this reason, integration testing is often done manually by people using the software. Unit tests ensure the individual components work properly, catching errors before they manifest as potentially confusing behavior to the user, leaving only integration-related problems for the tester to deal with. This clear delineation between “problem with component” versus “problem between components” simplifies the debugging process.