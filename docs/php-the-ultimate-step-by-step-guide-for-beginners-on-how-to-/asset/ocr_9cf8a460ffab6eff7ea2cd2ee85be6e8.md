# 3.1 Editing Data

We should now try altering our information and to do that we will need to utilize another function called “GET”. With our past routines, we have been utilizing POST as our http request but this time we will utilize GET for altering and erasing records. To begin with, we should change our home.php and add a little code to 2 segments:

home.php

![](bbox=[0.278, 0.271, 0.721, 0.477])

CODE ABOVE:

```
<html>
<head>
<title>My first PHP Website</title>
</head>
<?php
session_start(); //starts the session

if($_SESSION['user']){ // checks if the user is logged in
}
else{
header("location: index.php"); // redirects if user is not logged in
}

$user = $_SESSION['user']; //assigns user value
?>
```