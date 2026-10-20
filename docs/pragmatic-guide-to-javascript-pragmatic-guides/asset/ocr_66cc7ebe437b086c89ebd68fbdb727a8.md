# Load FancyBox.

Download ui/lightbox/index.html

```
<link rel="stylesheet" type="text/css"
    href="vendor/fancybox/jquery.fancybox-1.2.6.css" />
<script type="text/javascript" src="vendor/jquery-1.3.2.min.js"></script>
<script type="text/javascript"
    src="vendor/fancybox/jquery.fancybox-1.2.6.pack.js"></script>
```

# Link to individual images.

Download ui/lightbox/index.html

```
<a href="beach_normal.jpg" title="A gorgeous beach">
    <img src="beach.jpg" alt="Beach" />
</a>
```

# Link to images as a browsable group.

Download ui/lightbox/index.html

```
<li>
    <a href="beach_normal.jpg" rel="demo" title="A gorgeous beach">
        <img src="beach.jpg" alt="Beach" />
    </a>
</li>
<li>
    <a href="feline_normal.jpg" rel="demo" title="A cute cub">
        <img src="feline.jpg" alt="Feline" />
    </a>
</li>
```

# Initialize FancyBox (with some customization thrown in).

Download ui/lightbox/lightbox.js

```
$(function() {
    $('#thumbnails a').fancybox({
        zoomSpeedIn: 300, zoomOpacity: true, overlayColor: '#000',
        overlayOpacity: 0.6
    });
});
```

# Related Tasks

+   - Task 12, Pulling Off Classy Tooltips, on page 44
+   - Task 13, Making Unobtrusive Pop-Ups, on page 46