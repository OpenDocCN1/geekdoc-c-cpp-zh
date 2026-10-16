```
<?xml version="1.0" encoding="utf-8"?>
<!-- ... -->
```

> NOTE Because the HttpClient class used the GetAsync method call with the await keyword, the calling thread returned and could do some other work. When the result is available from the GetAsync method a thread continues with the method, and the response is written to the response variable. The await keyword is explained in Chapter 15, “Asynchronous Programming.” Creating and using tasks is explained in Chapter 21, “Tasks and Parallel Programming.”

# Throwing Exceptions

Invoking the GetAsync method of the HttpClient class by default doesn’t generate an exception if the method fails. This could be easily changed by invoking the EnsureSuccessStatusCode method with the HttpResponseMessage. This method checks whether IsSuccessStatusCode is false, and throws an exception otherwise (code file HttpClientSample/Program.cs):

```
private async Task GetDataWithExceptionsAsync()
{
    try
    {
        using (var client = new HttpClient())
        {
            HttpResponseMessage response = await client.GetAsync(IncorrectUrl);
            response.EnsureSuccessStatusCode();

            WriteLine($"Response Status Code: {((int)response.StatusCode)}" + $"{response.ReasonPhrase}");
            string responseBodyAsText = await response.Content.ReadAsStringAsync();
            WriteLine($"Received payload of {responseBodyAsText.Length} characters");
            WriteLine();
            WriteLine(responseBodyAsText);
        }
    }
    catch (Exception ex)
    {
        WriteLine($"{ex.Message}");
    }
}
```

# Passing Headers

You didn’t set or change any of the headers when you made the request, but the DefaultRequestHeaders property on HttpClient enables you to do just that. You can add headers to the collection using the Add method. After you set a header value, the header and header value are sent with every request that this instance of HttpClient sends.