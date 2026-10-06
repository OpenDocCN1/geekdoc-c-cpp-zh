# TABLE 12.1 2D Transform Values

| Value | Compatibility |
| --- | --- |
| rotate(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| rotateX(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| rotateY(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| scale(<num*2>) | FF3.5, S3, C5, O10.5, CSS3 |
| scaleX(<number>) | FF3.5, S3, C5, O10.5, CSS3 |
| scaleY(<number>) | FF3.5, S3, C5, O10.5, CSS3 |
| skew(<angle*2>) | FF3.5, S3, C5, O10.5, CSS3 |
| skewX(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| skewY(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| translate(<length*2>) | FF3.5, S3, C5, O10.5, CSS3 |
| translateX(<length>) | FF3.5, S3, C5, O10.5, CSS3 |
| translate(<length>) | FF3.5, S3, C5, O10.5, CSS3 |
| matrix(<various*6>) | FF3.5, S3, C5, O10.5, CSS3 |

# NEW IN CSS3: Transforming an Element ★

Transformations are a bit of a cheat. Yes, they enable you to create incredibly designs that finally break out of the rectangular layout grid, allowing you to rotate, scale, skew, and move elements. However, each "value" shown in Table 12.1 (for 2D) and Table 12.2 (for 3D) could be a property in and of itself takes its own parenthetical values. But, instead, they are all associated with the transform property, and we'll have to live with that.

Transform values, in turn, have basic value types we might use:

+   - Angle can be defined in degrees (90deg), grads (100deg), or radians (1.683rad). Negative values and values greater than 360deg are allowed but are translated into positive values.
- Number can be any integer or decimal value, positive or negative. Numbers are generally used as a multiplier.
- Length is a value as defined in the introduction of this book. This can include relative values (em, px, %) or absolute values (in, mm, cm).

# TABLE 12.2 Transform-Origin Values

| Value | Compatibility |
| --- | --- |
| <percentage> | FF3.5, S3, C5, O10.5 |
| <length> | FF3.5, S3, C5, O10.5, CSS3 |
| <keyword> | FF3.5, S3, C5, O10.5, CSS3 |

Many transform values can take multiple parenthetical values, separated by a comma:

```
scale(2,1.65)
```

Generally, two or three values will represent the X, Y, and Z axes. If only one value is included, it is assumed to be used for both or all.