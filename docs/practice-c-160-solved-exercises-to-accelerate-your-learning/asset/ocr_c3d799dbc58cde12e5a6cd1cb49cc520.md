```
for (int i = 0; i < m; i++) {
    for (int j = 0; j < n; j++) {
        if (matrix[i][j] == 1) std::cout << "M";
        else std::cout << result[i][j] << " ";
    }
    std::cout << "\n";
}

return 0;
}
```

# 135. Make a function that receives a 3x3 matrix representing the game of tic-tac-toe, and check if there is a winner, if there is a tie, or if the game is not over yet

#include <iostream>
#include <vector>

```
enum class GameState {
    X_Wins,
    O_Wins,
```