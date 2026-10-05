# 13.3 File Manipulation

Since you know a document exists, you may believe you're done, yet you're most certainly not. Just since the record there doesn't mean you can read, compose, or execute it. To check for these properties, is_readable to check for read access, is_writable to check for compose access, and is_executable to check for the capacity to execute the document. Every function takes a filename as its parameter. Unless you know the record is in the same catalog as your script, you must specify a full way to the record in the filename. You can use connecting to put the way and filename together, as in:

$file_name = $path_to_file . $file_name_only;

URL Wrappers

Two URL conventions that PHP has constructed in for utilization with the file system functions incorporate open and duplicate. Notwithstanding these two wrappers, as of PHP 4:3.0, you can compose your own wrappers utilizing a PHP script and stream_wrapper_register. The default wrapper is record://, utilized with PHP, and it is the nearby filesystem. If you specify a relative way, which is one that doesn't start with/, \, or a Windows drive letter, for example, C://, the way gave applies against the present working index.

Generally this is the place the script lives, unless obviously it's been changed. With a few functions, for example, fopen and file_get_contents, include_path can be used to hunt down relative ways too.