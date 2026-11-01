To show you how to work with complex data at the client, this code example returns two hard-coded Review instances. In later chapters you see how to work with reviews in a database so you could make this example truly dynamic. For now, it just serves the purpose of showing the reviews at the client.

The code sets up a generic collection of Review instances. For now, a Review is a simple class with two properties: an Id and a Title. The collection is then filled using a collection initializer that adds two Review instances, each of them created with an object initializer. Refer back to Chapter 5 for more information on collection and object initializers.

When you call the GetLatestReviews method from client code, you get back a collection of Review instances that you can loop over. The following code shows the getLatestReviewsCallback method that accomplishes this:

```
function getLatestReviewsCallback(result)
{
    var listItems = '';
    for (i = 0; i < result.length; i++)
    {
        listItems += '<li>' + result[i].Title + '</li>';
    }
    document.getElementById('Reviews').innerHTML = listItems;
}
```

This code first declares a string that will hold the titles of the reviews. It then loops over the reviews in the result variable. JavaScript doesn't support foreach, but using a standard for loop you can easily access all items in the collection. Within the for loop, the review's title is retrieved using result[i].Title, which is then wrapped in a pair of <li> tags and appended to a string variable. In the end, the string is added as the innerHTML of an element called Reviews (which could look like this in the code: <ul id="Reviews"></ul>) so the review titles end up in a bulleted list.

When you type this code, you'll notice you don't get IntelliSense for the result object. VS doesn't know the actual type of the result variable, and as such can't help you find properties such as Id and Title.

Note that this code is a bit clumsy. Using document.getElementById and innerHTML isn't the best way to write code like this. Therefore, the next chapter introduces you to better alternatives when it discusses jQuery. For now, though, this should suffice, showing the core concept of working with complex objects returned from a WCF service.

It's important to realize that the Reviews object you work with in JavaScript is not the exact same object as the one you use in the service. Your VB.NET or C# code targets the .NET Framework at the server, whereas your JavaScript runs at the client. To get the object to the client, WCF serializes the collection of reviews into JavaScript Object Notation (JSON)—a string representation of your objects that can be used directly in your JavaScript code. You see an example of JSON in a later exercise.