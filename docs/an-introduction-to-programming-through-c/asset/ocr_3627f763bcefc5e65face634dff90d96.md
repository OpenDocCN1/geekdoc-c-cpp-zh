The above observations gives us a recursive algorithm for determining if a given position P is winning or losing. We determine all moves m_i possible in P, and the positions P_i they lead to. The we determine (recursively!) whether P_i are winning or losing. If we find some P_i that is losing, we declare P to be winning. Otherwise if all P_i are winning, we declare P to be losing. We know that in order for a recursive algorithm to work we must ensure that two things:

+   1. Each subproblem we are required to solve is simpler than the original. In our case this is true in the sense that each P_i must have at least one stone less than P, and is hence simpler.
+   2. We can argue that eventually we will reach some ("simplest") problems which we can solve directly. Clearly, as the game progresses we will reach the situation in which no stone remains. As discussed, this is a losing position.

Thus we can write a program to determine whether a Nim position is winning or losing. We give this program for the case of 3 piles, but you can see that it can be easily extended for a larger number of piles. The function winning given below takes a game position and returns true if the position is winning, and false if the position is losing.

```
bool winning(int x, int y, int z)
// x,y,z = number of stones in the 3 piles.
// returns true if this is a winning position.
{
    if(x==0 && y==0 && z==0) return false; // base case

    for(int i=1; i<=x; ++i)            // Pick i stones from pile 1
        if (!winning(x-i,y,z)) return true; // if a losing next state is found

    for(int i=1; i<=y; ++i)            // Pick i stones from pile 2
        if (!winning(x,y-i,z)) return true; // if a losing next state is found

    for(int i=1; i<=z; ++i)            // Pick i stones from pile 3
        if (!winning(x,y,z-i)) return true; // if a losing next state is found

    return false;                      // if all next states are winning
}
```

The function can be called using a main program such as the one below.

```
int main(){
    int x,y,z;
    cout << 'Give the number of stones in the 3 piles: ';
    cin >> x >> y >> z;
    if (winning(x,y,z)) cout << 'Wins.' << endl;
    else cout << 'Loses.'<<endl;
}
```