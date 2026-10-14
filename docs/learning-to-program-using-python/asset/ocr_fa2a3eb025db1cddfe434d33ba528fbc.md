```
String c=
"{0,choice,0#no more bottles|1#1
 bottle|1<{0} bottles} of beer";
return java.text.MessageFormat.format(
 c.replace("n", "N")+" on the wall, "+c+
".\n"+
"{0,choice,0#Go to the store and buy
 some more"+
"|0<Take one down and pass it around},
"+c.replace("{0}","{1}")+
" on the wall.\n", count, (count+99)
%100);
}
```

```
class Song implements Iterator<Vers> {
private int verse=1;
public boolean hasNext() {
return verse <= 100;
}
public Verse next() {
if(!hasNext())
throw new NoSuchElementException("End
of song!");
return new Verse(verse++);
}
public void remove() {
throw new UnsupportedOperationException
("Cannot remove verses!");
}
}
```

```
public class Beer {
public static void main(String[] args) {
Iterable<Vers> song= new Iterable<
Verse>() {
public Iterator<Vers> iterator()
{
return new Song();
}
```