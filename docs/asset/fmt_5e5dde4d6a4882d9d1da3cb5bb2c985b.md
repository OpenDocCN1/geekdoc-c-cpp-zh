
`var e2 = 7;`

`queue.Enqueue(e2);`

`Console.WriteLine($"len = {queue.Count}");`

```
lock (queue) {

    foreach (var item in queue) {

        Console.WriteLine($"item = {item}");

    }

}
```

`var e3 = 9;`

```
try {

    queue.Enqueue(e3);

    Console.WriteLine($"len = {queue.Count}");

    lock (queue) {

        foreach (var item in queue) {

            Console.WriteLine($"item = {item}");

        }

    }

} catch (Exception ex) {

    Console.WriteLine(ex);

}
```

`var e = queue.Dequeue();`

`Console.WriteLine($"e = {e}");`

`Console.WriteLine($"len = {queue.Count}");`

```
lock (queue) {

    foreach (var item in queue) {

        Console.WriteLine($"item = {item}");

    }

}
```

```
try {

    queue.Enqueue(e3);

    Console.WriteLine($"len = {queue.Count}");

    lock (queue) {

        foreach (var item in queue) {

            Console.WriteLine($"item = {item}");

        }

    }

} catch (Exception ex) {

    Console.WriteLine(ex);

}
```

`e = queue.Dequeue();`

`Console.WriteLine($"e = {e}");`

`Console.WriteLine($"len = {queue.Count}");`

```
lock (queue) {

    foreach (var item in queue) {

        Console.WriteLine($"item = {item}");

    }

}
```

`var e4 = 11;`

```
try {

    queue.Enqueue(e4);

    Console.WriteLine($"len = {queue.Count}");

    lock (queue) {

        foreach (var item in queue) {

            Console.WriteLine($"item = {item}");

        }

    }

} catch (Exception ex) {

    Console.WriteLine(ex);

}
```

# `ring-buffer/src/Queue/Queue.cs`

```csharp

namespace Example;

using System.Collections;

public class ShortQueue<T> : IEnumerable<T> {

    private readonly object bufferLock = new();

    private readonly Ring.Buffer<T> buffer;

    public uint Capacity { get; init; }

    public int Count => buffer.Length;

    public ShortQueue(uint capacity) {

        Capacity = capacity;

        buffer = new Ring.Buffer<T>(Capacity);

    }

    public void Enqueue(T item) {

        lock (bufferLock) {

            buffer.PushFront(item);

        }

    }

    public T Dequeue() {

        lock (bufferLock) {

            return buffer.PopBack();

        }

    }

    public IEnumerator<T> GetEnumerator() => buffer.GetEnumerator();

    IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();

}

```

### MRU

# `ring-buffer/src/MRU/Program.cs`

```csharp

using MRU;

var cap = 3u;

var list = new ShortList<int>(cap);

list.Add(1);

list.Add(2);

Console.WriteLine($"len = {list.Count}");

lock (list) {

    foreach (var item in list) {

        Console.WriteLine($"item = {item}");

    }

}

list.Add(3);

Console.WriteLine($"len = {list.Count}");

lock (list) {

    foreach (var item in list) {

        Console.WriteLine($"item = {item}");

    }

}

list.Add(4);

Console.WriteLine($"len = {list.Count}");

lock (list) {

    foreach (var item in list) {

        Console.WriteLine($"item = {item}");

    }

}

list.Add(5);

Console.WriteLine($"len = {list.Count}");

lock (list) {

    foreach (var item in list) {

        Console.WriteLine($"item = {item}");

    }

}

```

# `ring-buffer/src/MRU/List.cs`

```csharp

namespace MRU;

using System.Collections;

public sealed class ShortList<T> : IEnumerable<T> {

    private readonly object bufferLock = new();

    private readonly Ring.Buffer<T> buffer;

    public uint Capacity { get; init; }

    public int Count => buffer.Length;

    public ShortList(uint capacity) {

        Capacity = capacity;

        buffer = new Ring.Buffer<T>(Capacity, overwrite: true);

    }

    public T this[int index] {

        get {

            lock (bufferLock) {

                return buffer[index];

            }

        }

        set {

            lock (bufferLock) {

                buffer[index] = value;

            }

        }

    }

    public void Add(T item) {

        lock (bufferLock) {

            buffer.PushFront(item);

        }

    }

    public IEnumerator<T> GetEnumerator() => buffer.GetEnumerator();

    IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();

}

```

# RingBufferTests

*`ring-buffer/test/RingBufferTests/BufferTest.cs`*

