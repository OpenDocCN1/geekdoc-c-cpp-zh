```
echo "Meow...";
}
/The cat eats
function eat() {
echo "*eats*";
}
/The cat purrs
function purr() {
echo "*Purr...*";
}
}
```

/Assign the new Cat object reference $myCat
$myCat=new Cat;
\?>

# Variable Scope Within Classes

Classes may contain variables that help in defining their structure and how they are used. Variables inside a class are declared with the var statement. The var statement announces a variable to have class scope. Class scope means they're instantly recognizable with any techniques for the class and can be referenced outside the class utilizing a special construct. Example 7.15 adds the $age variable to the Cat.

Illustration 5-15. Adding the $age variable to Cat

```
<?php
class Cat {
/How old the cat is
var $age;
/PHP 5 uses:
/public $age;
```