![](Images/cover00476.jpeg)

# PERL PROGRAMMING

# ![](Images/image00427.jpeg)<map name="awmap1"><area shape="rect" href="http://www.pudhiyadesambook.blogspot.com" coords="244, 676, 535, 693"></map>

# UNIT- I INTRODUCTION TO PERL

1.  INTRODUCTION TO PERL AND DATA  TYPES

Scalars are simple variables. They are preceded by a dollar sign ($). A scalar is either a number, a string, or a reference. A reference is actually an address of a variable, which we will see in the upcoming  chapters.

Arrays are ordered lists of scalars that you access with a numeric index which starts with 0\. They are preceded by an "at" sign (@).

Hashes are unordered sets of key/value pairs that you access using the keys as subscripts. They are preceded by a percent sign (%).

![](Images/image00428.jpeg)

# 2. Constructing  atgc.pl

![](Images/image00429.jpeg)

![](Images/image00430.jpeg)

3.  ~tr///  function

This is not a function. This is the transliteration operator; it replaces all occurrences of the characters in SEARCHLIST with the characters in REPLACEMENTLIST.

Syntax tr/SEARCHLIST/REPLACEMENTLIST/

Return Value

This function returns number of characters replaced or deleted. Example

Following is the example code showing its basic usage − #!/usr/bin/perl -w

$string = 'the cat sat on the mat.';

$string =~ tr/a-z/b/d;

print "$string\n";

When above code is executed, it produces the following result. Here option d is used to delete

![](Images/image00428.jpeg)

matched characters.

# 4. ~s/// function

Description

This is not a function. This is the regular expression-substitution operator. Based on the regular expression specified in PATTERN, data is replaced by REPLACE. Like m//, the delimiters are defined by the first character following s.

Syntax

s/PATTERN/REPLACE/

Return Value

This function returns 0 on failure and number of substitutions made on success. Example

Following is the example code showing its basic usage − #!/usr/bin/perl -w

$string = "This is Test";

# this will replcase Test with Best.

$string =~ s/Test/Best/;

print "$string\n";

When above code is executed, it produces the following result − This is Best

![](Images/image00428.jpeg)

5.  Formatting Numerical Output With Printf  function

![](Images/image00428.jpeg)

![](Images/image00428.jpeg)

![](Images/image00431.jpeg)

# 6. Chop and Chomp operators

![](Images/image00428.jpeg)

![](Images/image00432.jpeg)

![](Images/image00428.jpeg)

7.  THE COMMON GATEWAY INTERFACE(CGI) - Introduction and  Applications

The common gateway interface (CGI) is a standard way for a Web server to pass a Web user's request to an application program and to receive data back to forward to the user. When the user requests a Web page (for example, by clicking on a highlighted word or entering a Web site address), the server sends back the requested page. However, when a user fills out a form on a Web page and sends it in, it usually needs to be processed by an application program. The Web server typically passes the form information to a small application program that processes the data and may send back a confirmation message. This method or convention for passing data back and forth between the server and the application is called the common gateway interface (CGI). It is part of the Web's Hypertext Transfer Protocol (HTTP).

If you are creating a Web site and want a CGI application to get control, you specify the name of the application in the uniform resource locator (URL) that you code in an HTML file. This URL can be specified as part of the FORMS tags if you are creating a form. For example, you might code:

![](Images/image00428.jpeg)

<FORM METHOD=POST ACTION=[http://www.mybiz.com/cgi-bin/formprog.pl>](http://www.mybiz.com/cgi-bin/formprog.pl)

and the server at "mybiz.com" would pass control to the CGI application called "formprog.pl" to record the entered data and return a confirmation message. (The ".pl" indicates a program written in PERL but other languages could have been used.)

The common gateway interface provides a consistent way for data to be passed from the user's request to the application program and back to the user. This means that the person who writes the application program can makes sure it gets used no matter which operating system the server

uses (PC, Macintosh, UNIX, OS/390, or others). It's simply a basic way for information to be passed from the Web server about your request to the application program and back again.

The importance of CGI lies in the fact that its flexibility has made it a standard for running Executable files from Web servers. This standard allows for true interactivity, in endless ways, on Web sites.

![](Images/image00428.jpeg)

![](Images/image00433.jpeg)![](Images/image00434.jpeg)

# The limitation and problems of CGI

Problems:

![](Images/image00428.jpeg)

Performance Every time a user requests a CGI script, the server must launch the CGI program, which takes processor time.

*   When the CGI program is written in an interpreted language like Perl, then the program must run the entire Perl interpreter, and compile the program before it can be run, which takes even more processor  time.
*   For busy web sites running complex applications, the performance problems become critical  issue.
    *   It is free. --> not easy to sell the web server products with free  software.
    *   Not good to interact with database.(connecting  issue)

*   Not flexible or powerful to generate dynamic HTML  pages.

# Advantages and applications of CGI:

Platform independence: Most web servers support CGI, including

Unix: Apache, Netscape, NCSA, and CERN

Windows NT: Netscape, Microsoft IIS, and O’Reilly WebSite

Macintosh: WebStar

Language independence: (Perl, TCL, C, C++ Visual Basic, AppletScript, Java)

Scalability: The simplicity of the CGI interface means that it is extremely scalable.

![](Images/image00428.jpeg)An example of a CGI program is one implementing a Wiki. The user agent requests the name of an entry; the Web server executes the CGI; the CGI program retrieves the source of that entry's page (if one exists), transforms it into [HTML,](http://en.wikipedia.org/wiki/HTML) and prints the result. The web server receives the input from the CGI and transmits it to the user agent. If the "Edit this page" link is clicked, the CGI populates an HTML textarea or other editing control with the page's contents, and saves it

back to the server when the user submits the form.

Calling a command generally means the invocation of a newly created [process](http://en.wikipedia.org/wiki/Process_%28computing%29) on the server. Starting the process can consume much more time and memory than the actual work of generating the output, especially when the program still needs to be [interpreted](http://en.wikipedia.org/wiki/Interpret) or [compiled.](http://en.wikipedia.org/wiki/Compiler) If the command is called often, the resulting workload can quickly overwhelm the server.

****

![](Images/image00428.jpeg)

Unit-II

1.  Introduction to arrays and Hashes

Arrays

While we often work with single variables, it's sometimes useful to work with collections of variables. For this, Perl offers two options: arrays and hashes. Arrays are the simplest kind of collection, so we will start with them.

For example, let's say you want to test all possible output of the 'Hello' program. Of course, you could just run it three times, manually changing the value of the $status variable each time. But you could also use an array containing all the possible values of the status variable ('leaving', 'arriving', and 'other') and iterate through the array.

First, define the array like this:

@status = ("leaving", "arriving", "staying", "whatever");

Note that instead of a $ sign, arrays are preceded by an @ sign.

So now you could add something like the following to your hello program:

@status = ("leaving", "arriving", "staying", "whatever"); foreach $status (@status) {

if ($status eq "leaving") {

$greeting = "Goodbye";

}

elsif ($status eq "arriving") {

$greeting = "Hello";

}

else {

$greeting  ="Nice day if it don't  rain";

}

print $greeting . "\n";

}

print "All done.";

This illustrates a couple of things. First, it illustrates how to iterate through an array using the foreach statement. foreach means something like: "For each element in the array, do whatever is between the beginning and ending curly braces."

And it also illustrates a loop structure, so called because when the program gets to the bottom of the foreach loop (the last curly brace) it returns to the top again for as long as there are more values in the array. Once all the values in the array have been used, the loop terminates. If there were additional instructions after the loop, the program would continue on from there.

Notice that the 'print $greeting' instruction now has a dot and a \n (in quotes) before the semicolon. The \n is a newline character. It tells the interpreter to print a carriage return after the greeting. If it was not there, the greetings would all run together on the same line. The dot (in this context) is called a concatenation operator. It joins the carriage return with the $greeting variable immediately preceding it. You could also achieve the same thing by putting the whole thing between quotes, as in:

print "$greeting\n";

Besides the foreach function, there are a number of ways of getting at the variables contained in an array. Variables can be referred to by number, for example:

@status = ("leaving", "arriving", "staying", "whatever");

$status = $status[1]; print $status;

The output of this simple script might surprise you: it prints 'arriving', the second value in the array. The reason is that arrays start their numbering at zero, not 1\. To reference the first element in              the              array,              you              would              need              to use:

$status = $status[0];

One of the more confusing aspects of perl is that in this context, the array is preceded by a dollar sign. The reason is that $status[0] refers to a single element of the array, so it's really a scalar. This is not perhaps the most intuitive feature of the Perl language.

Hashes

Finally, there is another type of collection, called a hash. This course is not going to delve too deeply into hashes, but briefly, a hash is like an array, except that instead of referring to its elements by their number, in a hash you refer to them by an assigned key.

An example might be:

%names = (

'Durno' => 'John', 'Jordan' => 'Mark', 'Hacker' => 'J.R.'

);

Note that hashes are indicated by the percent sign. To find out the first name of the person named Durno, you could do something like:

$firstName = $names{'Durno'}; print $firstName;

Exercise

Goals: 1) To gain familiarity with conditionals

Instructions: Copy and run the script above that iterates through an array and changes the value of $greeting based on the contents of $status. Then add another elsif condition that changes the value of $greeting to "Set yourself down and rest a while" if the value of $status is  "staying".

Perl records

Perl allows us to create arrays of arrays, arrays of hashes, hashes of arrays, and hashes of hashes. These complex, nested data structures use special variables called "references" to create "records" (and you use "dereferences" to access parts of a record). We will not cover Perl references and records in much detail, but knowing what they are and how to use dereferences to express particular parts of records is useful when we start parsing  XML.

A regular array starts out like this:

@a_list = ();

We can add hashes as the elements in the array. The hashes don't have regular variable names  but are knows as "anonymous"  hashes:

@a_list = (

{ 'key_1' => 'value_1', 'key_2' => 'value_2', 'key_3' => 'value_3' },

{ 'key_4' => 'value_4', 'key_5' => 'value_5', 'key_6' => 'value_6' }

);

To print the value associated with "key_2", we dereference it using s special syntax:

print %{$a_list[0]}->{"key_2"} . "\n";

The result of this print command is "value_2". Some parts of the dereference are easily identifiable: the "$a_list[0]" represents the first item in the @a_list array, and "key_2" is one of the keys in our anonymous hashes. The tricky part is the "%" and the extra curly braces that you must use to indicate the actual dereference.

Don't worry about what these details mean right now, since their exact usage depends on whether you are dereferencing an array, a hash, or even a scalar, and on what context you use them in. The most important thing to note at this point is the use of the "->" to join together hierarchical levels of nested Perl records. We will encounter this type of data structure in a more meaningful context when we start to parse  XML.

Split Function

This function splits a string expression into fields based on the delimiter specified by PATTERN. If no pattern is specified whitespace is the default. An optional limit restricts the number of elements returned.

A negative limit has the same effect as no limit. This function is often used in conjunction with join() to create small text databases.

Syntax

Following is the simple syntax for this function −

split /PATTERN/, EXPR, LIMIT

split /PATTERN/, EXPR

split /PATTERN/ split

Return Value

*   Return Value in Scalar Context: Not recommended, but it returns the number of fields found and stored the fields in the @_  array.
*   Return Value in Array Context: A list of fields found in EXPR or $_ if no expression is specified.

Example

Following is the example code showing its basic usage −

#!/usr/bin/perl -w

@fields = split(/:/, "1:2:3:4:5"); print "Field values are: @fields\n";

When above code is executed, it produces the following result −

Field values are: 1 2 3 4 5

2.  Foreach  Loop

The foreach loop iterates over a list value and sets the control variable (var) to be each element

of the list in turn −

Syntax

The syntax of a foreach loop in Perl programming language is −

foreach var (list) {

...

}

Flow Diagram

![](Images/image00435.jpeg)

Example #!/usr/local/bin/perl

@list = (2, 20, 30, 40, 50);

# foreach loop execution foreach $a (@list){

print "value of a: $a\n";

}

When the above code is executed, it produces the following result −

