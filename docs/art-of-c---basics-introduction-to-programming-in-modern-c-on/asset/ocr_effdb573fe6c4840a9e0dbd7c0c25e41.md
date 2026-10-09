```
IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();
}
```

# ## RingBufferTests

*ring-buffer/test/RingBufferTests/BufferTest.cs*

```
```
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
```
```