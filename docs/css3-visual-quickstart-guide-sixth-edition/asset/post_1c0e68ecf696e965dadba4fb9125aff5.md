
## Setting Alpha Values for Color Transparency

Although the opacity property allows you to make elements transparent, this is applied to the entire element. CSS3 now allows you to make specific colors transparent. An alpha value is generally a fourth value in a color, but rather than representing a color, it sets the opacity of the color—a value from 0 (transparent) to 1 (opaque). So, an alpha of .5 is the equivalent of 50% opacity.

- **TIP** You can set an alpha channel for either RGB decimal or HSL color values, but currently there is no way to add alpha values to RGB hex values.

- **TIP** In addition to setting the color opacity, CSS includes the ability to set the opacity of an entire object and any of its content. See “Setting an Element’s Opacity” in Chapter 11 for more information.

Alpha (opacity: 0–1)

```
`rgba(255, 255, 255, 1.0)`
```

```
`hsla(360, 100%, 100%, 1.0)`
```

Alpha (opacity: 0–1)

RGBA and HSLA add an alpha value as a decimal (0–1) to represent the opacity of a color with 0 completely transparent and 1 completely opaque.

## Other Ways to Add Color

Although this chapter presents the primary methods for setting colors in your design, several other CSS properties include color values:

- text-shadow & box-shadow—Although generally thought of as black or gray, you can set a text-shadow to any color. I often use this with brighter colors to create a glow (see Chapter 6).

- border—An element’s border colors can be set as part of any of the border properties or directly in the border-color property (see Chapter 10).

- outline—Like the border property, outline allows you to define a color around the edge of an element (see Chapter 10).

![](img/e1ed1e3c1873fa9fc855210fb83699d0_212_0.png)

## Creating Color Gradients

Although not yet a finished part of the CSS3 standard, the ability to fill an element's background with a gradient has been introduced as extensions in Opera, Internet Explorer, Webkit, and Mozilla—which means you can add linear and radial gradients compatible with Opera, Internet Explorer, Safari, Chrome, and Firefox.

> Linear and radial gradients are available in all modern browsers, including IE9+.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_212_1.png)

To ensure maximum compatibility, you need to include the CSS3 standard version of the gradient property along with the browser extension versions: -o-, -ms-, -webkit, and -moz. Don't worry, they all take the same values. If you need to support really old browsers (Safari 3 and earlier or Internet Explorer 8 or earlier), you may also need to include values for them. For more details, see the sidebar "Older Gradient Syntax".

```
linear-gradient(
 45deg, -------- Angle
 purple 25%, -------- Color stop 1
 rgb(23, 136, 12), -------- Color stop 2
 #c00) -------- Color stop 3
```

> Linear gradients have an optional angle value, followed by two or more color stops separated by commas. The angle can be in degrees, or one or two keywords to indicate the starting side or corner. The color stop is a color value and an optional length or percentage value for the position of the stop—where it is at full color—along the gradient line.

## Linear Gradients

Linear gradients have two different value types, the angle of the gradient and the colors that make up the gradient.

- Angle (degrees)—The angle for the gradient expressed as a numeric value, using degrees (deg): such as 45deg.

- Angle (keyword)—Instead of an angle numeric value, you can use one or two keywords—separated by a spaces—defining the side or corner where the gradient should start and stop—and preceded by the word to. Values can include top, right, bottom, and/or left. If two values are used (separated by a space), they specify a corner, such as to top left, such as to bottom right.

- **Color stop**—The values of two or more colors at a particular point along the gradient with values separated by spaces. You should include at least two values (otherwise you’ll get a solid color), but you can follow them with as many values as you want. These may include any color value type as shown in Table 7.1, including transparent colors using RGBA or HSLA, and an optional percentage or length value to set where the color should be positioned along the gradient axis, such as **green 67%**: **rgba(221,160,221)**.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_213_0.png)

There's more than one way to create the same gradient.

At its simplest, a linear gradient can be two color values with the default angle at 270°, the start stop at 0%, and the end stop at 100%:

```
linear-gradient(navy, gold);
```

This is the same as:

```
linear-gradient(270deg, rgb(0,0,128),
rgb(255,215,0));
```

```
linear-gradient(to bottom, navy,
gold);
```

```
linear-gradient(to top, gold, navy);
```

```
linear-gradient(#008 0%, #ffd700
100%);
```

```
linear-gradient(180deg, gold 0%,
navy 100%);
```

All of these values produce the same gradient.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_214_0.png)

```
radial-gradient(
    center center, ------------ Origin position
    circle farthest-corner, - Shape/size
    purple 25%, --------------- Color stop 1
    rgb(23, 136, 12), --------- Color stop 2
    #c00) --------------------- Color stop 3
```

Radial gradients have optional values for the origin of the gradient, the shape and size, and two or more color stops. The position can be two values for the horizontal and vertical location. The shape is either circle or elliptical and the size can be keyword or two values. The color stop has a color value and an optional length or percentage value for the position of the stop—where it is at full color—along the gradient.

| Value | Description |
|---|---|
| closest-side | Gradient shaped to meet closest side from its center |
| closest-corner | Gradient shaped to meet closest corner from its center |
| farthest-side | Gradient shaped to meet farthest side from its center |
| farthest-corner | Gradient shaped to meet farthest corner from its center |

## Radial Gradients

Radial gradients get a little more complicated than linear gradients because they have four possible value types:

- Position—The location of the center of the gradient within its box (see Chapter 10). The value(s) are a numeric distance value (such as 5em), a percentage (such as 23%) or a keyword (such as center) that sets the center of the radial gradient (which is the same as setting background image positions shown later in Table 7.10). You can use two values to define the horizontal and vertical positions independently (such as at 2em 5em, at 23% 46%, or at left center). You can mix value types (such as at 2em center). The position is optional, and if omitted defaults to center.

- Size (keyword)—The size sets the radial gradient’s endpoint, using a keyword (Table 7.3). Currently, the webkit version of the property uses a different and more limited set of keywords, but they have equivalents in the new standard.

- Size (length)—If the shape is not explicitly stated, the size can be set as one or two length (such as 20px) or percentage (such as 89% 42%) values. If two values are used, the first is the horizontal length and the second is the vertical length. Negative values are not allowed.

- Shape—The shape of a radial gradient, either circle or ellipse. The shape value is optional; but if omitted, the value defaults to circle. Otherwise, the size is a single length, and ellipse.

- Color stop—The values of two or more colors at particular points along the gradient with values separated by spaces. You should include at least two values (otherwise you’ll get a solid color), but you can follow them with as many values as you want. These may include any color value type shown in Table 7.1—including transparent colors using RGBA or HSLA—and an optional percentage or length value to set where the color should be positioned along the gradient axis, such as green 67%, rgba(221,160,221,0.5).

At its simplest, a radial gradient can be two color values with the default position in the center, the shape an ellipse, the size set by the farthest-corner, and the start stop at 0% and end stop at 100%:

```
radial-gradient(navy,gold);
```

This is the same as:

```
radial-gradient(ellipse rgb(0,0,128),
rgb(255,215,0));
radial-gradient(center, navy, gold);
radial-gradient(farthest-corner, #008
0%, #ffd700 100%);
radial-gradient(center center,
ellipse farthest-corner, navy 0%,
gold 100%);
```

All of these values produce the same gradient.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_215_0.png)

There are many ways to create this elliptical gradient.
