# 27.3. Sample Code Snippets - led-clock-digital

led-clock-digital/Ascii/Display.cs (lines 7-41)

```
7 public sealed class LEDDisplay : Display, ILEDDisplay {
8     private readonly List<Cell> cells;
9
10    public int Size => cells.Count;
11
12    public LEDDisplay(int size) =>
13        cells = Enumerable.Range(0, size).Select(i => new
        Cell(Number.None)).ToList() ?? new();
14
15    public override void Clear() {
16        cells.ForEach(c => c.Reset());
17        Show();
18    }
19
20    private void Show() {
21        foreach (var m in cells.ToEnumerators()) {
22            foreach (var n in m) {
23                Console.Write(n);
24            }
25            Console.WriteLine();
26        }
27    }
28
29    public void Show(Digit[] digits) {
30        var arr = digits.Select(d => Number.Convert(d)).ToList();
31        for (var i = 0; i < Size; i++) {
32            if (i < arr.Count) {
33                cells[i].Set(arr[i]);
34            } else {
35                cells[i].Reset();
36            }
37        }
38
39        Show();
40    }
41 }
```