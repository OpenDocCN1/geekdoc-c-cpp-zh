# Creating Your Own Bullets

TABLE 8.3 List-Image-Values
| Value | Compatibility |
| --- | --- |
| <url> | IE4, FF1, S1, O3.5, CSS1 |
| none | IE4, FF1, S1, O3.5, CSS1 |
| inherit | IE7, FF1, S1, O4, CSS1 |

You're not limited to the preset bullet styles built into a browser. You can also use your graphics built from GIF, JPEG, and PNG files by applying the list-style-image property (Table 8.3).

Code 8.3 list-table-properties.css—I create a small arrow graphic A (saved as a transparent PNG) to be inserted as the bullet using list-style-image B.

To define your own graphic bullet:

```
*** CSS V5 | Chapter 8 |
list-table-properties.css ***

ul {
  list-style-type: circle;
  list-style-image: url(../images/bullet-01.png);
}
```

+   1. Add the list-style-image property to your CSS rule. Type list-style-image, followed by a colon: (Code 8.3).

list-style-image:

+   2. Specify the location of your image bullet. To include your own bullet, you have to tell the browser where your bullet graphic file is located.

url(arrow_02.png);

Type the complete Web address or relative path of the image. In this example, arrow_02.png is a local file.

Alternatively, use 'none' to override any inherited bullet images.

> Bullets are out of the layout frame by default, they may fall outside the width of the list if they are particularly long.

![](bbox=[0.135, 0.495, 0.315, 0.525])

CHARACTERS
Alice: The character has been based on Alice in Wonderland, but the little character was not based on any real child; Carroll wrote 'The White Rabbit, who was so late for a date' in 'Alice's Adventures in Wonderland'.
Alice: The Mad Hatter was made from the 'Alice' hat, and meant as a character. He talks constantly, so he imagines him in shapes.
Alice: The character of the author is a bit peculiar but not understandable; Dodgson chose the portrait to represent himself as the author, and thus used his own.
Alice: Alice is not the Caterpillar she met at first, because she does not know how to behave when appropriate; he is usually smoking, being rude, or asking difficult questions.
Alice: The Duchess is an opponent of the Queen of Hearts; it is her appears, and the Duchess is a mean character.
Alice: The Cheshire Cat: Alice first encounters the Duchess in her kitchen, and then she runs away.

> Code 8.3 applied to code 8.1: The bullet sits to the left of the text, but no padding is set, it actually goes off the edge of the page.

> Keep in mind that the text being bulleted has space for the graphic you use. A taller graphic will have more space between bulleted items, and a wider graphic will have items further to the right.

> To be honest, few developers use the list-style-image property to add padding to their designs. Most developers will use the background property with padding to get more precise styling. Want to know how to do this? Check out Chapter 17, 'Navigation, Buttons, and Controls.'

List and Table Properties 217