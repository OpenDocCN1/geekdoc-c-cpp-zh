```
1 ( ((p_cd[0] & 0x01) != 0)
2 ^ ((p_cd[0] & 0x10) != 0)
3 ^ ((p_ab[0] & 0x10) == 0)
4 ^ (e_puf[idx] == '\'+')
5 ^ (idx < 7) )
6 V
7 ( ((p_cd[0] & 0x01) != 0)
8 ^ ((p_cd[0] & 0x10) != 0)
9 ^ (e_puf[idx] == '\'-')
10 ^ ((p_ab[0] & 0x10) == 0)
11 ^ (e_puf[idx] != '\'+')
12 ^ (idx < 7) )
```

Figure 7.14: Static patch condition for ptb_like

```
1 .. , V
2 ( e_puf == <unknown>
3 ^ idx == 0
4 ^ p_cd == {1, 1}
5 ^ p_ab == {0, 1}
6 ^ ((p_cd[0] & 0x01) != 0)
7 ^ ((p_cd[0] & 0x10) != 0)
8 ^ (e_puf[idx] == '\'-')
9 ^ ((p_ab[0] & 0x10) == 0)
10 ^ (e_puf[idx] != '\'+')
11 ^ (idx < 7) )
12 V . . .
```

Figure 7.15: Excerpt of a dynamic patch condition for ptb_like