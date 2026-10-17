+   3. Under “Run Configuration”, from the “Run As” dropdown list, select “Script (run in command line)” as shown in **Figure 9–4**.

![](bbox=[0.044, 0.101, 0.981, 0.327])

**Figure 9–4** Selecting the configuration settings for a new PHP project

+   4. Click on the “Finish” button.

The project is created and opened in your NetBeans IDE. You should see the following components (see **Figure 9–5**):

+   ➢ the Projects window, which contains a tree view of the components of the projects, including source files, libraries that your code may depend on, and so on
+   
+   ➢ the Source Editor window with a file called “index.php” open. In this file you can write your PHP code. Of course, one single project can contain many such files.

![](bbox=[0.044, 0.56, 0.981, 0.822])

**Figure 9–5** Viewing the “Projects” and “Source Editor” windows in NetBeans IDE

# 9.2    Writing and Executing a PHP Script

You have just seen how to create a new PHP project. Let’s now write the following (terrifying, and quite horrifying!) PHP script and try to execute it.

```
```php
<?php
echo "Hello World";
```
```