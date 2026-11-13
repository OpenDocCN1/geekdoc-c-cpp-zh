```
```cpp
else // (image[i][j]==BACKGROUND)
{
    state [i][j]=Known; DT[i][j]=0;
}

while(!narrowband.empty()) // 2. March the narrowband
{
    Pixel p = narrowband. getSmallest ( );
    state[p.i][p.j] = Known;

    set<Pixel> nbs; // 3. Get non-Known neighbors of p
    for(all Pixels n neighbors of p)
    {
        if (state [n.i][n.j]==Known) continue ;
        nbs.insert (n);
        if (state [n.i][n.j]==Band)
        {
            state [n.i][n.j]=Band;
            narrowband. insert(DT[n.i][n.j].n);
        }
    }

    for(all Pixels n in nbs) // 4. Compute DT of neighbors of p
    {
        float d=DT[n.i][n.j];
        d = min(d,update(n.i-1,n.i.n.j,n.j-1));
        d = min(d,update(n.i+1,n.i.n.j,n.j-1));
        d = min(d,update(n.i-1,n.i.n.j,n.j+1));
        d = min(d,update(n.i+1,n.i.n.j,n.j+1));
        if (d!=DT [n.i][n.j])
        {
            reinsert n in narrowband in order of d;
            DT[n.i][n.j] = d;
        }
    }
}

float update(int lr,int i,int j,int tb)
/// 3. Find distance of (i,j) to its neighbors (lr,j) and (i,tb)
{
    Pixel a=(lr,j), b=(i,tb), a=(i,j);
    if (state [lr][j]==Known)
    {
        if (state [i][tb]==Known)
        {
            float D1 = distance from Equation (9.38);
            float D2 = distance from Equation (9.39);
            if (D2>DT[lr][j] && D2>DT[i][tb]) return D2;
            if (D1>DT[lr][j] && D1>DT[i][tb]) return D1;
        }
        return DT[i][j];
    }
}
```
```