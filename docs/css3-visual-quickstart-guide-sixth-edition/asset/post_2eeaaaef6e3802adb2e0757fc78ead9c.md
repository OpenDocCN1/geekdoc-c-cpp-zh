
Code 11.7 Added to visual-formatting-properties.css—When applied to Code 11.1, this CSS adds a drop shadow to the article and both a drop and inner shadow to the aside. It also adds shadows to the gallery images, but because they are clipped, they don't show up.

```
/*** visualformatting-properties.css ***/
header {
 box-shadow: 0 10px 10px
 rgba(0,0,0,.5);
}
article {
 box-shadow: 5px 5px 10px
 rgba(0,0,0,.7); }
aside {
 box-shadow: 1px 1px 5px 1px
 rgba(0,0,0,.25) inset,
 3px 3px 15px
 rgba(0,0,0,.5); }
figure {
 box-shadow: 5px 5px 10px
 rgba(0,0,0,.7); }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_324_0.png)

Code 11.7 applied to Code 11.1. The shadows add to the illusion of pages in a book, giving them a sense of weight and thickness.

- A blur length value is a positive value that increases the fuzziness of the shadow and spreads it out. The higher the value, the bigger and fainter the shadow. This value is optional but defaults to 0 when left unset.

- A spread length value—sometimes called the choke—is a positive value used to specify the break point for the shadow’s fade. It has the effect of increasing the darker area of the shadow before it begins to fade. This value is optional but defaults to 0 when left unset.

- A color value is any of the standard color values outlined in Chapter 7. This value is optional but defaults to transparent when left unset, rendering the shadow invisible.

- inset causes the shadow to appear within the element’s edges, creating an inner shadow. This is optional.

- Add more shadows as desired. 3px 3px 15px rgba(0,0,0,.5); You can repeat the shadow code as many times as desired to create multiple shadows under or within the element, separating each value list by a comma (, ) and always remembering to end your CSS rule with a semicolon (;). If only one length value is included after the x/y offset length values, it will be assumed to be the blur, not the spread.

## Box “Shadow” Effects

The box shadow can do some great effects that might all but replace the border and outline properties. Here are just a few examples that I created classes for:

### Frame

The frame effect uses drop shadows with the spread set to 0 to create a frame around the box. This has an advantage over border because you can have multiple borders, and has the advantage of the outline property in that it will not take up any space in the design.

```
.frame {
    box-shadow: 0 0 0 5px
    hsl(0,100%,0%),
    0 0 0 10px hsl(90,100%,20%),
    0 0 0 15px hsl(180,100%,40%),
    0 0 0 20px hsl(270,100%,80%),
    0 0 0 25px hsl(0,100%,80%),
    0 0 0 30px hsl(90,100%,100%); }
```

### Inset Frame

Like the frame effect, only the border is inside the element. You cannot do this with the border property.

```
.insetframe {
background: rgb(53,53,53);
box-shadow: 0 0 0 15px
hsla(0,0%,100%,.5) inset,
0 0 0 10px hsla(0,0%,100%,.5)
inset; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_325_0.png)

Using multiple Box-shadows to create a multiple border effect.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_325_1.png)

Using Box-shadows to create a transparent border inside the image.

## Code 11.8 Final visualformatting-properties.css

```
/*** visualformatting-properties.css ***/

header, footer {
    position: fixed;
    z-index: 999;
}
header {
    top: 0;
    left: 0;
    box-shadow: 0 10px 10px rgba(0,0,0,.5);
}
footer {
    bottom: 0;
    left: 0;
}
hgroup h2 {
    position: relative;
    top: 15px;
    right: 25px;
}
article {
    box-shadow: 5px 5px 10px rgba(0,0,0,.7);
}
aside {
    position: absolute;
    right: 4%;
    top: 150px;
    opacity: .5;
    clip: rect(30px 230px 60px 10px);
    box-shadow: 1px 1px 5px 1px rgba(0,0,0,.25)
    inset, 3px 3px 15px rgba(0,0,0,.5);
}
aside:hover {
    clip: auto;
    opacity: 1.0;
}
figure {
    box-shadow: 5px 5px 10px rgba(0,0,0,.7);
}
footer nav {
    position: relative;
    top: 20px;
}
strong {
    position: relative;
    top: -.15em;
}
```

## Putting It All Together

The completed code for visualformatting-properties.css should look something like Code 11.8.

