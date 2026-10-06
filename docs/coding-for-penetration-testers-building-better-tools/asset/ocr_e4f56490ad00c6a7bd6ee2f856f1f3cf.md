visit the PHP function reference for file system commands at www.php.php/manual/en/ref.filesystem.php.

```
<?php
if(\$_GET['read'])
{
  $file = $_GET['read'];
  if(file_exists($file) and is_file($file))
{
    $f = fopen($file,"r");
    print "<PRE>File contents are:\n";
    $out = "
    while($data = fread($f,1024))
{
      $out .= $data;
    }
    fclose($f);
    print $out;
  }
}
```

We segment the code into two sections. If the read GET variable is set, we set the $file variable to the value of the read key in the $_GET array. If the file exists, we open the file for reading with the fopen function. We specify that the file is read by setting the mode to r, as we have in Perl and Python. The fopen function returns a file handle which we set to $f. The file handle is what we will use to reference this file from now on. We initialize an $out variable, which will be used to store our output. To read the whole file, we create a while loop that will read data from our file, up to 1024 characters at a time. After each iteration, we append the data to our out variable using the concatenation operator, which sets $out to the value of $out plus $data. Once we run out of data, the loop stops. We close our file and print the output to the screen.

```
if(\$_GET['write'] && \$_GET['data'])
{
  $file = \$_GET['write'];
  $data = \$_GET['data'];
  $f = fopen($file,"a+");
  fwrite($f,$data . "\n");
  fclose($f)
```