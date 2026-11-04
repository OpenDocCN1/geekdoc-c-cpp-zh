# Part I: C# Fundamentals

(continued)

```
{
    return spamlist.Phrases[index];
}
}
bool System.Collections.IEnumerator.MoveNext()
{
    index++;
    return index < spamlist.Phrases.Length;
}
void System.Collections.IEnumerator.Reset()
{
    index = -1;
}
void IDisposable.Dispose() { }
}
```

```
protected string[] Phrases =
    new string[]{
        "pain relief","paxil","pharmacy","phendimetrazine",
        "phentermine","phentermine","pheramones","pherimones",
        "photos of singles","platinum-celebs","poker-chip",
        "poze","prescription","privacy assured","product for less",
        "products for less","protect yourself","psychic"
    };
```

```
public IEnumerator<string> GetEnumerator()
{
    return new SpamPhrasListEnum(this);
}

//---for non-generic version of the class---
System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator()
{
    return new SpamPhrasListEnum(this);
}
```

In this example, the SpamPhrasListEnum class implements the IEnumerable<string> interface and provides the implementation for the Current property and the MoveNext() and Reset() methods.

To print out all the elements contained within a SpamPhraseList object, you can use the same statements that you used in the previous section:

```
SpamPhraseList list = new SpamPhraseList();
foreach (string s in list) //---error---
Console.WriteLine(s);
```