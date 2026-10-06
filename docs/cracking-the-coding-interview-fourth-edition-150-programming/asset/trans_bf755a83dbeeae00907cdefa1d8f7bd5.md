

## 第 7 章解决方案 | 面向对象设计

7.3 使用面向对象的原理设计一个音乐自动点唱机。

让我们先了解基础系统组件：

- CD 播放器
- CD
- 显示器 ()（显示歌曲长度、剩余时间和播放列表）

现在，让我们进一步细分它：

- 播放列表创建（包括添加、删除、洗牌等子功能）
- CD 选择器
- 轨道选择器
- 歌曲入队
- 从播放列表中获取下一首歌曲

我们还可以引入用户：

- 添加
- 删除
- 额度信息

我们如何根据对象（结合在一起的数据 + 函数）对这些功能进行分组？

面向对象的设计建议将数据与其操作操作函数封装在单一的实体类中。

```java
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
    private CDPlayer cdPlayer;
    private User user;
    private Set<CD> cdCollection;
    private TrackSelector ts;

    public JukeBox(CDPlayer cdPlayer, User user, Set<CD> cdCollection,
        TrackSelector ts) { ... }
    public Song getCurrentTrack() { return ts.getCurrentSong(); }
    public void processOneUser(User u) { this.user = u; }
}
```

```java
public class Playlist {
    private Song song;
    private Queue<Song> queue;
    public Playlist(Song song, Queue<Song> queue) { ... }
    public Song getNextTrackToPlay() { return queue.peek(); }
    public void queueUpTrack(Song s) { queue.add(s); }
}
```

```java
public class Song {
    private String songName;
}
public class TrackSelector {
    private String currentSong;
    public TrackSelector(Song s) { currentSong= s; }
    public void setTrack(Song s) { currentSong = s; }
    public Song getCurrentSong() { return currentSong; }
}
```

```java
public class User {
    private String name;
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public long getID() { return ID; }
    public void setID(long ID) { ID = ID; }
    private long ID;
    private User(String name, long ID) { ... }
    public User getUser() { return this; }
    public static User addUser(String name, long ID) { {...} }
}
```

## 第 7 章解决方案 | 面向对象设计

7.4 使用面向对象的原理设计一个象棋游戏。

# 解决方案

```java
public class ChessPieceTurn { };
public class GameManager {
    void processTurn(PlayerBase player) { };
    boolean acceptTurn(ChessPieceTurn t) { return true; };
    Position currentPosition;
}
public abstract class PlayerBase {
    public abstract ChessPieceTurn getTurn(Position p);
}
class ComputerPlayer extends PlayerBase {
    public ChessPieceTurn getTurn(Position p) { return null };
    public void setDifficulty() { };
    public PositionEstimator estimator;
    public PositionBackTracker backtracker;
}
public class HumanPlayer extends PlayerBase {
    public ChessPieceTurn getTurn(Position p) { return null };
}
public abstract class ChessPieceBase {
    abstract boolean canBeChecked();
    abstract boolean isSupportCastle();
}
public class King extends ChessPieceBase { ... }
public class Queen extends ChessPieceBase { ... }
public class Position { // 代表紧凑形式的象棋位置
    ArrayList<ChessPieceBase> black;
    ArrayList<ChessPieceBase> white;
}
public class PositionBackTracker {
    public static Position getNext(Position p) { return null };
}
public class PositionEstimator {
    public static PositionPotentialValue estimate(Position p) { ... }
}
public abstract class PositionPotentialValue {
    abstract boolean lessThan(PositionPotentialValue pv);
}
```

## 第 7 章解决方案 | 面向对象设计

7.5 为在线图书阅读器系统设计数据结构。

# 解决方案

由于问题没有描述太多功能，让我们假设我们要设计一个基础的在线阅读系统，提供以下功能：

- 用户会员的创建和扩展。
- 搜索书籍数据库
- 阅读书籍

为了实现这些功能，我们可能需要许多其他函数，如 get、set、update 等。需要的对象可能包括 User、Book 和 Library。

以下代码类通过面向对象的设计描述了这些功能：

```java
public class Book {
    private long ID;
    private String details;
    private static Set<Book> books;

    public Book(long ID, String details) { ... }
    public static void addBook(long ID, String details) {
        books.add(new Book(id, details));
    }

    public void update() { }
    public static void delete(Book b) { books.remove(b); }
    public void find(long id) {
        for (Book b : books) {
            if (b.getID() == id) return b;
        }
        return null;
    }
}
```

```java
public class User {
    private long ID;
    private String details;
    private int accountType;
    private Set<User> users;

    public User(long ID, String details, int accountType) { ... }
    public static void addUser(long ID, String details, int accountType) {
        users.add(new User(ID, details, accountType));
    }

    public void renewMembership() { }
    public static void delete(User u) { users.remove(u); }
    public static User find(long id) {
        for (User u : users) {
            if (u.getID() == id) return u;
        }
        return null;
    }
}
```

```java
public class OnlineReaderSystem {
    private Book b;
    private User u;
    public OnlineReaderSystem(Book b, User u) { ... }
    public void list() { }
    public void search(long id) { }
    public void display() { }
}
```
（注：此处部分代码逻辑根据上下文进行了结构补全以保持逻辑性，原文意为设计描述）