value of a: 2 value of a: 20 value of a: 30 value of a: 40 value of a: 50

Copying and creating an array

Copying a Perl array is actually so simple it seems like a trick question, but unfortunately it's  one of those things that is only easy once you know how to do it. (Personally I find the syntax a little non-standard.)

A Perl copy array example

To copy a Perl array named @array1 to a Perl array named @array2, just use this syntax: @array2 = @array1;

In other languages that seems more like @array2 is a reference to @array1, but in Perl it's a copy.

To demonstrate that this actually copies the first Perl array, here's a short Perl array copy example script to prove the point:

sub print_arr() { my (@arr) = @_;

foreach $elem (@arr) { print "  $elem\n";

}

}

# create an integer array using the range operator @arr1 = qw/cheese pepperoni veggie/;

@arr2 = @arr1; push @arr1,  'works';

print "array1:\n"; &print_arr(@arr1);

print "\narray2:\n"; &print_arr(@arr2);

Populating arrays with sequential data

Perl offers a shortcut for sequential numbers and letters. Rather than typing out each element

when counting to 100 for example, we can do something like as follows −

#!/usr/bin/perl @var_10 = (1..10);

@var_20 = (10..20);

@var_abc = (a..z);

print "@var_10\n"; # Prints number from 1 to 10 print "@var_20\n"; # Prints number from 10 to 20 print "@var_abc\n"; # Prints number from a to z

Here double dot (..) is called range operator. This will produce the following result −

1 2 3 4 5 6 7 8 9 10

10 11 12 13 14 15 16 17 18 19 20

a b c d e f g h i j k l m n o p q r s t u v w x y z

3.  qw  function

This function is a quick way to specify a lot of little single-quoted words. For example, qw(foo bar baz) is equivalent to ('foo', 'bar', 'baz'). Some programmers feel that using qw make Perl scripts easier to read. You can actually use any set of delimiters, not just the parentheses.

Simply you can use qw() to prepare an array as shown in the example below.

Syntax

Following is the simple syntax for this function −

qw EXPR

Return Value

This function return a list consisting of the element of LIST evaluated as if they were single- quoted.

Example

Following is the example code showing its basic usage −

#!/usr/bin/perl -w

@array = qw(This is a list of words without interpolation); foreach $key (@array){

print"Key is $key\n";

}

When above code is executed, it produces the following result −

Key is This Key is is Key is a Key is list Key is of

Key is words Key is without

Key is interpolation

4.  Determination of the size of an  array

The size of an array can be determined using the scalar context on the array - the returned value

will be the number of elements in the array −

@array = (1,2,3);

print "Size: ",scalar @array,"\n";

The value returned will always be the physical size of the array, not the number of valid elements. You can demonstrate this, and the difference between scalar @array and $#array, using this fragment is as follows −

#!/uer/bin/perl @array = (1,2,3);

$array[50] =  4;

$size =  @array;

$max_index = $#array;

print  "Size:$size\n";

print "Max Index:  $max_index\n";

This will produce the following result  −

Size: 51

Max Index: 50

There are only four elements in the array that contains information, but the array is 51 elements long, with a highest index of 50.

5.  Accessing first and last element of an  array

Shift function

This function returns the first value in an array, deleting it and shifting the elements of the array list to the left by one. If ARRAY is not specified, shifts the @_ array within a subroutine, or @ARGV otherwise. shift is essentially identical to pop, except values are taken from the start of the array instead of the end.

Syntax

Following is the simple syntax for this function −

shift ( [ARRAY] )

shift

Return Value

This function returns undef if the array is empty else returns first element in array.

Example

Following is the example code showing its basic usage −

#!/usr/bin/perl

@array = (1..5);

while ($element = shift(@array)) { print("$element - ");

}

print("The End\n");

When above code is executed, it produces the following result −

1 - 2 - 3 - 4 - 5 - The End

6.  Unshift  function

This function places the elements from LIST, in order, at the beginning of ARRAY. This is opposite function to shift().

Syntax

Following is the simple syntax for this function −

unshift ARRAY, LIST

Return Value

This function returns the number of new elements in ARRAY.

Example

Following is the example code showing its basic usage −

#!/usr/bin/perl -w @array = ( 1, 2, 3, 4);

print "Value of array is @array\n" ; unshift( @array, 20, 30, 40 );

print "Now value of array is @array\n" ;

When above code is executed, it produces the following result −

Value of array is 1 2 3 4

Now value of array is 20 30 40 1 2 3 4

7.  Push  function

This function pushes the values in LIST onto the end of the list ARRAY. Used with pop to implement stacks.

Syntax

Following is the simple syntax for this function −

push ARRAY, LIST

Return Value

This function returns number of elements in new array.

Example

Following is the example code showing its basic usage −

#!/usr/bin/perl -w

$, = ",";

@array = ( 1, 2 );

print "Before pushing elements @array \n"; push(@array, (3, 4, 5));

print "After pushing elements @array \n";

When above code is executed, it produces the following result −

Before pushing elements 1 2

After pushing elements 1 2 3 4 5

8.  Pop  function

This function returns the last element of ARRAY, removing the value from the array. Note that ARRAY must explicitly be an array, not a list.

If ARRAY is omitted, it pops the last value from @ARGV in the main program or when called within eval STRING, or the BEGIN, CHECK, INIT, or END blocks. Otherwise, it attempts to pop information from the @_ array within a subroutine. It is the opposite of push, which when used in combination, allows you to implement "stacks".

Note that after applying pop the array will be shortened by one element.

Syntax

Following is the simple syntax for this function −

pop ARRAY

pop

Return Value

This function returns undef if list is empty else last element from the array.

Example

Following is the example code showing its basic usage −

#!/usr/bin/perl  -w

@a = (1, 2, 3,  4);

print("pop() ", pop(@a), " leaves ",@a, "\n");

When above code is executed, it produces the following result −

pop() 4 leaves 123

9.  Array  Slices

An array is a variable that stores an ordered list of scalar values. Array variables are preceded by an "at" (@) sign. To refer to a single element of an array, you will use the dollar sign ($) with  the variable name followed by the index of the element in square  brackets.

Here is a simple example of using the array variables −

#!/usr/bin/perl

@ages = (25, 30, 40);

@names = ("John Paul", "Lisa", "Kumar");

print "\$ages[0] = $ages[0]\n"; print "\$ages[1] = $ages[1]\n"; print "\$ages[2] = $ages[2]\n"; print "\$names[0] = $names[0]\n"; print "\$names[1] = $names[1]\n"; print "\$names[2] = $names[2]\n";

Here we have used the escape sign (\) before the $ sign just to print it. Other Perl will understand

it as a variable and will print its value. When exected, this will produce the following result −

$ages[0] =  25

$ages[1] =  30

$ages[2] = 40

$names[0] = John Paul

$names[1] = Lisa

$names[2] = Kumar

10.  Splice  Function

This function removes the elements of ARRAY from the element OFFSET for LENGTH elements, replacing the elements removed with LIST, if specified. If LENGTH is omitted, removes everything from OFFSET onwards.

Syntax

Following is the simple syntax for this function −

splice ARRAY, OFFSET, LENGTH, LIST splice ARRAY, OFFSET, LENGTH

splice ARRAY, OFFSET

Return Value

This function returns −

*   In scalar context undef if no elements  removed
*   In scalar context last element  removed
*   In list context empty list on  failure
*   In list context list of elements  removed

Example

Following is the example code showing its basic usage −

#!/usr/bin/perl -w

@array= ("a", "e", "i", "o",  "u");

@removedItems = splice(@array, 0 , 3, ("A", "E", "I"));

print "Removed items: @removedItems\n";

When above code is executed, it produces the following result −

Removed items: a e i

11.  Sorting  Arrays

Perl has a built-in function called sort that can, unsurprisingly, sort an array. In its most simple form, you just give it an array, and it returns the elements of that array in a sorted order. @sorted

= sort @original.

Comparison function

The way sort works in Perl is, that it goes over every two elements of the original array; In every turn it puts the value from the left side into the variable $a, and the value on the right side in the variable $b. Then it calls a comparison function. That "comparison function" will return 1 if the content of $a should be on the left, -1 if the content of $b should be on the left, or 0 if it does not matter as the two values are the same.

By default you don't see this comparison function and sort compares the values according to the ASCII table, but if you want, you can write it explicitly:

1\. sort { $a cmp $b } @words;

This code will provide the exact same result as the one without the block: sort @words.

Here you can see that, by default, perl uses cmp in the comparison function. That's because cmp is doing exactly what we need here. It compares the values on its two sides as strings, returns 1 if the left argument is "less than" the right argument; returns -1 if the left argument is "greater than" the right argument; and returns 0 if they are the same.

Sorting in alphabetical order

If you want to disregard the case in the strings - what is usually called alphabetical order - you can do so as given in the next example:

1. my @sorted_words = sort { lc($a) cmp lc($b) }  @words;

Here, for the sake of comparison, we call the lc function that returns the lower case version of its argument. Then cmp compares those lower case versions and decides which of the original strings must go first and which second.

The result is

1\. $VAR1 = [

2. 'bar',

3. 'foo',

4. 'moo',

5. 'Zorg'

6.];

Sorting numbers in Perl

If we take an array of numbers and sort them with the default sorting, the result is probably not what we are expecting.

1\. my @numbers = (14, 3, 12, 2, 23);

2. my @sorted_numbers = sort  @numbers;

3. say Dumper  \@sorted_numbers; 1\. $VAR1 =  [

2.12,

3.14,

4.2,

5.23,

6.3

7.];

If you think about it, of course, this is not surprising. When the comparison function sees 12 and 3 it compares them as strings. That means comparing the first character in both strings. "1" to "3". "1" is ahead of "3" in the ASCII table and thus the string "12" will come before the string "3".

Perl does not magically understand that you want to order these values as numbers.

No problem though as we can write a comparison function that will compare the two values as numbers. For that we use the <=> (also called [spaceship operator](http://en.wikipedia.org/wiki/Spaceship_operator)) that will compare its two parameters as numbers and return 1, -1 or 0.

1\. my @sorted_numbers = sort { $a <=> $b } @numbers; Results in:

1\. $VAR1 = [

2.2,

3.3,

4.12,

5.14,

6.23

7.];

12. Reversing  Arrays

*   Reverse  LIST

In list context, returns a list value consisting of the elements of LIST in the opposite order. In scalar context, concatenates the elements of LIST and returns a string value with all characters in the opposite  order.

1. print join(", ", reverse "world", "Hello"); # Hello,  world 2.

3. print scalar reverse "dlrow  ,", "olleH";# Hello, world Used without arguments in scalar context, reverse() reverses $_  .

4. $_ = "dlrow  ,olleH";

5. print  reverse;# No output, list context

6. print scalar  reverse;# Hello, world

Note that reversing an array to itself (as in @a = [reverse](http://perldoc.perl.org/functions/reverse.html) @a ) will preserve non-existent elements whenever possible; i.e., for non-magical arrays or for tied arrays with EXISTS and DELETE methods.

13. Creating Hashes-Adding elements to Hashes-deleting, sorting and printing hash elements

A hash is a set of key/value pairs. Hash variables are preceded by a percent (%) sign. To refer to a single element of a hash, you will use the hash variable name preceded by a "$" sign and followed by the "key" associated with the value in curly brackets.

Here is a simple example of using the hash variables −

#!/usr/bin/perl

%data = ('John Paul', 45, 'Lisa', 30, 'Kumar', 40);

print "\$data{'John Paul'} = $data{'John Paul'}\n"; print "\$data{'Lisa'} = $data{'Lisa'}\n";

print "\$data{'Kumar'} = $data{'Kumar'}\n";

This will produce the following result −

$data{'John Paul'} = 45

$data{'Lisa'} = 30

$data{'Kumar'} = 40

Creating Hashes

Hashes are created in one of the two following ways. In the first method, you assign a value to a named key on a one-by-one basis −

$data{'John Paul'} = 45;

$data{'Lisa'} = 30;

$data{'Kumar'} = 40;

In the second case, you use a list, which is converted by taking individual pairs from the list: the first element of the pair is used as the key, and the second, as the value. For example −

%data = ('John Paul', 45, 'Lisa', 30, 'Kumar', 40);

For clarity, you can use => as an alias for , to indicate the key/value pairs as follows −

%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40);

Here is one more variant of the above form, have a look at it, here all the keys have  been preceded by hyphen (-) and no quotation is required around  them:

%data = (-JohnPaul => 45, -Lisa => 30, -Kumar =>  40);

But it is important to note that there is a single word, i.e. without spaces keys have been used in this form of hash formation and if you build-up your hash this way then keys will be accessed using hyphen only as shown below.

$val = %data{-JohnPaul}

$val = %data{-Lisa}

Accessing Hash Elements

When accessing individual elements from a hash, you must prefix the variable with a dollar sign ($) and then append the element key within curly brackets after the name of the variable. For example −

#!/usr/bin/perl

%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40); print "$data{'John Paul'}\n";

print "$data{'Lisa'}\n"; print "$data{'Kumar'}\n";

This will produce the following result −

45

30

40

Extracting Slices

You can extract slices of a hash just as you can extract slices from an array. You will need to use

@ prefix for the variable to store the returned value because they will be a list of values −

#!/uer/bin/perl

%data = (-JohnPaul => 45, -Lisa => 30, -Kumar => 40); @array = @data{-JohnPaul, -Lisa};

print "Array : @array\n";

This will produce the following result −

Array : 45 30

Extracting Keys and Values

You can get a list of all of the keys from a hash by using keys function, which has the following

syntax −

keys %HASH

This function returns an array of all the keys of the named hash. Following is the example −

#!/usr/bin/perl

%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40); @names = keys  %data;

print "$names[0]\n"; print "$names[1]\n"; print  "$names[2]\n";

This will produce the following result −

Lisa

John Paul Kumar

Similarly, you can use values function to get a list of all the values. This function has the

following syntax −

values %HASH

This function returns a normal array consisting of all the values of the named hash. Following is

the example −

#!/usr/bin/perl

%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40); @ages = values %data;

