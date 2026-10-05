# 0.3 Adding users to the database

Since we have our tables, we should proceed to the fun part, getting your enlistment page usable. From your registration.php, include the html codes add-on below:

register.php

![](bbox=[0.298, 0.215, 0.702, 0.375])

Here’s the amplification to the code:

```
<html>
<head>
<title>My first PHP Website</title>
</head>
<body>
<h2>Registration Page</h2>
<a href="index.php">Click here to go back</a><br/>
<form action="checklogin.php" method="POST">
Enter Username: <input type="text" name="username" required="required" /><br>
Enterter password: <input type="password" name="password" required="required" /><br>
<input type="submit" value="Register"/>
</form>
</body>
</html>
```