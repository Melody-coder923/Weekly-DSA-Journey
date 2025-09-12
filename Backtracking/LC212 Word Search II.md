"""
class TrieNode:
    def __init__(self):
        self.children={}
        self.is_end=False
        self.is_word=None
class Trie:
    def __init__(self):
        self.root=TrieNode()
    def insert(self,word):
        cur=self.root
        for char in word:
            if char not in cur.children:
                cur.children[char]=TrieNode()
            cur=cur.children[char]
        cur.is_end=True
        cur.is_word=word

class Solution:   
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        trie = Trie()
        for word in words:
            trie.insert(word)
        m,n=len(board),len(board[0])
        visited = [[False]*n for _ in range(m)]
        directions = [(-1,0), (1,0), (0,-1), (0,1)]
        res = []
        
        def dfs(x,y,node):
            if x<0 or x>=m or y<0 or y>=n or visited[x][y]==True:
                return 
            ch = board[x][y]
            if ch not in node.children:
                return
            visited[x][y] = True
            node = node.children[ch]
            if node.is_end:
                res.append(node.is_word)
                node.is_end=False
            for dx, dy in directions:
                dfs(x + dx, y + dy, node)
            visited[x][y] = False

        for i in range(m):
            for j in range(n):
                dfs(i, j, trie.root)
        return res
"""