print "$ages[0]\n"; print "$ages[1]\n"; print "$ages[2]\n";

This will produce the following result −

30

45

40

*****

Unit-III REGULAR EXPRESSIONS

1.  Perl Regular Expressions and regex operator and pattern modifier  operators

A regular expression is a string of characters that defines the pattern or patterns you are viewing. The syntax of regular expressions in Perl is very similar to what you will find within other regular expression.supporting programs, such as sed, grep, and  awk.

The basic method for applying a regular expression is to use the pattern binding operators =~ and

!~. The first operator is a test and assignment operator. There are three regular expression operators within Perl.

*   Match Regular Expression -  m//
*   Substitute Regular Expression -  s///
*   Transliterate Regular Expression - tr///

The forward slashes in each case act as delimiters for the regular expression (regex) that you are specifying. If you are comfortable with any other delimiter, then you can use in place of forward slash.

2.  The Match  Operator

The match operator, m//, is used to match a string or statement to a regular expression. For example, to match the character sequence "foo" against the scalar $bar, you might use a statement like this  −

#!/usr/bin/perl

$bar = "This is foo and again foo"; if ($bar =~ /foo/){

print "First time is matching\n";

}else{

print "First time is not matching\n";

}

$bar = "foo";

if ($bar =~ /foo/){

print "Second time is matching\n";

}else{

print "Second time is not matching\n";

}

When above program is executed, it produces the following result − First time is matching

Second time is matching

The m// actually works in the same fashion as the q// operator series.you can use any combination of naturally matching characters to act as delimiters for the expression. For example, m{}, m(), and m>< are all valid. So above example can be re-written as follows − #!/usr/bin/perl

$bar = "This is foo and again foo"; if ($bar =~ m[foo]){

print "First time is matching\n";

}else{

print "First time is not matching\n";

}

$bar = "foo";

if ($bar =~ m{foo}){

print "Second time is matching\n";

}else{

print "Second time is not matching\n";

}

You can omit m from m// if the delimiters are forward slashes, but for all other delimiters you must use the m prefix.

Note that the entire match expression that is the expression on the left of =~ or !~ and the match operator, returns true (in a scalar context) if the expression matches. Therefore the statement −

$true = ($foo =~ m/foo/);

will set $true to 1 if $foo matches the regex, or 0 if the match fails. In a list context, the match returns the contents of any grouped expressions. For example, when extracting the hours, minutes, and seconds from a time string, we can use −

my ($hours, $minutes, $seconds) = ($time =~ m/(\d+):(\d+):(\d+)/);

3.  Match Operator  Modifiers

The match operator supports its own set of modifiers. The /g modifier allows for global matching. The /i modifier will make the match case insensitive. Here is the complete list of modifiers

| Modifier | Description |
| i | Makes the match case insensitive. |
| m | Specifies that if the string has newline or carriage return characters, the ^ and $ operators will now match against a newline boundary, instead of a string boundary. |
| o | Evaluates the expression only once. |
| s | Allows use of . to match a newline character. |
| x | Allows you to use white space in the expression for clarity. |
| g | Globally finds all matches. |
| cg | Allows the search to continue even after a global match fails. |

Matching Only Once

There is also a simpler version of the match operator - the ?PATTERN? operator. This is basically identical to the m// operator except that it only matches once within the string you are searching between each call to reset.

For example, you can use this to get the first and last elements within a list − #!/usr/bin/perl

@list = qw/food foosball subeo footnote terfoot canic footbrdige/; foreach (@list)

{

$first = $1 if ?(foo.*)?;

$last = $1 if /(foo.*)/;

}

print "First: $first, Last: $last\n";

When above program is executed, it produces the following result − First: food, Last: footbrdige

4.  Regular Expression  Variables

Regular expression variables include $, which contains whatever the last grouping match matched; $&, which contains the entire matched string; $`, which contains everything before the matched string; and $', which contains everything after the matched string. Following code demonstrates the result −

#!/usr/bin/perl

$string = "The food is in the salad bar";

$string =~ m/foo/; print "Before: $`\n"; print "Matched: $&\n"; print "After:  $'\n";

When above program is executed, it produces the following result − Before: The

Matched: foo

After: d is in the salad bar

5.  The Substitution  Operator

The substitution operator, s///, is really just an extension of the match operator that allows you to replace the text matched with some new text. The basic form of the operator is − s/PATTERN/REPLACEMENT/;

The PATTERN is the regular expression for the text that we are looking for. The REPLACEMENT is a specification for the text or regular expression that we want to use to replace the found text with. For example, we can replace all occurrences of dog with cat using the following regular expression −

#/user/bin/perl

$string = "The cat sat on the mat";

$string =~ s/cat/dog/;

print "$string\n";

When above program is executed, it produces the following result − The dog sat on the mat

Substitution Operator Modifiers

Here is the list of all modifiers used with substitution operator.

| Modifier | Description |
| i | Makes the match case insensitive. |
| m | Specifies that if the string has newline or carriage return characters, the ^ and $ operators will now match against a newline boundary, instead of a string boundary. |

| o | Evaluates the expression only once. |
| s | Allows use of . to match a newline character. |
| x | Allows you to use white space in the expression for clarity. |
| g | Replaces all occurrences of the found expression with the replacement text. |
| e | Evaluates the replacement as if it were a Perl statement, and uses its return value as the replacement text. |

6.  The Translation  Operator

Translation is similar, but not identical, to the principles of substitution, but unlike substitution, translation (or transliteration) does not use regular expressions for its search on replacement values. The translation operators are −

tr/SEARCHLIST/REPLACEMENTLIST/cds y/SEARCHLIST/REPLACEMENTLIST/cds

The translation replaces all occurrences of the characters in SEARCHLIST with the corresponding characters in REPLACEMENTLIST. For example, using the "The cat sat on the mat." string we have been using in this chapter −

#/user/bin/perl

$string = 'The cat sat on the mat';

$string =~ tr/a/o/;

print "$string\n";

When above program is executed, it produces the following result − The cot sot on the mot.

Standard Perl ranges can also be used, allowing you to specify ranges of characters either by letter or numerical value. To change the case of the string, you might use the following syntax in place of the uc function.

$string =~ tr/a-z/A-Z/;

7.  Translation Operator  Modifiers

Following is the list of operators related to translation.

| Modifier | Description |
| c | Complements SEARCHLIST. |
| d | Deletes found but unreplaced characters. |
| s | Squashes duplicate replaced characters. |

The /d modifier deletes the characters matching SEARCHLIST that do not have a corresponding entry in REPLACEMENTLIST. For example −

#!/usr/bin/perl

$string = 'the cat sat on the mat.';

$string =~ tr/a-z/b/d; print "$string\n";

When above program is executed, it produces the following result − b b b.

The last modifier, /s, removes the duplicate sequences of characters that were replaced, so − #!/usr/bin/perl

$string =  'food';

$string =  'food';

$string =~ tr/a-z/a-z/s;

print "$string\n";

When above program is executed, it produces the following result − fod

8.  More Complex Regular  Expressions

You don't just have to match on fixed strings. In fact, you can match on just about anything you could dream of by using more complex regular expressions. Here's a quick cheat sheet − Following table lists the regular expression syntax that is available in Python.

| Pattern | Description |
| ^ | Matches beginning of line. |
| $ | Matches end of line. |
| . | Matches any single character except newline. Using m option allows it to match newline as  well. |
| [...] | Matches any single character in brackets. |
| [^...] | Matches any single character not in brackets. |
| * | Matches 0 or more occurrences of preceding expression. |
| + | Matches 1 or more occurrence of preceding expression. |
| ? | Matches 0 or 1 occurrence of preceding expression. |
| { n} | Matches exactly n number of occurrences of preceding expression. |
| { n,} | Matches n or more occurrences of preceding expression. |
| { n, m} | Matches at least n and at most m occurrences of preceding expression. |
| a&#124; b | Matches either a or b. |
| \w | Matches word characters. |
| \W | Matches nonword characters. |
| \s | Matches whitespace. Equivalent to [\t\n\r\f]. |
| \S | Matches nonwhitespace. |
| \d | Matches digits. Equivalent to [0-9]. |
| \D | Matches nondigits. |
| \A | Matches beginning of string. |
| \Z | Matches end of string. If a newline exists, it matches just before newline. |
| \z | Matches end of string. |

| \G | Matches point where last match finished. |
| \b | Matches word boundaries when outside brackets. Matches backspace (0x08) when inside brackets. |
| \B | Matches nonword boundaries. |
| \n, \t, etc. | Matches newlines, carriage returns, tabs, etc. |
| \1...\9 | Matches nth grouped subexpression. |
| \10 | Matches nth grouped subexpression if it matched already. Otherwise refers to the octal representation of a character code. |
| [aeiou] | Matches a single character in the given set |
| [^aeiou] | Matches a single character outside the given set |

The ^ metacharacter matches the beginning of the string and the $ metasymbol matches the end of the string. Here are some brief examples.

# nothing in the string (start and end are adjacent)

/^$/

# a three digits, each followed by a whitespace # character (eg "3 4 5 ")

/(\d\s){3}/

# matches a string in which every

# odd-numbered letter is a (eg "abacadaf")

/(a.)+/

# string starts with one or more digits

/^\d+/

# string that ends with one or more digits

/\d+$/

Lets have a look at another example. #!/usr/bin/perl

$string = "Cats go Catatonic\nWhen given Catnip"; ($start) = ($string =~ /\A(.*?)  /);

@lines = $string =~ /^(.*?)  /gm;

print "First word: $start\n","Line starts: @lines\n";

When above program is executed, it produces the following result − First word: Cats

Line starts: Cats When

9.  Matching  Boundaries

The \b matches at any word boundary, as defined by the difference between the \w class and the

\W class. Because \w includes the characters for a word, and \W the opposite, this normally means the termination of a word. The \B assertion matches any position that is not a word boundary. For example −

/\bcat\b/ # Matches 'the cat sat' but not 'cat on the mat'

