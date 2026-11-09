
![](img/5a907eb39993e80f28c82efc2e4632b3_159_0.png)

For a list of additional string and number methods see W3Schools www.w3schools.com/js/js_number_methods.asp and www.w3schools.com/js/js_string_methods.asp.

## Alerting users and prompting them for input

Displaying messages to the user and collecting input are the beginnings of the interactivity that JavaScript provides. Although more sophisticated techniques exist today, the `alert()` method and `prompt()` method are easy ways to show a pop-up box with a message, and prompt the user for input.

The syntax for creating an alert or a prompt is to write the method with text in quotes placed inside the parentheses like so:

```
alert("You have mail!");
prompt("What do you want for dinner?");
```

Figure 9-6 shows the alert pop-up box created by the `alert()` method, and the prompt for user input created by the `prompt()` method.

![](img/5a907eb39993e80f28c82efc2e4632b3_159_1.png)

**Figure 9-6:** A JavaScript alert pop-up box and a user prompt.

## Naming code with functions

Functions are a way of grouping JavaScript statements, and naming that group of statements for easy reference with a function name. These statements are typically grouped together because they achieve a specific coding goal. You can use the statements repeatedly by just writing the function name instead of having to write the statements over and over again. Functions prevent repetition and make your code easier to maintain.

When I was younger every Saturday morning my mother would tell me to brush my teeth, fold the laundry, vacuum my room, and mow the lawn. Eventually, my mother tired of repeating the same list over and over again, wrote the list of chores on paper, titled it “Saturday chores,” and put it on the fridge. A function names a group of statements, just like “Saturday chores” was the name for my list of chores.

Functions are defined once using the word `function`, followed by a function name, and then a set of statements inside curly brackets. This is called a *function declaration*. The statements in the function are executed only when the function is called by name. In the following example, I have declared a function called `greeting` that asks for your name using the `prompt()` method, returns the name you entered storing it in a variable called `name`, and displays a message with the name variable using the `alert()` method:

```javascript
function greeting() {
    var name=prompt("What is your name?");
    alert("Welcome to this website " + name);
}

greeting();
greeting();
```

Beneath the function declaration, I have called the function twice, and so I will trigger two prompts for my name, which are stored in the variable name, and two messages welcoming the value in the variable name to this website.

![](img/5a907eb39993e80f28c82efc2e4632b3_160_0.png)

The “+” operator is used to concatenate (combine) strings with other strings, values, or variables.

Functions can take inputs, called *parameters*, to help the function run, and can return a value when the function is complete. After writing my list of chores, each Saturday morning my mother would say “Nik, do the Saturday chores,” and when my brother was old enough she would say “Neel, do the Saturday chores.” If the list of chores is the function declaration, and “Saturday chores” is the function name, then “Nik” and “Neel” are the parameters. Finally, after I was finished, I would let my mom know the chores were complete, much as a function returns values.

In the following example, I have declared a function called `amountdue`, which takes `price` and `quantity` as parameters. The function, when called, calculates the subtotal, adds the tax due, and then returns the total. The function `amountdue(10,3)` returns 31.05.

```javascript
function amountdue(price, quantity) {
    var subtotal=price * quantity;

    var tax = 1.05;
    var total = subtotal + tax;
    return total;
}

alert("The amount due is $" + amountdue(10,3));
```

![](img/5a907eb39993e80f28c82efc2e4632b3_160_1.png)

Every opening parenthesis has a closing parenthesis, every opening curly bracket has a closing curly bracket, and every opening double quote has a closing double quote. Can you find all the opening and closing pairs in the example above?

## Adding JavaScript to the web page

The two ways to add JavaScript to the web page are:

- Embed JavaScript code in an HTML file using the script tag.
- Link to a separate JavaScript file from the HTML file using the script tag.

To embed JavaScript code in an HTML file, use an opening and closing `<script>` tag, and write your JavaScript statements between the two tags, as shown in the following example:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Embedded JavaScript</title>
    <script>
      alert("This is embedded JavaScript");
    </script>
  </head>
  <body>
    <h1>Example of embedded JavaScript</h1>
  </body>
