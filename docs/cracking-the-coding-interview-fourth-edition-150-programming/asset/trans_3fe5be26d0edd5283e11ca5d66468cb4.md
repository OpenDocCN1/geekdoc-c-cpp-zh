

# 第3章解答 | 栈与队列

```java
13 disks = new Stack<Integer>();
14 index = i;
15 
16 
17 public int index() {
18     return index;
19 }
20 
21 public void add(int d) {
22     if (!disks.isEmpty() && disks.peek() <= d) {
23         System.out.println("Error placing disk " + d);
24     } else {
25         disks.push(d);
26     }
27 }
28 
29 public void moveTo(Tower t) {
30     int top = disks.pop();
31     t.add(top);
32     System.out.println("Move disk " + top + " from " + index + 
         " to " + t.index());
34 }
```

```java
43 public void move(int n, Tower destination, Tower buffer) {
44     if (n > 0) {
45         moveDisks(n - 1, buffer, destination);
46         moveTo(destination);
47         buffer.moveDisks(n - 1, destination, this);
48     }
49 }
```

# 第3章解答 | 栈与队列

3.5 实现一个 `MyQueue` 类，该类使用两个栈来实现队列。

# 解答

由于队列和栈的主要区别在于顺序（先进先出 vs. 后进先出），我们知道需要修改 `peek()` 和 `pop()` 以实现相反的顺序。我们可以使用第二个栈来反转元素的顺序（通过从 `s1` 弹出元素并推入 `s2`）。在这样的实现中，在每次执行 `peek()` 和 `pop()` 操作时，我们都会将 `s1` 中的所有元素弹出到 `s2`，执行 `peek`/`pop` 操作，然后将所有元素推回去。

这种方法可行，但如果连续执行两次 `pop` / `peek` 操作，我们就会徒谓地移动元素。我们可以实现一种“懒性”方法，让元素留在 `s2` 中。

因此，`s1` 的顺序将是最新元素在栈顶，而 `s2` 将是最旧元素在栈顶。我们将新元素推入 `s1`，并从 `s2` 进行 `peek` 和 `pop`。当 `s2` 为空时，我们将 `s1` 中的所有元素按反序转移到 `s2`。

```java
public class MyQueue<T> {
    Stack<T> s1, s2;
    public MyQueue() {
        s1 = new Stack<T>();
        s2 = new Stack<T>();
    }
    public int size() {
        return s1.size() + s2.size();
    }
    public void add(T value) {
        s1.push(value);
    }
    public T peek() {
        if (s2.empty()) return s2.peek(); // 注意：此处代码逻辑似乎有误，但按原文
        while (!s1.empty()) s2.push(s1.pop());
        return s2.peek();
    }
    public T remove() {
        if (s2.empty()) return s2.pop(); // 注意：此处代码逻辑似乎有误，但按原文
        while (!s1.empty()) s2.push(s1.pop());
        return s2.pop();
    }
}
```

# 第3章解答 | 栈与队列

3.6 编写一个程序对栈进行升序排序。你不应该对栈的实现方式做任何假设。编写此程序时只能使用以下函数：`push` | `pop` | `peek` | `isEmpty`。

# 解答

排序可以通过额外的栈来完成。思路是从原始栈中取出一个元素并将其推入另一个栈中。如果推入该元素会违反新栈的排序顺序，我们需要从新栈中移除足够的元素，以便推入新元素。由于我们移除的元素在原始栈中，我们回到了起点。该算法的时间复杂度为 O(N^2)，如下如下所示。

```java
1 public static Stack<Integer> sort(Stack<Integer> s) {
2   Stack<Integer> r = new Stack<Integer>();
3   while(!s.isEmpty()) {
4     int tmp = s.pop();
5     while(!r.isEmpty() && r.peek() > tmp) {
6       s.push(r.pop());
7     }
8     r.push(tmp);
9   }
10  return r;
11 }
```

# 第4章解答 | 树与图

