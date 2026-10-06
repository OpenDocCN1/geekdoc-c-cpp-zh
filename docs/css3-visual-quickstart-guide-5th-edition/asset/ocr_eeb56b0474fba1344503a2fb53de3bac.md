# Making HTML5 work in
Internet Explorer

Although Internet Explorer does not know
HTML5 tags, there is a partial fix (or kludge)
that involves using JavaScript to create the
HTML5 elements:

```
document.createElement('header');
```

Referred to as the "HTML5 Shiv," this will
"teach" Internet Explorer 6 (and later ver-
sions) these elements exist, and that
they should be treated as HTML tags. You
can add one of these lines of JavaScript
each of the HTML5 elements you need.

To make it simple to add these new
tags, create an external JavaScript
file (Code 2.2) and link to it from your
HTML document using the IE conditional
(Code 2.3), which you'll explore in greater
detail in 13.

Code 2.2 HTML5forIE.js This adds a blank
HTML tag for each of the HTML5 tags Internet
Explorer is missing.

```
*** CSS VQ Chapter 2 - HTML5forIE.js ***
document.createElement('abbr');
document.createElement('article');
document.createElement('aside');
document.createElement('audio');
document.createElement('bb');
document.createElement('canvas');
document.createElement('center');
document.createElement('datalist');
document.createElement('details');
document.createElement('dialog');
document.createElement('eventsource');
document.createElement('figure');
document.createElement('footer');
document.createElement('header');
document.createElement('group');
document.createElement('mark');
document.createElement('menu');
document.createElement('meter');
document.createElement('nav');
document.createElement('output');
document.createElement('progress');
document.createElement('section');
document.createElement('time');
document.createElement('video');
```

# Why Use a Doctype?

If you do not use a doctype, modern
browsers are forced into Quirks Mode.
That's a bad situation if you create-
new Web pages because it leaves
the interpretation of the code solely
to the discretion of the browsers,
which can translate into a lot of display
inconsistencies.

If you do not include the doctype in
Web page, newer browsers may not
recognize all of your code.