# Table 10.4 OBST computation for Example 10.2 after step 4

| | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 0 | w<sub>00</sub> = 2<br>c<sub>00</sub> = 0<br>r<sub>00</sub> = 0 | w<sub>11</sub> = 3<br>c<sub>11</sub> = 0<br>r<sub>11</sub> = 0 | w<sub>22</sub> = 1<br>c<sub>22</sub> = 0<br>r<sub>22</sub> = 0 | w<sub>33</sub> = 1<br>c<sub>33</sub> = 0<br>r<sub>33</sub> = 0 | w<sub>44</sub> = 1<br>c<sub>44</sub> = 0<br>r<sub>44</sub> = 0 |
| 1 | w<sub>01</sub> = 8<br>c<sub>01</sub> = 8<br>r<sub>01</sub> = 1 | w<sub>12</sub> = 7<br>c<sub>12</sub> = 7<br>r<sub>12</sub> = 2 | w<sub>23</sub> = 3<br>c<sub>23</sub> = 3<br>r<sub>23</sub> = 3 | w<sub>34</sub> = 3<br>c<sub>34</sub> = 3<br>r<sub>34</sub> = 4 | |
| 2 | w<sub>02</sub> = 12<br>c<sub>02</sub> = 19<br>r<sub>02</sub> = 1 | w<sub>13</sub> = 9<br>c<sub>13</sub> = 12<br>r<sub>13</sub> = 2 | w<sub>24</sub> = 5<br>c<sub>24</sub> = 8<br>r<sub>24</sub> = 3 | | |
| 3 | w<sub>03</sub> = 14<br>c<sub>03</sub> = 25<br>r<sub>03</sub> = 2 | w<sub>14</sub> = 11<br>c<sub>14</sub> = 19<br>r<sub>14</sub> = 2 | Here j - i = 3,<br>that is, while<br>computing c,<br>a took three<br>values. | | |
| 4 | | | | | |

Step 5: Compute c(i, j) for j - i = 4
w(0, 4) = p(4) + q(4) + w(0, 3) = 1 + 1 + 14 = 16
c(0, 4) = w(0, 4) + min[c(0, 0) + c(1, 4) for a = 1, c(0, 1) + c(2, 4) for a = 2,
c(0, 2) + c(3, 4) for a = 3, c(0, 3) + c(4, 4) for a = 4]
= 16 + min[0 + 19, 8 + 8, 19 + 3, 25 + 0]
= 16 + min[19, 16, 22, 25]
= 16 + 16 = 32
r(0, 4) = 2

All these computations are shown in Table 10.5.

# Table 10.5 OBST computation for Example 10.2 after step 5

| | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 0 | w<sub>00</sub> = 2<br>c<sub>00</sub> = 0<br>r<sub>00</sub> = 0 | w<sub>11</sub> = 3<br>c<sub>11</sub> = 0<br>r<sub>11</sub> = 0 | w<sub>22</sub> = 1<br>c<sub>22</sub> = 0<br>r<sub>22</sub> = 0 | w<sub>33</sub> = 1<br>c<sub>33</sub> = 0<br>r<sub>33</sub> = 0 | w<sub>44</sub> = 1<br>c<sub>44</sub> = 0<br>r<sub>44</sub> = 0 |
| 1 | w<sub>01</sub> = 8<br>c<sub>01</sub> = 8<br>r<sub>01</sub> = 1 | w<sub>12</sub> = 7<br>c<sub>12</sub> = 7<br>r<sub>12</sub> = 2 | w<sub>23</sub> = 3<br>c<sub>23</sub> = 3<br>r<sub>23</sub> = 3 | w<sub>34</sub> = 3<br>c<sub>34</sub> = 3<br>r<sub>34</sub> = 4 | |
| 2 | w<sub>02</sub> = 12<br>c<sub>02</sub> = 19<br>r<sub>02</sub> = 1 | w<sub>13</sub> = 9<br>c<sub>13</sub> = 12<br>r<sub>13</sub> = 2 | w<sub>24</sub> = 5<br>c<sub>24</sub> = 8<br>r<sub>24</sub> = 3 | | |
| 3 | w<sub>03</sub> = 14<br>c<sub>03</sub> = 25<br>r<sub>03</sub> = 2 | w<sub>14</sub> = 11<br>c<sub>14</sub> = 19<br>r<sub>14</sub> = 2 | | | |
| 4 | w<sub>04</sub> = 16<br>c<sub>04</sub> = 32<br>r<sub>04</sub> = 2 | | | | |