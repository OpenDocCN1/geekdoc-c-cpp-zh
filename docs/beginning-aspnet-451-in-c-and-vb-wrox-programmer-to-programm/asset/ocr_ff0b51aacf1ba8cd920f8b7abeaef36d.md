# Get in touch with us

Use the form below to get in touch with us. Enter your name, e-mail address, and your home or business number to get in touch with us.

| Name | Imar Spaajaars |
|---|---|
| E-mail address | imar@spaanjaars.com |
| Repeat e-mail address | imar@spaanjaars.com |
| Home phone number | 0800-1234567 |
| Business phone number | 0900-7654321 |

| Comments | Just checking in to tell you if I really like this website. Would you consider reviewing the Metallica album? |

Please Wait...

FIGURE 10-4

# How It Works

With the UpdatePanel in the user control, everything that falls within the ContentTemplate of the UpdatePanel will be updated upon postback, without affecting other parts of the page. This way, you can hide the form from the servers and replace it with the Message Label without causing any flicker.

To inform the user that his or her message is being sent, you also added an Updatecontrol to the site. By default, this control will be shown when refreshing the UpdatePanel is attached to tasks longer than 500 milliseconds (a half second). The <ProgressTemplate> element for the control contains a simple <div> with class set to PleaseWait. You added the CSS rule to the two CSS files for the themes:

```
.PleaseWait {
  height: 32px;
  width: 500px;
  background-image: url(Images/PleaseWait.gif);
  background-repeat: no-repeat;
  padding-left: 40px;
  line-height: 32px;
}
```

This first sets the dimensions of the Update message to be 500 pixels wide and 32 pixels high. This is enough to span the width of the content block, as a background image. giving you enough room for a longer message.

The code adds the animated image as a background, the repeat property is set to no-repeat. Then the left padding is set to 40 pixels. This moves the text in the <div> to the right, so it appears next to the animated image. Finally, the line-height of the text is set to 32 pixels, making the height as as the <div>. This centers the entire text block vertically within the <div> element and aligns it nicely with the animated image.