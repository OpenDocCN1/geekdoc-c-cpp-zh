```
```java
public void setValue(Object value)
{
    if (!(value instanceof String)) throw new IllegalArgumentException();
    word = (String) value;
    fireStateChanged();
}

public Object getNextValue()
{
    int[] codePoints = toCodePointArray(word);
    for (int i = codePoints.length - 1; i > 0; i--)
    {
        if (codePoints[i - 1] < codePoints[i])
        {
            int j = codePoints.length - 1;
            while (codePoints[i - 1] > codePoints[j])
                j--;
            swap(codePoints, i - 1, j);
            reverse(codePoints, i, codePoints.length - 1);
            return new String(codePoints, 0, codePoints.length);
        }
    }
    reverse(codePoints, 0, codePoints.length - 1);
    return new String(codePoints, 0, codePoints.length);
}

public Object getPreviousValue()
{
    int[] codePoints = toCodePointArray(word);
    for (int i = codePoints.length - 1; i > 0; i--)
    {
        if (codePoints[i - 1] > codePoints[i])
        {
            int j = codePoints.length - 1;
            while (codePoints[i - 1] < codePoints[j])
                j--;
            swap(codePoints, i - 1, j);
            reverse(codePoints, i, codePoints.length - 1);
            return new String(codePoints, 0, codePoints.length);
        }
    }
    reverse(codePoints, 0, codePoints.length - 1);
    return new String(codePoints, 0, codePoints.length);
}

private static int[] toCodePointArray(String str)
{
    int[] codePoints = new int[str.codePointCount(0, str.length())];
```
```