

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_617_0.png)

# 图 12.4 间接递归

# 自测题（答案见附录 N）

SR 12.6 递归是必要的吗？

SR 12.7 何时应避免使用递归？

SR 12.8 描述以下递归方法返回的内容。

```
private static int exercise (int n)
{
    if (n < 0)
        return -1;
    else
        if (n < 10)
            return 1;
        else
            return 1 + exercise (n/10);
}
```

SR 12.9 编写一个递归方法，返回 5 * n 的值，其中 n > 0。参见自测题 12.5。解释为什么你通常不会使用递归来解决这个问题。

SR 12.10 什么是间接递归？

## 12.3 使用递归

以下每个部分描述了一个特定的递归问题。对于每个问题，我们检查递归在解决方案中如何发挥作用以及如何使用基本情况终止递归。在你检查这些示例时，请考虑为每个问题设计非递归解决方案的复杂程度。

## 遍历迷宫

解决迷宫涉及大量的试错：沿着一条路径前进，在无法继续时回溯，并尝试其他未尝试过的选项。这种活动通常使用递归处理得很好。清单 12.1 所示的程序创建一个 Maze 对象并尝试遍历它。

## 清单 12.1

```
//****************************************************************
// MazeSearch.java      Author: Lewis/Lofthus
//
// Demonstrates recursion.
//****************************************************************
public class MazeSearch
{
    //-------------------------------------------------------------
    // Creates a new maze, prints its original form, attempts to
    // solve it, and prints out its final form.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        Maze labyrinth = new Maze();

        System.out.println (labyrinth);

        if (labyrinth.traverse (0, 0))
            System.out.println ("The maze was successfully traversed!");
        else
            System.out.println ("There is no possible path.");

        System.out.println (labyrinth);
    }
}
```

## 输出

1110110001111
1011101111001
0000101010100
1110111010111
101000111001
1011111101111
1000000000000
1111111111111

## 清单 12.1 继续

```
The maze was successfully traversed!

7770110001111
307707771001
000707070300
7770777070333
7070000773003
7077777703333
7000000000000
7777777777777
```

Maze 类如清单 12.2 所示，使用二维整数数组表示迷宫。目标是从左上角（入口点）移动到右下角（出口点）。最初，1 表示畅通路径，0 表示被阻塞路径。随着迷宫被解决，这些数组元素会被更改为其他值，以指示尝试过的路径以及如果存在的话最终通过迷宫的成功路径。

## 清单 12.2

```java
/**
 * Maze.java Author: Lewis/Loftus
 */
// Represents a maze of characters. The goal is to get from the
// top left corner to the bottom right, following a path of 1s.
public class Maze
{
    private final int TRIED = 3;
    private final int PATH = 7;
    private int[][] grid = {
        {1,1,1,0,1,1,0,0,0,1,1,1},
        {1,0,1,1,0,1,1,1,1,0,1,0,1},
        {0,0,0,0,0,1,0,1,0,1,0,1,0,0},
        {1,1,1,0,1,1,0,1,0,1,1,1},
    };
}
```

## 清单 12.2 继续

