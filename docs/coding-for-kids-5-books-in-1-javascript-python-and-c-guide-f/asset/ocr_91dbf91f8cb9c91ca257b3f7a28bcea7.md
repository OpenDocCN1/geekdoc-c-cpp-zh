# Breaking down the code:

```
    <form id="form1">
    Enter Name: <input name="Enter Name" type="text" id="name" size="20"><br>
    Enter Favorite Hobby: <input type="text" id="hobby" size="20"><br>
    Enter Age: <input type="number" id="age" size="20"><br>
    </form>
```

The html code creates a form with 3 form elements for name, hobby and age. They all have a length of 20 pixels. They are referenced by ids; with id’s of **name**, **hobby** and **age**.

```
    <button onclick="writename()">Print Intro</button>
```

This html buttons activates the JavaScript function called **writename()** and the text on the button is **Print Intro**.

```
    function writename()
    {
        var nameValue=document.getElementById("name").value;
        var hobbyValue=document.getElementById("hobby").value;
        var ageValue=document.getElementById("age").value;
        document.write("This is "+nameValue+". I am "+ ageValue+" years old. My favorite hobby is "+hobbyValue);
    }
```

The above Javascript code is activated when the button is pressed. **nameValue**, **hobbyValue** and **ageValue** store the values of stuff that is typed into the form elements with id **“name”**, **“hobby”** and **“age”**. **document.write** writes out the intro on the screen.