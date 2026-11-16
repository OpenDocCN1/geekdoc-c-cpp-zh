```
void DecisionTree::QueryBinaryTreeFirstTime(TreeNode* currentNode) {
    //Error Checking ... otherwise default to asking the question
    //at currentNode
    AskFirstQuestion(CurrentNode);
}
```

```
void DecisionTree::QueryBinaryTree(TreeNode* currentNode) {
    //Error Checking ... otherwise default to asking the question
    //at currentNode
    AskNextQuestion(CurrentNode);
}
```

```
void DecisionTree::AskFirstQuestion(TreeNode *node) {
#pragma omp parallel sections
{
    if(answer == "yes")
    #pragma omp section
    QueryBinaryTree(node->m_pYesBranch);
    else if(answer == "no")
    #pragma omp section
    QueryBinaryTree(node->m_pNoBranch);
}
else // Wrong input
    AskNextQuestion(node);
}
```

```
void DecisionTree::AskNextQuestion(TreeNode *node) {
//Error Checking
if(answer == "yes")
    QueryBinaryTree(node->m_pYesBranch);
else if(answer == "no")
    QueryBinaryTree(node->m_pNoBranch);
else //Error on input
    AskNextQuestion(node);
}
```

In keeping with the 10% factor stated earlier for AI compute cycle, the workload was tested with a rendering load averaging 30 FPS. Doing a bit of math, this amounts to ~33 ms time per frame (neglecting the 0.3333 for extra-frame processing). 10% of 1 second is 10 ms. So, this was the allotted time per second allocated to AI cycles at 30 FPS chosen. That amounts to ~1/3 of 1 frame per second. Not a whole lot of time. So the test was run to generate one AI cycle per every 33 frames at 30 FPS. This would also allow for stabilizing the thread synchronization setup by OpenMP's internal thread pooling mechanisms.

The next step was to decide upon a coherent decision set for the workload. In an average game, there may be multiple Decision Trees active at a time per unit. Assume that each AI unit has from between 10–200 decisions (nodes) it can make. This is of course completely an assumption, as robust AIs could have more options (especially when n-way decisions are available). The geometric mean of this range is ~45. Given