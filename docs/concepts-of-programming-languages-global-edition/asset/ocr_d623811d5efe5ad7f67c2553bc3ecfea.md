# Figure 9.3

Two possible execution control sequences for two coroutines without loops

![](bbox=[0.26, 0.115, 0.88, 0.38])

(a)

![](bbox=[0.22, 0.47, 0.85, 0.73])

(b)

# Figure 9.4

Coroutine execution sequence with loops

![](bbox=[0.26, 0.79, 0.94, 0.94])

causes control to return to coroutine A, the semantics is that A continues from where it ended its last execution. In particular, its local variables have the values left them by the previous activation. Figure 9.3b shows an alternative execution sequence of coroutines A and B. In this case, B is started by the master unit.