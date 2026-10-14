```
*tptr++ = qPop(q);
printf("\tQ popping %c...\n", *(tptr-1));
}
while(!sEmpty(s)) {
char popop = sPop(s);
printf("\tS popping %c...\n", popop);
if( popop == ')' )
break;
*tptr++ = popop;
}
break;
default: {
int priop; // priority of op.
char topop; // operator on stack top.
int pritop; // priority of topop.
char asstop; // associativity of topop.
while(!sEmpty(s)) {
priop = getPriority(op);
topop = sTop(s);
pritop = getPriority(topop);
asstop = getAssociativity(topop);
if((pritop < priop) || (pritop == priop && asstop == 'L') || (topop == ')'))// IMP. break;
while(!qEmpty(q)) {
*tptr++ = qPop(q);
```