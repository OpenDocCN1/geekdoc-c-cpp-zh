# Using Web Services in Ajax Websites

the service encounters an error or is not available). The final parameter is called useContext and enables you to pass additional data to your callback methods. This is useful if you need additional context data to correctly process the success callback. In this example, the first parameter is required and the other three are optional. However, in real-world scenarios you implement the least onSuccess callback in order to work with the data returned from the service.

In this example, the code in the success callback HelloWorldCallback is really simple; all it does is alert the value returned from the service. However, it doesn't have to be this simple. The values you can return from the service are not limited to simple strings, as you see in the following section.

# Exchanging Objects with WCF

Although a simple string can be enough as the response from a service, you typically need more information. For example, you may want to load the last two reviews from a service when a user clicks a refresh button. Rather than posting the entire page, you could call a service, retrieve reviews from the database, and then display them in the page somehow. Here is an example of how a service that retrieves reviews could look:

```
VB.NET
<ServiceContract(Namespace="")
[AspNetCoreCompatibilityRequirements(RequirementMode=AspNetCoreCompatibilityRequirementsMode.Allowed)]
Public Class ReviewsService

<OperationContract>
Public Function GetLatestReviews() As List(Of Review)
Dim temp As List(Of Review) From
{
    New Review() With {.Id = 1,
    .Title = "21st Century Breakdown by Green Day",n    New Review() With {.Id = 2,
    .Title = "Sonic Youth: Daydream Nation live in Roundhouse, London"
}
Return temp
End Function
End Class

Public Class Review
Public Property Id As Integer
Public Property Title As String
End Class
```

```
C#
[ServiceContract(Namespace = "")
[AspNetCoreCompatibilityRequirements(RequirementMode=AspNetCoreCompatibilityRequirementsMode.Allowed)]
public class ReviewsService
{
    [OperationContract]
    public List<Review> GetLatestReviews()
    {
        List<Review> temp = new List<Review>()
```