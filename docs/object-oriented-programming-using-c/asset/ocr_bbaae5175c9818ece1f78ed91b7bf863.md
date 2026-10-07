# Object Oriented Programming using C#

The code for this is shown below...

```
namespace MessageManagerTests
{
    TestClass
    public class TestFixture_Clients.Client
{
        private MessageManagerSystem.Clients.Client c;

        [Initialize]
        public void TestInitialize()
        {
            c = new MessageManagerSystem.Clients.Client("Simon",
                "Room 1234", "n200", 10);
        }

        [TestCleanup]
        public void TestCleanup()
        {
            c = null;
        }

        [TestMethod]
        public void IncreaseCredit_TestAdd5UnitsOfCreditCreditShouldBe5()
        {
            c.IncreaseCredit(5);
            Assert.AreEqual(15, c.Credit, "Credit after adding 5
                units is not as expected. Expected: 15 Actual:
                "c.Credit");
        }
    }
}
```

This test creates a client with 10 units of credit, adds an additional 5 units of credit and then checks that this client has
15 units of credit.

One test does not alone sufficiently prove that the IncreaseCredit() method will always work so we may need to define
additional tests.

We also need to create test cases to test the DeleteClient() method in the ClientBook class. As this is a separate class we
need to create a new test fixture appropriately named and we need to set up a test to test this method.