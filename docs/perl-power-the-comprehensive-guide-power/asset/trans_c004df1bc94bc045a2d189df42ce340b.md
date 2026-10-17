

# 第 10 章 控制结构

> 她欲望的无休止是灵魂永恒的预兆。
> 
> 奥菲克箴言

```perl
#2 Split the text at numbers
@ABAlcott = split(/\d\.\s/, $OrphicSayings);

#3 Set up strings for display
# Create random numbers

$Title = "
Orphic Sayings";
$Author = "\nAmos Bronson Alcott 1799-1888";
$Source=
"\nPerry Miller, ed. The American Transcendentalists"
"\n(Baltimore: Johns Hopkins U. Press, 1957), pp. 86-88.";

$Str = 0;
$Str = 1 + int(rand(6));
print "\n(---)" . $Str;

#4 Various forms of selection statement
# Compounded

if($Str != 2 && $Str != 4){
    print "\n(***)" . $Author . $Title . "\n"
        . $ABAlcott[$Str] . "\n" . $Source;
}
#5 valuation of equality

if($Str == 2){
    print "\n(**)" . $Author . $Title . "\n"
        . $ABAlcott[$Str] . "\n" . $Source;
}

#6 Compound: less than greater than
if($Str > 3 && $Str < 5)
```

# The unless Structure

The `unless` selection statement tests for a negative condition. Whereas the `if` statement processes statements in its block when an expression is true, the `unless` statement processes statements only when the expression is *not* true. Listing10_08 provides an example of the use of `unless` to provide a slightly different appearance for quotes from Henry D. Thoreau’s *Walden*.

```perl
#Listing10_08
#1 block containing text
$Itr = 1;
($WaldenLines=<<WALDENLINES);
1. The mass of men live lives of quiet desperation.
2. Most of the luxuries, and many of the so-called
comforts of life, are not only not indispensable,
but positive hindrances to the elevation of mankind.
3. Every child begins the world again, to some extent,
and loves to stay outdoors, even in wet and cold.
4. If I knew for a certainty that a man was coming to
my house with the conscious design of doing me good,
I should run for my life . . . .
5. The heroic books, even if printed in the character
of our mother tongue, will always be in a dead
language to degenerate times . . . .
6. No man ever followed his genius until it misled him.
WALDENLINES

#2 Split the text at numbers
@HDThoreau = split(/\d\.\s/, $WaldenLines);

#3 Set up strings for display
```

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_264_0.png)

**Figure 10.10**  
Different expressions embedded in `if` selection statements allow you to display a range of six items.

```perl
# Create random numbers
$Author = "\nHenry D. Thoreau 1817–1862";
$Source=

"\nHenry D. Thoreau, Walden " .
"\n(Philadelphia: Courage Press, 1990).";

$Itr = 0;
$Itr = 1 + int(rand(6));
print "\n(---)" . $Itr;

#4 Various forms of selection statement

#Can be 1 2 3
unless($Itr == 6 || $Itr == 5 || $Itr == 4){
    print "\n(***)" . $Author . "\n"
          $HDThoreau[$Itr] . "\n" . $Source;
}
#5 valuation of equality
#It can be 4 5 6
unless($Itr == 1 || $Itr == 2 || $Itr == 3){
    print "\n(**)" . $Author . "\n"
          . $HDThoreau[$Itr] . "\n" . $Source;
}
```

At comment #1 in Listing10_08, you set up a block of text and assign it to a scalar, `$WaldenLines`. Six quotes from Thoreau’s *Walden* appear in the block. A number, a period, and a space separate them from each other. At comment #2, you use the `split()` function to separate the quotes in the text into elements of an array (`@HDThoreau`). The first argument of the `split()` function designates the criteria you want to use to separate a body of text into segments. In this case, you provide a regular expression (`/\d.\s/`), which designates that whenever the function finds a number (`\d`), any character (`.`), and a blank space (`\s`) together, it should break the text.

The lines associated with comment #3 define scalars to identify the author and his work and then generate a random number using the `rand()` function. The `rand()` function generates a range of numbers that is greater than or equal to zero and less than the number you supply as an argument to the `rand()` function. For this reason, you “shift” the value by one, so the range becomes 1 to 6. You do not need 0 because the 0 index of the `@HDThoreau` array holds no data.

# 第 10 章 控制结构

In the lines trailing comment #4, you set up two `print()` functions. The print functions possess slightly different adornments. The user of the program sees different adornments, depending on where the quote lies in the `@HDThoreau` array. The first `unless` selection statement determines that unless the number of the quote lies in the range of 4, 5, and 6, you see vertical lines, as Figure 10.11 shows. The second `unless` selection statement excludes the range of 1, 2, and 3. If you execute the program several times, you can see the adornments change.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_266_0.png)

