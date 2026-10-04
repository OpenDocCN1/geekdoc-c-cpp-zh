
## Exercise 2 Solution

If you don't check the IsValid property, your system is vulnerable to invalid data. Users can disable JavaScript in their browsers and submit invalid data directly into your page. By checking the IsValid property you can tell whether or not it's safe to continue with the submitted data.

## Exercise 3 Solution

The From property of the MailMessage class is of type MailAddress, meaning that you can directly assign a single instance of this class to it. Because you potentially have more than one recipient, the To property is a collection of MailAddress objects, and so you need to use its Add method to add instances of MailAddress to it.

## Exercise 4 Solution

To call a client-side validation function, you need to set the ClientValidationFunction property of the CustomValidator like this:

```
<asp:CustomValidator Id="CustomValidator1" runat="server"
    ClientValidationFunction="functionName*"></asp:CustomValidator>
```

The client function you need to add to the markup of the page must have the following signature:

```
function functionName(source, args)
{ ... }
```

The source argument contains a reference to the actual CustomValidator control in the client-side HTML code. The args argument provides context information about the data and enables you to indicate whether or not the data is valid. The names of the arguments don't have to be source and args; however, when using the client-side function looks as close to its server-side counterpart as possible. Another common naming scheme, used for almost all other event handlers in ASP.NET, is to use sender and e, respectively.

## Exercise 5 Solution

To tell the mechanism whether the data you checked is valid, you set the IsValid property of the args argument in your custom validation. This applies to both client- and server-side code. The following snippet shows how this is done in the client-side validation method for the ContactForm.ascx control.

```
if (phoneHome.value != '' || phoneBusiness.value != '')
{
    args.IsValid = true;
}
else
{
    args.IsValid = false;
}
```

## CHAPTER 10

## Exercise 1 Solution

ScriptManager control is a required component in almost all Ajax-related operations. It takes care of registering client-JavaScript files, handles interaction with web services in your website, and is responsible for the partial page updates. You usually place the ScriptManager directly in a content page if you need Ajax capabilities on a handful of pages. However, you can also place the ScriptManager in a master page so it becomes available throughout the entire site.

When you have the ScriptManager in the master page you can use the ScriptManagerProxy to register individual web services or script files on content pages. Because you have only one ScriptManager in a page, you cannot add another one in a content page that uses your master page with the ScriptManager. The ScriptManagerProxy serves as a bridge between the content page and the ScriptManager, giving you flexibility as to where you register your services.

## Exercise 2 Solution

You can let your users know a partial page update is progress by adding an UpdateControl to the page. You connect this control to an UpdatePanel using its AssociatedUpdatePanelID. Inside the <ProgressTemplate> you define whatever markup you see to inform your user that an update is in progress. A <ProgressTemplate> contains an animated icon, text, or both.

## Exercise 3 Solution

To create a script-callable service, you first need to add an AJAX-enabled WCF service file to your site using the Add New Item dialog. The class file that is created for you already has the ServiceContract and AspNetCompatibilityRequirements attributes.

```
VB.NET
<ServiceContract(Namespace = "")
<AspNetCoreCompatibilityRequirements(
RequirementMode:=AspNetCompatibilityRequirementsMode.Allowed)>
  Public Class NameOfYourService
```

```C#
[ServiceContract(Namespace = "")
[AspNetCoreCompatibilityRequirements(
RequirementMode = AspNetCompatibilityRequirementsMode.Allowed)]
public class NameOfYourService
```

You then need to decorate each method within this class that you want exposed as a web method with the OperationContract attribute:

```
VB.NET
<OperationContract()>
Public Function NameOfYourMethod(parameters) As DataType
```

## 768 | APPENDIX A EXERCISE ANSWERS

### C#

```
[OperationContract]
public DataType NameOfYourMethod(parameters) in ScriptManager or ScriptManagerProxy,
```

Once you have registered the Wcf service with your client-side JavaScript, you can call the service as follows from your client-side JavaScript:

```
NameOfYourService.NameOfYourMethod(
    parameters, successCallback, errorCallback);
```

## CHAPTER 11

## Exercise 1 Solution

To accomplish this, you first need to set the ClientIDMode of VerticalPanel to Static in the marker of Banner.ascx. This makes it easier to work with the client IDs of the controls inside the panel:

```
<asp:Panel ID="VerticalPanel" runat="server" ClientIDMode="Static">
```

Then you need to add a `<span>` element just below VerticalPanel with the text Header Banner. The style attribute changes the mouse cursor to a hand so users understand the text is clickable when they hover over it. You also need to add a `runat` attribute and a server-side ID so you can hide the link in the Code Behind. You also need to give it a `class` attribute so you can find the element using jQuery. You would end up with this `span` element:

```
<span id="HideBanner" style="cursor:pointer;" runat="server" class="HideBanner">Header Banner/</span>
```

In a script block below the last panel, you need to add the following code:

```
<script>
$(function () {
{
    $('.HideBanner').bind('click', function () {
        $('#VerticalPanel').slideToggle('fast', function () {
            if ($(this).css('display') == 'block') {
                $('.HideBanner').text('Hide Banner');
            } else {
                $('.HideBanner').text('Show Banner');
            }
        });
    });
});
});
</script>
```

This code dynamically binds some class to the click event of the <span> element found by using $('.HideBanner'). Then inside the handler for the click, the code finds the whole panel (VerticalPanel) and calls slideToggle, which hides in the matched set when they are visible and show them when they aren't. If the check uses the css method on the VerticalPanel element (now referred with this keyword) and asks for its display property. When it is block it means the banner and the text must be Hide Banner. Otherwise, the text is set to Show Banner. Finally, you need to hide the link when the banner is in horizontal mode in the banner's Code Behind:

### VB.NET

```
Case Direction.Horizontal
HorizontalPanel.Visible = True
VerticalPanel.Visible = False
HorizontalLink.HRef = NavigateUrl
HideBanner.Visible = False
```

### C#

```
case Direction.Horizontal:
HorizontalPanel.Visible = true;
VerticalPanel.Visible = false;
HorizontalLink.HRef = NavigateUrl;
HideBanner.Visible = false;
break;
```

## Exercise 2 Solution

The slideUp method hides elements by slowly decreasing its height. slideDown shows hidden elements by doing the reverse: slowly increasing the height of an element until it's fully visibleble. Both methods accept, among others, a speed parameter that either accepts a fixed value (slow, normal, or fast) or a number specifying the speed of the animation in milliseconds.

## Exercise 3 Solution

jQuery document ready functions fires when the page is loading in the browser, during the initial request. The pageLoad method fires both when the page loads first and after an asynchronous postback, for example, using an UpdatePanel. This difference enables you to choose the desired behavior. Need to fire some code on initial load and after a postback? Choose pageLoad. Otherwise, use document ready function.

## Exercise 4 Solution

You use the _references.js file in the Scripts folder to enable IntelliSense. VS will read this file and all JavaScript files that you added with this syntax:

```
/// <reference path="Path/To/File.js" />
```

This way, you get IntelliSense in files where it would not be supported (such as user controls) or for JavaScript files that you're not linking linking to your website.
