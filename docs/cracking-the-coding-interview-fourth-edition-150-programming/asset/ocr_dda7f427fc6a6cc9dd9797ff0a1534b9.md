# # Solutions to Chapter 7 | Object Oriented Design

```
16 private CDPlayer cdPlayer;
17 private User user;
18 private Set<CD> cdCollection;
19 private TrackSelector ts;
20
21 public JukeBox(CDPlayer cdPlayer, User user, Set<CD> cdCollection,
22     TrackSelector ts) { ... }
23 public Song getCurrentTrack() { return ts.getCurrentSong(); }
24 public void processOneUser(User u) { this.user = u; }
25 }
```

```
27 public class Playlist {
28 private Song song;
29 private Queue<Song> queue;
30 public Playlist(Song song, Queue<Song> queue) { ... }
31 public Song getNextTrackToPlay() { return queue.peek(); }
32 public void queueUpTrack(Song s) { queue.add(s); }
33 }
```

```
35 public class Song {
36 private String songName;
37 }
39 public class TrackSelector {
40 private String currentSong;
41 public TrackSelector(Song s) { currentSong= s; }
42 public void setTrack(Song s) { currentSong = s; }
43 public Song getCurrentSong() { return currentSong; }
44 }
```

```
46 public class User {
47 private String name;
48 public String getName() { return name; }
49 public void setName(String name) { this.name = name; }
50 public long getID() { return ID; }
51 public void setID(long ID) { ID = ID; }
52 private long ID;
53 private User(String name, long ID) { ... }
54 public User getUser() { return this; }
55 public static User addUser(String name, long ID) { {...}
56 }
```