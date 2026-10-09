# shuffle-playlist/Playlist.cs (lines 3–72)

```
```
3  public sealed class Playlist {
4      private readonly object listLock = new();
5      private static readonly Random rng = new();

7      public string Name { get; }

9      private readonly List<Song> list;

       public Playlist(string name) : this(name, new List<Song>()) { }
       public Playlist(string name, Song[] songs) : this(name, new List<Song>(songs)) { }
13     public Playlist(string name, List<Song> list) => (Name, this.list) = (name, list);

15     public Playlist Copy() => GetRange(0, Size);

17     private Playlist GetRange(int index, int count) {
18         lock (listLock) {
19             return new(Name, list.GetRange(index, count));
20         }
21     }

23     public Song[] ToArray() {
24         lock (listLock) {
25             return list.ToArray();
26         }
27     }

29     public void Add(Song song) {
30         lock (listLock) {
31             list.Add(song);
32         }
33     }

35     public Song this[int index] {
36         get {
```
```