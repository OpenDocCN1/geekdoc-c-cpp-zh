```
public:
Puzzle(int disks);
void move_single_disk(int from, int to);
void move(int ndisk, int from, int to);
void print() const;
private:
vector<int> towers[3];
};
```

The constructor populates the leftmost tower with the given number of disks, with the largest disk at the bottom:

```
Puzzle::Puzzle(int ndisk)
{
    for (int d = ndisk; d >= 1; d--)
    {
        towers[0].push_back(d);
    }
}
```

The move_single_disk member function moves a single disk from one tower to another:

```
void Puzzle::move_single_disk(int from, int to)
{
    int last = towers[from].size() - 1;
    int disk = towers[from][last];
    towers[from].pop_back();
    towers[to].push_back(disk);
}
```

As with the preceding solution, the move function recursively moves a smaller pile of disks, then a single disk, and then again the smaller pile:

```
void Puzzle::move(int disks, int from, int to)
{
    if (disks > 0)
    {
        int other = 3 - from - to;
        move(disks - 1, from, other);
        move_single_disk(from, to);
        print();
        move(disks - 1, other, to);
    }
}
```

We also print the towers. The program output is:

5 4 3 2 1 | | 
5 4 3 2 | 1 | 
5 4 3 | 2 | 1 
5 4 3 | 2 1 | 
5 4 | 2 1 | 3 
5 4 1 | 2 | 3 
5 4 1 | | 3 2 
5 | 4 | 3 2 1 
5 | 4 1 | 3 2 
5 2 | 4 1 | 3 
5 2 1 | 4 | 3 
5 2 1 | 4 3 | 
5 2 | 4 3 | 1