
20. Prefer shorthand properties. The short-hand properties, such as font, allow you to set multiple values with a single property. This not only cuts down on the amount of code, it also keeps similar property values together, making editing easier.

See “Setting Multiple Font Values” in Chapter 5.

21. Use RGB for color. You may see hex color values more often than RGB, but there is no really good reason to use one over the other from a code stand-point. Because RGB values are easier for mere mortals to understand and you can now set transparent colors using RGBA, I recommend always using RGB.

See “Choosing Color Values” in Chapter 7.

22. Use background images or other styles for interface chrome. The <img> tag should be used for images that are content: photographs, figures, or illustrations. Chrome constitutes the visual elements of the interface such as backgrounds, buttons, and other controls.

Instead of using the <img> tag to add these, interface chrome should be added using background images. This makes it easier to make changes or to completely rework the design without touching the HTML code.

See “Setting Background Images” in Chapter 7.

23. Use CSS sprites. CSS sprites can be used to add images to different dynamic states with only a single file that changes position to reveal each state. CSS sprites are faster to load than multiple images and do not flash as the states change.

See “Using CSS Sprites” in Chapter 14.

24. Use CSS for simple background gradients. Simple gradients are supported in most browsers now and can be used in backgrounds. Rather slowing things down with images, use CSS gradients.

See "Color Gradients in Backgrounds" in Chapter 7.

25. Start with a clean slate. CSS resets allow you to set a level playing field, making it easier to design across multiple browsers.

See "Using CSS Reset" in Chapter 13.

26. Favor margin over padding. Due to problems with Internet Explorer and the box model, padding can cause problems with elements that have a width or height. If you have a choice, use margin.

See "Adjusting CSS for Internet Explorer" in Chapter 13.

27. Test your code in Firefox, Chrome, and/or Safari while building, and then fix it for Internet Explorer. Although IE still has the lion's share of the browser market, it's easiest to build a site to Web standards, and then accommodate for IE's idiosyncrasies rather than the other way around.

See "Adjusting CSS for Internet Explorer" in Chapter 13.

28. Style all link states. Many designers will style only the default link state and maybe the hover state. However, you can also style visited and active states, which provide visual feedback to the user when clicking a link.

See "Styling Links Versus Navigation" in Chapter 14.

29. Use comments to keep notes and organize your code, especially for constant values. Notes are helpful for recording notes about your design, especially in color or font values that you will be using consistently throughout your design. Notes can also be used to create section dividers in your code to help organize and make scanning for particular parts easier.

See "Creating Readable Style Sheets" earlier in this chapter.

30. Use specificity to organize your code.
Specificity is not just a great idea for styling; you can use it to create an outline-format for your code, making it easier to scan and find related elements.

See "Creating Readable Style Sheets" earlier in this chapter.

31. Favor <link> over @import. Although both can be used to bring style sheets into Web documents, tests have shown that most browsers will link style sheets faster than imported ones. This is even true if the @import is in an external style sheet because the parent external style sheet has to be loaded before its children are considered.

See "Style Sheet Strategies" earlier in this chapter.

32. Minify your CSS before you launch.
Mean and lean code leads to faster download speeds, which always make for a better user experience. While you are developing your site, your code should be as readable as possible. But when you launch the site, you can remove all spaces, returns, and notes from your code.

See "Minifying Your CSS" earlier in this chapter.

# CSS Quick Reference

Throughout this book, wherever new properties were introduced, I included a table showing the values for property and the specific browser version in which support first appeared. But for quick reference, use the tables below. The tables show whether a property or selector is supported in Internet Explorer, Firefox, Chrome, and Opera. A checkmark indicates support.

## Appendix

| Type | IE | FF | C | O |
| :--- | :--- | :--- | :--- | :--- |
| Basic Selectors | | | | |
| Type | | | | |
| .class | | | | |
| #id | | | | |
| Contextual | | | | |
| * | | | | |
| Child | | | | |
| Adjacent Sibling | | | | |
| General Sibling | | | | |
| [ATTR] | | | | |

| Pseudo-Classes | IE | FF | C | O |
| :--- | :--- | :--- | :--- | :--- |
| :active | | | | |
| :hover | | | | |
| :focus | | | | |
| :link | | | | |
| :target | | | | |
| :visited | | | | |
| :root | | | | |
| :empty | | | | |
| :only-child | | | | |
| :only-of-type | | | | |
| :first-child | | | | |
| :nth-child(n) | | | | |
| :nth-of-type(n) | | | | |
| :nth-last-of-type(n) | | | | |
| :last-child | | | | |
| :first-of-type | | | | |
| :lang() | | | | | |
| :not(s) | | | | |

| Pseudo-Elements | IE | FF | C | O |
| :--- | :--- | :--- | :--- | :--- |
| ::first-letter | | | | | |
| ::first-line | | | | | |
| ::after | | | | | |
| ::before | | | | | |
