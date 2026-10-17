
```cpp
// C++ version of 99 Bottles of Beer, object oriented paradigm
// programmer: Tim Robinson timtroyr@ionet.NET
#include <fstream.h>

enum Bottle { BeerBottle };

class Shelf {
unsigned BottlesLeft;
public:
    Shelf( unsigned bottlesbought )
    : BottlesLeft( bottlesbought )
    {}
    void TakeOneDown()
    {
        if (!BottlesLeft)
            throw BeerBottle;
        BottlesLeft--;
    }
    operator int () { return BottlesLeft; }
};

int main( int, char ** )
{
    Shelf Beer(99);
    try {
        for (;;) {
            char *plural = (int)Beer !=1 ? "s" : "";
            cout << (int)Beer << " bottle" << plural
                 << " of beer on the wall," << endl;
            cout << (int)Beer << " bottle" <<
                 plural
                 << " of beer," << endl;
            Beer.TakeOneDown();
            cout << "Take one down, pass it around"
                 << "," << endl;
            plural = (int) Beer !=1 ? "s":"";
            cout << (int) Beer << " bottle" <<
                 plural
                 << " of beer on the wall." << endl
                 ;
        }
    }
    catch ( Bottle ) {
        cout << "Go to the store and buy some more"
             << "," << endl;
        cout << "99 bottles of beer on the wall."
             << endl;
    }

    return 0;
}
```

### 3.3 Java

```java
/**
 * Java 5.0 version of the famous "99 bottles of
 *    beer on the wall".
 * Note the use of specific Java 5.0 features and
 * the strictly correct output.
 *
 * @author kvols
 */
import java.util.*;

class Verse {
    private final int count;
    Verse(int verse) {
        count = 100 - verse;
    }
    public String toString() {
        String c = "{0,choice,0#no more bottles|1#1 bottle|1<{0} bottles} of beer";
        return java.text.MessageFormat.format(
                c.replace("n", "N") + " on the wall, " + c +
                ".\n" +
                "{0,choice,0#Go to the store and buy some more" +
                "|0<Take one down and pass it around}, " +
                c.replace("{0}", "{1}") +
                " on the wall.\n", count, (count + 99) % 100);
    }
}

class Song implements Iterator<Verse> {
    private int verse = 1;
    public boolean hasNext() {
        return verse <= 100;
    }
    public Verse next() {
        if (!hasNext())
            throw new NoSuchElementException("End of song!");
        return new Verse(verse++);
    }
    public void remove() {
        throw new UnsupportedOperationException("Cannot remove verses!");
    }
}

public class Beer {
    public static void main(String[] args) {
        Iterable<Verse> song = new Iterable<Verse>() {
            public Iterator<Verse> iterator() {
                return new Song();
            }
        };

        // All this work to utilize this feature:
        // "For each verse in the song..."
        for (Verse verse : song) {
            System.out.println(verse);
        }
    }
}
```

### 3.4 C#

```csharp
/// Implementation of Ninety-Nine Bottles of Beer Song in C#.
/// What's neat is that .NET makes the Binge class
/// a full-fledged component that may be called
/// from any other .NET component.
///
/// Paul M. Parks
/// http://www.parkscputing.com/
/// February 8, 2002
using System;

namespace NinetyNineBottles
{
    /// <summary>
    /// References the method of output.
    /// </summary>
    public delegate void Writer(string format, params object[] arg);

    /// <summary>
    /// References the corrective action to take
    /// when we run out.
    /// </summary>
    public delegate int MakeRun();

    /// <summary>
    /// The act of consuming all those beverages.
    /// </summary>
    public class Binge
    {
        /// <summary>
        /// What we'll be drinking.
        /// </summary>
        private string beverage;

        /// <summary>
        /// The starting count.
        /// </summary>
        private int count = 0;

        /// <summary>
        /// The manner in which the lyrics are output.
        /// </summary>
        private Writer Sing;

        /// <summary>
        /// What to do when it's all gone.
        /// </summary>
        private MakeRun RiskDUI;

        public event MakeRun OutOfBottles;

        /// <summary>
        /// Initializes the binge.
        /// </summary>
        /// <param name="beverage">What to drink during this binge.</param>
        /// <param name="count">How many we're consuming.</param>
        /// <param name="writer">How our drinking song will be heard.</param>
        public Binge(string beverage, int count, Writer writer)
        {
            this.beverage = beverage;
            this.count = count;
            this.Sing = writer;
        }

        /// <summary>
        /// Let's get started.
        /// </summary>
        public void Start()
        {
            while (count > 0)
            {
                Sing(
                    @"{0} bottle{1} of {2} on the wall,
{0} bottle{1} of {2}.
Take one down, pass it around,",
                    count, (count == 1) ? "" : "s", beverage);

                count--;

                if (count > 0)
                {
                    Sing("{0} bottle{1} of {2} on the wall.",
                         count, (count == 1) ? "" : "s", beverage);
                }
                else
                {
                    Sing("No more bottles of {0} on the wall.",
                         beverage, null);
                }
            }

            Sing(
                @"No more bottles of {0} on the wall,
No more bottles of {0}.", beverage, null);

            if (this.OutOfBottles != null)
            {
                count = this.OutOfBottles();
                Sing("{0} bottles of {1} on the wall.", count, beverage);
            }
            else
            {
                Sing("First we weep, then we sleep.");
                Sing("No more bottles of {0} on the wall.",
                     beverage, null);
            }
        }
    }

    /// <summary>
    /// The song remains the same.
    /// </summary>
    class SingTheSong
    {
        /// <summary>
        /// Any other number would be strange.
        /// </summary>
        const int bottleCount = 99;

        /// <summary>
        /// The entry point. Sets the parameters
        /// of the Binge and starts it.
        /// </summary>
        /// <param name="args">unused</param>
        static void Main(string[] args)
        {
            Binge binge =
                new Binge("beer", bottleCount,
                    new Writer(Console.WriteLine));
            binge.OutOfBottles += new MakeRun(SevenEleven);
            binge.Start();
        }

        /// <summary>
        /// There's bound to be one nearby.
        /// </summary>
        /// <returns>Whatever would fit in the trunk.</returns>
        static int SevenEleven()
        {
            Console.WriteLine("Go to the store, get some more...");
            return bottleCount;
        }
    }
}
```

### 3.5 Python

```python
#!/usr/bin/env python
# -*- coding: iso-8859-1 -*-

"""
99 Bottles of Beer (by Gerold Penz)
Python can be simple, too :-)"""

for quant in range(99, 0, -1):
    if quant > 1:
        print(quant, "bottles of beer on the wall,", quant, "bottles of beer.")
        if quant > 2:
            suffix = str(quant - 1) + " bottles of beer on the wall."
        else:
            suffix = "1 bottle of beer on the wall."
    elif quant == 1:
        print("1 bottle of beer on the wall, 1 bottle of beer.")
        suffix = "no more beer on the wall!"
    print("Take one down, pass it around,", suffix)
    print("__")
```

## 第 4 章

### Python 解释器

#### 4.1 启动 Python 解释器

Python 可以通过交互式命令行（也称为解释器或 IDE）进行编程，但你编写的任何代码都不会被保存。一旦关闭会话，所有内容都会消失。为了保存你的程序，最简单的方法是将其输入到文本文件中并保存（请务必使用 `.py` 扩展名，即 `foo.py`）。