## Transformation and Transition Properties

Although the use of transform and transition properties is still somewhat controversial, the ability to apply these changes to elements without using JavaScript will be a boon for Web designers and developers. Think of these as temporal styles that not only change the appearance of an element—as do other styles—but also change that element’s appearance over time and space.

The styles presented in this chapter are extremely new, at least by Web standards. Although Webkit has had them in one form or another for a while and Firefox and Opera have started adopting them, it is only recently that many of them have been added to Internet Explorer and that work has started toward making them part of the standard CSS3 canon. I’d approach these with some caution while making sure they degrade gracefully in older browsers, but I can’t wait to see how you use them.

- In This Chapter
- Getting Started 308
- Transforming an Element 311
- Adding Transitions Between Element States 320
- Putting It All Together 325

## Getting Started

For this chapter's example, I'll be using the text and images from Chapter 8 of Alice's Adventures in Wonderland (Code 12.1A), which includes several black-and-white figures that I've collected into a "gallery" so that we can play around with using transforms and transitions on them. We'll be building the CSS file transformation-transition-properties.css (Code 12.1B) in this chapter. Start out by adding a few styles that position the images in our figure (IDed as f1, f2, and f3). See the finished version of this CSS file in the section "Putting It All Together" at the end of the chapter.

### Code 12.1A The HTML5 code for Chapter 12 is similar to the previous chapter. It links to the final CSS from Chapters 5, 6, 7, 8, 9, 10, and 11, as well as a new file we will be building in this chapter called transformation-transition-properties.css.

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>Alice&#8217;s Adventures In Wonderland | Chapter VIII</title>
<link href=".../css/font-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/text-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/color-background-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/list-table-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/ui-generatedcontent-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/box-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/visualformatting-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/transformation-transition-properties.css" type="text/css" rel="stylesheet" media="all">
</head>
<body id="chapter8" class="book aaaiw chapter">
<header class="page">
<hgroup>
<h1>Alice&#8217;s Adventures in Wonderland</h1>
<h2>by <cite>Lewis Carroll</cite></h2>
</hgroup>
</header>
<article>
<h2>Chapter VIII</h2>
<span class="chaptertitle">The Queen's Croquet-Ground</span>
</article>

<p>A large rose-tree stood near the entrance of the garden: the roses growing on it were white,
but there were three gardeners at it, busily painting them red. Alice thought this a very curious
thing, and she went nearer to watch them, and just as she came up to them she heard one of them
say <q>look out now, five! Don't go splashing paint over me like that!</q></p>

...

<p>The Cat's head began fading away the moment he was gone, and by the time he had come back with
the Duchess, it had entirely disappeared; so the King and the executioner ran wildly up and down
looking for it, while the rest of the party went back to the game.</p>
<div class="gallery">
<figure id="f1" class="illo bw-illo" style="width: 300px;">
<img src=".../images/illos/p0103-image.png" width="300" height="400" alt="Playing croquet" title="" />
</figure>
<figure id="f2" class="illo bw-illo" style="width: 380px;">
<img src=".../images/illos/p0106-Image.png" width="380" height="179" alt="The Cat" title="" />
</figure>
<figure id="f3" class="illo bw-illo" style="width: 286px;">
<img src=".../images/illos/p0109-Image.png" width="286" height="300" alt="The Executioner" title="" />
</figure>
</div>
</article>
<aside>
<h2>About the Author</h2>
<p><b>Charles Lutwidge Dodgson</b> (7 January 1832 – 14 January 1898), better known by the
pseudonym Lewis Carroll was an English author, mathematician, logician, Anglican deacon and
photographer. His most famous writings are Alice's Adventures in Wonderland and its sequel
Through the Looking-Glass, as well as the poems "The Hunting of the Snark" and "Jabberwocky",
all examples of the genre of literary nonsense. He is noted for his facility at word play,
logic, and fantasy, and there are societies in many parts of the world (including the United
Kingdom, Japan, the United States, and New Zealand) dedicated to the enjoyment and promotion
of his works and the investigation of his life.</p>
</aside>
<footer>
<nav>
<a href=".../AIWL-ch07.html" class="prev">The Mock Turtle's Story</a>
<a href="...toc.html">Table of Contents</a>
<a href=".../AIWL-ch09.html" class="next">Who Stole the Tarts?</a>
</nav>
</footer>
</body>
</html>
```