4.1 实现一个函数来检查树是否平衡。对于本题，平衡树定义为：没有任何叶子节点到根节点的距离差超过1的树。

# 解答

该思路非常简单：最小深度和最大深度之差不应超过1，因为最小深度与最大深度之差是树中可能的最大差异。

```java
public static int maxDepth(TreeNode root) {
    if (root == null) {
        return 0;
    }
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
public static int minDepth(TreeNode root) {
    if (root == null) {
        return 0;
    }
    return 1 + Math.min(minDepth(root.left), minDepth(root.right));
}
public static boolean isBalanced(TreeNode root) {
    return (maxDepth(root) - minDepth(root) <= 1);
}
```

# 第4章解答 | 树与图

4.2 给定一个有向图，设计一个算法判断两个节点之间是否存在路径。

# 解答

这个问题可以通过图遍历来解决，例如深度优先搜索或广度优先搜索。我们从一个节点开始，并在遍历检查是否找到了另一个节点。我们应该将算法过程中发现的任何节点标记为已访问，以避免循环和节点重复。

```java
public enum State {
    Unvisited, Visited, Visiting;
}
public static boolean search(Graph g, Node start, Node end) {
    LinkedList<Node> q = new LinkedList<Node>(); // 作为栈操作
    for (Node u : g.getNodes()) {
        u.state = State.Unvisited;
    }
    start.state = State.Visiting;
    q.add(start);
    Node u;
    while (!q.isEmpty()) {
        u = q.removeFirst();
        if (u != null) {
            for (Node v : u.getAdjacent()) {
                if (v.state == State.Unvisited) {
                    if (v == end) {
                        return true;
                    } else {
                        v.state = State.Visiting;
                        q.add(v);
                    }
                }
            }
        }
        u.state = State.Visited;
    }
    return false;
}
```

# 第4章解答 | 树与图

4.3 给定一个排序好的（升序）数组，编写一个算法创建一个高度最小的二叉树。

# 解答

我们将尝试创建一个二叉树，使得对于每个节点，如果可能，左子树和右子树的节点数相等。

算法：
1. 将数组的中间元素插入树中。
2. 将左子数组插入（左子树）。
3. 将右子数组插入（右子树）。
4. 递归

```java
1 public static TreeNode addTree(int arr[], int start, int end) {
2   if (end < start) {
3     return null;
4   }
5   int mid = (start + end) / 2;
6   TreeNode node = new TreeNode(arr[mid]);
7   node.left = addTree(arr, start, mid - 1);
8   node.right = addTree(arr, mid + 1, end);
9   return node;
10 }
```

# 第4章解答 | 树与图

4.4 给定一个二叉搜索树，设计一个算法找到给定节点的“下一个”节点（例如中序后继），其中每个节点都有指向父节点的链接。

# 解答

我们通过仔细思考中序遍历的情况来处理这个问题。我们访问 X.left，然后是 X，最后是 X.right。

所以，如果我们想找到 X.successor()执行以下操作：

1. 如果 X 有右孩子，那么后继节点在 X 的右侧（根据访问顺序）。具体来说，最左的节点是该子树中第一个被访问的节点。
2. 否则，前往 X 的父节点（称为 P）。
2.a. 如果 X 是左孩子（P = X），那么 P 就是 X 的后继节点。
2.b. 如果 X 是右孩子（P.right = X），那么我们已经完全访问了 P，因此调用 successor(P)。

```java
public static TreeNode inorderSucc(TreeNode e) {
    if (e == null) return null;
    TreeNode p;
    // 找到右孩子 -> 返回右侧第一个中序节点
    if (e.parent == null || e.right != null) {
        p = leftMostChild(e.right);
    } else {
        // 向上直到我们处于左侧而不是 e.parent（情况 2b）
        while ((p = e.parent) != null) {
            if (p.left == e) {
                break;
            }
            e = p;
        }
    }
    return p;
}

public static TreeNode leftMostChild(TreeNode e) {
    if (e == null) return null;
    while (e.left != null) e = e.left;
    return e;
}
```

