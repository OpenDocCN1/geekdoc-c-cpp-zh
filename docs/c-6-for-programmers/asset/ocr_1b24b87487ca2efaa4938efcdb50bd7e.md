# # 21.6 Invoking a Flickr Web Service Asynchronously with HttpClient

As shown in Fig. 21.4, you can type one or more tags (e.g., "pdeitel flowers") into the TextBox. When you click the Search Button, the application invokes the Flickr web service that searches for photos, which returns an XML document containing links to the first 500 (or fewer if there are not 500) results that match the tags you specify. We use LINQ to XML to parse the results and display a list of photo titles in a ListBox. When you select an image's title in the ListBox, the app uses another asynchronous Task to download the full-size image from Flickr and display it in a PictureBox.

# # 21.6.1 Using Class HttpClient to Invoke a Web Service

This app uses class HttpClient (namespace System.Net.Http) to interact with Flickr's web service and retrieve photos that match the search tags. Line 21 creates the static HttpClient object flickrClient that's used in this app to download data from Flickr. Class HttpClient is one of many .NET classes that support asynchronous programming with async and await. In SearchButton_Click (lines 32–96), we use class HttpClient's GetStringAsync method to start a new Task (line 65). When we create that Task, we assign it to instance variable flickrTask (declared in line 23) so that we can test whether the Task is still executing when the user initiates a new search.

![](bbox=[0.157, 0.396, 0.89, 0.466])

# # 21.6.2 Invoking the Flickr Web Service's flickr.photos.search Method

Method searchButton_Click (lines 32–96) initiates the asynchronous Flickr search, so it's declared as an async method. First, lines 35–51 check whether you started a search previously and, if so, whether that search has already completed (lines 34–35). If an existing search is still being performed, we display a dialog asking if you wish to cancel the search (lines 37–40). If you click No, the event handler simply returns. Otherwise, we call the HttpClient's CancelPendingRequests method to terminate the search (line 49).

Lines 54–57 create the URL that invokes Flickr's flickr.photos.search web-service method, which searches for photos, based on the provided parameters. You can learn more about this method's parameters and the format of the URL for invoking the method at

 https://www.flickr.com/services/api/flickr.photos.search.html

```
https://www.flickr.com/services/api/flickr.photos.search.html
```

In this example, we specify values for the following flickr.photos.search parameters:

+   - api_key—Your Flickr API key. Remember that you must obtain your own key from https://www.flickr.com/services/apps/create/apply/.
+   - tags—A comma-separated list of the tags for which to search. In our sample executions it was "pdeitel,flowers". If the user separates the tags with spaces, the app replaces the spaces with commas.
+   - tag_mode—We use the all mode to get results that match *all* the tags specified in the search. You also can use any to get results that match *one or more* of the tags.