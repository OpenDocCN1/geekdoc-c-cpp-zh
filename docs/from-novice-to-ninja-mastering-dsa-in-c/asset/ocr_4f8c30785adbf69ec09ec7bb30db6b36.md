```
for (int neighbor : graph[currentNode]) {
    if (!visited[neighbor]) {
        visited[neighbor] = true;
        nodeQueue.push(neighbor);
    }
}
}
}

int main() {
    // Performing BFS starting from node 0
    std::cout << "BFS starting from node 0: ";
    bfs(0);
    std::cout << std::endl;

    return 0;
}
```

# Combining Stacks and Queues for Complex Problems:

Now we’ll solve a problem using stack & queue together.

# Problem: Evaluating Postfix Expressions::

Combining stacks and queues can be effective in solving more complex problems. For instance, in evaluating postfix expressions, a stack can be used to track operands, and a queue can help manage the sequence of operations.

```
#include <iostream>
#include <stack>
#include <queue>
#include <sstream>

int evaluatePostfix(const std::string& expression) {
    std::stack<int> operandStack;
    std::istringstream iss(expression);
    std::string token;

    while (iss >> token) {
        if (isdigit(token[0])) {
            operandStack.push(std::stoi(token));
        } else {
            int operand2 = operandStack.top();
            operandStack.pop();
```