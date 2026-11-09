
- b. Take frequent breaks: I recommend taking breaks every 20-30 minutes. Take a walk in between periods.
- c. Diet: Maintain a healthy diet high in good fats, protein and complex carbs. Minimize simple carbs and sugar.
- d. Exercise: Maintain a regular exercise regime or play a sport. It’s important to exercise at least 3-4 times a week (maybe more).
- e. Sleep: Get at least 7-8 hours of sleep every night. If you’re unable to sleep, ask a qualified doctor how you can improve your sleep.

One can write entire books on each of the above topics; but this is a coding book, so I will leave it there. Just remember that the above soft skills are very important and you can work on them while you are coding as well.

## Setting Up Your Workspace

### What You Need

You need a laptop/desktop with an internet connection, and a web browser installed. I recommend using Mozilla Firefox or Google Chrome.

### Download/Install Text Editing software

Download the latest version of a text editing software. I recommend downloading NotePad++. Once you download, double click the Setup.exe file and follow the installation prompts.

[https://notepad-plus-plus.org/downloads/](https://notepad-plus-plus.org/downloads/)

### Start using NotePad++

Open Notepad++ from your Desktop or Start Menu

![](img/443990a0ec620659ce8be783c0758bc6_229_0.png)

Now, click **File>New** to open a New File.

Now, choose **File > Save As** and choose **.html** as the file type

![](img/443990a0ec620659ce8be783c0758bc6_231_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_231_1.png)

### Test Program

Now, let’s test if the program connects with the browser.
Just type in random text in your file. In my file, I’ve typed **“This is a Test Message.”**
Now **File>Save.**
After that, click **Run>Launch in Firefox/Chrome/IE** depending on which browser you are using.
If it is working, the text that you typed in should show in the browser window.

![](img/443990a0ec620659ce8be783c0758bc6_232_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_233_0.png)

- Run... F5
- **Launch in Firefox** Ctrl+Alt+Shift+X
- Launch in IE Ctrl+Alt+Shift+I
- Launch in Chrome Ctrl+Alt+Shift+R
- Launch in Safari Ctrl+Alt+Shift+A
- Get PHP help Alt+F1
- Wikipedia Search Alt+F3
- Open file in another instance Alt+F6
- Send via Outlook Ctrl+Alt+Shift+O
- Modify Shortcut/Delete Command...

Result:

![](img/443990a0ec620659ce8be783c0758bc6_234_0.png)

This is a great simple way to ensure that your program is working before moving forward.

### Aside:

One issue that some students have encountered is that the run browser option sometimes does not work and gives an error. This is because the path is not set right. If, for some reason, it doesn’t work, you can still run the program.

- 1. Just save the Notepad++ as a html document.
- 2. Close the Notepad++ file.
- 3. Go the folder where the html document is.
- 4. Double click on the html file and it should work.

## What is html?

html stands for Hyper Text Markup Language. It is the programming language that we use to interact with the internet through web pages. The basic structure of all web pages is defined by html. It is simple enough for beginner programmers to grasp quickly. Most html programming is done by items called tags. These tags start with <> and end with </>. For example, a common tag is the paragraph tag which begins with <p> and ends with </p>.

### Common html Tags

- **<html>** - This tag is used at the start of every webpage to denote the start of html code
- **<head>** - This piece of html code is executed before the rest of the program
- **<title>** - This tag is used set the title the web page. It writes the text on to the top ribbon of the webpage.
- **<body>** - This is the information on the body of the web page.
- **<h1>** - Used to denote a heading tag. This is the largest size heading tag.
- **<h2>,<h3>,<h4>,<h5>,<h6>** - Used to denote subheadings of decreasing size.
- **<p>** - Used to denote paragraphs of text
- **<img>** - This shows an image on the web page. This image either links to an external web page or to an internal file.
- **<strong>** - Added to make text bold
- `<ul>` - This is for an unordered list. An example of this would be a list of items in bullet form.
- `<li>` - Adds a bullet item to an unordered list.
- `<ol>` - This is for ordered lists such as numbered lists from 1,2,3….
- `<div>` - Used to denote larger sections of text; that contain several paragraphs..
- `<a>` - Used to link items in a web page to another web page.
- `<br>` - Adds a line break to the code and moves to the next line.

### Example of html code

Below is an example of basic html code. It has examples of all the above html codes. You can type these out or copy paste the example below that.

![](img/443990a0ec620659ce8be783c0758bc6_237_0.png)

### Copy Paste Version of html code

You can copy and paste below code into your html browser to see if it works

```html
<html>
<head>
<title>My first html website......</title>
</head>
<body>
<h1>Welcome to Programming in Javascript (this is a h1 tag)</h1>
<h2>Let’s get started (this is a h2 tag)</h2>
<h3>This is the start of bigger things (this is a h3 tag)</h3>
<p>We’re going over a few basic html tags here but you can feel free to
play around them and experiment.
There are 1000's of html tags that you can learn in the long run. Here's a list
of topics you can learn below (This is a paragraph tag)</p>

<ul> Below is the example of an unordered bulleted list
<li>Basics of html</li>
<li>CSS</li>
<li>JavaScript</li>
<li>Loops</li>
<li>Arrays</li>
<li>Canvas</li>
</ul>
<a href="https://www.google.com">Example of hyperlink to Google</a>
<br>
<a href="https://www.facebook.com">Example of hyperlink to Facebook</a><br>
<a href="https://www.amazon.com">Example of hyperlink to Amazon</a>
<br>
</body>
</html>
```

### Code Output

![](img/443990a0ec620659ce8be783c0758bc6_238_0.png)

Now, let’s break down the different elements: Below is the title tag `<title>`.

![](img/443990a0ec620659ce8be783c0758bc6_239_0.png)

Below are the heading tags `<h1>`, `<h2>`, `<h3>`

![](img/443990a0ec620659ce8be783c0758bc6_239_1.png)

Below is the paragraph tag `<p>`

![](img/443990a0ec620659ce8be783c0758bc6_239_2.png)

Below is an unordered bulleted list `<ul>` `<li>`

- Basics of html
- CSS
- JavaScript
- Loops
- Arrays
- Classes

Below are 3 hyperlink tags to 3 popular websites `<a href>`

- [Example of hyperlink to YouTube](#)
- [Example of hyperlink to Facebook](#)
- [Example of hyperlink to Instagram](#)

### Practice Problems

- 1. Make a website with a title tag that has a list of grocery items in an unordered list. Use a paragraph tag to indicate any special instructions you may have for particular items. At the end of the list, use a hyperlink tag to link to the website of the closest grocery store.
- 2. Create a website with a list of all the players on your soccer team. Use a title, heading and paragraph tag to welcome users to your website and describe the team and the philosophy of the team. Use an ordered list to list the players.
- 3. Make a website that lists all your favorite restaurants and coffee shops in your area in an unordered list. Use a title, heading and paragraph tag to introduce yourself and the dining experience in your area.

## Sample html Program

### What This Project Does

This html project creates two buttons. These two buttons switch between two images of Day and Night. The two buttons are labelled ‘Day’ and ‘Night’

This is a simple html project that creates a button that can switch a light bulb on the page on/off. We are going to use two bulb images to make this happen. The button will switch between the two images.
