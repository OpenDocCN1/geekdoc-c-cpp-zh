
The following example code shows the syntax for creating the table in Figure 5-10 with align, valign, width, and height attributes.

![](img/5a907eb39993e80f28c82efc2e4632b3_83_0.png)

**Figure 5-10:** A table with deprecated align, valign, width, and height attributes.

```
<table align="right" width=50% border=1>
    <tr align="right" valign="bottom">
        <td height=100>The Social Network</td>
        <td>Generation Like</td>
    </tr>
    <tr>
        <td height=200 align="center" valign="middle">Tron</td>
        <td align="center" valign="top" width=20%>Games</td>
    </tr>
</table>
```

> ⚠️ Remember, these attributes are no longer supported and should not be used in your code.

### Filling Out Forms

Forms allow you to capture input from your website visitors. Until now we have displayed content as-is, but capturing input from visitors allows you to:

- **Modify existing content on the page.** For example, price and date filters on airline websites allow for finding a desired flight more quickly.
- **Store the input for later use.** For example, a website may use a registration form to collect your email, username, and password information to allow you to access it at a later date.

### Understanding How Forms Work

Forms pass information entered by a user to a server by using the following process:

1. The browser displays a form on the client machine.
2. The user completes the form and presses the submit button.
3. The browser submits the data collected from the form to a server.
4. The server processes and stores the data and sends a response to the client machine.
5. The browser displays the response, usually indicating whether the submission was successful.

See Chapter 2 for an additional discussion about the relationship between the client and server.

![](img/5a907eb39993e80f28c82efc2e4632b3_84_0.png)

A full description of how the server receives and stores data (Steps 3 to 5) is beyond the scope of this book. For now, all you need to know is that server-side programming languages such as Python, PHP, and Ruby are used to write scripts that receive and store form submissions.

Forms are very flexible, and can record a variety of user inputs. Input fields used in forms can include free text fields, radio buttons, checkboxes, drop-down menus, range sliders, dates, phone numbers, and more. (See Table 5-4.) Additionally, input fields can be set to initial default values without any user input.

**Table 5-4 Selected form attributes**

| Attribute name | Possible values | Description |
|---|---|---|
| type | checkbox<br>email<br>submit<br>text<br>password<br>radio<br>(a complete list of values has been omitted here for brevity) | Defines the type of input field to display in the form. For example, text is used for free text fields, and submit is used to create a submit button. |
| value | text | The initial value of the input control. |

View the entire list of form input types and example code at www.w3schools.com/tags/att_input_type.asp.

![](img/5a907eb39993e80f28c82efc2e4632b3_85_0.png)

### Creating Basic Forms

You create a basic form by

1. **Defining a form with the form element.**

    Start by adding an opening `<form>` tag and closing `</form>` tag.

2. **Using the action attribute, specify in the form element where to send form data.**

    Add an action attribute to your opening `<form>` tag and set it equal to the URL of a script that will process and store the user input.

3. **Using the method attribute, specify in the form element how to send form data.**

    Add a method attribute to your opening `<form>` tag and set it equal to POST.

    The method attribute is set equal to GET or POST. The technicalities of each are beyond the scope of this book, but, in general, POST is used for storing sensitive information (such as credit card numbers), whereas GET is used to allow users to bookmark or share with others the results of a submitted form (such as, for example, airline flight listings).

4. **Providing a way for users to input and submit responses with the input element.**

    Between the opening `<form>` and closing `</form>` tags, create one `<input>` tag.

    Your form will have only one opening and closing `<form>` tag; however, you will have at least two `<input>` tags to collect and submit user data.

5. **Specify input types using the type attribute in the input element.**

    For this example, set the type attribute equal to `"text"`.

    The `<input>` tag does not have a closing tag, which is an exception to the “close every tag you open” rule. These tags are called self-closing tags, and you can see more examples in Chapter 4.

6. **Finally, create another `<input>` tag and set the type attribute equal to submit.**

![](img/5a907eb39993e80f28c82efc2e4632b3_85_1.png)

![](img/5a907eb39993e80f28c82efc2e4632b3_85_2.png)

![](img/5a907eb39993e80f28c82efc2e4632b3_85_3.png)

The following example code shows the syntax for creating the form shown in Figure 5-11.

![](img/5a907eb39993e80f28c82efc2e4632b3_86_0.png)

**Figure 5-11:** A form with one user input and a submit button.

```html
<form action="mailto:nikhil.abraham@gmail.com" method="POST">
    <input type="text" value="Type a short message here">
    <input type="submit">
</form>
```

![](img/5a907eb39993e80f28c82efc2e4632b3_86_1.png)

The action attribute in this form is set equal to mailto, which signals to the browser to send an email using your default mail client (such as Outlook or Gmail). If your browser is not configured to handle email links, then this form won’t work. Ordinarily, forms are submitted to a server to process and store the form’s contents, but in this example form the contents are submitted to the user’s email application.

### Practicing More with HTML

Practice your HTML online using the Codecademy website. Codecademy is a free website created in 2011 to allow anyone to learn how to code right in the browser, without installing or downloading any software. Practice all of the tags (and a few more) that you learned in this chapter by following these steps:

1. **Open your browser, go to** www.dummies.com/go/coding **and click on the link to Codecademy.**

2. **Sign in to your Codecademy account.**

    Signing up is discussed in Chapter 3. Creating an account allows you to save your progress as you work, but it’s optional.

3. **Navigate to and click on HTML Basics II to practice creating lists, and HTML Basics III to practice creating tables.**

4. Background information is presented in the upper left portion of the site, and instructions are presented in the lower left portion of the site.

5. Complete the instructions in the main coding window. As you type, a live preview of your code is generated.

6. After you have finished completing the instructions, click the Save and Submit Code button.

If you have followed the instructions correctly, a green checkmark appears, and you proceed to the next exercise. If an error exists in your code a warning appears with a suggested fix. If you run into a problem or a bug you cannot fix, click on the hint, use the Q&A Forum, or tweet me at @nikhilabraham and include hashtag #codingPD.

## Part II: Building the Silent and Interactive Web Page

### 6 Getting Stylish with CSS

### In This Chapter

- Understanding CSS and its structure
- Formatting text, color, and style
- Styling images
- Using CSS in three different contexts

> Create your own style . . . let it be unique for yourself and yet identifiable for others.
>
> —Anna Wintour

The website code examples I have shown you in the preceding chapters resemble websites you may have seen from a previous era. Websites you browse today are different, and have a more polished look and feel. Numerous factors enabled this change. Twenty years ago you might have browsed the Internet with a dial-up modem, but today you likely use a very fast Internet connection and a more powerful computer. Programmers have used this extra bandwidth and speed to write code to further customize and style websites.

In this chapter you learn modern techniques to style websites using Cascading Style Sheets (CSS). First, I discuss basic CSS structure, and then the CSS rules to style your content. Finally, I show you how to apply these rules to your websites.

### What Does CSS Do?

CSS styles HTML elements with greater control than just using HTML. Take a look at Figure 6-1. On the left, Facebook appears as it currently exists; on the right, however, the same Facebook page is shown without all the CSS styling. Without the CSS, all the images and text appear left-justified, borders and shading disappear, and text has minimal formatting.
