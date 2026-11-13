# Parent (\(\pi\))

| Steps | S | U | V | Y | X |
|---|---|---|---|---|---|
| | Nil | Nil | Nil | Nil | Nil |
| 1 | | S | | | S |
| 2 | | X | X | X | |
| 3 | | | Y | | |
| 4 | | | U | | |

**STEP-1** Consider the vertex S
Now Since the Adj(S) = (X,U) now implement Relax with (S,U) and (S,X,Y)
Relax(s,u,w)
d[s] + w(s,u) < d[u] = 0 + 10 < \(\infty\) so d[u] = 10 and \(\pi\)(u) = S
Relax(s,x,w)
d[s] + w(s,x) < d[x] = 0 + 5 < \(\infty\) so d[x] = 5 and \(\pi\)(x) = S delete S

**STEP-2** Consider the vertex X (minimum)
Now Since the Adj(X) = (U,Y,V) now implement Relax with (X,U) (X,Y)and (X,V)
Relax(x,u,w)
d[x] + w(x,u) < d[u] = 5 + 3 < 10 so d[u] = 8 and \(\pi\)(u) = X
Relax(x,v,w)
d[x] + w(x,v) < d[v] = 5 + 9 < \(\infty\) so d[v] = 14 and \(\pi\)(v) = X
Relax(x,y,w)
d[x] + w(x,y) < d[y] = 5 + 2 < \(\infty\) so d[y] = 7 and \(\pi\)(x) = X delete X

**STEP-3** Consider the vertex Y (minimum)
Now Since the Adj(Y) = (S,V) now implement Relax with (Y,S) (Y,V)
Relax(y,s,w)
d[y] + w(y,s) < d[s] = 7 + 7 < 0 (False)
Relax(y,v,w)
d[y] + w(y,v) < d[v] = 7 + 6 < 14 so d[v] = 13 and \(\pi\)(v) = Y
delete Y