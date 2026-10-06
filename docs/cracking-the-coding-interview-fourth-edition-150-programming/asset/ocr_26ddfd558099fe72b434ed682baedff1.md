# Solutions to Chapter 7 | Object Oriented Design

7.3 Design a musical juke box using object oriented principles.

Let's first understand the basic system components:

+   - CD player
- CD
- Display () (displays length of song, remaining time and playlist)

Now, let's break this down further:

+   - Playlist creation (includes add, delete, shuffle etc sub functionalities)
- CD selector
- Track selector
- Queueing up a song
- Get next song from playlist

A user also can be introduced:

+   - Adding
- Deleting
- Credit information

How do we group this functionality based on Objects (data + functions which go together)?

Object oriented design suggests wrapping up data with their operating functions in a single entity class.

```
public class CD {
  public class CDPlayer {
    private Playlist p;
    private CD c;
    public Playlist getPlaylist() { return p; }
    public void setPlaylist(Playlist p) { this.p = p; }
    public CD getCD() { return c; }
    public void setCD(CD c) { this.c = c; }
    public CDPlayer(Playlist p) { this.p = p; }
    public CDPlayer(CD c, Playlist p) { ... }
    public CDPlayer(CD c) { this.c = c; }
    public void playTrack(Song s) { ... }
  }
}
public class JukeBox {
```