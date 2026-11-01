
| METHOD NAME | PURPOSE |
|---|---|
| `toggle()` | The toggle method uses show and hide internally and changes the display of the matched elements. That is, visible items are hidden, and vice versa. Example: `$('h1').toggle(2000); // hide or show the h1 in 2 seconds` |
| `slideDown()`<br>`slideUp()`<br>`slideToggle()` | Just like hide and show, these methods make matched elements appear or disappear. However, they do this by adjusting the height from its current size to zero or vice versa, causing the element to 'slide up' or 'slide down.' The slideToggle method slides down hidden elements and slides up visible elements, which makes it easy to show and hide elements repeatedly with a single action. Examples: `$('h1').slideUp(1000);` `$('h1').slideDown(1000);` `$('h1').slideToggle(1000);` |
| `fadeIn()`<br>`fadeOut()`<br>`fadeTo()` | These methods make the matched elements visible or invisible by changing their opacity. fadeOut sets the opacity to 0, making the item completely transparent, and then sets the CSS display property to none, hiding the item completely. fadeTo lets you specify an opacity (a number between 0 and 1) to determine the transparency level of the elements and fadeIn makes the item visible again and sets the opacity to 1. All three methods enable you to define a fixed speed (slow, normal, and fast) or a number defining the duration of the animation in milliseconds. Examples: `$('h1').fadeOut(1000); // dissolve the h1 in 1 second` `$('h1').fadeIn(1000); // h1 reappears in 1 second` `$('h1').fadeTo(1000, 0.5); // fade to semi-transparent` |
| `animate()` | Internally, animate is used for many of the animation methods like show and hide. However, it's also externally available to give you great flexibility in animating your matched elements. With the animate method you can specify a bunch of properties to animate. Consider this example: `$('h1').animate({ opacity: 0.4, marginLeft: '50px', fontSize: '50px' }, 1500);` In one smooth animation with a duration of 1.5 seconds, this code takes the h1 element and increases its font size to 50 pixels, sets the opacity to 0.4 to make the element semi-transparent, and changes the left margin to 50 pixels. The first argument of the animate method is an object holding one or more properties you want to animate, each one separated by a comma. Notice how you need to use JavaScript's marginLeft and fontSize, rather than the CSS margin-left and font-size properties. You can only animate properties that take numeric values. That is, you can use properties like margin, fontSize, opacity, and so on, but not properties like color or fontFamily. |

`_references.js` as well to light up IntelliSense for other JavaScript libraries. I really like this feature because it gives you IntelliSense everywhere without messy hacks or double script references. You never have to include a reference to this special file in the pages or controls in your site; it serves purely as a development-time feature.

### 4.

Back in the user control `ContactForm.ascx`, scroll down to the end of the control's markup, and add a `<script>` element and the following jQuery code that fires when the form is about to be submitted:

```html
<script type="text/javascript">
$(function() {
  $('form').bind('submit', function()
  {
    if (Page_IsValid)
    {
      $('#TableWrapper').slideUp(3000);
    }
  });
});
// Code from step 5 goes here
</script>
```

### 5.

Right before the closing `</script>` tag and after the closing curly brace, parenthesis, and semicolon of the jQuery document ready function, add the following bold piece of JavaScript:

```javascript
});
function pageLoad()
{
  $('.Attention').animate({ width: '600px' }, 3000).
    animate({ width: '100px' }, 3000).fadeOut('slow');
}
</script>
```

The `pageLoad` method (which is part of the client-side JavaScript made available by ASP.NET AJAX) serves the same purpose as jQuery's document ready, with one exception: it also fires after a partial page update, which is what takes place after you submit the form because of the `UpdatePanel` in the user control.

### 6.

Switch to Code Behind and add the following line of code to the `SendButton_Click` method. This code makes the text paragraph visible when the form is submitted and the e-mail message is sent:

**VB.NET**

```vbnet
Message.Visible = True
MessageSentPara.Visible = True
FormTable.Visible = False
```

