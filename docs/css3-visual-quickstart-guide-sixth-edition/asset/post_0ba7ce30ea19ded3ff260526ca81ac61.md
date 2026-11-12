
## Graceful degradation

This means that you can use styles like border-radius, box-shadow, text-shadow, and others that may not work in older browsers, as long as they do not prevent the user from using the site and all of its functionality when they do not appear. The design may not look equally polished in all situations, but the site still performs all necessary tasks.

Graceful degradation might require you to use conditional styles for older versions of Internet Explorer, but generally, it should not take nearly as much extra work as pixel perfection.

## Why should I use progressive enhancement?

Pixel perfection has a strong track record in Web design, and it may take a while to convince clients and other teammates that progressive enhancement is a better way. However, I generally find these arguments do the trick:

- **Faster to develop**—Rather than spending time kludging together a bunch of images for rounded corners, drop shadows, and other effects, a few lines of code take care of it all.
- **Cheaper to maintain**—Changing code is much more cost effective than reworking, recutting, and redeploying images.
- **Better looking**—Since the styles are native to the browser, they will display more precisely than images that are shoehorned in.

If these arguments don't sway your client, then compare a budget for designing with progressive enhancements to a pixel perfect budget. Usually the relative costs will convince even the most stubborn client to approve progressive enhancement.

## A Multi-Screen Strategy?

The world of Web design is becoming an increasingly complex place to live. Just as computer screens get larger, browsers get more consistent, and connection speeds get faster, the landscape is undergoing a seismic shift to accommodate the smaller screens and slower speeds of mobile devices. The number of different screen sizes and resolutions is constantly growing. I won’t even bother to list the most common mobile devices in this book, because they will probably change between now and the time the book is published.

So what’s a designer to do? You need to develop a multi-screen strategy, ensuring that your audience gets the best experience, regardless of what device is being used. There are several strategies you could deploy, but one is the clear leader:

- Mobile app: You could build separate applications to run on the various devices. Unfortunately, since each device will require separate design and development, this can get expensive, or require you to ignore possible users.
- Mobile site: You can build a site—with a separate URL—customized for mobile devices. Generally, these are built separately from the general Web site, take more design and development time, and are generally designed for the lowest-level browser.
- Responsive design site: You can build a site that adapts to its environment using media queries. It may require a little extra work to adapt the design to different “break points,” but these sites will likely run efficiently on the widest number of devices.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_378_0.png)

The Solar Energy Industries Association uses a responsive design multi-screen strategy that allows the same Web page to appear optimally across a wide range of screen sizes and user contexts.

Of these three strategies, responsive design is the most promising. It uses the same HTML files for all browsers, then applies progressive enhancement to tweak the design for each device.

Responsive design works simply by using CSS media queries to ask the device about its specific properties, and then delivering styles to tailor the HTML being displayed to best fit the environment it is being presented in.

## Resetting Browser Default Styles

In Chapter 2, you learned about browser default styles. Recall that browser developers set the default styles applied by HTML tags. Before you get too far into the responsive design weeds, start by resetting those default styles to make sure they are the same regardless of the browser you are designing for.

Far too many Web sites are designed by default. The designers and developers allow the browser to have the final word on how the content is displayed. Additionally, all browser default styles are not the same. CSS resets were developed to level the playing field and help prevent “vanilla” designs.

The exact CSS reset you choose will depend on your design needs. I like to keep my reset simple, adding styles to specific tags only as needed. However, several styles are inconsistent or (in my opinion) poorly set in most browsers.

Redefining important CSS properties (generally to none or 0) provides a few benefits:

- Reduces bad styles. Undoes some of the questionable and downright annoying styles added by browsers, and eliminates the styles that simply do not work. One example is using an outline to highlight items that are in focus, such as form fields. Although highlighting is useful for keyboard navigation, you should design this yourself.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_379_0.png)

A page with no CSS applied.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_379_1.png)

The same page with the simple reset applied.

- **Eliminates design by default.** Sets a level playing field from which to begin a design. Rather than allowing the browser to dictate your page appearance, you take control.

- **Makes browser styles consistent.** Ensures that values across all browser types and versions are the same. Because browsers slightly vary their default style values, a good reset will allow your designs to appear with greater consistency regardless of how your visitor is viewing it.

To use a CSS reset, simply add the desired code at the very top of your CSS code. That's it. The code does the rest.

### What Should You Reset?

As a designer, I recommend resetting many of the typographic and box styles and then setting your own defaults. In addition to not allowing the browser to set the direction, another good argument for resetting styles is that different browsers have slightly different values.

- **Padding, borders, and margins**—These are the main styles that designers like to reset, largely because they vary so much from browser to browser.

- **Text underlining**—Never use the `text-decoration` property to underline text. I have never seen a design in which underlining did anything other than add visual noise, even for links. Instead of using `underline`, apply `border-bottom` to achieve a similar effect with more precise control that allows you to specify the thickness, color, and line style of the underline.

- **Line height**—The default value for line height on text is 1em, which means that the text has little or no breathing room. All text can benefit by bumping this up to at least 1.4em.

- **Outline**—Outlines are applied by some browsers to highlight elements, such as form fields, when they come into focus. Although this is a good idea for accessibility reasons, the nature of this highlight should be up to you, not the browser.

- **Vertical alignment**—Vertical alignment is tricky to deal with and rarely works the way you expect. The best procedure is to set the vertical alignment to the baseline and then use relative positioning to move elements up or down manually.

- **Other**—These are the basics, but most CSS resets will go beyond this, cleaning up other perceived problems, generally with specific tag implementation.

### A simple CSS reset

The easiest way to reset styles is to use the universal selector and set the default styles you want applied to all tags, as shown in Code 14.2. Remember that you want to keep your CSS reset compact. Code 14.3 does the same thing but removes all spaces and returns.

This is a quick way to reset the most important styles, but it has one drawback: IE6 does not recognize the universal selector. If you are concerned about supporting IE6, you will want to include all the HTML tags in the selector list. The advantage of using the universal selector, other than compactness, is that it will always apply itself to new HTML tags as they become available.

Code 14.2 cssreset-simple.css—This version of the CSS uses the universal selector to reset the browser default values of several key properties, including margin, padding, border, outline, line-height, vertical-align, and text-decoration.

```css
/*** cssreset-simple.css ***/
* { margin: 0;
   padding: 0;
   border: 0;
   outline: 0;
   font-size: 100%;
   font-style: normal;
   font-weight: normal;
   line-height: 1;
   vertical-align: baseline;
   text-decoration: none; }
```

Code 14.3 cssreset-simple.css—The same code as Code 14.2, but compressed by removing all line breaks and spaces.

```css
/*** cssreset-simple.css ***/
*{margin:0;padding:0;outline:0;font-size:100%;font-style:normal;font-weight:normal;line-height:1;vertical-align:baseline;text-decoration:none;}
```
