
## A Future Value page that uses CSS

Figure 5-11 presents the design of a Future Value page that uses an external style sheet. This page works just like the Future Value page you saw back in figure 2-6 of chapter 2. Before I present the HTML and CSS code for this page, then, you might want to compare the appearance of these two pages.

First, you can see that the page that uses CSS is centered in the browser window and displayed against a shaded background. Although you can’t tell here, the page has a fixed width so the size of the page won’t change if you change the size of the browser window. In contrast, the page that doesn’t use CSS is always displayed on a white background at the left side of the browser window.

Another noticeable difference is that all of the text on the page that uses CSS is displayed in a sans-serif font. In contrast, the page that doesn’t use CSS uses the default serif font. In addition, some of the spacing on the page that uses CSS has been improved.

## The design of the Future Value page

![](img/c024ccf88e28c30c07dd410d4342288f_202_0.png)

## Description

- The Future Value page shown above is similar to the Future Value page you saw in chapter 2. However, this page uses an external style sheet for all formatting.
- The CSS for this page centers the page in the browser window; sets the font size, font family, and color for the text on the page; sets the size of the server controls; and sets the spacing for the elements.
- The CSS also positions the text to the left of the server controls and aligns the controls using a technique called floating.

## The aspx code for the Future Value form

Figure 5-12 presents the aspx code for the Future Value form. As you can tell from the link element for this form, it uses an external style sheet named Main.css. In a moment, you’ll see that this style sheet contains rule sets for each element, ID, and class that’s highlighted in this figure.

Notice here that this form doesn’t use a table to lay out the text and controls like the form in chapter 2 did. Instead, the text and controls are coded within paragraphs. Then, CSS is used to format the paragraphs and lay them out on the page. In addition, CSS is used to format several of the controls.

## The CSS for the Future Value form

```
/* The styles for the elements */
body
{
    font-family: Arial, Helvetica, sans-serif;
    font-size: 85%;
    margin: 0;
    padding: 0;
    background-color: #D3D3D3;
}
h1
{
    font-size: 140%;
    color: #0000FF;
    margin-top: 20px;
    margin-bottom: 15px;
}

/* The style for the page division */
#page
{
    width: 500px;
    margin: 0 auto;
    padding: 10px;
    background-color: White;
}

/* The style for the paragraphs that contain
the text that identifies the server controls */
.label
{
    float: left;
    width: 140px;
    margin-top: 2px;
    margin-bottom: 5px;
}
```

## Notes

- Each browser can have its own defaults for font family and font size. Because of that, you’ll want to set these properties explicitly in the style for the body element.
- You typically set the margins and padding for the body to zero so the body starts at the outer edges of the browser window. Then, if you set the left and right margins of the page division to auto, the page will be centered within the window.
- Each browser also has its own defaults for the spacing above and below headings and paragraphs. To control this spacing, you can set the margins and padding for these elements. The padding controls the space between the contents of the element and the border around it, if there is one, and the margins affect the space outside the border.
- You can use the float property to display a block element or image to the left or right of the block elements that follow it. This technique can be used to align the controls on a form without using a table.

Another rule set of note is the one for the class named validator. If you look back at figure 5-12, you’ll see that this name is coded on the CssClass attribute for each of the validation controls. This illustrates how you can apply CSS to a server control using a class.

The last five rule sets in this figure illustrate how you can apply CSS to a server control using an ID. In this case, the rule sets specify heights, widths, and margins, which is typical of the rule sets for controls. Notice that the rule sets for these controls look just like the ones for the paragraphs that are selected by ID.

You should also notice the different ways that you can code some of the properties and values. For example, the margin property for the body element specifies a single value to set all four margins to that value. In contrast, the margin property for the page division specifies two values to set the left and right margins to a different value than the top and bottom margins. You can also see two ways to set the background-color property in the body element and page division: using a color name and using a hexadecimal value. As you learn more about CSS, you’ll see that there are a variety of ways to code property values.

## The CSS for the Future Value form

```css
/* The styles for the paragraphs that contain
the server controls */
.entry
{
    margin-top: 0;
    margin-bottom: 5px;
}
.validator
{
    font-size: 95%;
    color: Red;
    margin-left: 5px;
}
#future_value
{
    height: 1em;
    font-weight: bold;
    margin-top: 0;
}
#buttons
{
    margin-top: 15px;
    margin-bottom: 0;
}

/* The styles for the server controls */
#logo
{
    width: 150px;
    height: 65px;
}
#ddlMonthlyInvestment
{
    width: 106px;
}
#txtInterestRate, #txtYears
{
    width: 100px;
}
#btnCalculate
{
    margin-right: 30px;
}
#btnCalculate, #btnClear
{
    width: 106px;
}
```

## Visual Studio features for working with CSS

Although the CSS you just saw may seem daunting, you should know that when you use Visual Studio, you don’t have to keep track of all the CSS properties that are available. Instead, Visual Studio can generate rule sets for you using a visual interface. You’ll see how that works in the next two topics. Then, you’ll learn about some additional features that Visual Studio provides for working with style sheets.

### How to work with styles from Design view

In chapter 2, you learned that you can use the Formatting toolbar to apply formatting to literal text. Now, figure 5-14 describes some additional ways to use the Formatting toolbar. It also shows how to work with margins and padding from Design view.

One way to use the Formatting toolbar is to enclose literal text within a block element. To do that, you select the text and then choose the element you want to use to format the text from the Block Format drop-down list. If a style is already defined for that element, the text is formatted according to that style. Otherwise, the default formatting for the element is applied. You can also use this technique to enclose one or more controls within a block element.

Many of the other controls on the Formatting toolbar let you apply formatting to a selected element or selected text. Depending on the selection you make and the formatting you apply, Visual Studio will either insert an inline style or add a class with a style rule that’s defined in an internal style sheet. The exception is if you apply formatting to an element for which a style rule is already defined. Then, the formatting is added to that style rule whether it’s in an internal or external style sheet. In this figure, for example, the first drop-down list (Target Rule) indicates that a style rule is defined for the h1 element in the Main.css style sheet. So any formatting that’s applied to this element will be added to the h1 style rule.

If you want to change how this works, you can do that by selecting a different option from the Target Rule drop-down list. If you want formatting to be applied as an inline style, for example, you can select the (New Inline Style) option. Or, you can select the Apply New Style option to create a new style in an internal or external style sheet as described in the next figure.

In addition to applying basic formatting to an element in Design view, you can change its margins and padding. To do that, you start by clicking on the element to select it. Then, you click on the box that appears around the element to display the margins and padding that have been applied to the element. Finally, you drag the edge of a margin to change the margin, or you press the Shift key and drag a padding edge to change the padding. In this figure, for example, you can see that I’m dragging the bottom margin of the h1 element. If you experiment with this feature, you’ll see how easy it is to use.
