
## 4 Obtaining References to DOM Elements

Grabbing elements on a page and “traversing” the DOM (moving around from one element to another) are two cornerstones of any web page scripting. Although the grabbing part is finally being addressed properly in latest crop of browsers—it took more than a decade, though!—DOM walking without libraries remains an incredible mess. That’s why we all use one library or another, either consistently or on a per-project basis.

There are only a few points I’d like to touch on here.

First, be warned that all code relying on document.getElementById falls victim to IE’s unbelievable quirk. It will look into any and all name attributes, too. Now, if you work with strict DOCTYPES (which you should!), this seems to only mean “Beware of field names!” That’s because you unconsciously rule out the <head> and its <meta> tag’s name= attribute. So, what happens when you unwittingly define an element with an id= of description or keywords and you try to grab it? You get the <meta> element instead of your intended target! So, just avoid these id values.

On the facing page, I mention that most techniques for selecting elements let you specify a context node or root node, which acts as root element within which to perform the selection. By default, that context is the whole document. If you look at API docs for utilities such as $(), query(), jQuery’s all-purpose $(…), and the like, you’ll always find an optional argument (usually the second one) that lets you pass your context element. Remember that the narrower the search, the faster the selection!

Finally, the bare-bones DOM API is not well suited to common moving-around use cases, because it works with nodes, not elements. You get bogged down in whitespace, comments, text nodes, and so on. This is why most libraries provide nifty, element-oriented helpers. Prototype, jQuery, and MooTools provide a rich API, with previous() (or prev()), next(), siblings(), ancestors(), and the like, or get-prefixed versions of these. The YUI 3 API is slightly less rich. Dojo and Ext JS seem to lack this cores.

Most libraries support ID- and CSS3-based selections.

### Grab an element by its ID.

```
document.getElementById('elementId')  // Plain W3C DOM
$('elementId')                     // Prototype, MooTools
$('#elementId')                    // jQuery
Y.one('#elementId')                // YUI 3
dojo.byId('elementId')             // Dojo
Ext.getDom('elementId')            // Ext JS 3
```

### Grab elements by XPath/CSS selection.

Supported syntaxes vary depending on the library, and the W3C Selectors API is available (but blazingly fast) only in recent-enough browsers: Firefox 3.1+, Safari 3.1+, IE8+ (standards mode), Chrome, and Opera 10+.

Also, note that all libraries provide some way to specify the context, the root node within which to explore (by default the entire document). Narrowing the context down whenever possible speeds up your code and reduces memory usage.

```
document.querySelectorAll('selectors')  // Native (see above)
$$('selectors')                        // Prototype, MooTools
someRootElement.select('selectors')    // Prototype
$('selectors')                         // jQuery
Y.all('selectors')                     // YUI 3
dojo.query('selectors')                // Dojo
Ext.query('selectors')                 // Ext JS 3
```

### Move around (DOM traversals).

Here are a couple of quick Prototype-based examples. For context and extra information, check out the facing page.

```
// From element with id=some..., get the nearest <h2> container with class
// "category", then walk along its later sibling elements until one has a
// "summary" class.
$('someDeeplyNestedElement').up('h2.category').next('.summary');

// Set the text-indent CSS property for every immediate container of
// links with a "sifr" class.
$$('a.sifr').invoke('up').invoke('setStyle', 'text-indent: -9999px');
```

## 5 Dynamically Styling Content

The ability to get the current value (specified or computed) of a CSS property for an element—and even more importantly to *change* that styling—is of paramount importance when creating a web UI. Unfortunately, browsers and W3C specs leave us pretty much in the dark here. All libraries provide more or less the same API, as you can see on the facing page.

The answer, for dynamic styling, is to use *classes*.

Being able to tweak styles manually is useful for developing your own visual effects, but that’s an exercise best left to library authors and JavaScript ninjas. I believe that you, as a front-end developer, should cleanly separate the specific styling from your JavaScript code and rely only on toggling CSS class names for your own stuff and built-in effects provided by your library of choice.

Indeed, all libraries provide a uniform API to add, remove, and check the presence of CSS class names from an element. MooTools, jQuery, YUI, Dojo, and Ext all use `addClass()`, `hasClass()`, `removeClass()`, and `toggleClass()`. Prototype just appends a Name suffix to those (that is, `hasClassName()`).

