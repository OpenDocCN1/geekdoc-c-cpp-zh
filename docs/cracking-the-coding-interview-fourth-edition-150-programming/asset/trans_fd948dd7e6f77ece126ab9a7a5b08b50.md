

## 第 12 章解答 | 系统设计与内存限制

这种情况下呢？

通常，在 BFS 中，我们通过在节点类中设置一个 `visited` 标志来将节点标记为已访问。在这里我们不想这样做（因为可能同时有多个搜索在运行，所以直接修改我们的数据是不好的）。在这种情况下，我们可以使用哈希表来模拟节点的标记，通过查找节点 ID 来判断它是否被访问。

其他跟进问题：

- 在现实世界中，服务器会故障。这会对你产生什么影响？
- 你可以如何利用缓存？
- 你会一直搜索到图的末尾（无限）吗？你如何决定何时放弃？
- 在现实生活中，有些人的朋友的朋友比其他人多，因此他们更有可能在你和某人之间建立路径。你如何利用这些数据来选择从何处开始遍历？

以下代码演示了我们的算法：

```java
public class Server {
    ArrayList<Machine> machines = new ArrayList<Machine>();
}

public class Machine {
    public ArrayList<Person> persons = new ArrayList<Person>();
}

public class Person {
    private ArrayList<Integer> friends;
    private int ID;
    private int machineID;
    private String info;
    private Server server = new Server();

    public String getInfo() { return info; }
    public void setInfo(String info) {
        this.info = info;
    }

    public int[] getFriends() {
        int[] temp = new int[friends.size()];
        for (int i = 0; i < temp.length; i++) {
            temp[i] = friends.get(i);
        }
        return temp;
    }
}
```

```java
public int getID() { return ID; }
public int getMachineID() { return machineID; }
public void addFriend(int id) { friends.add(id); }

// 给定 ID 和 Machine ID 查找人员
public Person lookupFriend(int machineID, int id) {
    for (Machine m : server.machines) {
        if (m.machineID == machineID) {
            for (Person p : m.persons) {
                if (p.ID == ID)
                    return p;
            }
        }
    }
    return null;
}

// 给定 machine ID 查找机器
public Machine lookupMachine(int machineID) {
    for (Machine m : server.machines) {
        if (m.machineID == machineID)
            return m;
    }
    return null;
}

public Person(int ID, int machineID) {
    this.ID = ID;
    this.machineID = machineID;
}
```

## 12.3 给定一个包含四十亿个整数的输入文件，提供一个算法生成一个不在文件中的整数。假设你有 1 GB 的内存。

### 跟进问题
如果你只有 10 MB 内存怎么办？

### 解答

总共有 2^32 或 40 亿个不同的整数。我们有 1 GB 内存，即 80 亿位（bits）。

因此，通过 80 亿位，我们可以利用内存将所有可能的整数映射到不同的位上。逻辑如下：

1. 创建一个大小为 40 亿的位向量 (BV)。
2. 将 BV 初始化为全 0。
3. 扫描文件中的所有数字 (num) 并写入 BV[num] = 1；
4. 现在再次从索引 0 开始扫描 BV。
5. 返回第一个值为 0 的索引。

```java
byte[] bitfield = new byte[0xFFFFFFFF];
void findOpenNumber(int number) throws FileNotFoundException {
    Scanner in = new Scanner(new FileReader("input_file_q1_4.txt"));
    while (in.hasNextInt()) {
        int n = in.nextInt();
        /** 使用 OR 运算符设置字节的第 n 位，在 bitfield
        * 中查找对应的数字（例如，10 对应于
        * 字节数组索引 2 的第 2 个位）。 */
        bitfield[n / 8] |= 1 << (n % 8);
    }
    for (int i = 0; i < bitfield.length; i++) {
        for (int j = 0; j < 8; j++) {
            /** 获取每个字节的各个位。当发现 0 位
            * 时，找到对应的值。 */
            if ((bitfield[i] & (1 << j)) == 0) {
                System.out.println(i * 8 + j);
                return;
            }
        }
    }
}
```

## 跟进：如果我们只有 10 MB 怎么办？

只需对数据进行两次扫描即可找到缺失的整数。我们可以将整数分成若干大小的块（稍后我们将讨论如何决定大小）。假设我们将整数分成 1000 个一组的块。所以块 0 代表 0 到 999，块 1 代表 1000-1999，以此此类推。由于 int 的范围是有限的，我们知道需要的块数量也是有限的。

在第一次扫描中，我们统计每个块中有多少个整数。也就是说，如果我们看到 52，我们就知道它在块 0 中，增加计数器 counter[0]。如果我们看到 1415，我们就知道它在块 1 中，增加 counter[1]。在第二次扫描中，我们从索引 0 开始扫描 BV（注：原文此处逻辑略有误，应为扫描块，译文根据语境调整）。返回第一个值为 0 的索引。

（注：原文此部分逻辑描述存在部分重复和表述混乱，译文已根据原意进行翻译）

