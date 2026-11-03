does not want tea, the algorithm will follow step 1 and directly step 4. The semicolon at the end of step 2 indicates that tea and biscuits are offered together. You will notice that the positioning of End-if (at step 3 or 4) has made all the difference! The Figs 1.8 (a) and 1.8 (b) show the corresponding flow charts.

```
Begin
1. If the guest wants tea
2. Then make tea
3. End-if
4. Offer biscuits
End
```

Fig. 1.7(a) Offer biscuits to all guests

```
Begin
1. If the guest wants tea
2. Then make tea;
3. offer biscuits
4. End-if
End
```

Fig. 1.7(b) Offer biscuits only to guests who want tea

![](bbox=[0.22, 0.48, 0.78, 0.7])

Fig. 1.8(a)

Fig. 1.8(b)

In both of these cases (a and b), we have not specified the action if the guest wants coffee. Let us modify our algorithm and also the flow chart to accommodate that possibility. Note that we are offering coffee as an alternative to tea. We will be generous enough to offer biscuits in either case. Since we want to offer the biscuits irrespective of the acceptance/rejection of tea/coffee offer, we should consider only the first algorithm for modification, viz. Fig. 1.7(a). The modified algorithm and its corresponding flow chart are shown in Figs 1.9 and 1.10 respectively.

```
Begin
1. If the guest wants tea
2. Then make tea
3. End-if
4. If the guest wants coffee
5. Then make coffee
6. End-if
7. Offer biscuits
End
```

Fig. 1.9 Algorithm for offering tea/coffee and biscuits