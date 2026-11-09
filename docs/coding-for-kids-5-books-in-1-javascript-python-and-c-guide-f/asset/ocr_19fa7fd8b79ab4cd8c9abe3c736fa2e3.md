# html forms

Remember those forms you see online where you enter your name and age and date of birth? Those are html forms.

Today, we’re going to learn how to make those.

Before we start making forms, we need to learn about a few basic form elements:

**Button `<button>`** - It is an element that allows the user to perform an action when clicked.

**Textbox `<input>`** - This element allows the user to type text into a box on the browser screen. It’s used to collect small text items like name, city etc.

**Textarea `<textarea>`** - This allows the user to input larger quantities of text. It is bigger in size than the textbox. It’s used for larger text items like address, comments etc.

**Option Select `<select>`** - This element allows the user to select between several available options. It’s basically a drop-down box.

**Date Input `<input type="date">`** - This elements allows the user to choose a date from a calendar drop down.

Now, let’s go through each of these examples through a sample form below.

# Sample Form

```
```html
<html>
<head><title>Sample Form</title></head>
<body>
<form id="form1">
Enter First Name:<input name="firstname" type="text" id="firstname" size="20"><br>
Enter Last Name:<input name="lname" type="text" id="lname" size="20"><br><br>
Enter Address:<textarea name="TextBox" cols="40" rows="5" id="txtbox"></textarea><br><br>
Enter Country: <select id="country" name="country">
               <option value="USA">USA</option>
               <option value="Mexico">Mexico</option>
               <option value="Canada">Canada</option>
               <option value="Australia">Australia</option>
               </select>
Date of Birth: <input type="date" id="start" name="trip-start"
value="2020-07-02"
min="1918-01-01" max="2020-06-31"><br>
<button onclick="">Submit</button>
</form>
</body>
</html>
```
```

Now, let’s go through each part of the code.