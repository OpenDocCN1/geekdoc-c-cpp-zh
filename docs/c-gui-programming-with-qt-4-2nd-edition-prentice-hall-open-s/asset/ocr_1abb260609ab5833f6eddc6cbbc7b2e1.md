![](bbox=[0.011, 0.012, 0.085, 0.066])

![](bbox=[0.109, 0.012, 0.185, 0.066])

![](bbox=[0.207, 0.012, 0.283, 0.066])

![](bbox=[0.305, 0.012, 0.381, 0.066])

![](bbox=[0.403, 0.012, 0.479, 0.066])

![](bbox=[0.501, 0.012, 0.547, 0.066])

![](bbox=[0.011, 0.076, 0.085, 0.152])

![](bbox=[0.109, 0.076, 0.185, 0.152])

![](bbox=[0.207, 0.076, 0.283, 0.152])

![](bbox=[0.305, 0.076, 0.381, 0.152])

![](bbox=[0.403, 0.076, 0.479, 0.152])

![](bbox=[0.501, 0.076, 0.597, 0.152])

![](bbox=[0.011, 0.166, 0.085, 0.242])

![](bbox=[0.109, 0.166, 0.185, 0.242])

![](bbox=[0.207, 0.166, 0.283, 0.242])

![](bbox=[0.305, 0.166, 0.381, 0.242])

![](bbox=[0.403, 0.166, 0.479, 0.242])

![](bbox=[0.501, 0.166, 0.597, 0.242])

![](bbox=[0.011, 0.256, 0.085, 0.332])

![](bbox=[0.109, 0.256, 0.185, 0.332])

![](bbox=[0.207, 0.256, 0.283, 0.332])

![](bbox=[0.305, 0.256, 0.381, 0.332])

![](bbox=[0.403, 0.256, 0.479, 0.332])

![](bbox=[0.501, 0.256, 0.597, 0.332])

Composition modes are set using `QPainter::setCompositionMode()`. For example, here how to create a `QImage` containing the XOR of the butterfly and the checker pattern:

```
QImage resultImage = checkerPatternImage;
QPainter painter(&resultImage);
painter.setCompositionMode(QPainter::CompositionMode_Xor);
painter.drawImage(0, 0, butterflyImage);
```

One is to be aware of that the `QImage::CompositionMode_Xor` operation also applies to the alpha channel. This means that if we XOR the white color (`0xFFFFFF`) with itself, we obtain a transparent color (`0x00000000`), not black (`0xFF000000`).