
```cpp
#include "MicroBit.h"

MicroBit uBit;
int clickCount = 0;

void startGame();
int playGame();
void endGame(int position);
void countDown();
void drawPlayArea();
void flashMan(int x, int y, int p, int vx, int vy);
void setupButton();
void moveHorizontal();
void moveVertical(int x, int h);
void buttonClickCount(MicroBitEvent e);

int main() {
 uBit.init();
  startGame();
  int position = playGame();
  endGame(position);
  sleep_fiber();
  return 0;
}

void startGame() {
  countDown();
  uBit.display.setDisplayMode(DISPLAY_MODE_GRESCALE);
  drawPlayArea();
  setupButton();
}

void countDown() {
  int t;
  for (t = 5; t >= 0; t--) {
    uBit.display.scroll(t);
  }
  uBit.display.scroll("!");
}
```

```cpp
void drawPlayArea() {
  uBit.display.clear();
  int y;
  for (y = 1; y <= 5; y++) {
    uBit.display.image.setPixelValue(2, y, 255);
  }
}
```

```cpp
int playGame() {
  int position = 4;
  int clickCount = 0;
  int t1 = uBit.systemTime();
  while (uBit.systemTime() - t1 < 20000) {
    flashMan(4, position, clickCount, 0, -1);
    if (clickCount > 10) {
      position = position - 1;
      clickCount = 0;
      if (position == 0) break;
    }
  }
  return position;
}
```

```cpp
void endGame(int position) {
  if (position == 0) {
    moveHorizontal();
    moveVertical(0, 0);
  } else {
    moveVertical(4, position);
  }
}
```

```cpp
void setUpButton() {
  uBit.buttonB.setEvent(MICROBIT_BUTTON_ALL_EVENTS);
  uBit.messageBus.listen(MICROBIT_ID_BUTTON_B, MICROBIT_BUTTON_EVT_CLICK, buttonClickCount);
}
```

```cpp
void buttonClickCount(MicroBitEvent e) {
  clickCount++;
}

void flashMan(int x, int y, int p, int vx, int vy) {
  uBit.display.image.setPixelValue(x, y, 0);
  uBit.display.image.setPixelValue(x + vx, y + vy, 0);
  uBit.sleep(100);
  uBit.display.image.setPixelValue(x, y, 25 * (10 - p));
  uBit.display.image.setPixelValue(x+vx, y+vy, 25*p);
  uBit.sleep(100);
}

void moveHorizontal() {
  int x, fraction;
  for (x = 4; x >= 0; x--) {
    for (fraction = 0; fraction <= 10; fraction++) {
      flashMan(x, 0, fraction, -1, 0);
    }
  }
}

void moveVertical(int x, int h) {
  if (h != 0) {
    uBit.display.image.setPixelValue(x, h - 1, 0);
    for (y = h; y <= 4; y++) {
      for (fraction = 0; fraction <= 10; fraction++) {
        flashMan(x, y, fraction, 0, 1);
      }
    }
  }
}
```

![](img/23976341c9281123e7b181beea6e9dbd_230_0.png)

如果你尝试一下，你会发现使用灰度模式来提高分辨率效果良好，但如果能像第 5 章提到的脉冲宽度调制那样，使用幂律来缩放 LED 亮度，效果会更好。

我不认为 5x5 显示器很快就能运行《毁灭战士》的实现，但谁知道呢！

加上一些声音，它不是一个坏的游戏……

## 总结

当 `p` 从 0 变化到 10 时，亮度位置会从第一个 LED 移动到第二个 LED。