**C#**

```csharp
Message.Visible = true;
MessageSentPara.Visible = true;
FormTable.Visible = false;
```

### 7.

Save all your changes and close the user control because you're done with it.

### 8.

Open the `Monochrome.css` file from its theme folder and add the following CSS declaration to the bottom of the file:

```css
.Attention
{
border: 4px solid red;
padding: 10px 0;
width: 100px;
margin: auto;
display: block;
text-align: center;
}
```

### 9.

Copy the same declaration to the DarkGrey theme's CSS file.

### 10.

Save your changes and then request the Planet Wrox site in your browser. Choose the Contact Us item (under About) from the Menu or TreeView control, fill in the form, and click Send. Notice how shortly after clicking the button the form slides up slowly until it completely disappears. Figure 11-6 shows the form halfway during the slideUp operation.

![](img/eadab2ccd79b253c01a3fdff2321202d_457_0.png)

FIGURE 11-6

### 11.

Once the page is done loading, the Message Sent label and the thank you text appear. Notice how the label first grows in size to span the full content width, then shrinks again and finally disappears completely. Figure 11-7 shows the message while it's being resized. If you don't see this animation appear, press Ctrl+F5 or Ctrl+R to get a fresh copy of the CSS file from the server and then fill in the contact form again.

![](img/eadab2ccd79b253c01a3fdff2321202d_457_1.png)

FIGURE 11-7

## How It Works

A lot of the steps involved in this exercise deal with things you've already seen: adding `<div>` elements, classes, and CSS declarations. However, there's some jQuery and some Ajax code in this example

As you saw in the previous sections, jQuery is really powerful. You can use it to find elements in your page, manipulate them through code, change the appearance of elements and create animations. However, jQuery can be used for more than that. The remaining section of this chapter deals with the topic of using jQuery for validation.

## JQUERY AND VALIDATION

Remember the validation controls you used in Chapter 9 to validate the contact form? The validation controls work by generating JavaScript that is added to the page. The downside of that approach is that your page becomes unnecessarily large because a lot of repetitive code is added to each page that uses these controls. The developers of ASP.NET have thought of this too and decided to leverage the power of jQuery to improve client-side validation. They have done this through a concept known as *unobtrusive JavaScript*, where the functionality (the code that gets executed) has been separated from the structure and content of the page. Rather than embedding large chunks of JavaScript code in the page, they have written a small JavaScript library that uses jQuery under the hood to perform the validation. This leads to cleaner code and reduces the size of the page. For the Contact Us page, enabling unobtrusive JavaScript validation decreased the size of the final HTML from 20.7 KB to 14.9 KB, a reduction of more than 25 percent.

Configuring the validation framework to use unobtrusive validation with jQuery instead of the built-in code that is generated is a two-step activity:

1. Enable unobtrusive validation in the `Web.config` file.
2. Register the jQuery library with the `ScriptManager` in the `Global.asax` file.

The `Global.asax` file is a special ASP.NET file that you add to the root of the site. Inside this file you can write code that responds to global events that happen within your application. These events work the same as other events you've seen so far, such as the `Button`'s `Click` event. The biggest difference is that these events fire for the entire application (your website) and not for a single control or page. For example, when your ASP.NET application starts up, the `Application_Start` event is fired, enabling you to execute your own code. Other events that fire include `BeginRequest`, which fires for each request to the site and `Application_Error`, which fires when an unhandled exception in your site occurs. You make use of this last event in Chapter 18, which deals with debugging and exception handling.

In the next exercise you see how to add the `Global.asax` file to your site and then enable unobtrusive JavaScript validation.

## TRY IT OUT Enabling Unobtrusive JavaScript Validation

In this exercise you revisit the current Contact Us page to look at the code that the controls generate. You'll then add a `Global.asax` file and enable unobtrusive JavaScript validation so you can see the effect this has on the code that is generated.

1. Start by opening the `Contact.aspx` file from the `About` folder and then press Ctrl+F5 to view that page in your browser.