/\Bcat\B/ # Matches 'verification' but not 'the cat on the mat'

/\bcat\B/ # Matches 'catatonic' but not  'polecat'

/\Bcat\b/ # Matches 'polecat' but not  'catatonic'

Selecting Alternatives

The | character is just like the standard or bitwise OR within Perl. It specifies alternate matches within a regular expression or group. For example, to match "cat" or "dog" in an expression, you might use this −

if ($string =~ /cat|dog/)

You can group individual elements of an expression together in order to support  complex matches. Searching for two peoples names could be achieved with two separate tests, like this − if (($string =~ /Martin Brown/) || ($string =~ /Sharon  Brown/))

This could be written as follows

if ($string =~ /(Martin|Sharon) Brown/)

Grouping Matching

From a regular-expression point of view, there is no difference between except, perhaps, that the former is slightly clearer.

$string =~ /(\S+)\s+(\S+)/; and

$string =~ /\S+\s+\S+/;

However, the benefit of grouping is that it allows us to extract a sequence from a regular expression. Groupings are returned as a list in the order in which they appear in the original. For example, in the following fragment we have pulled out the hours, minutes, and seconds from a string.

my ($hours, $minutes, $seconds) = ($time =~ m/(\d+):(\d+):(\d+)/);

As well as this direct method, matched groups are also available within the special $x variables, where x is the number of the group within the regular expression. We could therefore rewrite the preceding example as follows −

#!/usr/bin/perl

$time = "12:05:30";

$time =~ m/(\d+):(\d+):(\d+)/;

my ($hours, $minutes, $seconds) = ($1, $2, $3);

print "Hours : $hours, Minutes: $minutes, Second: $seconds\n"; When above program is executed, it produces the following result − Hours : 12, Minutes: 05, Second: 30

When groups are used in substitution expressions, the $x syntax can be used in the replacement text. Thus, we could reformat a date string using this −

#!/usr/bin/perl

$date = '03/26/1999';

$date =~ s#(\d+)/(\d+)/(\d+)#$3/$1/$2#;

print "$date\n";

When above program is executed, it produces the following result − 1999/03/26

A regular expression is a string of characters that define the pattern or patterns you are viewing. The syntax of regular expressions in Perl is very similar to what you will find within other regular expression.supporting programs, such as sed, grep, and  awk.

The basic method for applying a regular expression is to use the pattern binding operators =~ and

!~. The first operator is a test and assignment operator. There are three regular expression operators within Perl

*   Match Regular Expression -  m//
*   Substitute Regular Expression -  s///
*   Transliterate Regular Expression - tr///

The forward slashes in each case act as delimiters for the regular expression (regex) that you are specifying. If you are comfortable with any other delimiter then you can use in place of forward slash.

10.  The Match  Operator

The match operator, m//, is used to match a string or statement to a regular expression. For example, to match the character sequence "foo" against the scalar $bar, you might use a statement like  this:

![](Images/image00436.jpeg)

The m// actually works in the same fashion as the q// operator series.you can use any combination of naturally matching characters to act as delimiters for the expression. For example, m{}, m(), and m>< are all  valid.

You can omit the m from m// if the delimiters are forward slashes, but for all other delimiters you must use the m prefix.

Note that the entire match expression.that is the expression on the left of =~ or !~ and the match operator, returns true (in a scalar context) if the expression matches. Therefore the statement:

![](Images/image00437.jpeg)

Will set $true to 1 if $foo matches the regex, or 0 if the match fails.

In a list context, the match returns the contents of any grouped expressions. For example, when extracting the hours, minutes, and seconds from a time string, we can use:

![](Images/image00438.jpeg)

11.  Match Operator  Modifiers

The match operator supports its own set of modifiers. The /g modifier allows for global matching. The /i modifier will make the match case insensitive. Here is the complete list of modifiers

![](Images/image00439.jpeg)

Matching Only Once

There is also a simpler version of the match operator - the ?PATTERN? operator. This is basically identical to the m// operator except that it only matches once within the string you are searching between each call to reset.

For example, you can use this to get the first and last elements within a list:

![](Images/image00440.jpeg)

![](Images/image00441.jpeg)

The Substitution Operator

The substitution operator, s///, is really just an extension of the match operator that allows you to replace the text matched with some new text. The basic form of the operator is:

![](Images/image00442.jpeg)

The PATTERN is the regular expression for the text that we are looking for. The REPLACEMENT is a specification for the text or regular expression that we want to use to replace the found text with.

For example, we can replace all occurrences of .dog. with .cat. using

![](Images/image00443.jpeg)

Another example:

![](Images/image00444.jpeg)

Substitution Operator Modifiers

Here is the list of all modifiers used with substitution operator

![](Images/image00445.jpeg)

![](Images/image00446.jpeg)

Translation

Translation is similar, but not identical, to the principles of substitution, but unlike substitution, translation (or transliteration) does not use regular expressions for its search on replacement values. The translation operators are:

![](Images/image00447.jpeg)

The translation replaces all occurrences of the characters in SEARCHLIST with the corresponding characters in REPLACEMENTLIST. For example, using the "The cat sat on the mat." string we have been using in this chapter:

![](Images/image00448.jpeg)

Standard Perl ranges can also be used, allowing you to specify ranges of characters either by letter or numerical value. To change the case of the string, you might use following syntax in place of the uc function.

![](Images/image00449.jpeg)

Translation Operator Modifiers

Following is the list of operators related to translation

![](Images/image00450.jpeg)

The /d modifier deletes the characters matching SEARCHLIST that do not have a corresponding entry in REPLACEMENTLIST. For example:

![](Images/image00451.jpeg)

The last modifier, /s, removes the duplicate sequences of characters that were replaced, so:

![](Images/image00452.jpeg)

More complex regular expressions

You don't just have to match on fixed strings. In fact, you can match on just about anything you could dream of by using more complex regular expressions. Here's a quick cheat sheet:

![](Images/image00453.jpeg)

![](Images/image00454.jpeg)

Quantifiers can be used to specify how many of the previous thing you want to match on, where "thing" means either a literal character, one of the metacharacters listed above, or a group of characters or metacharacters in parentheses.

![](Images/image00455.jpeg)

The ^ metacharacter matches the beginning of the string and the $ metasymbol matches the end of the string.

Here are some brief examples

![](Images/image00456.jpeg)

Lets have alook at another example

![](Images/image00457.jpeg)

![](Images/image00458.jpeg)

Matching Boundaries

The \b matches at any word boundary, as defined by the difference between the \w class and the

\W class. Because \w includes the characters for a word, and \W the opposite, this normally means the termination of a word. The \B assertion matches any position that is not a word boundary. For example:

![](Images/image00459.jpeg)

Selecting Alternatives

The | character is just like the standard or bitwise OR within Perl. It specifies alternate matches within a regular expression or group. For example, to match "cat" or "dog" in an expression, you might use this:

![](Images/image00460.jpeg)

You can group individual elements of an expression together in order to support complex matches. Searching for two people.s names could be achieved with two separate tests, like this:

![](Images/image00461.jpeg)

Grouping Matching

From a regular-expression point of view, there is no difference between except, perhaps, that the former is slightly clearer.

![](Images/image00462.jpeg)

However, the benefit of grouping is that it allows us to extract a sequence from a regular expression. Groupings are returned as a list in the order in which they appear in the original. For example, in the following fragment we have pulled out the hours, minutes, and seconds from a string.

![](Images/image00463.jpeg)

As well as this direct method, matched groups are also available within the special $x variables, where x is the number of the group within the regular expression. We could therefore rewrite the preceding example as follows:

![](Images/image00464.jpeg)

When groups are used in substitution expressions, the $x syntax can be used in the replacement text. Thus, we could reformat a date string using this:

![](Images/image00465.jpeg)

Using the \G Assertion

The \G assertion allows you to continue searching from the point where the last match occurred.

For example, in the following code we have used \G so that we can search to the correct position and then extract some information, without having to create a more complex, single regular expression:

![](Images/image00466.jpeg)

The \G assertion is actually just the metasymbol equivalent of the pos function, so between regular expression calls you can continue to use pos, and even modify the value of pos (and therefore \G) by using pos as an lvalue subroutine:

Regular Expression Variables

