Next, we synthesize all the properties:

```
@synthesize margin = _margin;
@synthesize cornerRadius = _cornerRadius;
@synthesize graphBorderColor = _graphBorderColor;
@synthesize graphFillColor = _graphFillColor;
@synthesize graphBorderWidth = _graphBorderWidth;
@synthesize gridColor = _gridColor;
@synthesize gridSquareSize = _gridSquareSize;
@synthesize gridLineWidth = _gridLineWidth;
@synthesize trendLineColor = _trendLineColor;
@synthesize trendLineWidth = _trendLineWidth;
@synthesize referenceLineColor = _referenceLineColor;
@synthesize referenceLineWidth = _referenceLineWidth;
@synthesize textColor = _textColor;
@synthesize fontSize = _fontSize;
@synthesize units = _units;
@synthesize graphStats = _graphStats;
```

Now let's implement our default initializer. Unlike most of the other classes we've seen so far, GraphView uses the same designated initializer as its superclass. This means we do not need a separate method just to override the superclass's initializer.

On the other hand, we will want to override our class's `initWithCoder:` method. We will discuss `initWithCoder:` in more detail in Chapter 6, when we discuss loading and saving files. For now, just understand that loading a view from a nib file (and by extension, loading from a storyboard) does not call the view's designated initializer, it calls `initWithCoder:` instead.