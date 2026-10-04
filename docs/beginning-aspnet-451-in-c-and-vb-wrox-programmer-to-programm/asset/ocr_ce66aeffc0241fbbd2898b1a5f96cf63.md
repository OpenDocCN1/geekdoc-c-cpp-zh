Fortunately, since ASP.NET 4.5 this is very easy; the Control class (from which controls as TextBox inherit) has been extended with a ValidateRequestMode property that controls check for invalid data. When set to Enabled, the control does not accept HTML; set to Disabled the control does accept HTML, similar to how ValidateRequest enables this for all controls in the page. The final value for ValidateRequestMode Inherit, gives it the value by the parent of the control such as a Placeholder. This is convenient because you can wrap multiple controls that should accept HTML in a Placeholder and then the ValidateRequestMode on the container instead of each individual control.

Before you set this on a control, make sure you really want to allow users to submit HTML in your controls. This opens up your site for Cross Site Scripting attacks if you're not careful. Depending on the situation, you may need to sanitize the data by removing dangerous pieces of code such as <script> elements. When displaying the data on a page, you could use a Literal control, with its Mode to Encode in order for the HTML to be encoded and rendered harmless. With this property, the text is displayed verbatim, without being interpreted as HTML or JavaScript.

# PROCESSING DATA AT THE SERVER

The information that a user inputs on your Web Forms is typically the only data that makes your website an interactive, data-driven system. In most websites, you have information coming from other sources such as databases, XML files, and web services. In addition, there is also data coming out of your system. You may want to send an e-mail to the owner of the website when someone posts information through the contact page, or you may want to notify people whenever you add a new feature or review to the website. For these scenarios, it's important to understand how ASP.NET enables you to send e-mail. This is discussed in the next section.

# Sending E-mail from Your Website

Writing code that sends e-mail from an ASP.NET page is pretty straightforward. Inside the .Net namespace you find a number of classes that make it easy to create and send e-mail messages. These classes enable you to create new messages; addressees in the To, CC, and Bcc fields; add attachments; and, of course, send the messages.

The following table describes four classes that you typically work with when sending e-mail from a .NET application.

| CLASS | DESCRIPTION |
|--- |--- |
| MailMessage | This class represents the message you're going to send. It has properties such as Subject and Body to set the message contents; To, CC, and Bcc properties to set the addressees; and an Attachments collection to attach files to the message. |
| MailAddress | This class represents a sender or receiver address used in the e-mail. It has a few constructors that enable you to set the e-mail address and display name.