
从继承的类中引用，因为原始字段用于协调这些点（参见示例 5.72 和 CD-ROM 示例 Patterns.cs）。

### 示例 5.72. Patterns.cs

```
using System;
using System.Drawing;
using System.Drawing.Drawing2D;

namespace GameClasses {
    public class Patterns : Shapes {
        public Patterns(int n) : base(0) {}

        public Patterns(int posX, int posY) : base(0) {
            imagePosX = posX;
            imagePosY = posY;
            isActive = false;
            animationStep = DEFAULTSTEP;
        }

        public void ItemPattern28(Graphics g, Brush bItemColor,
            Pen pItemColor, int current) {
            if(current >= 0 && current <= 6) {
                this.Window(g, bItemColor);
            }
            else if(current >= 7 && current <= 13) {
                this.Flower(g, bItemColor, pItemColor);
            }
            else if(current >= 14 && current <= 20) {
                this.TV(g, bItemColor, pItemColor);
            }
            else if(current >= 21 && current <= 28) {
                this.Lamp(g, bItemColor, bItemColor);
            }
        }

        public void AlienPattern20(Graphics g, Brush bAlienColor,
            int current) {
            if(current >= 0 && current <= 4) {
                this.Alien0(g, bAlienColor);
            }
            else if(current >= 5 && current <= 9) {
                this.Alien1(g, bAlienColor);
            }
            else if(current >= 10 && current <= 14) {
                this.Alien2(g, bAlienColor);
            }
            else if(current >= 15 && current <= 19) {
                this.Alien3(g, bAlienColor);
            }
        }
}
}
public void ItemPattern1(Graphics g, Brush bAlienColor,
    int current) {
    if(current >= 0 && current <= 4) {
        this.Alien0(g, bAlienColor);
    else if(current >= 5 && current <= 9) {
        this.Alien1(g, bAlienColor);
    else if(current >= 10 && current <= 14) {
        this.Alien2(g, bAlienColor);
    else if(current >= 15 && current <= 19) {
        this.Alien3(g, bAlienColor);
    }
}
}
}
```

## GameState.cs

GameState.cs 包含 GameState 类，该类负责维护有关游戏的简单状态信息，例如速度、状态（已启动、已停止等）和模式（演示、单人游戏等）。GameState 类是一个独立的类，但它是本教材中构建的所有游戏的重要组成部分（参见示例 5.73 和 CD-ROM 上的 GameState.cs）。

### 示例 5.73. GameState.cs

```
using System;

namespace GameClasses {
    public class GameState {
        // Different speeds the game can be run in.
        public const int SPEED_MINIMUM = 1;
        public const int SPEED_DEFAULT = 3;
        public const int SPEED_MAXIMUM = 10;
// Different "states" the game can be in.
public enum State : int {
    Unknown = 0,
    Started = 1,
    Stopped = 2,
}

// Different "modes" the game can be run in.
[Flags]
public enum Mode : int {
    Normal = 0,
    SinglePlayer = 0,
    TwoPlayer = 1,
    Demo = 2,
}

// Member variables
public int currentSpeed;
public State currentState;
public Mode currentMode;

// Constructors
public GameState() {
    currentSpeed = SPEED_DEFAULT;
    currentState = State.Stopped;
    currentMode = Mode.Normal;
}

public GameState(int initialSpeed, State gameState) {
    currentSpeed = initialSpeed;
    currentState = gameState;
    currentMode = Mode.Normal;
}

public GameState(int initialSpeed, State gameState,
    Mode gameMode) {
    currentSpeed = initialSpeed;
    currentState = gameState;
    currentMode = gameMode;
}
}
```

## GameTimer.cs

GameTimer 类用作游戏事件的衡量标准；例如，可以添加、计时或移除事件——addEvent、TimedEvent 和 removeEvent。游戏依赖于定时事件，以便允许玩家无法控制的操作（参见示例 5.74 和 CD-ROM 上的 GameTimer.cs）。

### 示例 5.74. GameTimer.cs

```csharp
using System;
using System.Windows.Forms;
using System.Collections;

namespace GameClasses {
    public class GameTimer {
        // Member fields
        Timer gameTimer;  // main timer object
        int baseInterval; // base interval in ms
        Hashtable events; // list of TimedEvent objects

        // Default constructor
        public GameTimer(int interval) {
            events = new Hashtable();
            gameTimer = new Timer();
            gameTimer.Interval = interval;
            gameTimer.Tick += new EventHandler(Tick);
            baseInterval = interval;
        }

        // Simple start and stop functionality.
        public void Start() {gameTimer.Start();}
        public void Stop() {gameTimer.Stop();}

        // Add an event to our game timer. Use stepFactor to control the
        // frequency the given TimedEvent's Tick() will be called.
        // Use the given "key" for future reference to this TimedEvent.
        public void addEvent(TimedEvent timedEvent, int stepFactor,
            string key) {
            TimedEventNode node = new TimedEventNode();
            node.data = timedEvent;
            node.timeStep = stepFactor;
            node.stepCount = 0;
            events.Add(key, node);
        }

        // Returns the event marked with the given key
        public TimedEvent getEvent(String key) {
            return ((TimedEventNode) events[key]).data;
        }

        // Removes an event from the list
        public void removeEvent(String key) {
            events.Remove(key);
        }

        // Changes the step associated with the event indexed by key
        public void changeStep(String key, int stepFactor) {
            ((TimedEventNode) events[key]).timeStep = stepFactor;
        }

        // Tick() -- passes on tick event to proper TimedEvent objects
        public void Tick(object sender, EventArgs e) {
            IDictionaryEnumerator itemEnumerator = events.GetEnumerator();
            TimedEventNode node;

            while (itemEnumerator.MoveNext()) {
                node = (TimedEventNode) itemEnumerator.Value;
                if (node.stepCount >= node.timeStep) {
                    node.stepCount = 0;
                    node.data.Tick();
                } else {
                    node.stepCount++;
                }
            }
        }

        // Helper class to hold a extra information relevant to
        // timer event processing.
        class TimedEventNode {
            public int timeStep;  // how many baseInterval ticks to wait
            public int stepCount; // counter to compare with timeStep
            public TimedEvent data; // the TimedEvent object
        }
    }
}
```

## TimedEvent.cs

TimedEvent.cs 是一个表示计时器的类；它用于基于固定数量的处理周期来监控事件。它可以监控事件发生固定次数等。从此类派生并重写 Tick() 方法可以实现自定义行为（参见示例 5.75）。

### 示例 5.75. TimedEvent.cs

```csharp
using System;

namespace GameClasses {
    public delegate void TickHandler(TimedEvent e, Object payload);

    public class TimedEvent {
        // Member fields
        public int ticks;
        public int tickCounter;
        public bool isCountdown;
        public bool isActive;
        public TickHandler remoteHandler;
        public object payload;

        public TimedEvent() {
            ticks = 0;
            isCountdown = false;
            SetTickHandler(new TickHandler(DoNothing));
        }

        public TimedEvent(TickHandler handler) {
            SetTickHandler(handler);
        }

        public TimedEvent(int numTicks, TickHandler handler) {
            SetCountdown(numTicks);
            SetTickHandler(handler);
        }

        public void SetTickHandler(TickHandler handler) {
            remoteHandler = handler;
        }
    }
```
