
## 114 Plug-In JavaScript: 100 Power Solutions

```javascript
{
  O(id).FA_Start = start
  O(id).FA_Level = start
}
```

```javascript
O(id).FA_Flag = true
O(id).FA_End = end
O(id).FA_Int = interruptible
O(id).FA_Step = end > O(id).FA_Start ? stepval : -stepval
O(id).Fadeout = end = O(id).FA_Start ? true : false
O(id).FA_IID = setInterval(DoFade, INTERVAL)
```

```javascript
function FadeOut() {
  O(id).FA_Level += O(id).FA_Step
```

```javascript
if (O(id).FA_Level >= Math.max(O(id).FA_Start, O(id).FA_End) ||
    O(id).FA_Level <= Math.min(O(id).FA_Start, O(id).FA_End)) {
```

```javascript
O(id).FA_Level = O(id).FA_End
O(id).FA_Flag = false
clearInterval(O(id).FA_IID)
  if (typeof CB != UNDEFINED) eval(CB)
}
```

```javascript
Opacity(id, O(id).FA_Level)
```

## 36 FadeOut()

This plug-in will fade out any object or objects passed to it. In Figure 5-8, each of the images has some text above it that will fade out the image below when the mouse passes over it.

![](img/95e4c43b430487125c342550cc090977_131_0.png)

FIGURE 5-8 The right-hand image has been faded out.

## Chapter 5: Visibility 115

### About the Plug-In

This plug-in will fade out an object over a period of time specified. It takes the following arguments:

- **id** An object, an object ID, or an array of objects and/or object IDs
- **msecs** The number of milliseconds the transition should take
- **interruptible** If set, the fade out can be interrupted; otherwise it cannot

### Variables, Arrays, and Functions

| Function | Description |
| :--- | :--- |
| Fade () | Plug-in to fade an object between two levels of opacity |

## How It Works

This plug-in calls the Fade() plug-in, but it requires fewer arguments. Because of the way Fade() works this plug-in also accepts an object, an object ID, or an array of objects and/or object IDs.

## How To Use It

Place a call to FadeOut() wherever you would like an object to fade out. This can be from within HTML in the form of an onmouseover or onclick event, for example, or you can place the calls within a section of a JavaScript code, as in the following:

```html
<center><br />
<span id='sp1'>Mouseover 1</span>
<span id='sp2'>Mouseover 2</span><p>
<img id='id1' src='il1.gif' />
<img id='id2' src='il2.gif' />
```

```javascript
<script>
window.onload = function () {
  O('sp1').onmouseover = function () { FadeOut('id1', 500, 1) }
  O('sp2').onmouseover = function () { FadeOut('id2', 500, 1) }
}
</script>
```

The HTML portion of this example creates two spans to accompany two images. The <script> section then attaches to the onmouseover events of each span so that the image below each will fade out if the mouse is passed over the span text.

Once an image has been faded out, you can still pass the mouse over each span and the image will then fade out. This doesn't look very good, as the images suddenly appear before fading, but it can be corrected with the following plug-in.

### The Plug-In

```javascript
function FadeOut(id, msecs, interruptible, CB) {
  Fade(id, 100, 0, msecs, interruptible, CB)
}
```

## FadeIn()

This plug-in is a simple front-end to the Fade () plug-in; it fades in an object that has previously faded out, as can be seen in Figure 5-9.

### About the Plug-In

This plug-in will fade in an object over a period of time specified. It takes the following arguments:

- **id** An object, an object ID, or an array of objects and/or IDs
- **msecs** The number of milliseconds the transition should take
- **interruptible** If set, the fade can be interrupted; otherwise it cannot

### Variables, Arrays, and Functions

| Function | Description |
| :--- | :--- |
| Fade () | Plug-in to fade an object between two levels of opacity |

## How It Works

This plug-in calls the Fade () plug-in, but requires fewer arguments. Because of the way Fade () works this plug-in also accepts an object, an object ID, or an array of objects and/or object IDs.

