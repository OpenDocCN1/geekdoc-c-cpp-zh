
*If you want to compare floating point values subtract them and see if the difference is very small.*

`==`

**equals.** If the left hand side and the right hand side are equal the expression has the value true. If they are not equal the value is false.

`4 == 5`

- would evaluate to false. Note that it is not particularly meaningful to compare floating point variables to see if they hold exactly the same values. Because of the fact that they are held to limited precision you might find that conditions fail when they should not for example the following equation:

`x = 3.0 * (3.0 / 3.0) ;`

- may well result in x containing 0.9999999, which would mean that:

`x == 1.0`

- would be false - even though mathematically the test should evaluate to true.

`!=`

**not equal.** The reverse of equals. If the operands are not equal the expression has the value true, if they are equal it has the value false. Again, this test is not advisable for use with floating point numbers.

`<`

**less than.** If the operand on the left is less than the one on the right the value of the expression is true. If the left hand operand is larger than or equal to the right hand one the expression gives false. It is quite valid to compare floating point numbers in this way.

`>`

**greater than.** If the operand on the left is greater than the one on the right the result is true. If the operand on the left is less than or equal to the one on the right the result is false.

`<=`

**less than or equal to.** If the operand on the left is less than or equal to the one on the right you get true, otherwise you get false.

`>=`

**greater than or equal to.** If the operand on the left is greater than or equal to the one on the right you get true, otherwise it is false.

`!`

**not.** This can be used to invert a particular value or expression, for example you can say !true, which is false, or you could say: `!(x==y)` - which means the same as `(x!=y)`. You use not when you want to invert the sense of an expression.

## Combining Logical Operators

Sometimes we want to combine logical expressions, to make more complicated choices, for example to test for a window width being valid we have to test that it is greater than the minimum and less than the maximum. C# provides additional operators to combine logical values:

`&&`

**and.** If the operands each side of the && are true the result of the && is true. If one of them is false the result is false, for example

```
(width > 0.5) && (width < 5.0)
```

- this would be true if the width was valid according to our above description. I've put brackets around each of the conditions in this example, so that it is easier to see what is going on. However, the compiler is able to work out that the && needs to be applied between the result of the two logical expressions, so they are not actually required.

`||`

> De Morgan's theorem is the basis of this.

**or.** If either of the operands each side of the || are true the result of the expression is true. The expression is only false if both operands are false; for example:

```
width <= 0.5 || width >= 5.0
```

- this would be true if the width was invalid. We are saying that the width is invalid if it is less than the minimum or larger than the maximum. Note that to reverse the sense of the condition (i.e. true when the value is invalid) we not only have to change the > into <= in each expression, but also change the && into an ||.

Using these operators in conjunction with the if construction we can make decisions and change what our program will do in response to the data we get.

### Programmer's Point: Break down your conditions

If you find that you are making huge and complicated conditions to get a statement obeyed you might find that you can make things clearer by using more than one if statement, and indenting the code in an appropriate way. This will make the code easier to debug as well, because you can watch the program step through your conditions one at a time, instead of going off in a particular direction based on a huge condition you will then have to unpick.

### Using Blocks to Combine Statements

We have decided that if the user gives a value outside our allowed range an error is generated and the value is then set to the appropriate maximum or minimum. To do this we have to do two statements which are selected on a particular condition, one to print out the message and the other to perform an assignment. You can do this by using the { and } characters. A number of statements lumped together between { and } characters is regarded as a single statement, so we do the following:

```
if ( width > 5.0 )
{
    Console.WriteLine ("width too big, using maximum\n") ;
    width = 5.0 ;
}
```

The two statements are now a block, which is performed only if width is greater than 5.0. You can lump many hundreds of statements together in this way, the compiler does not mind. You can also put such blocks of code inside other blocks, this is called nesting.

The number of { and } characters must agree in your program, otherwise you will get strange and incomprehensible errors when the compiler hits the end of the file in the middle of a block or reaches the end of your program half way down your file!

### Programmer's Point: Use Layout to Inform the Reader

I make things much easier to understand by indenting a particular block by a number of spaces, i.e. each time I open a block with the { character I move my left margin in a little way. I can then see at a glance whereabouts I am in the levels at any time. This is what proper programmers do.

### Metadata, Magic Numbers and const

A magic number is a value with a special meaning. It will never be changed within the program; it is instead a constant which is used within it. When I write my glazing program I will include some magic numbers which give the maximum and minimum values for heights and widths. These come from the *metadata* I was so careful to gather when I wrote the specification for the program.

Now I could just use the values 0.5, 5.0, 0.75 and 3.0 - but these are not packed with meaning and make the program hard to change. If, for some reason, my maximum glass size becomes 4.5 metres I have to look all through the program and change only the appropriate values. I do not like the idea of "magic numbers" in programs. What I would like to do is replace each number with something a bit more meaningful.

We can do this by making a variable which is constant, i.e. it can never be changed.

```
const double PI=3.141592654;
```

This means that you can do things like:

```
circ = rad * 2 * PI ;
```

This is both more meaningful (we are using PI not some anonymous value) and makes the program quicker to write. Anywhere you use a magic number you should use a constant of this form, for example:

```
const double MAX_WIDTH = 5.0 ;
```

This makes your programs much easier to read, and also much easier to change.

There is a convention that you always give constant variables names which are expressed in CAPITAL LETTERS. This is so that when you read your program you can tell which things have been defined.

We can therefore modify our double glazing program as follows:

```csharp
using System;

class GlazerCalc
{
    static void Main()
    {
        double width, height, woodLength, glassArea;

        const double MAX_WIDTH = 5.0 ;
        const double MIN_WIDTH = 0.5 ;
        const double MAX_HEIGHT = 3.0 ;
        const double MIN_HEIGHT = 0.75 ;

        string widthString, heightString;

        Console.Write ( "Give the width of the window : " );
        widthString = Console.ReadLine();
        width = double.Parse(widthString);

        if (width < MIN_WIDTH) {
            Console.WriteLine ( "Width is too small" );
            Console.WriteLine ( "Using minimum" );
            width = MIN_WIDTH ;
        }

        if (width > MAX_WIDTH) {
            Console.WriteLine ( "Width is too large.\n\n" );
            Console.WriteLine ( "Using maximum" );
            width = MAX_WIDTH ;
        }

        Console.Write ( "Give the height of the window : " );
        heightString = Console.ReadLine();
        height = double.Parse(heightString);
```