Regular expression variables include $, which contains whatever the last grouping match matched; $&, which contains the entire matched string; $`, which contains everything before the matched string; and $', which contains everything after the matched string.

The following code demonstrates the result:

![](Images/image00467.jpeg)

12.  Match Quantifiers and Boundary  operators

Quantifiers can be used to specify how many of the previous thing you want to match on, where "thing" means either a literal character, one of the metacharacters listed above, or a group of characters or metacharacters in parentheses.

![](Images/image00468.jpeg)

The ^ metacharacter matches the beginning of the string and the $ metasymbol matches the end of the string.

Here are some brief examples

![](Images/image00469.jpeg)

Lets have alook at another example

![](Images/image00470.jpeg)

Matching Boundaries

The \b matches at any word boundary, as defined by the difference between the \w class and the

\W class. Because \w includes the characters for a word, and \W the opposite, this normally means the termination of a word. The \B assertion matches any position that is not a word boundary. For example:

![](Images/image00471.jpeg)

Selecting Alternatives

The | character is just like the standard or bitwise OR within Perl. It specifies alternate matches within a regular expression or group. For example, to match "cat" or "dog" in an expression, you might use this:

![](Images/image00472.jpeg)

You can group individual elements of an expression together in order to support complex matches. Searching for two people.s names could be achieved with two separate tests, like this:

![](Images/image00473.jpeg)

Unit-IV

1.  PERL CONTROL  STATEMENTS

Perl control statements– if statements – if-else – if-elsif – if-elsif-else – while loop –  until loop –unless for loop – foreach loop

There may be a situation when you need to execute a block of code several number of times. In general, statements are executed sequentially: The first statement in a function is executed first, followed by the second, and so on.

Programming languages provide various control structures that allow for more complicated execution paths.

A loop statement allows us to execute a statement or group of statements multiple times and following is the general form of a loop statement in most of the programming languages −

![](Images/image00474.jpeg)

Perl programming language provides the following types of loop to handle the looping requirements.

| Loop Type | Description |
| [while loop](http://www.tutorialspoint.com/perl/perl_while_loop.htm) | Repeats a statement or group of statements while a given condition is true. It tests the condition before executing the loop body. |
| [until loop](http://www.tutorialspoint.com/perl/perl_until_loop.htm) | Repeats a statement or group of statements until a given condition becomes true. It tests the condition before executing the loop body. |
| [for loop](http://www.tutorialspoint.com/perl/perl_for_loop.htm) | Executes a sequence of statements multiple times and abbreviates |

|  | the code that manages the loop variable. |
| [foreach loop](http://www.tutorialspoint.com/perl/perl_foreach_loop.htm) | The foreach loop iterates over a normal list value and sets the variable VAR to be each element of the list in turn. |
| [do...while loop](http://www.tutorialspoint.com/perl/perl_do_while_loop.htm) | Like a while statement, except that it tests the condition at the end of the loop body |
| [nested loops](http://www.tutorialspoint.com/perl/perl_nested_loops.htm) | You can use one or more loop inside any another while, for or do..while loop. |

2.  Loop Control  Statements

Loop control statements change the execution from its normal sequence. When execution leaves a scope, all automatic objects that were created in that scope are  destroyed.

C supports the following control statements. Click the following links to check their detail.

| Control Statement | Description |
| [next statement](http://www.tutorialspoint.com/perl/perl_next_statement.htm) | Causes the loop to skip the remainder of its body and immediately retest its condition prior to reiterating. |
| [last statement](http://www.tutorialspoint.com/perl/perl_last_statement.htm) | Terminates the loop statement and transfers execution to the statement immediately following the loop. |
| [continue statement](http://www.tutorialspoint.com/perl/perl_continue_statement.htm) | A continue BLOCK, it is always executed just before the conditional is about to be evaluated again. |
| [redo statement](http://www.tutorialspoint.com/perl/perl_redo_statement.htm) | The redo command restarts the loop block without evaluating the conditional again. The continue block, if any, is not executed. |
| [goto statement](http://www.tutorialspoint.com/perl/perl_goto_statement.htm) | Perl supports a goto command with three forms: goto label, goto expr, and goto &name. |

3.  The Infinite  Loop

A loop becomes infinite loop if a condition never becomes false. The for loop is traditionally used for this purpose. Since none of the three expressions that form the for loop are required, you can make an endless loop by leaving the conditional expression empty.  #!/usr/local/bin/perl

for( ; ; )

{

printf "This loop will run forever.\n";

}

You can terminate the above infinite loop by pressing the Ctrl + C keys.

When the conditional expression is absent, it is assumed to be true. You may have an initialization and increment expression, but as a programmer more commonly use the for (;;) construct to signify an infinite loop.

Perl conditional statements helps in the decision making, which require that the programmer specifies one or more conditions to be evaluated or tested by the program, along with a statement or statements to be executed if the condition is determined to be true, and optionally, other statements to be executed if the condition is determined to be false.

Following is the general from of a typical decision making structure found in most of the programming languages −

![](Images/image00475.jpeg)

The number 0, the strings '0' and " " , the empty list () , and undef are all false in a boolean context and all other values are true. Negation of a true value by ! or not returns a special false value.

Perl programming language provides the following types of conditional statements.

| Statement | Description |
| if statement | An if statement consists of a boolean expression followed by one or more statements. |
| if...else statement | An if statement can be followed by an optional else |

|  | statement. |
| if...elsif...else statement | An if statement can be followed by an optional elsif statement and then by an optional else statement. |
| unless statement | An unless statement consists of a boolean expression followed by one or more  statements. |
| unless...else statement | An unless statement can be followed by an optional else statement. |

4.  PERL Scoping of  Variable

There are two major variable types in Perl. One of them is the package global variable declared either with the now obsolete use vars construct or with our.

The other one is the lexical variable declared with my.

Let's see what happens when you declare a variable using my? In which parts of the code will that variable be visible? In other words, what is the scope of the  variable?

Variable scope: enclosing block

1. #!/usr/bin/perl

2. use  strict;

3. use  warnings; 4.

5\. {

6. my $email = 'foo@bar.com';

7. print  "$email\n";# [foo@bar.com](mailto:foo@bar.com) 8.  }

9. # print  $email;

10. # $email does not  exists

11. # Global symbol "$email" requires explicit package name at  ...

Inside the anonymous block (the pair of curly braces {}), first we see the declaration of a new variable called $email. This variable exists between the point of its declaration till the end of the block. Thus the line after the closing curly brace } had to be commented out. If you removed the # from the # print $email; line, and tried to run the script, you'd get the following compile-time error: Global symbol "$email" requires explicit package name at ....

In other words, the scope of every variable declared with my is the enclosing block..

Variable scope: visible everywhere

The variable $lname is declared at the beginning of the code. It will be visible till the end of the file everywhere. Even inside blocks. Even if those are function declarations. If we change the variable inside the block, that will change the value for the rest of the code. Even when you leave the block:

1. #!/usr/bin/perl

2. use  strict;

3. use warnings; 4.

5. my $lname =  "Bar";

6. print  "$lname\n";# Bar 7.{

8. print  "$lname\n";# Bar

9. $lname =  "Other";

10. print  "$lname\n";# Other

11\. }

12.  print "$lname\n";# Other

Variable hidden by other declaration

1. #!/usr/bin/perl

2. use strict;

3. use  warnings;

4.

5. my $fname =  "Foo";

6. print  "$fname\n";# Foo 7.{

8. print  "$fname\n";#  Foo

9. my $fname =  "Other";

10. print  "$fname\n";#  Other

11\. }

12\. print "$fname\n"; # Foo

In this case the variable $fname is declared at the beginning of the code. As written earlier, it will be visible till the end of the file everywhere, except in places where they are hidden by locally declared variables with the same name.

Inside the block we used my to declare another variable with the same name. This will effectively hide the $fname declared outside the block till we leave the block. At the end of the block (at the closing}), the $fname declared inside will be destroyed and the original $fname will be accessible again. This feature is especially important as this makes it easy to create variables inside small scopes without the need to think about possible use of the same name  outside.

Same name in multiple blocks

You can freely use the same variable name in multiple blocks. These variables have no connection to each other.

1. #!/usr/bin/perl

2. use strict;

3. use  warnings;

4.  {

5. my $name =  "Foo";

6. print  "$name\n";# Foo 7.  }

8\. {

9. my $name =  "Other";

10. print  "$name\n";# Other

11\. }

In-file package declaration

This a bit more advanced example, but it might be important to mention it here:

Perl allows us to switch between name-spaces using the package keyword inside a file. A package declaration does NOT provide scope. If you declare a variable in the implicit main package which is just the regular body of your script, that $fname variable will be visible even in other name-spaces in the same  file.

If you declare a variable called $lname in the 'Other' name-space, it will be visible when later you might switch back to the main name-space. If the package Other declaration was in another file, then the variables would have separate scope created by the  file.

1. #!/usr/bin/perl

2. use strict;

3. use  warnings;

4.

5. my $fname =  "Foo";

6. print  "$fname\n";# Foo 7.

8. package  Other;

9. use strict;

10. use  warnings;

11. 11.

12. print  "$fname\n";#  Foo

13. my $lname =  'Bar';

14. print  "$lname\n";# Bar 15.

16.

17\. package main;

18.

19. print  "$fname\n";#  Foo

20. print  "$lname\n";#  Bar

5.  Bioperl and its  applications

BioPerl is a collection of Perl modules that facilitate the development of Perl scripts for bioinformatics applications. It has played an integral role in the Human Genome Project. BioPerl is an active open source software project supported by the Open Bioinformatics Foundation. The

first set of Perl codes of Bioperl was created by Tim Hubbard and Jong Bhak at MRC Centre Cambridge where the first genome sequencing was carried out by Fred Sanger. MRC Centre was one of the hubs and birth places of modern bioinformatics as it had large amount of DNA sequences and 3D protein structures. The name Bioperl was coined jointly by Jong Bhak and Steve Brenner in a small room of Centre for Protein Engineering (CPE) of MRC Centre where Alan Fersht was the director. In that small room, Cyrus Chothia and Tim Hubbard were working with some of their Ph.D. students and colleagues. Tim Hubbard is an expert Perl programmer and he was using th_lib.pl that contained many useful Perl subroutines for bioinformatics. Jong Bhak, being the first Ph.D. student of Tim Hubbard created jong_lib.pl. Jong merged the two Perl subroutine libraries into Bio.pl. One day in 1995, Steve Brenner, a Ph.D. student of Cyrus Chothia visited the room and started to discuss what they would call the perl library after some lengthy (a few months) debate on whether Perl is superior to C for bioinformatics as Steve Brenner had his own C library for bioinformatics. The two Ph.D. students named the net Perl library for biology Bioperl after going through names such as protein perl, protperl, PerlBio, and so on. Steve Brenner organized a Bioperl session in 1995 at ISMB Cambridge although it did not really happen. Bioperl had some users in coming months including Georg Fuellen who organized a training course in Germany. Georg's colleagues and students extended the Bioperl much and this was joined later by other people such as Steve Chervitz who was actively developing Perl codes for his yeast genome DB. The major expansion came when another Cambridge student Ewan Birney joined the wagon after another lengthy debate on if Perl was superior to C for bioinformatics and Ewan and many other people were very active in developing  Bioperl.

The first stable release was on 11 June 2002; the most recent stable (in terms of API) release is

1.6.9 from 14 April 2011\. There are also developer releases produced periodically. Version  series 1.6.0 is considered to be the most stable (in terms of bugs) version of BioPerl and is recommended for everyday use, but the nightly builds are also extremely stable, and many BioPerl users stay current with  those.

In order to take advantage of BioPerl, the user needs a basic understanding of the Perl programming language including an understanding of how to use Perl references, modules, objects and methods.

Features and Applications

BioPerl provides software modules for many of the typical tasks of bioinformatics programming. These include:

*   Accessing nucleotide and peptide sequence data from local and remote  databases
*   Transforming formats of database/ file  records
*   Manipulating individual  sequences
*   Searching for similar  sequences
*   Creating and manipulating sequence  alignments
*   Searching for genes and other structures on genomic  DNA
*   Developing machine readable sequence  annotations

In addition to being used directly by end-users, BioPerl has also provided the base for a wide variety of bioinformatic tools, including amongst others:

*   SynBrowse,
*   Gene Comber, TFBS, MIMOX, BioParser, Degenerate primer design, Querying the public databases, Current Comparative  Table
*   New tools and algorithms from external developers are often integrated directly into BioPerl  itself:
*   Dealing with phylogenetic trees and nested taxa FPC Web tools Related Libraries in Other Programming  Languages.

Several related bioinformatics libraries implemented in other programming languages exist as part of the [Open Bioinformatics Foundation](https://en.wikipedia.org/wiki/Open_Bioinformatics_Foundation) including: Biopython, BioJava, BioRuby, BioPHP, BioJS, Bioconductor, etc.

*****

Unit-V

1.  INTRODUCTION TO PERL MODULES Getopt::Long - Extended processing of command line options SYNOPSIS

1. use  Getopt::Long;

2. my $data =  "file.dat";

3. my $length =  24;

4. my  $verbose;

5. GetOptions ("length=i"  =>  \$length,# numeric

6. "file=s" =>  \$data,# string

7. "verbose" => \$verbose) # flag

8. or die("Error in command line  arguments\n"); DESCRIPTION

The Getopt::Long module implements an extended getopt function called GetOptions(). It parses the command line from @ARGV , recognizing and removing specified options and their possible values.

This function adheres to the POSIX syntax for command line options, with GNU  extensions. In general, this means that options have long names instead of single letters, and are introduced with a double dash "--". Support for bundling of command line options, as was the case with the more traditional single-letter approach, is provided but not enabled by default.

Command Line Options, an Introduction

Command line operated programs traditionally take their arguments from the command line, for example filenames or other information that the program needs to know. Besides arguments, these programs often take command line options as well. Options are  not

necessary for the program to work, hence the name 'option', but are used to modify its default behaviour. For example, a program could do its job quietly, but with a suitable option it could provide verbose information about what it  did.

Command line options come in several flavours. Historically, they are preceded by a single dash - , and consist of a single letter.

1. -l -a  -c

Usually, these single-character options can be bundled:

1. -lac

Options can have values, the value is placed after the option character. Sometimes with whitespace in between, sometimes not:

1.-s 24  -s24

Due to the very cryptic nature of these options, another style was developed that used long names. So instead of a cryptic -l one could use the more descriptive --long . To distinguish between a bundle of single-character options and a long one, two dashes are used to precede the option name. Early implementations of long options used a plus + instead. Also, option values could be specified either like

1.--size=24 or

1. --size  24

The + form is now obsolete and strongly deprecated.

Getting Started with Getopt::Long

Getopt::Long is the Perl5 successor of newgetopt.pl . This was the first Perl module that provided support for handling the new style of command line options, in particular long

option names, hence the Perl5 name Getopt::Long. This module also supports single- character options and bundling.

To use Getopt::Long from a Perl program, you must include the following line in your Perl program:

1.use  Getopt::Long;

This will load the core of the Getopt::Long module and prepare your program for using it. Most of the actual Getopt::Long code is not loaded until you really call one of its functions.

In the default configuration, options names may be abbreviated to uniqueness, case does not matter, and a single dash is sufficient, even for long option names. Also, options may be placed between non-option arguments.

Simple options

The most simple options are the ones that take no values. Their mere presence on the command line enables the option. Popular examples are:

1.--all --verbose --quiet --debug Handling simple options is  straightforward:

1. my $verbose  =  '';# option variable with default value  (false)

2. my $all  = '';# option variable with default value  (false)

3. GetOptions ('verbose' => \$verbose, 'all' =>  \$all);

The call to GetOptions() parses the command line arguments that are present in @ARGV and sets the option variable to the value 1 if the option did occur on the command line. Otherwise, the option variable is not touched. Setting the option value to true is often called enabling the option.

The option name as specified to the GetOptions() function is called the option specification. Later we'll see that this specification can contain more than just the option name. The reference to the variable is called the option destination.

GetOptions() will return a true value if the command line could be processed successfully. Otherwise, it will write error messages using die() and warn(), and return a false result.

A little bit less simple options

Getopt::Long supports two useful variants of simple options: negatable options and incremental options.

A negatable option is specified with an exclamation mark ! after the option name:

1. my $verbose  =  '';# option variable with default value  (false)

2. GetOptions ('verbose!' =>  \$verbose);

Now, using --verbose on the command line will enable $verbose , as expected. But it is also allowed to use --noverbose , which will disable $verbose by setting its value to 0 . Using a suitable default value, the program can find out whether $verbose is false by default, or disabled by using --noverbose .

An incremental option is specified with a plus + after the option name:

1. my $verbose  =  '';# option variable with default value  (false)

2. GetOptions ('verbose+' =>  \$verbose);

Using --verbose on the command line will increment the value of $verbose . This way the program can keep track of how many times the option occurred on the command line. For example, each occurrence of --verbose could increase the verbosity level of the program.

Mixing command line option with other arguments

Usually programs take command line options as well as other arguments, for example, file names. It is good practice to always specify the options first, and the other arguments last.

Getopt::Long will, however, allow the options and arguments to be mixed and 'filter out' all the options before passing the rest of the arguments to the program. To stop Getopt::Long from processing further arguments, insert a double dash -- on the command line:

1. --size  24-------------all

In this example, --all will not be treated as an option, but passed to the program unharmed, in @ARGV  .

Options with values

For options that take values it must be specified whether the option value is required or not, and what kind of value the option expects.

Three kinds of values are supported: integer numbers, floating point numbers, and strings.

If the option value is required, Getopt::Long will take the command line argument that follows the option and assign this to the option variable. If, however, the option value is specified as optional, this will only be done if that value does not look like a valid command line option itself.

1. my $tag  =  '';# option variable with default value

2.  GetOptions ('tag=s' =>  \$tag);

In the option specification, the option name is followed by an equals sign = and the letter s. The equals sign indicates that this option requires a value. The letter s indicates that this value is an arbitrary string. Other possible value types are i for integer values, and f for floating point values. Using a colon : instead of the equals sign indicates that the option value is optional. In this case, if no suitable value is supplied, string valued options get an empty string '' assigned, while numeric options are set to 0 .

Options with multiple values

Options sometimes take several values. For example, a program could use multiple directories to search for library files:

--library lib/stdlib --library lib/extlib

To accomplish this behaviour, simply specify an array reference as the destination for the option:

GetOptions ("library=s" =>  \@libfiles);

Alternatively, you can specify that the option can have multiple values by adding a "@", and pass a scalar reference as the destination:

GetOptions ("library=s@" => \$libfiles);

Used with the example above, @libfiles (or @$libfiles ) would contain two strings upon completion: "lib/stdlib" and "lib/extlib" , in that order. It is also possible to specify that only integer or floating point numbers are acceptable values.

Often it is useful to allow comma-separated lists of values as well as multiple occurrences of the options. This is easy using Perl's split() and join() operators:

GetOptions ("library=s" => \@libfiles); @libfiles =  split(/,/,join(',',@libfiles));

Of course, it is important to choose the right separator string for each  purpose. Warning: What follows is an experimental  feature.

Options can take multiple values at once, for example

--coordinates 52.2 16.4 --rgbcolor 255 255 149

This can be accomplished by adding a repeat specifier to the option specification. Repeat specifiers are very similar to the {...} repeat specifiers that can be used with regular expression patterns. For example, the above command line would be handled as follows:

GetOptions('coordinates=f{2}' => \@coor, 'rgbcolor=i{3}' => \@color);

The destination for the option must be an array or array reference.

It is also possible to specify the minimal and maximal number of arguments an option takes. foo=s{2,4} indicates an option that takes at least two and at most 4 arguments. foo=s{1,} indicates one or more values; foo:s{,} indicates zero or more option values.

Options with hash values

If the option destination is a reference to a hash, the option will take, as value, strings of the form key= value. The value will be stored with the specified key in the hash.

GetOptions ("define=s" => \%defines); Alternatively you can use:

GetOptions ("define=s%" => \$defines); When used with command line options:

--define os=linux --define vendor=redhat

the hash %defines (or %$defines ) will contain two keys, "os" with value "linux" and "vendor" with value "redhat" . It is also possible to specify that only integer or floating point numbers are acceptable values. The keys are always taken to be strings.

User-defined subroutines to handle options

Ultimate control over what should be done when (actually: each time) an option is encountered on the command line can be achieved by designating a reference to a subroutine (or an anonymous subroutine) as the option destination. When GetOptions() encounters the option, it will call the subroutine with two or three arguments. The first argument is the name of the option. (Actually, it is an object that stringifies to the name of the option.) For a scalar or array destination, the second argument is the value to be stored. For a hash destination, the second argument is the key to the hash,  and the third argument

the value to be stored. It is up to the subroutine to store the value, or do whatever it thinks is appropriate.

A trivial application of this mechanism is to implement options that are related to each other. For example:

1. my $verbose  =  '';# option variable with default value  (false)

2. GetOptions ('verbose' =>  \$verbose,

3. 'quiet' => sub { $verbose = 0  });

Here --verbose and --quiet control the same variable $verbose , but with opposite values.

If the subroutine needs to signal an error, it should call die() with the desired error message as its argument. GetOptions() will catch the die(), issue the error message, and record that an error result must be returned upon completion.

If the text of the error message starts with an exclamation mark ! it is interpreted specially by GetOptions(). There is currently one special command implemented: die("!FINISH") will cause GetOptions() to stop processing options, as if it encountered a double dash --  .

In version 2.37 the first argument to the callback function was changed from string to object. This was done to make room for extensions and more detailed control. The object stringifies to the option name so this change should not introduce compatibility  problems.

Here is an example of how to access the option name and value from within a  subroutine:

1. GetOptions ('opt=i' =>  \&handler);

2. sub handler  {

3. my ($opt_name, $opt_value) =  @_;

4. print("Option name is $opt_name and value is  $opt_value\n"); 5.}

Options with multiple names

Often it is user friendly to supply alternate mnemonic names for options. For example -- height could be an alternate name for --length . Alternate names can be included in the option specification, separated by vertical bar | characters. To implement the above  example:

GetOptions ('length|height=f' => \$length);

The first name is called the primary name, the other names are called aliases. When using a hash to store options, the key will always be the primary name.

Multiple alternate names are possible. Case and abbreviations

Without additional configuration, GetOptions() will ignore the case of option names, and allow the options to be abbreviated to uniqueness.

GetOptions ('length|height=f' => \$length, "head" => \$head);

This call will allow --l and --L for the length option, but requires a least --hea and --hei for the head and height options.

Summary of Option Specifications

Each option specifier consists of two parts: the name specification and the argument specification.

The name specification contains the name of the option, optionally followed by a list of alternative names separated by vertical bar characters.

1.  lengthoption name is  "length"
2.  length|size|lname is "length", aliases are "size" and  "l"

The argument specification is optional. If omitted, the option is considered boolean, a value of 1 will be assigned when the option is used on the command line.

The argument specification can be

*   !

The option does not take an argument and may be negated by prefixing it with "no" or "no-".

E.g. "foo!" will allow --foo (a value of 1 will be assigned) as well as --nofoo and --no-foo (a value of 0 will be assigned). If the option has aliases, this applies to the aliases as well.

Using negation on a single letter option when bundling is in effect is pointless and will result in a  warning.

•+

The option does not take an argument and will be incremented by 1 every time it appears on the command line. E.g. "more+" , when used with --more --more --more, will increment the value three times, resulting in a value of 3 (provided it was 0 or undefined at first).

The + specifier is ignored if the option destination is not a scalar.

•= type [ desttype ] [ repeat  ]

The option requires an argument of the given type. Supported types are:

*   s

String. An arbitrary sequence of characters. It is valid for the argument to start with - or -- .

*   i

Integer. An optional leading plus or minus sign, followed by a sequence of digits.

oo

Extended integer, Perl style. This can be either an optional leading plus or minus sign, followed by a sequence of digits, or an octal string (a zero, optionally followed by '0', '1', ..

'7'), or a hexadecimal string (0x followed by '0' .. '9', 'a' .. 'f', case insensitive), or a binary string (0b followed by a series of '0' and '1').

*   f

Real number. For example 3.14 , -6.23E24 and so on.

The desttype can be @ or % to specify that the option is list or a hash valued. This is only needed when the destination for the option value is not otherwise specified. It should be omitted when not needed.

The repeat specifies the number of values this option takes per occurrence on the command line. It has the format { [ min ] [ , [ max ] ] }.

min denotes the minimal number of arguments. It defaults to 1 for options with = and to 0 for options with : , see below. Note that min overrules the = / :  semantics.

max denotes the maximum number of arguments. It must be at least min. If max is omitted, but the comma is not, there is no upper bound to the number of argument values taken.

*   : type [ desttype  ]

Like = , but designates the argument as optional. If omitted, an empty string will be assigned to string values options, and the value zero to numeric options.

Note that if a string argument starts with - or -- , it will be considered an option on itself.

*   : number [ desttype  ]

Like :i , but if the value is omitted, the number will be assigned.

*   : + [ desttype  ]

Like :i , but if the value is omitted, the current value for the option will be incremented.

3.  LWP::Simple  Module

LWP - The World-Wide Web library for Perl

SYNOPSIS

use LWP;

print "This is libwww-perl-$LWP::VERSION\n";

DESCRIPTION

The libwww-perl collection is a set of Perl modules which provides a simple and consistent application programming interface (API) to the World-Wide Web. The main focus of the library is to provide classes and functions that allow you to write WWW clients. The library also contain modules that are of more general use and even classes that help you implement simple HTTP servers.

Most modules in this library provide an object oriented API. The user agent, requests sent and responses received from the WWW server are all represented by objects. This makes a simple and powerful interface to these services. The interface is easy to extend and customize for your own needs.

The main features of the library are:

*   Contains various reusable components (modules) that can be used separately or  together.
*   Provides an object oriented model of HTTP-style communication. Within this framework we currently support access to http, https, gopher, ftp, news, file, and mailto  resources.
*   Provides a full object oriented interface or a very simple procedural  interface.
*   Supports the basic and digest authorization  schemes.
*   Supports transparent redirect  handling.
*   Supports access through proxy  servers.
*   Provides parser for robots.txt files and a framework for constructing  robots.
*   Supports parsing of HTML  forms.
*   Implements HTTP content negotiation algorithm that can be used both in protocol modules and in server scripts (like CGI  scripts).
*   Supports HTTP  cookies.
*   Some simple command line clients, for instance lwp-request and  lwp-download.

HTTP STYLE COMMUNICATION

The libwww-perl library is based on HTTP style communication. This section tries to describe what that means.

LetusstartwiththisquotefromtheHTTPspecificationdocument

<URL[:http://www.w3.org/Protocols/](http://www.w3.org/Protocols/)>:

*   The HTTP protocol is based on a request/response paradigm. A client establishes a connection with a server and sends a request to the server in the form of a request method, URI, and protocol version, followed by a MIME-like message containing request modifiers, client information, and possible body content. The server responds with a status line, including the message's protocol version and a success or error code, followed by a MIME-like message containing server information, entity meta-information, and possible body  content.

What this means to libwww-perl is that communication always take place through these steps: First a request object is created and configured. This object is then passed to a server and we get a response object in return that we can examine. A request is always independent of any previous requests, i.e. the service is stateless. The same simple model is used for any kind of service we want to  access.

For example, if we want to fetch a document from a remote file server, then we send it a request that contains a name for that document and the response will contain the document itself. If we access a search engine, then the content of the request will contain the query parameters and the response will contain the query result. If we want to send a mail message to somebody then we send a request object which contains our message to the mail server and the response object will contain an acknowledgment that tells us that the message has been accepted and will be forwarded to the recipient(s).

It is as simple as that!

The Request Object

The libwww-perl request object has the class name HTTP::Request. The fact that the class name uses HTTP:: as a prefix only implies that we use the HTTP model of communication. It does not limit the kind of services we can try to pass this request to. For instance, we will send HTTP::Requests both to ftp and gopher servers, as well as to the local file system.

The main attributes of the request objects are:

*   method is a short string that tells what kind of request this is. The most common methods are GET, PUT, POST and  HEAD.
*   uri is a string denoting the protocol, server and the name of the "document" we want to access. The uri might also encode various other  parameters.
*   headers contains additional information about the request and can also used to describe the content. The headers are a set of keyword/value  pairs.
*   content is an arbitrary amount of  data.

The Response Object

The libwww-perl response object has the class name HTTP::Response. The main attributes of objects of this class are:

*   code is a numerical value that indicates the overall outcome of the  request.
*   message is a short, human readable string that corresponds to the  code.
*   headers contains additional information about the response and describe the  content.
*   content is an arbitrary amount of  data.

Since we don't want to handle all possible code values directly in our programs, a libwww-perl response object has methods that can be used to query what kind of response this is. The most commonly used response classification methods are:

is_success()

The request was successfully received, understood or accepted. is_error()

The request failed. The server or the resource might not be available, access to the resource might be denied or other things might have failed for some reason.

The User Agent

Let us assume that we have created a request object. What do we actually do with it in order to receive a response?

The answer is that you pass it to a user agent object and this object takes care of all the things that need to be done (like low-level communication and error handling) and returns a response object. The user agent represents your application on the network and provides you with an interface that can accept requests and return responses.

The user agent is an interface layer between your application code and the network. Through this interface you are able to access the various servers on the network.

The class name for the user agent is LWP::UserAgent. Every libwww-perl application that wants to communicate should create at least one object of this class. The main method provided by this object is request(). This method takes an HTTP::Request object as argument and (eventually) returns a HTTP::Response  object.

The user agent has many other attributes that let you configure how it will interact with the network and with your  application.

*   timeout specifies how much time we give remote servers to respond before the library disconnects and creates an internal timeout  response.
*   agent specifies the name that your application uses when it presents itself on the  network.
*   from can be set to the e-mail address of the person responsible for running the application. If this is set, then the address will be sent to the servers with every  request.
*   parse_head specifies whether we should initialize response headers from the <head> section of HTML  documents.
*   proxyandno_proxyspecifyifandwhentogothroughaproxyserver.

<URL[:http://www.w3.or](http://www.w3.org/History/1994/WWW/Proxies/)g[/History/1994/WWW/Proxies/>](http://www.w3.org/History/1994/WWW/Proxies/)

*   credentials provides a way to set up user names and passwords needed to access certain services.

Many applications want even more control over how they interact with the network and they get this by sub-classing LWP::UserAgent. The library includes a sub-class, LWP::RobotUA, for robot applications.

3.  Files – operating files – file modes – file test  operators

*   -X  FILEHANDLE
*   -X  EXPR
*   -X  DIRHANDLE
*   -X

A file test, where X is one of the letters listed below. This unary operator takes one argument, either a filename, a filehandle, or a dirhandle, and tests the associated file to see if something is true about it. If the argument is omitted, tests $_ , except for -t , which tests STDIN. Unless otherwise documented, it returns 1 for true and '' for false. If the file doesn't exist or can't be examined, it returns [undef](http://perldoc.perl.org/functions/undef.html) and sets $! (errno). Despite the funny names, precedence is the same as any other named unary operator. The operator may be any  of:

1. -r File is readable by effective  uid/gid.

2. -w File is writable by effective  uid/gid.

3. -x File is executable by effective  uid/gid.

4. -o File is owned by effective uid. 5.

6. -R File is readable by real  uid/gid.

7. -W File is writable by real  uid/gid.

8. [-X](http://perldoc.perl.org/functions/-X.html) File is executable by real  uid/gid.

9. -O File is owned by real uid. 10.

11. -e File  [exists](http://perldoc.perl.org/functions/exists.html).

12. -z File has zero size (is  empty).

13. -s File has nonzero size (returns size in bytes). 14.

15. -f File is a plain  file.

16. -d File is a  directory.

17. -l File is a sy[mbolic link](http://perldoc.perl.org/functions/link.html) (false [if](http://perldoc.perl.org/functions/if.html) symlinks  aren't

18. supported by the file  [system](http://perldoc.perl.org/functions/system.html)).

19. -p File is a named [pipe](http://perldoc.perl.org/functions/pipe.html) (FIFO), [or](http://perldoc.perl.org/functions/or.html) Filehandle is a  [pipe](http://perldoc.perl.org/functions/pipe.html).

20. -S File is [a  socket.](http://perldoc.perl.org/functions/socket.html)

21. -b File is a block special  file.

22. -c File is a character special  file.

23. -t Filehandle is opened to a tty.

24. 24.

25. -u  File has setuid bit  set.

26. -g  File has setgid bit  set.

27. -k File has sticky bit set. 28.

29. -T File is an ASCII [or](http://perldoc.perl.org/functions/or.html) UTF-8 text file (heuristic  guess).

30. -B File is a "binary" file (opposite of -T). 31.

32. -M Script start [time](http://perldoc.perl.org/functions/time.html) minus file modification [time](http://perldoc.perl.org/functions/time.html), in  days.

33. -A Same [for](http://perldoc.perl.org/functions/for.html) access  [time](http://perldoc.perl.org/functions/time.html).

34. -C Sa[me for](http://perldoc.perl.org/functions/for.html) inode change [time](http://perldoc.perl.org/functions/time.html) (Unix, may differ [for](http://perldoc.perl.org/functions/for.html) other

35. platforms)

Example:

| 36. |  | while (<>) { |
| 37. |  | [chomp](http://perldoc.perl.org/functions/chomp.html); |
| 38. |  | [next](http://perldoc.perl.org/functions/next.html) unless -f $_; # ignore specials |
| 39. |  | #... |
| 40. |  | } |

Note that -s/a/b/ does not do a negated substitution. Saying -[exp](http://perldoc.perl.org/functions/exp.html)($foo) still works as expected, however: only single letters following a minus are interpreted as file tests.

These operators are exempt from the "looks like a function rule" described above. That is, an opening parenthesis after the operator does not affect how much of the following code constitutes the argument. Put the opening parentheses before the operator to separate it from code that follows (this applies only to operators with higher precedence than unary operators, of course):

41. -s($file) + 1024 # probably wrong; same as -s($file +  1024)

42. (-s $file) + 1024 #  correct

The interpretation of the file permission operators -r , -R , -w , -W , -x , and [-X](http://perldoc.perl.org/functions/-X.html) is by default based solely on the mode of the file and the uids and gids of the user. There may be other reasons you can't actually read, write, or execute the file: for example network filesystem access controls, ACLs (access control lists), read-only filesystems, and unrecognized executable formats. Note that the use of these six specific operators to verify if some operation is possible is usually a mistake, because it may be open to race  conditions.

Also note that, for the superuser on the local filesystems, the -r , -R , -w , and -W tests always return 1, and -x and [-X](http://perldoc.perl.org/functions/-X.html) return 1 if any execute bit is set in the mode. Scripts run by the superuser may thus need to do a stat() to determine the actual mode of the file, or temporarily set their effective uid to something else.

If you are using ACLs, there is a pragma called filetest that may produce more accurate results than the bare stat() mode bits. When under [use](http://perldoc.perl.org/functions/use.html) filetest 'access' the above-mentioned filetests test whether

the permission can(not) be granted using the access(2) family of system calls. Also note that the -x and [-X](http://perldoc.perl.org/functions/-X.html) may under this pragma return true even if there are no execute permission bits set (nor any extra execute permission ACLs). This strangeness is due to the underlying system calls' definitions. Note also that, due to the implementation of [use](http://perldoc.perl.org/functions/use.html) filetest 'access' , the _ special filehandle won't cache the results of the file tests when this pragma is in effect. Read the documentation for the filetest pragma for more  information.

The -T and -B switches work as follows. The first block or so of the file is examined to see if it is valid UTF-8 that includes non-ASCII characters. If, so it's a -T file. Otherwise, that same portion of the file is examined for odd characters such as strange control codes or characters with the high bit set. If more than a third of the characters are strange, it's a -B file; otherwise it's a -T file. Also, any file containing a zero byte in the examined portion is considered a binary file. (If executed within the scope of a [use locale](http://perldoc.perl.org/perllocale.html) which includes LC_CTYPE , odd characters are anything that isn't a printable nor space in the current locale.) If -T or -B is used on a filehandle, the current IO buffer is examined rather than the first block. Both -T and -B return true on an empty file, or a file at EOF when testing a filehandle. Because you have to read a file to do the -T test, on most occasions you want to use a -f against the file first, as in [next](http://perldoc.perl.org/functions/next.html) unless -f $file && -T $file  .

If any of the file tests (or either the [stat](http://perldoc.perl.org/functions/stat.html) or [lstat](http://perldoc.perl.org/functions/lstat.html) operator) is given the special filehandle consisting of a solitary underline, then the stat structure of the previous file test (or stat operator) is used, saving a system call. (This doesn't work with -t , and you need to remember that lstat() and -l leave values in the stat structure for the symbolic link, not the real file.) (Also, if the stat buffer was filled by an [lstat](http://perldoc.perl.org/functions/lstat.html) call, -T and -B will reset it with the results of [stat](http://perldoc.perl.org/functions/stat.html) _ ).  Example:

43. [print](http://perldoc.perl.org/functions/print.html) "Can do.\n" if -r $a || -w _ || -x _; 44.

45. [stat](http://perldoc.perl.org/functions/stat.html)($filename);

46. [print](http://perldoc.perl.org/functions/print.html) "Readable\n" if -r  _;

47. [print](http://perldoc.perl.org/functions/print.html) "Writable\n" if -w _;

48. [print](http://perldoc.perl.org/functions/print.html) "Executable\n" if -x  _;

49. [print](http://perldoc.perl.org/functions/print.html) "Setuid\n" if -u  _;

50. [print](http://perldoc.perl.org/functions/print.html) "Setgid\n" if -g  _;

51. [print](http://perldoc.perl.org/functions/print.html) "Sticky\n" if -k  _;

52. [print](http://perldoc.perl.org/functions/print.html) "Text\n" if -T  _;

53. [print](http://perldoc.perl.org/functions/print.html) "Binary\n" if -B  _;

As of Perl 5.10.0, as a form of purely syntactic sugar, you can stack file test operators, in a way that -f -w -x $file is equivalent to -x $file && -w _ && -f _ . (This is only fancy syntax: if you use the return value of -f $file as an argument to another filetest operator, no special magic will happen.)

Portability issues: [-X in perlport.](http://perldoc.perl.org/perlport.html#-X)

To avoid confusing would-be users of your code with mysterious syntax errors, put something like this at the top of your script:

54. [use](http://perldoc.perl.org/functions/use.html) 5.010; # so filetest ops can  stack

4.  @ ARGV  variable

ARGV array elements: In the ARGV array, $ARGV[0] contains the first argument, $ARGV[1] contains the second argument, etc. So if you're just looking for one command line argument you can test for $ARGV[0], and if you're looking for two you can also test for $ARGV[1], and so on.

ARGV array size: The variable $#ARGV is the subscript of the last element of the @ARGV array, and because the array is zero-based, the number of arguments given on the command line is

$#ARGV + 1.

Perl automatically provides an array called @ARGV, that holds all the values from the command line. You don't have to declare the variable, even if you use strict.

This variable always exists and the values from the command line are automatically placed in this variable.

If there are no parameters, the array will be empty. If there is one parameter on the command line, that value will be the only element in @ARGV. In the above example the @ARGV will have the following elements: -a, --machine, remote, /etc

Let's see this in action:

Save this code as programming.pl:

1. use strict;

2. use  warnings;

3. use Data::Dumper qw(Dumper); 4.

5.print Dumper  \@ARGV;

Run it like this: perl programming.pl -a --machine remote /etc and this is the output:

$VAR1 = [

'-a',

'--machine', 'remote', '/etc'

];

5.  CWD  Module

Cwd - get pathname of current working directory

SYNOPSIS

[use](http://perldoc.perl.org/functions/use.html) Cwd;

[my](http://perldoc.perl.org/functions/my.html) $dir = getcwd; [use](http://perldoc.perl.org/functions/use.html) Cwd 'abs_path';

[my](http://perldoc.perl.org/functions/my.html) $abs_path = abs_path($file);

DESCRIPTION

This module provides functions for determining the pathname of the current working directory. It is recommended that getcwd (or another *cwd() function) be used in all code to ensure portability.

By default, it exports the functions cwd(), getcwd(), fastcwd(), and fastgetcwd() (and, on Win32, getdcwd()) into the caller's namespace.

getcwd and  friends

Each of these functions are called without arguments and return the absolute path of the current working  directory.

getcwd

[my](http://perldoc.perl.org/functions/my.html) $cwd = getcwd();

Returns the current working directory.

Exposes the POSIX function getcwd(3) or re-implements it if it's not available. cwd

[my](http://perldoc.perl.org/functions/my.html) $cwd = cwd();

The cwd() is the most natural form for the current architecture. For most systems it is identical to

`pwd` (but without the trailing line terminator). fastcwd

[my](http://perldoc.perl.org/functions/my.html) $cwd = fastcwd();

A more dangerous version of getcwd(), but potentially faster.

It might conceivably chdir() you out of a directory that it can't chdir() you back into. If fastcwd encounters a problem it will return undef but will probably leave you in a different directory. For a measure of extra security, if everything appears to have worked, the fastcwd() function will check that it leaves you in the same directory that it started in. If it has changed it will [die](http://perldoc.perl.org/functions/die.html) with the message "Unstable directory path, current directory changed unexpectedly". That should never happen.

fastgetcwd

[my](http://perldoc.perl.org/functions/my.html) $cwd = fastgetcwd();

The fastgetcwd() function is provided as a synonym for cwd(). getdcwd

[my](http://perldoc.perl.org/functions/my.html) $cwd = getdcwd(); [my](http://perldoc.perl.org/functions/my.html) $cwd =  getdcwd('C:');

The getdcwd() function is also provided on Win32 to get the current working directory on the specified drive, since Windows maintains a separate current working directory for each drive. If no drive is specified then the current drive is  assumed.

This function simply calls the Microsoft C library _getdcwd() function. abs_path and friends

These functions are exported only on request. They each take a single argument and return the absolute pathname for it. If no argument is given they'll use the current working  directory.

abs_path

[my](http://perldoc.perl.org/functions/my.html) $abs_path = abs_path($file);

Uses the same algorithm as getcwd(). Symbolic links and relative-path components ("." and "..") are resolved to return the canonical pathname, just like realpath(3).

realpath

[my](http://perldoc.perl.org/functions/my.html) $abs_path = realpath($file); A synonym for abs_path(). fast_abs_path

[my](http://perldoc.perl.org/functions/my.html) $abs_path = fast_abs_path($file);

A more dangerous, but potentially faster version of abs_path.

$ENV{PWD}

If you ask to override your chdir() built-in function, [use](http://perldoc.perl.org/functions/use.html) Cwd qw(chdir);

then your PWD environment variable will be kept up to date. Note that it will only be kept up to date if all packages which use chdir import it from  Cwd.

Since the path separators are different on some operating systems ('/' on Unix, ':' on MacPerl, etc...) we recommend you use the File::Spec modules wherever portability is a concern.

Actually, on Mac OS, the getcwd() , fastgetcwd() and fastcwd() functions are all aliases for the cwd() function, which, on Mac OS, calls `pwd`. Likewise, the abs_path() function is an alias for fast_abs_path() .

6.  Perl System  Function

The system() function executes an operating system command by forking a child process and waiting for the child process to complete, returning some sort of exit status for the child that you can test.

The arguments to the system() function can take three forms (parenthesis optional):

1. system($STRING);

2. system($PROGRAM,  @ARGUMENT_LIST);

3. system { $PROGRAM } $FAUX_PROGRAM,  @ARGUMENT_LIST

The first form is the most commonly used. What determines which form you use (or which Perl will really use) depends on whether the command you're trying to execute contains shell metacharacters. Shell metacharacters include things like pipes, redirects and statement separators: (ps -aux | column 1 > pids); date. Specifically the characters:

& ; ` ' \ " | * ? ~ < > ^ ( ) [ ] { } $ \n \r

If the operating system command you're trying to execute uses any of these, you must use the first form, e.g:

system ("$tace < $tcmd > $tout");

In this case the sole string argument is passed to a command shell.

One key thing to remember is that once you introduce the system() function, your script is no longer portable, without modification, to Perl running under Windows and possibly other Unix operating systems.

7\. PERL Subroutines and functions

Perl subroutine or function is a group of statements that together performs a task. You can divide up your code into separate subroutines. How you divide up your code among different subroutines is up to you, but logically the division usually is so each function performs a specific task.

Perl uses the terms subroutine, method and function interchangeably. Define and Call a Subroutine

The general form of a subroutine definition in Perl programming language is as follows −

sub subroutine_name{ body of the subroutine

}

The typical way of calling that Perl subroutine is as follows − subroutine_name( list of arguments );

In versions of Perl before 5.0, the syntax for calling subroutines was slightly different as shown below. This still works in the newest versions of Perl, but it is not recommended since it bypasses the subroutine prototypes.

&subroutine_name( list of arguments );

Let's have a look into the following example, which defines a simple function and then call it. Because Perl compiles your program before executing it, it doesn't matter where you declare your subroutine.

#!/usr/bin/perl

# Function definition sub Hello{

print "Hello, World!\n";

}

# Function call Hello();

