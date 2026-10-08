Most effect methods take one or more arguments describing the effect. Generally, the first argument is the time of the animation specified in milliseconds or literally such as "slow" or "fast". All effect methods take an optional callback invoked when the animation is completed.

> For more detail on animations and visual effects, see the jQuery reference and tutorial at http://api.jquery.com/category/effects/. You will also find examples there to help you understand how a specific effect works.

# jQuery Ajax Features

In jQuery, you can easily leverage the Ajax infrastructure and call asynchronously postbacks. The key of this behavior is the Ajax function which you can control all aspects of a web request. jQueryAjax.htm page demonstrates how easy it is to call a web service with this. The page has a link, and when you click on it, it initiates the asynchronous postback. When the call is completed, the result is displayed, as shown in Figure 20-32.

The ajax method is called as the following code snippet shows:

```
function pageLoad() {
  $('a').click(callAjax)
}

function callAjax(event) {
  $.ajax(
    type: "POST",
    url: "/ExpertiseService.asmx/GetExpertises",
    data: "",
    success: function (response) {
      $("#result")[0].innerText = response.xml;
    }
  });
  event.preventDefault();
}
```

![](bbox=[0.545, 0.303, 0.855, 0.535])

FIGURE 20-32: Calling a Web service from jQuery

You can see that the success parameter defines the function to run when the web service call completed. This method simply copies the XML result into a literal text field in the page.

The web service at the back-end is also very simple, as Listing 20-58.