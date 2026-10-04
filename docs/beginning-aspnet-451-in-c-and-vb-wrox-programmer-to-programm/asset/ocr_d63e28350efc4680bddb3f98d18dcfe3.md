This code first tries to get the value from View State using ViewState("NavigateUrl") in VB.NET or ViewState["NavigateUrl"] in C#, which use square brackets to access items in a collection. The value that is returned is Nothing or null, the getter returns the default value for the property: http://p2p.wrox.com.

However, if the value is not Nothing, it is cast to a string using CType in VB.NET and (string) in C# and eventually returned to the calling code. At the end, the NavigateUrl returned from the View property is assigned to the Href property of the anchor tag, which is used as the URL users are taken when they click the image.

# View State Considerations

Although View State is designed to overcome the problems of maintaining state as outlined in the previous exercise, you should carefully consider whether or not use it. When you store in View State are sent to the browser and back to the server on every request. When you store many or large values in View State, this increases the size of the page and negatively impacts performance. Never large objects like database records in View State; it is often quicker to get the data from the database on each request than to pass it along the hidden View Field if the amount of data that needs to be stored is large. Also, because the View State is stored within the page and is thus transferred over the wire, you shouldn't use it to store sensitive values such as passwords.

# PRACTICAL TIPS ON USER CONTROLS

The following list provides some practical tips for working with user controls:

+   - Don't overuse user controls. User controls are great for encapsulating repeating content, but they also make it a little harder to manage your site because code and logic is contained in multiple files. If you are not sure if control will be reused in another part of the site, start by embedding it directly in the page. You can always move it to a separate user control if the need arises.

+   - Keep controls focused on a single task. Don't create a user control that is able to display five different types of unrelated content with a property that determines what to display. This makes the control difficult to maintain and use. Instead, create lightweight controls and use them appropriately.

+   - When you create user controls that contain styled markup, don't hardcode style information like the CssClass for the server controls contained in the user control. Instead, creating separate CssClass properties on the user control, which are then used to set the CssClass of your server controls. This improves the reusability of your user control, making it easier to incorporate the control in different designs.