When above program is executed, it produces the following result − Hello, World!

Passing Arguments to a Subroutine

You can pass various arguments to a subroutine like you do in any other programming language and they can be acessed inside the function using the special array @_. Thus the first argument to the function is in $_[0], the second is in $_[1], and so on.

You can pass arrays and hashes as arguments like any scalar but passing more than one array or hash normally causes them to lose their separate identities. So we will use references ( explained in the next chapter ) to pass any array or hash.

Let's try the following example, which takes a list of numbers and then prints their average − #!/usr/bin/perl

# Function definition sub Average{

# get total number of arguments passed.

$n = scalar(@_);

$sum = 0;

foreach $item (@_){

$sum += $item;

}

$average = $sum / $n;

print "Average for the given numbers : $average\n";

}

# Function call Average(10, 20, 30);

When above program is executed, it produces the following result − Average for the given numbers : 20

Passing Lists to Subroutines

Because the @_ variable is an array, it can be used to supply lists to a subroutine. However, because of the way in which Perl accepts and parses lists and arrays, it can be difficult to extract the individual elements from @_. If you have to pass a list along with other scalar arguments, then make list as the last argument as shown below  −

#!/usr/bin/perl

# Function definition sub  PrintList{

my @list = @_;

print "Given list is @list\n";

}