```
{1,0,1,0,0,0,0,1,1,1,0,0,1},
{1,0,1,1,1,1,1,0,1,1,1,1},
{1,0,0,0,0,0,0,0,0,0,0,0},
{1,1,1,1,1,1,1,1,1,1,1,1} };

//------------------------------------------------------------
// Attempts to recursively traverse the maze. Inserts special
// characters indicating locations that have been tried and that
// eventually become part of the solution.
//------------------------------------------------------------
public boolean traverse (int row, int column)
{
    boolean done = false;

    if (valid (row, column))
    {
        grid[row][column] = TRIED;  // this cell has been tried

        if (row == grid.length-1 && column == grid[0].length-1)
            done = true;  // the maze is solved
        else
        {
            done = traverse (row+1, column);     // down
            if (!done)
                done = traverse (row, column+1);  // right
            if (!done)
                done = traverse (row-1, column);  // up
            if (!done)
                done = traverse (row, column-1);  // left
        }

        if (done)  // this location is part of the final path
            grid[row][column] = PATH;
    }
    return done;
}

//------------------------------------------------------------
// Determines if a specific location is valid.
//------------------------------------------------------------
private boolean valid (int row, int column)
{
    boolean result = false;

    // check if cell is in the bounds of the matrix
    if (row >= 0 && row < grid.length &&
        column >= 0 && column < grid[row].length)

        // check if cell is not blocked and not previously tried
        if (grid[row][column] == 1)
            result = true;

    return result;
}

//--------------------------------------------------
// Returns the maze as a string.
//--------------------------------------------------
public String toString ()
{
    String result = "\n";
    for (int row=0; row < grid.length; row++)
    {
        for (int column=0; column < grid[row].length; column++)
            result += grid[row][column] + "";
        result += "\n";
    }

    return result;
}
}
```

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_621_0.png)

VideoNote
追踪 MazeSearch 程序。

迷宫中唯一有效的移动方向是四个基本方向：下、右、上和左。不允许对角移动。在此示例中，迷宫为 8 行 13 列，尽管代码设计为可处理任意大小的迷宫。

让我们递归地思考这个问题。迷宫可以成功遍历，如果它可以从位置 (0, 0) 成功遍历。因此，迷宫可以成功遍历，如果它可以从 (0, 0) 相邻的任何位置成功遍历，即位置 (1, 0)、位置 (0, 1)、位置 (−1, 0) 或位置 (0, −1)。选择一个潜在的下一步，比如 (1, 0)，我们发现自己处于与之前相同类型的情况。要从新的当前位置成功遍历迷宫，我们必须从相邻位置成功遍历它。在任何时候，

一些相邻位置可能无效，可能被阻塞，或可能代表一条可能的成功路径。我们继续递归地进行此过程。如果到达基本情况位置 (7, 12)，则迷宫已成功遍历。

Maze 类中的递归方法称为 traverse。它返回一个布尔值，表示是否找到解决方案。首先该方法确定移动到指定行和列是否有效。移动被认为有效，如果它保持在网格边界内，并且网格中该位置包含 1，表示该方向的移动未被阻塞。对 traverse 的初始调用传入左上角位置 (0, 0)。

如果移动有效，则网格条目从 1 改为 3，标记此位置为已访问，以便以后我们不会重复走这一步。traverse 方法然后确定是否已通过到达右下角完成迷宫。因此，对于此问题，终止任何特定递归路径的基本情况实际上有三种可能性：

- 移动无效，因为移动超出边界
- 移动无效，因为移动之前已尝试过
- 移动到达最终位置

如果当前位置不是右下角，我们会在每个基本方向上搜索解决方案（如有必要）。首先，我们通过递归调用 traverse 方法并传入新位置向下查找。traverse 方法的逻辑使用此新位置重新开始。解决方案要么最终通过首先尝试从当前位置向下移动而找到，要么找不到。如果找不到，我们尝试向右移动。如果失败，我们尝试向上。最后，如果其他方向均未产生正确路径，我们尝试向左。如果从当前位置的任何方向都得不到正确解决方案，则此位置没有路径，traverse 返回 false。

如果从当前位置找到解决方案，则网格条目更改为 7。第一个 7 放置在右下角。下一个 7 放置在通向右下角的位置，依此类推，直到最后一个 7 放置在左上角。因此，当最终迷宫打印出来时，零仍表示被阻塞的路径，1 表示从未尝试过的开放路径，3 表示尝试过但未能产生正确解决方案的路径，7 表示迷宫最终解决方案的一部分。

请注意，在每次对 traverse 方法的调用中都有多个递归机会。取决于迷宫配置，可能会跟随其中任何一个或全部。虽然迷宫中可能存在多条路径，但递归在找到路径时终止。仔细跟踪此代码的执行，同时跟随迷宫数组，看看递归如何解决这个问题。然后考虑生成非递归解决方案的难度。

