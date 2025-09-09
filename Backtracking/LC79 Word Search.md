```python
from typing import List

class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        m, n = len(board), len(board[0])
        if len(word) > m * n:
            return False

        directions = [(1,0), (-1,0), (0,1), (0,-1)]

        def dfs(x, y, index):
            if x < 0 or x >= m or y < 0 or y >= n:
                return False
            if board[x][y] != word[index]:
                return False
            if index == len(word) - 1:
                return True

            temp = board[x][y]
            board[x][y] = '#'

            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if dfs(nx, ny, index + 1):
                    return True

            board[x][y] = temp
            return False

        for i in range(m):
            for j in range(n):
                if board[i][j] == word[0]:
                    if dfs(i, j, 0):
                        return True
        return False
```