## How To Use It

You can use this plug-in in much the same way as the previous one: from within HTML or from a JavaScript section of code. The following example is a modified version of the previous one:

![](img/95e4c43b430487125c342550cc090977_133_0.png)

FIGURE 5-9 The right-hand image has been faded in and the left one has faded back out.

## Chapter 5: Visibility 117

this example will fade the images in and out as you pass the mouse over the Mouseover1 and Mouse 2 sections:

```html
<center> />
<span id='sp1'>Mouseover1</span>
<span id='sp2'>Mouseover2</span><p>
<img id='i1' src='i1.gif' />
<img id='i2' src='i2.gif' />

<script>
window.onload = {
  O('sp1').onmouseover = function () { FadeOut('i1', 500, 1) };
  O('sp2').onmouseover = function () { FadeOut('i2', 500, 1) };
  O('sp1').onmouseout = function () { FadeIn('i1', 500, 1) };
  O('sp2').onmouseout = function () { FadeIn('i2', 500, 1) };
}
</script>
```

The main benefit of using this plug-in with FadeOut () is that they require fewer arguments than the Fade (), in are easier to remember, and are shorter. They are also used by the next two plug-ins, which toggle an object between faded out or fade smoothly between two objects, respectively.

### The Plug-in

```javascript
function FadeIn(id, msecs, interruptible, CB)
{
  Fade(id, 0, 100, msecs, interruptible, CB)
}
```

## 38 FadeToggle

If you use this, you don't need to know the current faded out or in state of an object; it tracks the state for you and inverts whatever that state is. Figure 5-10 shows an icon of a house that is being refaded into view with this plugin.

![](img/95e4c43b430487125c342550cc090977_134_0.png)

FIGURE 5-10 The house being refaded into view.

## Chapter 5: Visibility 119

### Plug-In JavaScript: 100 Power Solutions

### About the Plug-In

This plug-in will fade in an object over a period of time specified. It takes the following arguments:

- **id** An object, an object ID, or an array of objects and/or IDs
- **msecs** The number of milliseconds the transition should take
- **interruptible** If set, the fade can be interrupted; otherwise it cannot

### Variables, Arrays, and Functions

| Function | Description |
| :--- | :--- |
| Fade () | Plug-in to fade an object between two levels of opacity |
| Fadeout | Plug-in to fade an object out |
| FadeIn() | Plug-in to fade an object in |

## How It Works

This plug-in calls the Fade () plug-in, but requires fewer arguments. Because of the way Fade () works this plug-in also accepts an object, an object ID, or an array of objects and/or object IDs.

- The plug-in calls the Fade () plug-in, but requires fewer arguments.
- Because of the way Fade () works this plug-in also accepts an object, an object ID, or an array of objects and/or object IDs.
- The plug-in calls the Fade () plug-in, but requires fewer arguments.
- The house will smoothly fade in and out because the interruptible argument is set to 1..

## How To Use It

You can use this plug-in in much the same way as the previous one: from within HTML or from a JavaScript section of code. The following example is a modified version of the previous one:

```html
<center> />
<span id='sp1'>Mouseover</span>
<span id='sp2'>Mouseover</span><p>
<img id='id1' src='id1.gif' />
<img id='id2' src='id2.gif' />

<script>
window.onload = function () {
  O('sp1').onmouseover = function () { FadeOut('id1', 500, 1) }
  O('sp2').onmouseover = function () { FadeOut('id2', 500, 1) }
  O('sp1').onmouseout = function () { FadeIn('id1', 500, 1) }
  O('sp2').onmouseout = function () { FadeIn('id2', 500, 1) }
}
</script>
```

## 39 FadeBetween()

This plug-in fades smoothly between two images in a similar manner to a fade transition in a slideshow program. 5-11 shows two overlaid images in the process of fading between each other.

![](img/95e4c43b430487125c342550cc090977_136_0.png)

5-11 The house and people icons are fading between each other.
