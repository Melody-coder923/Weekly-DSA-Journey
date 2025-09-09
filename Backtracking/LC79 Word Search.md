"""
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        if not board or not board[0] or not word:
            return False
        m, n = len(board), len(board[0])
        directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]

        def dfs(x, y, index):
            if x<0 or y<0 or x>=m or y>=n or board[x][y]==1 or board[x][y]!=word[index]:
                return False
            if index==len(word)-1:
                return True
            temp=board[x][y]
            board[x][y]=1
            for dx,dy in directions:
                nx,ny=x+dx, y+dy
                if dfs(nx, ny, index + 1):
                        return True
            board[x][y] = temp
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == word[0]:  # 找到首字母
                    if dfs(i, j, 0):  # 从这里开始DFS
                        return True
        return False
  """
