```
lock (listLock) {
return new(Name, list.GetRange(index, count));
}
public Song[] ToArray() {
lock (listLock) {
return list.ToArray();
}
}
public void Add(Song song) {
lock (listLock) {
list.Add(song);
}
}
public Song this[int index] {
get {
lock (listLock) {
return list[index];
}
}
set {
lock (listLock) {
list[index] = value;
}
}
}
public int Size {
get {
lock (listLock) {
return list.Count;
}
}
}
public Playlist Shuffle() {
```