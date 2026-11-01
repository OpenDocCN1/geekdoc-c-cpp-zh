```
```csharp
using Moq;
using NUnit.Framework;
using System.Threading.Tasks;

[TestFixture]
public class MyServiceTests
{
    [Test]
    public async Task
ProcessDataAsync_ReturnsProcessedValue()
    {
        // Arrange
        var mockDataService = new Mock<IDataService>();
        mockDataService.Setup(d =>
            d.GetDataAsync()).Returns(async () =>
        {
            await Task.Delay(100); // Simulate async delay
            return 42;
        });

        var myService = new
            MyService(mockDataService.Object);

        // Act
        int result = await myService.ProcessDataAsync();

        // Assert
        Assert.AreEqual(84, result); // Expected processed
            value
        mockDataService.Verify(d => d.GetDataAsync(),
            Times.Once); // Verify data service call
    }
}
```
```

In this NUnit example, we use Moq to set up the asynchronous behavior of `GetDataAsync` by using