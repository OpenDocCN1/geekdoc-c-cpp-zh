**TIP** You can also type a space and add another text-decoration value (Table 6.13). As long as the first value is not none, you can use multiple text decorations by adding more values in a list separated by spaces, as follows: overline underline line-through

**TIP** Ding dong, the blink is dead. With CSS3, the blink value has been officially removed as a text decoration option, and the <blink> HTML tag is long gone. Now if you want to annoy your visitors with blinking text, you'll have to use Adobe Flash.

**TIP** Text decorations are applied across an entire text block element rather than on a letter-by-letter basis. This means that a child element cannot override the text decoration set by its parent.

**TIP** Although a child element cannot override its parent's text decoration, child elements can have additional text decoration added to them. In the example, notice that the emphasis tag uses strikethrough, which is added to the underlining already supplied by the paragraph tag.

**TIP** Striking through text is useful for text that you want to show as deleted. For example, I've used strikethrough in online catalogs that include sale prices. I show the original price in strikethrough with the sale price next to it. That said, using the <del> tag is a better option because it communicates deletion.

**TIP** Honestly, the only time I use text decoration is to turn off hypertext link underlining. Underlining is just too indiscriminate, placing a hard line under the text in the same color as the text. Some work is being done to provide more underline control to set the space, color, and style of the underline.

# Underlining Links?

Setting text-decoration: none; in the <a> tag overrides the underline in hypertext links, even if the visitor's browser is set to underline links. In my experience, many visitors look for underlining to identify links. Although I don't like underlining for links—it clutters the page, and CSS offers many superior alternatives—I receive angry emails from visitors when I turn off underlining.

One alternative to the text-decoration property is to use the border-bottom property with the link tag to provide faux underlining. This gives you much better control over the underline appearance, and it even allows you to use different colors.