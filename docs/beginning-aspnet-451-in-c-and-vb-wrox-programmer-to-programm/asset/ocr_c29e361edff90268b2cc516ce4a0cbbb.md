You see more of the UpdatePanel in later exercises in this chapter.

# # UpdatePanel Caveats

As useful as the UpdatePanel seems (and is), its usage comes at a price. Although it appears as if only part of the page is refreshed, the entire page (and all of its data) is sent posted back to the server. At the server, the page still goes through its normal life cycle and then sends back the HTML that is needed to update the page. However, the data that is sent isn't in a very optimal format because it contains some other data (required by ASP.NET AJAX to understand how to interpret it). This means that the UpdatePanel carries some overhead in terms of postbacks, page processing, and network traffic. In this chapter, you will see some ways to get data to and the server from client-side code to minimize this overhead.

As demonstrated in the previous exercise, the UpdatePanel control is capable of refreshing parts of a page. Controls that defined either inside the UpdatePanel or outside of it can cause a refresh of the UpdatePanel. However, in order to function, the UpdatePanel needs a ScriptManager control that manages the client-side JavaScript, among other things.

# # The ScriptManager Control

The ScriptManager control serves as the bridge between the client page and the server. It manages script resources (the JavaScript files used at the client), takes care of partial-page updates as shown earlier, and handles interaction with your website for things like WCF services.

You usually place the ScriptManager control directly in a content page if you need AJAX capabilities on a handful of pages. However, you can also place the ScriptManager in a master page so it becomes available throughout the site. You will do this in a later exercise in this chapter.

The ScriptManager class has a number of properties, of which most are used in advanced scenarios. As you saw, you don't need to change any of the properties of a page using the UpdatePanel. In other scenarios, you may need to change or set some of its properties. The following table lists some of the common properties of the ScriptManager control.

| PROPERTY | DESCRIPTION |
| --- | --- |
| AllowCustomErrorsRedirect | This property determines whether errors that occur during an AJAX operation cause the customized error page to be loaded. The default is True; with a setting of False, the error is shown as a JavaScript alert in the browser or is hidden from the client when debugging is disabled. Note that if you haven't configured any customized error page, the error is always shown as a JavaScript alert, regardless of the value of this setting. Chapter 18 talks more about setting up customized error pages and debugging your application.