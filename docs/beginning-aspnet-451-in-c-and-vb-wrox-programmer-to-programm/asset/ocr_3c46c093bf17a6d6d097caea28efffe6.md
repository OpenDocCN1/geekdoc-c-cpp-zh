UpdateProgress panel. For example, in the exercise from this chapter, you should move the <div id="PleaseWait"></div> outside any other controls so it's always visible. You can then change the HTML and the CSS for the <div> until it looks exactly right. Then you can move the <div> back into the UpdateProgress panel so it's only shown during a partial page update.

+   - Whenever you use an UpdatePanel, consider adding an associated UpdateProgress control. Even if you don't see the UpdatePanel refreshes really fast, it might be worth adding the UpdateProgress for people on slow computers or slow networks. Or better yet: add UpdateProgress to the master page in a convenient and reliable area (in the Footer, section). Don't set AssociatedUpdatePanelID to anything so the progress panel will show on an Ajax callback. This way, you don't need to lost waiting indicators in different areas of your site.

+   - Don't use UpdatePanel controls. In many situations, the perceived performance of an application increases when the true performance is false. This is a good thing, because users think your application is faster than without UpdatePanel. However, using too many UpdatePanel controls may confuse your users, especially when the controls are not bound to an UpdateProgress control that tells users what is going on. Consider web services instead, because they can decrease the overhead and the data that gets transferred over the wire.

+   - You may be tempted to wrap the entries of a master page in an UpdatePanel control to avoid page flicker when browsing from page to page. However, this won't work because browsing to a new page is a GET request whereas the UpdatePanel control works only during postbacks.

# SUMMARY

Ajax is a broad and very interesting technology that can add a lot of value to your site.

The UpdatePanel control enables you to create flicker-free pages in no time, whereas the ScriptManager control serves as the bridge between the server and the client and is responsible for tasks requiring the necessary client scripts. Other controls in the AJAX extensions of the Toolbox include the ScriptManagerProxy, the UpdateProgress, and the Timer controls.

Besides these very server-side controls, the ASP.NET AJAX Framework also brings functionality that enables you to access web services in your site with just a few lines of code. Web services can be used to exchange data without the server blocking or fully reloading the web interface.

Ajax itself is a very compelling technology, it becomes even more useful in richer, data-driven scenarios. For example, using an UpdatePanel control around the records returned from a database to avoid page flicker when sorting, filtering, or paging your data greatly enhances the user’s browsing experience. You learn how to work with databases in Chapter 12. With the knowledge about Ajax you gained from this chapter, you will quickly create flicker-free, database-driven web pages.