</html>
```

The `<script>` tag can be placed inside the opening and closing `<head>` tag, as shown above, or inside the opening and closing `<body>` tag. There are some performance advantages when choosing one approach over the other, and you can read more at http://stackoverflow.com/questions/436411/where-is-the-best-place-to-put-script-tags-in-html-markup.

The `<script>` tag is also used when linking to a separate JavaScript file, which is the recommended approach. The `<script>` tag includes:

- A `type` attribute, which for JavaScript is always set equal to `"text/javascript"`.
- A `src` attribute, which is set equal to the location of the JavaScript file.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Linking to a separate JavaScript file</title>
    <script type="text/javascript" src="script.js"></script>
  </head>
  <body>
    <h1>Linking to a separate JavaScript file</h1>
  </body>
</html>
```

![](img/5a907eb39993e80f28c82efc2e4632b3_162_0.png)

The `<script>` tag has an opening and closing tag, whether the code is embedded between the tags or linked to a separate file using the `src` attribute.

## Writing Your First JavaScript Program

Practice your JavaScript online using the Codecademy website. Codecademy is a free website created in 2011 to allow anyone to learn how to code right in the browser, without installing or downloading any software. Practice all of the tags (and a few more) that you learned in this chapter by following these steps:

- 1. **Open your browser, go to** `www.dummies.com/go/codingfd`, **and click on the link to Codecademy.**
- 2. **Sign in to your Codecademy account.** Signing up is discussed in Chapter 3. Creating an account allows you to save your progress as you work, but it’s optional.
- 3. **Navigate to and click on Getting Started with Programming.**
- 4. **Background information is presented in the upper left portion of the site, and instructions are presented in the lower left portion of the site.**
- 5. **Complete the instructions in the main coding window.**
- 6. **After you have finished completing the instructions, click the Save and Submit Code button.**

If you have followed the instructions correctly, a green checkmark appears and you proceed to the next exercise. If an error exists in your code a warning appears with a suggested fix. If you run into a problem, or have a bug you cannot fix, click on the link, use the Q&A Forums, or tweet me at @nikhilgabraham and include hashtag #codingFD.

## Working with APIs

Although APIs (*application programming interfaces*) have existed for decades, the term has become popular over the last few years as we hear more conversation and promotion around their use. *Use the Facebook API! Why doesn't Craigslist have an API?* Stripe's entire business is to allow developers to accept payments online using its payments API.

Many people use the term API, but few understand its meaning. This section will help clarify what APIs do and how they can be used.

## What do APIs do?

An API allows Program A to access select functions of another separate Program B. Program B grants access by allowing Program A to make a data request in a structured, predictable, documented way, and Program B responds to this data request with a structured, predictable, documented response, as follows (see Figure 9-7):

- **It’s structured** because the fields in the request and the data in the response follow an easy-to-read standardized format. For example, the Yahoo Weather API data response includes these selected structured data fields:

```json
"location": {
    "city": "New York",
    "region": "NY"
},
"units": {
    "temperature": "F"
},
"forecast": [
    {
        "date": "29 Oct 2014",
        "high": "68",
        "low": "48",
        "text": "PM Showers"
    }
]
```

See the full Yahoo Weather API response by visiting `http://developer.yahoo.com/weather/`.

- **It’s predictable** because the fields that must be included and can be included in the request are pre-specified, and the response to a successful request will always include the same field types.

- **It’s documented** because the API is explained in detail. Any changes usually are communicated through the website, social media, email, and even after the API changes, there is often a period of backward compatibility when the old API requests will receive a response. For example, when Google Maps issued version 3 of their API, version 2 still operated for a certain grace period.

![](img/5a907eb39993e80f28c82efc2e4632b3_163_0.png)

**Figure 9-7:** An API allows two separate programs to talk to each other.