```csharp

namespace test;

using Xunit;

using Ring;

public sealed class BufferTest {

    [Fact]

    public void TestBasics() {

        var cap = 3u;

        var buffer = new Buffer<int>(cap);

        Assert.Equal(0, buffer.Length);

        Assert.Equal((int)cap, buffer.Capacity);

    }

    [Fact]

    public void TestPush() {

        var cap = 3u;

        var buffer = new Buffer<int>(cap);

        var e1 = 5;

        buffer.PushFront(e1);

        var e2 = 7;

        buffer.PushFront(e2);

        Assert.Equal(2, buffer.Length);

        Assert.Equal((int)cap, buffer.Capacity);

    }

    [Fact]

    public void TestPop() {

        var cap = 3u;

        var buffer = new Buffer<int>(cap);

        var e1 = 5;

        buffer.PushFront(e1);

        var e2 = 7;

        buffer.PushFront(e2);

        Assert.Equal(2, buffer.Length);

        Assert.Equal((int)cap, buffer.Capacity);

        var e = buffer.PopBack();

        Assert.Equal(1, buffer.Length);

        Assert.Equal(e1, e);

    }

}

```

### LED 数字时钟

*`led-clock-digital/Program.cs`*

```csharp

using LED;

var clock = new Clock();

await clock.Run();

```

# `led-clock-digital/Clock.cs`

```csharp

namespace LED; using LED.Ascii; public sealed class Clock { const int NumDigits = 4; private readonly ILEDDisplay display; public Clock() => display = new LEddDisplay(NumDigits); public async Task Run(int milliDelay = 60_000) { while (true) { Console.WriteLine("Current time is:"); DisplayCurrentTime(); await Task.Delay(milliDelay); Console.WriteLine(); } } public void DisplayCurrentTime() { var time = DateTime.Now; var str = $"{time.Hour:D2}{time.Minute:D2}"; var digits = str.Select(c => Digit.Get(c)).ToArray(); display.Show(digits); }}

```

# `led-clock-digital/Common/Digits.cs`

```csharp

namespace LED; public sealed record Digit { public static readonly Digit None = new(new byte[] { 0, 0, 0, 0, 0, 0, 0, 0 });

public static readonly Digit Zero = new(new byte[] {

1, 1, 1, 0, 1, 1, 1

});

public static readonly Digit One = new(new byte[] {

0, 0, 1, 0, 0, 1, 0

});

public static readonly Digit Two = new(new byte[] {

1, 0, 1, 1, 1, 0, 1

});

public static readonly Digit Three = new(new byte[] {

1, 0, 1, 1, 0, 1, 1

});

public static readonly Digit Four = new(new byte[] {

0, 1, 1, 1, 0, 1, 0

});

public static readonly Digit Five = new(new byte[] {

1, 1, 0, 1, 0, 1, 1

});

public static readonly Digit Six = new(new byte[] {

1, 1, 0, 1, 1, 1, 1

});

public static readonly Digit Seven = new(new byte[] {

1, 0, 1, 0, 0, 1, 0

});

public static readonly Digit Eight = new(new byte[] {

1, 1, 1, 1, 1, 1, 1

});

public static readonly Digit Nine = new(new byte[] {

1, 1, 1, 1, 0, 1, 0

});

public static Digit Get(char c) =>

    c switch {

        '0' => Zero,

        '1' => One,

        '2' => Two,

        '3' => Three,

        '4' => Four,

        '5' => Five,

        '6' => Six,

        '7' => Seven,

        '8' => Eight,

        '9' => Nine,

        _ => None,

    };

private readonly byte[] leds;

private Digit(byte[] leds) {

    this.leds = leds;

}

}

```

# `led-clock-digital/Common/Display.cs`

```csharp

namespace LED;

public interface IDisplay {

    void Clear();

}

public interface ILEDDisplay : IDisplay {

    void Show(Digit[] digits);

}

```

# `led-clock-digital/Ascii/Number.cs`

```csharp

namespace LED.Ascii;

using System.Text;

sealed record Number {

    internal static readonly Number None = new(new char[,] {

        { ' ' , ' ' , ' ' } ,

        { ' ' , ' ' , ' ' } ,

        { ' ' , ' ' , ' ' } ,

    });

    internal static readonly Number Zero = new(new char[,] {

        { ' ' , ' ' , ' ' } ,

        { ' | ' , ' ' , ' | ' } ,

        { ' | ' , ' ' , ' | ' } ,

    });

    internal static readonly Number One = new(new char[,] {

        { ' ' , ' ' , ' ' } ,

        { ' ' , ' ' , ' | ' } ,

        { ' ' , ' ' , ' | ' } ,

    });
```
