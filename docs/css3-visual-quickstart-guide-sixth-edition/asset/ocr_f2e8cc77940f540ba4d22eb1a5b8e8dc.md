| Name | Appearance (varies depending on OS) |
| :--- | :--- |
| crosshair | + |
| e-resize | → |
| help | ? |
| move | ⇅ |
| ne-resize | ↗ |
| n-resize | ↑ |
| nw-resize | ↖ |
| pointer | ☞ |
| progress | ⌛ |
| se-resize | ↘ |
| s-resize | ↓ |
| sw-resize | ↙ |
| text | I |
| wait | ⌛ |
| w-resize | ← |

3. Add a graphic mouse pointer. You can also create your own pointer by adding the URL reference to an image file (generally in PNG format) to use as a custom cursor. You can specify the complete Web address or the local filename of the image.

```
cursor: url(../images/chrome/cursor-02.png) 20 20, crosshair;
```

★ Hotspot: CSS3 adds the ability to define the pointer's hotspot (the point at which the active click will happen) as determined from the upper-left corner of the image. Always include a backup pointer type.

Firefox, Safari, Opera, and Chrome allow you to use CUR, ANI, GIF, PNG, or JPEG images as a custom pointer by specifying the URL for the image file. Unfortunately, Internet Explorer supports only CUR and ANI file formats for custom pointers.

> TIP CUR and ANI are not standard image formats and can only be created using specialized software.

> TIP Remember that the exact appearance of the pointer depends on the operating system and the Web browser in use.

> TIP Although it's fun to play around with switching the mouse pointers, I've tested this feature on my own Web site and have received several emails asking me to cut it out. Most Web users have learned to recognize the common functions of specific pointers and when they should appear. Breaking these conventions tends to confuse users.