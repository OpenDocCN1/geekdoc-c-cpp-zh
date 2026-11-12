![](bbox=[0.106, 0.073, 0.468, 0.332])

# Fire

The fire effect creates the illusion of heat coming off the letters. To create the effect, start with white text, and then stack shadows, going from white to yellow to orange to red, while increasing the y-offset and blur with each.

```
.fire {
    background-color: #333;
    color: #fff;
    text-shadow: 0px -1px 4px white,
    0px -2px 10px yellow,
    0px -10px 20px orange,
    0px -18px 40px red; }
```

![](bbox=[0.553, 0.073, 0.922, 0.332])

# 3D Text Blocks

The 3D text block effect creates the illusion that the letters have depth and mass, like lettering in retro science-fiction movies. To create the effect, start with white text and then stack successively darker shadows, increasing the increment by 1px for as many levels as you want to achieve the desired depth. The offset will depend on the direction you want the text to be angled.

```
.d3 {
    background-color: #ccc;
    color: #fff;
    text-shadow: 0px 1px 0px #999,
    0px 2px 0px #888,
    0px 3px 0px #777,
    0px 4px 0px #666,
    0px 5px 0px #555,
    0px 6px 0px #444,
    0px 7px 0px #333,
    0px 8px 7px #001135; }
```