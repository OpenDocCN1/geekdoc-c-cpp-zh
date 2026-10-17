# Substituting

The substitution function allows you to replace a given expression with another expression. The most elementary approach to using the substitution function involves substituting one word for another. The basic substitution function replaces the first occurrence of a term you identify. As the example in Listing15_02 shows, you name the expression you want to replace in the first part of the expression. You name the replacement term in the second. Here is the example:

```
```perl
#Listing15_02
$TestStringA = "Say hello to the world.";
$ResultString = $TestStringA;
$ResultString =~ s/hello/your greetings/;
print("Result: $ResultString $NL");
```
```

The output appears as follows:

```
```text
Result: Say your greetings to the world.
```
```

You can use the substitution statement as you traverse a string with a repetition control statement. As Example 2 in Listing15_02 shows, you can employ a repetition statement to traverse a string and sequentially alter words in the string.

```
```perl
$ResultString = "Tell me about the world as a world in the world";
$Count = 1;
do{
        print("$ResultString $NL");
        $ResultString =~ s/world/planet/;
        $Count++;
}while($Count < 5);
```
```

The output of Example 2 shows you how the substitution function alters a new term with each repetition of the block:

```
```text
Tell me about the world as a world in the world
Tell me about the planet as a world in the world
Tell me about the planet as a planet in the world
Tell me about the planet as a planet in the planet
```
```

# Global Changes

The g (global) argument provides an alternative to using a repetition control structure. It detects all instances of the terms you have designated for substitution and changes them. Example 3 in Listing15_02 explores both how to use global substitution and how to obtain the number of substitutions the function performs: