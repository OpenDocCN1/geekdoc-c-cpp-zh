
deliver more steady records. While stricter lapse checking may sound like a weight, the proposal for programs to post an lapse as opposed to endeavor to render mistakenly shaped substance ought to dispose of the issue by driving creators to redress their errors.

## 14.2 XHTML and XML Namespaces

XML is fantastically nonexclusive. It characterizes punctuation and fundamental structure, however it does not specify much about queries, for example, what elements ought to be named. This makes a issue: Title in one connection may mean something completely different than in another. The Namespaces in XML specification (which can be found at http://www.w3.org/TR/xml-names/) gives a system that designers can use to identify specific vocabularies utilizing Resource Identifiers (URIs). URIs are a blend of well known Resource Locators (URLs) and Resource Names (URNs). From the point of view of XML namespaces, URIs are helpful on the grounds that they join effortlessly with possession. The W3C claims names that begin with so bodes well for them to utilize those as identifiers. In plain XHTML with no vocabularies blended in, the namespace is announced on the html component utilizing the XHTML property. Example:

```html
<html xmlns="http://www.w3.org/1999/xhtml">
```

The namespace URI http://www.w3.org/1999/xhtml now applies to the html component itself and to any elements as they don't have their own attributes or names that begin with a prefix.

## 14.3 XHTML Versions

Since its beginning, the XHTML standard has been evolving. There are three noteworthy forms used today:

### XHTML 1.0

XHTML 1.0 has the same contents as HTML 4.0, however it needs the use of XML syntax.

### XHTML 1.1

XHTML 1.1 is a reformatted form of 1.0. It is strict since it utilizes an arrangement of elements from a bigger set. This is a W3C suggestion that gives structure, elements that have standard attributes and various definitions that need to conform to the XHTML environment. Any elements of HTML, for example, presentational elements and framesets, have been expelled from this variant. All presentation is controlled by Cascading Style Sheets (CSS). Moreover, 1.1 includes markup support, which is required for Asian dialects.

## 14.4 Creating XHTML with PHP

Producing XHTML from your PHP code is not any difficult than making old HTML (see Example 14.4).

Example 14.4. Making a XHTML record from PHP

```php
<?php
// Ask the program if it thinks about application/xhtml+xml
// This is necessary as a result of
if(strstr($_SERVER["HTTP_ACCEPT"], "application/xhtml+xml")) {
  header('Content-Type: application/xhtml+xml; charset=utf-8');
} else {
  header('Content-Type: text/html; charset=utf-8');
}
// Create the doctype
$doctype = '<?xml version="1.0" encoding="UTF-8"?>
$doctype .= '<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN">';
$doctype .= 'http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">';
// Create the header
$head = '<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">';
$head .= "<head>";
$head .= "<title>Document Example</title>";
$head .= "</head>";
// Create the body content
$body = "<body>";
$body .= " <p>The substance of the page goes here.</p>";
$body .= "</body>";
```

```php
// Create the footer content
$footer = '</html>';
// Display it all together
echo $doctype;
echo $head;
echo $body;
echo $footer;
?>
```

Because we've secured XHTML, which enhances standard HTML and the compatibility of your site, we're prepared to proceed onward to concepts that start to blend PHP and MySQL procedures together. In the following chapter, we'll discuss modifying database objects and information in MySQL from within PHP. We'll also learn how to make dynamic HTML pages that perform actions on specific data from the database.

# CHAPTER 15: MODIFYING MYSQL OBJECTS AND PHP DATA

## 15.1 Changing Database Objects from PHP

The SQL query string remains the basic apparatus for giving database commands. You can simply create and modify database objects with standard SQL that is called the same way you execute queries. Some of the time you'll need to create database objects from within PHP. We'll start with making a table, which is an example of making objects.

## 15.2 Manipulating Table Data

We've previously made the books and authors tables, but we haven't made the buyers table. We'll make one using the PHP shown as a part of Example 15.1.

Example 15.1. Making a table from a PHP page in create_table.php

```php
<?php
include('db_login.php');
require_once('DB.php');

$connection = DB::connect(
  "mysql://$db_username:$db_password@$db_host/$db_database");
if (!$connection) {
  die("Could not interface with the database: " . DB::error_message());
}

$query = 'CREATE TABLE buys (
  purchase_id int(11) NOT NULL AUTO_INCREMENT,
  firstname varchar(50) NOT NULL,
  lastname varchar(50) NOT NULL,
  amount decimal(10,2) NOT NULL,
  PRIMARY KEY (purchase_id)
) ENGINE=InnoDB';

$result = $connection->query($query);
if (DB::isError($result)) {
  die("Could not query the database: " . DB::error_message());
}

echo "Table created successfully!";
?>
```

## Dropping a Table

To drop the table you created from above, use the following code.

Example 15.2. Dropping the buyers table in drop.php

```php
<?php
require_once('db_login.php');
require_once('DB.php');

$connection = DB::connect(
  "mysql://$db_username:$db_password@$db_host/$db_database");

if (!$connection) {
  die("Could not interface with the database: " . DB::error_message());
}

$query = "DROP TABLE buys";

$result = $connection->query($query);
if (DB::isError($result)) {
  die("Could not query the database: " . DB::error_message());
}

echo "Table dropped effectively!";

$connection->disconnect();
?>
```

Since you've worked on executing a couple SQL commands that control database objects, you're prepared to work with the data in your tables. Actually, you'll have to add rows to your tables because you're embedding new data.

## Adding Data

To add a buy to your new buyers table, you'll use an INSERT statement in your query. Illustration 15.3 shows how this is done. Feel free to run example 15.1 again so you have a table in which to insert the information.

Example 15.3. Using a predefined INSERT statement as a part of insert.php

```php
<?php
require_once('db_login.php');
require_once('DB.php');

$connection = DB::connect(
  "mysql://$db_username:$db_password@$db_host/$db_database");

if (!$connection) {
  die("Could not interface with the database: " . DB::error_message());
}

$query = "INSERT INTO buys VALUES (NULL,'mdavis',2,NULL);";

$result = $connection->query($query);

if (DB::isError($result)) {
  die("Could not query the database: " . DB::error_message());
}

echo "Embedded effectively!";

$connection->disconnect();
?>
```