$a = 10;

@b = (1, 2, 3, 4);

# Function call with list parameter PrintList($a, @b);

When above program is executed, it produces the following result −

Given list is 10 1 2 3 4 Passing Hashes to  Subroutines

When you supply a hash to a subroutine or operator that accepts a list, then hash is automatically translated into a list of key/value pairs. For example −

#!/usr/bin/perl

# Function definition sub PrintHash{

my (%hash) = @_;

foreach my $key ( keys %hash ){ my $value = $hash{$key}; print "$key : $value\n";

}

}

%hash = ('name' => 'Tom', 'age' => 19);

# Function call with hash parameter PrintHash(%hash);

When above program is executed, it produces the following result − name : Tom

age : 19

Returning Value from a Subroutine

You can return a value from subroutine like you do in any other programming language. If you are not returning a value from a subroutine then whatever calculation is last performed in a subroutine is automatically also the return value.

You can return arrays and hashes from the subroutine like any scalar but returning more than one array or hash normally causes them to lose their separate identities. So we will use references ( explained in the next chapter ) to return any array or hash from a function.

Let's try the following example, which takes a list of numbers and then returns their average − #!/usr/bin/perl

# Function definition sub Average{

# get total number of arguments passed.

$n = scalar(@_);

$sum = 0;

foreach $item (@_){

$sum += $item;

}

$average = $sum / $n;

return $average;

}

# Function call

$num = Average(10, 20, 30);

print "Average for the given numbers : $num\n";

When above program is executed, it produces the following result − Average for the given numbers : 20

Private Variables in a Subroutine

By default, all variables in Perl are global variables, which means they can be accessed from anywhere in the program. But you can create private variables called lexical variables at any time with the my operator.

The my operator confines a variable to a particular region of code in which it can be used and accessed. Outside that region, this variable cannot be used or accessed. This region is called its scope. A lexical scope is usually a block of code with a set of braces around it, such as those defining the body of the subroutine or those marking the code blocks of if, while, for, foreach, and eval statements.

Following is an example showing you how to define a single or multiple private variables using my operator  −

sub somefunc {

my $variable; # $variable is invisible outside somefunc()

my ($another, @an_array, %a_hash); # declaring many variables at once

}

Let's check the following example to distinguish between global and private variables − #!/usr/bin/perl

# Global variable

$string = "Hello, World!";

# Function definition sub PrintHello{

# Private variable for PrintHello function

my $string;

$string = "Hello, Perl!";

print "Inside the function $string\n";

}

# Function call PrintHello();

print "Outside the function $string\n";

When above program is executed, it produces the following result − Inside the function Hello, Perl!

Outside the function Hello, World! Temporary Values via local()

The local is mostly used when the current value of a variable must be visible to called subroutines. A local just gives temporary values to global (meaning package) variables. This is known as dynamic scoping. Lexical scoping is done with my, which works more like C's auto declarations.

If more than one variable or expression is given to local, they must be placed in parentheses. This operator works by saving the current values of those variables in its argument list on a hidden stack and restoring them upon exiting the block, subroutine, or eval.

Let's check the following example to distinguish between global and local variables − #!/usr/bin/perl

# Global variable

$string = "Hello, World!";

sub PrintHello{

# Private variable for PrintHello function local $string;

$string = "Hello, Perl!"; PrintMe();

print "Inside the function PrintHello $string\n";

}

sub PrintMe{

print "Inside the function PrintMe $string\n";

}

# Function call PrintHello();

print "Outside the function $string\n";

When above program is executed, it produces the following result −

Inside the function PrintMe Hello, Perl! Inside the function PrintHello Hello, Perl! Outside the function Hello, World!

State Variables via state()

There are another type of lexical variables, which are similar to private variables but they maintain their state and they do not get reinitialized upon multiple calls of the subroutines. These variables are defined using the state operator and available starting from Perl 5.9.4.

Let's check the following example to demonstrate the use of state variables − #!/usr/bin/perl

use feature 'state';

sub PrintCount{

state $count = 0; # initial value

print "Value of counter is $count\n";

$count++;

}

for (1..5){ PrintCount();

}

When above program is executed, it produces the following result  − Value of counter is  0

Value of counter is 1 Value of counter is 2 Value of counter is 3 Value of counter is  4

Prior to Perl 5.10, you would have to write it like this − #!/usr/bin/perl

{

my $count = 0; # initial value

sub PrintCount {

print "Value of counter is $count\n";

$count++;

}

}

for (1..5){ PrintCount();

}

Subroutine Call Context

The context of a subroutine or statement is defined as the type of return value that is expected. This allows you to use a single function that returns different values based on what the user is expecting to receive. For example, the following localtime() returns a string when it is called in scalar context, but it returns a list when it is called in list context.

my $datestring = localtime( time );

In this example, the value of $timestr is now a string made up of the current date and time, for example, Thu Nov 30 15:21:33 2000\. Conversely −

($sec,$min,$hour,$mday,$mon, $year,$wday,$yday,$isdst) = localtime(time);

Now the individual variables contain the corresponding values returned by localtime() subroutine.

*****