![](bbox=[0.095, 0.075, 0.145, 0.153])

```
function onComplete(results)
{
  find('dvResults').set_data(results);
}
```

Code file 4-ServerSideDataV8-JSONP.htm available for download at Wrox.com

The DataView is rendered by the browser, as you can see in Figure 19-15.

That's very straightforward — but, wait a minute, is the callback function required passed to the web service?

The Sys.WebServiceProxy class has two properties that support switching from JSON to JSONP, but for most cases, you do not have to set them manually:

+   * By setting the enableJson property to true, you can make the web services use JSONP,

the WebWebServiceProxy should use JSONP instead of JSON. The default value of this property is false. However the invoke method executes the URI and returns JSON when it detects a cross-domain request.

+   * In the JsonCallbackParameter, you can set the name of the query string variable that is expected by the web service to contain the name of the callback function. The default value is "callback" that is appropriate for most JSONP web services. If your web service differs from the de facto standard, you can override the default here.

+   * Charlie Brown Christmas Dance book music waiting for conference call to start: Nice :)
* @VNext (ISBN 9781596988973D Primer )
* Wed Dec 05 07:11+0000 2019
* @Gorgeous our Professional Architectural Handbook Book will be available by end of month
* Tue Dec 03 14:28+0006 2019
* #Winter #Peak Season Indian (Jan 30th Call for Speakers for our tour) Regularly Needed Spicy
* Mon Dec 02 23:11+0000 2019
* RT :Sign up for our DevNetSkills Essentials Webinar, starts in
* Sun Dec 01 18:25+1000 2019

FIGURE 19-15: JSONP to query Twitter

You can use Fiddle to examine the communication between the client and the remote server to see how these properties work. The request contains the following headers (in addition to others that are omitted for clarity):

```
GET /status/user_timeline/wrox.jsoncount=3&callback=Sys._jsonpl HTTP/1.1
Host: twitter.com
```

As you can see, the WebWebService class automatically handles the callback parameter and generated an internal callback function called Sys._jsonpl. As expected, the response contains a for this function, and the result object array is passed as an input parameter:

```
HTTP/1.0 200 OK
Content-Type: application/json; charset=utf-8

Sys._jsonpl({ JSON object array omitted });
```

The auto-generated Sys._jsonpl will pass the service to the onComplete callback function, where it is displayed with the DataView.