# The if...else Selection Structure

The if...else selection structure accommodates exclusive choices. You can use it to make one choice or another. To make a choice, you set up one condition. If the condition proves true, then the selection statement directs the flow of the program to the primary `if` block. If the condition does not prove true, then the statement directs the flow to a catch-all `else` block. No conditional expression governs the `else` portion of the structure. Listing10_09 explores the use of the if...else selection structure, but it adds to the basic use by embedding a second if...else selection structure in the first if...else selection structure.

```perl
#Listing10_09
#1 Generate a random number
#convert it to a character
$Itr = 0;
$Itr = 1 + int(rand(3));
$Itr += 96; #Make it 97, 98, 99;
$Char = sprintf("%c", $Itr);
#2 Set up two strings with the names of poems
#Ralph Waldo Emerson
$RWE = join("\n ", " Ralph Waldo Emerson",
"The Apology", "Uriel", "Destiny",
"Each and All", "The Eternal Pan",
```

246

TEAM LinG

```perl
"Hamatreya", "Earth-Song", "Brahma");
#Henry D. Thoreau
$HDT = join("\n " , " Henry D. Thoreau ",
 "Sympathy ", "Sic Vita",
 "Friendship", "Prayer",
 "Independence", "The Inward Morning",
 "My Love Must Be as Free");
#Sarah Margaret Fuller
$SMF = join ("\n " , " Sarah Margaret Fuller ",
 "Encouragement" , "Dryad Song",
 "The Highlands", "Winged Sphinx",
 "The Passion-Flower");
#3 Make an exclusive choice with an embedded
# selection statement and print
if($Char eq 'a'){
 $ToPrint = $RWE;
}
else{
 if($Char eq 'b'){
 $ToPrint = $SMF;
 }
 else{ #only with c
 $ToPrint = $HDT;
 }
}
print "\n(" . $Char . ")". $ToPrint;
```

The lines in Listing10_09 that comment #1 identifies generate a random number each time the program executes. The number falls in a range that extends from 1 to 3, and you add 96 to it so that the three resulting integer possibilities are 97, 98, and 99. As is discussed in Chapter 5, these three values represent the ASCII values for lowercase “a,” “b,” and “c.” To convert the numbers to characters, you use the sprintf() function and the %c type specifier. You assign the resulting letter to a scalar, $Char.

In the lines associated with comment #2, you create three strings using the join() function. The strings identify one of three Transcendentalist poets, Emerson, Fuller, or Thoreau, and then name a few of their poetical works. For the first argument of the join() function, you designate

# 第 10 章 控制结构

the character you want to use to separate items as the function concatenates them into a string.
You assign a new line character to this argument.

At comment #3 you set up an if...else selection statement. The control expression for the
if statement tests $Char for the letter a. If the expression evaluates to true, then inside the
if block, you assign the string that stores information related to Emerson ($RWE) to another
scalar, $ToPrint. The flow of the statement then exits the conditional blocks, and the next
statement it encounters is the print() function. The print() function prints the string you
have assigned to $ToPrint.

If the evaluation of $Char for the letter a renders a false outcome, then the flow of the program
passes to the else block. When the flow enters this block, another if...else selection statement awaits it. This time $Char is evaluated in relation to b. If the evaluation results in true,
then information on Margaret Fuller is assigned to $ToPrint, and as you see in Figure 10.12,
her name and the list of her works appear as the program’s output.

The else block of the embedded loop accepts the program flow whenever the control expression of the embedded if selection renders false. Only the third value (c) causes this to occur.
With this occurrence, as Figure 10.12 illustrates, you see the information on Thoreau appear as
output.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_268_0.png)

# The if...elseif...else Statement

When you use the if...elseif...else selection statement, it is important to notice that the
spelling of the middle term is “elseif” rather than “else if.” Likewise, the terminating statement
is spelled “else.” This is known as a cascading or multiple-case selection structure. The structure
works on a fairly efficient basis. The flow of the program enters the if statement that heads the
structure. If the control expression evaluates to true, then the first block executes. Following
this, the flow of the program exits the structure completely.

If the first evaluation renders a false outcome, then the flow of the program passes to the first
elseif control statement. If this proves true, the statements in this first block are executed.
When this activity concludes, the flow of the program exits the structure completely.

You set up only one if statement in the structure. You likewise set up only one else statement.
The else statement is a default condition. Since it does not support an evaluation expression,

