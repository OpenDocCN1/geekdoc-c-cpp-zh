
# Home Page

```html
<body>

<h2>Home Page</h2>

<hello>!
<!--Display's user name-->
<a href="logout.php">Click here to go logout</a><br><br>
<form action="add.php" method="POST">
Add more to list: <input type="text" name="details" /><br>
Public post? <input type="checkbox" name="public[]" value="yes" /><br>
<input type="submit" value="Add to list"/>
</form>
<h2 align="center">My list</h2>
;

Print "";

Print "";

Print "";

Print "";

Print "";

Print "";

Print "";

Print "";
}
?>
As you have seen, we just included URL parameter for the alter and erase interfaces to be for a specific ID. We will be utilizing this later to handle the information. The motivation behind why we use ID is on the entered that it's an exceptional identifier. It is possible for the individual to have entered the same information so it's not advisable to utilize the details as a method of control later.

Try putting your cursor into the edit link and you will see the estimation of the ID on the lower left:

![](img/8e0a31fe30a159a13fdfed13405b5ed7_34_0.png)

<br/> Enter new detail: <input type="text" name="details"/><br> open post? <input type="checkbox" name="public[]" value="yes"/><input type="submit" value="Update List/></form>'; ' } else <h2 align="center">There is not information to be edited.</h2> } ?></body></html> Click here for the complete edit.php code (Only allude to the front-end code.

```html
<html>
<head>
<title>My first PHP Website</title>
</head>
<?php
session_start(); //starts the session

if($_SESSION['user']){ // checks if the user is logged in
}
else{
header("location:index.php"); // redirects if user is not logged in
}
$user = $_SESSION['user']; //assigns user value
?>
<body>
<h2>Home Page</h2>
<hello>!?
```

<!--Display's user name-->
<a href="logout.php">Click here to go logout</a><br><br>
<a href="home.php">Return to home page</a></a>

## Currently Selected

```php
{
while($row = mysql_fetch_array($query))
{
```

Some explanations to the code:
- `!empty()` - a method that checks if the value is not empty. The syntax can be reversed if you want to check if it's empty by removing the explanation point (!), therefore it's syntax would be empty().
- `$_GET['id']` - Used to get the value from the parameter. In our case, we use id as our URL parameter so the syntax would be `$_GET['id']`.
- `$id_exists` - the variable that checks whether the given id exists.
- `$_SESSION['id']` - we place the value of id into session to use it on another page.

Lines 42-76

![](img/8e0a31fe30a159a13fdfed13405b5ed7_35_0.png)

How about we attempt adjusting the URL parameter by getting rid of id=1. This should result to localhost/MyFirstWebsite/edit.php and it ought to result like this:
edit.php?id=1

![](img/8e0a31fe30a159a13fdfed13405b5ed7_36_0.png)

Go ahead and click Update list and you should be redirected to home.php and see the updated list.

![](img/8e0a31fe30a159a13fdfed13405b5ed7_36_1.png)

Since we secured our URL parameters, lets now put the alter syntax. We should backpedal to edit.php and add some complementary code to restore the data to the database:

Congrats! We have now done the edit function!

## 3.2 Deleting data

Taking back to CRUD, we have now done creating (adding), reading (displaying), and updating (editing) records. At this point, the last part is erasing records. For this part, it's generally the same as what we have done on edit, however, what varies is only the SQL statement. Rather than utilizing UPDATE, we will be utilizing DELETE syntax. In erasing records, we need to prompt individuals that they truly need to erase the record so we will including a little JavaScript in home.php. To do that, we should alter our code and include some.

home.php
![](img/8e0a31fe30a159a13fdfed13405b5ed7_37_0.png)

CODE ABOVE:
<table border="1px" width="100%">
| Id | Details | Post Time | Edit Time | Delete | Public Post |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Print $row['id'] | | | | | |
</table>

```php
Print $row['details']
```

As you have seen, we altered the link for delete. We changed href into "#" and included onclick for JavaScript and inside it's parameter is the id of the row. Below the table is the JavaScript syntax wherein it prompts the user on chance he/she needs to erase the record. In the client side, the page then connects to delete.php with the value of the id. Next, let us make delete.php and here's the syntax:

## Delete.php

![](img/8e0a31fe30a159a13fdfed13405b5ed7_39_0.png)

CODE ABOVE:
```php
<?php
session_start(); //starts the session

if($_SESSION['user']){ //checks if user is logged in
}
else {
header("location:index.php"); //redirects if user is not logged in
}

if($_SERVER['REQUEST_METHOD'] == "GET")
{
mysql_connect("localhost", "root", "") or die(mysql_error()); //connect to server
mysql_select_db("first_db") or die("cannot connect to database");

$id = $_GET['id'];
mysql_query("DELETE FROM list WHERE id='$id");

header("location:home.php");
}
?>
```

The code is simply straightforward and the syntax is as well as the ones that we utilized although you may notice we have changed our request technique into GET. At this stage, we are utilizing the GET request. Now try refreshing home.php and let us attempt erasing the record. This ought to be the outcome:

## Prompting

Congrats! At this point we have finished our CRUD operations!

## 3.3 Displaying public data

Subsequently, let us see how public information should play. We will be showing information that has been set to yes in our index.php, which is a page for non-authenticated users. It's exceptionally simple. We simply need to alter our index.php and include some PHP code and table. Here's our upgraded index.php:

index.php
![](img/8e0a31fe30a159a13fdfed13405b5ed7_41_0.png)

Now log-out and see your default page. It should look something like this:

![](img/8e0a31fe30a159a13fdfed13405b5ed7_41_1.png)

Note: You won't see the data yet since we haven't set any information to public.

Now let's log-in again and this time, let's add some more data. In my case I've added the following:
- Salad - public
- Corn - non-public
- Pasta - public
- Chicken - public
- Spaghetti - non-public

With a total of 6 data with 3 of each privacy setting:

home.php
![](img/8e0a31fe30a159a13fdfed13405b5ed7_42_0.png)

Now let’s log-out and see our default page (index.php). It should now look like this:

index.php
![](img/8e0a31fe30a159a13fdfed13405b5ed7_42_1.png)

As you can see, it only displays data that are set to public.

# CHAPTER 4: DYNAMIC CONTENT AND THE WEB

To the normal client, a web page is simply just a web page. It opens in the browser and gives information. Looking closer, however, various pages stay for the most part same, while other pages change routinely. Pages that don't change—static pages—are generally simple to make. Somebody needs to make an HTML document, by hand or with apparatuses/tools, and transfer it to a website where browsers can visit. A standout amongst the most well-known instruments to make HTML docs is Adobe Dreamweaver. At the point when changes are required, you simply supplant the old file with another one. Dynamic pages are made with HTML as well, although, rather than a basic and-post approach, the pages are upgraded routinely, even sometimes every time that they are asked.
