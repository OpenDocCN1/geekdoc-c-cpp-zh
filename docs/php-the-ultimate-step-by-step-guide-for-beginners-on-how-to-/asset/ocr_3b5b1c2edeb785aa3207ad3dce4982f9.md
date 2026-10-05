# CHAPTER 3: DISPLAYING DATA IN THE HOME PAGE

Since we have seen that the information has been effectively included, we should now show the information in our landing page. We should change our home.php and how about we include a few sections for the date?

home.php

![](bbox=[0.256, 0.266, 0.743, 0.488])

```
<html>
<head>
<title>My first PHP Website</title>
</head>

<?php
session_start(); // starts the session

if($_SESSION['user']) { // checks if the user is logged in
}
else{
header("location: index.php"); // redirects if user is not logged in
}
$user = $_SESSION['user']; // assigns user value
?>
```