*But don’t forget the shortcuts!*

All libraries provide various shortcuts for common use cases, both on the get and the set sides, such as visibility (hide/show/toggle), opacity (as per CSS’s spec, even on IE), dimensions, and so on. Check the docs—the method names are often obvious.

## 6 Changing an Element’s Contents

You may ask, why not just use innerHTML to change an element’s contents?

It is often tempting to just go and assign the desired markup to the innerHTML property of the container element. Indeed, this orders of magnitude faster than other methods. However, on many browsers, innerHTML chokes on various bits of markup. Libraries switch to other mechanisms (such as manual DOM building or markup preprocessing) when necessary. When dealing with content injection instead of full-on replacement—or when the markup includes inline scripts, as discussed a couple paragraphs later—using libraries also proves easier, more concise, and less error-prone than manually tweaking markup.

Be careful not to confuse updating with replacing. Most methods do updating by default—for example, the only position for dojo.place(). Updating changes the inside of the element, but replacing changes the element itself, thereby invalidating its ID and any event listeners attached to it. It is equivalent to setting the outerHTML property, when available.

Fortunately, several libraries provide a wealth of special-case methods supplementing the basic update/insert need, such as element wrapping, selector-based multiple-element operations, cleanup of superfluous empty text nodes, and the like. Be sure to check your preferred library’s API documentation for details.

But if you’re injecting <script> tags, watch out! By default, embedded <script> tags in natively injected markup will not run, and this is sometimes an issue. Whenever you can, work around this by leveraging event delegation. But this need is common enough that several libraries specifically address it:

- Prototype actually runs inline <scripts> by default in update(), replace(), and insert(). (For Ajax updates, you’ll need to set the evalScripts option to true.)
- jQuery’s html() method also runs inline scripts by default.
- Ext’s update() method accepts a second argument that, when true, runs inline scripts.

These script runnings sometimes operate within a special evaluation context for security purposes. Check out your preferred library’s documentation for details.

> See Task 9, Leveraging Event Delegation, on page 36 for details.

### Update the entire contents of an element.

// Prototype
$(element).update('<p>new internal HTML</p>')
$(element).replace('<p>This will replace the element itself</p>')

// jQuery
$(element).html('<p>new internal HTML</p>')
$(element).text('The <div> and <span> elements carry no inherent semantics.')

// MooTools
$(element).set('html', '<p>new internal HTML</p>')
$(element).set('text', 'The semantics of << and >> varies across languages.')

// YUI 3
Y.one('#id').setContent('<p>new internal HTML</p>')

// Dojo
dojo.place('<p>new internal HTML</p>', element, 'only')
dojo.place('<p>This will replace the element itself</p>', element, 'replace')

// Ext JS
Ext.get(element).update('<p>new internal HTML</p>')

Notice how jQuery and MooTools have special updaters that will escape whatever tags are present in the passed text, this is handy when trying to actually display code.

### Inject extra contents into an element.

// Prototype. Positions: 'before', 'top', 'bottom', 'after'
$(element).insert('<p>This gets at bottom</p>')
$(element).insert({ pos: 'markup', pos2: 'markup2...' })
// jQuery (many more methods available)
$(element).before('<p>This gets before the element</p>')
$(element).prepend('<p>This gets at top</p>')
$(element).append('<p>This gets at bottom</p>')
$(element).after('<p>This gets after the element</p>')
// YUI 3
Y.one('#id').prepend('<p>This gets at top</p>')
Y.one('#id').append('<p>This gets at top</p>')
Y.one('#id').insert('<p>This gets where told</p>', nextChildElement)
Y.one('#id').insert('<p>This gets where told</p>', childIndex)
// Dojo. Positions: 'before', 'first', 'last', 'after'
dojo.place('<p>This gets where told</p>', element, pos)
// Ext JS. Positions: 'beforeBegin', 'afterBegin', 'beforeEnd', 'afterEnd'
Ext.get(element).insertHtml(pos, '<p>This gets where told</p>')

- Task 5, Dynamically Styling Content, on page 28
