"""
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
        if not mat or not mat[0]:
            return []
        m, n = len(mat), len(mat[0])
        result = []

        for k in range(m+n-1):
            temp=[]
            i=0 if k<n else k-n+1
            j=k if k<n else n-1
            while i < m and j >= 0:
                temp.append(mat[i][j])
                i += 1
                j -= 1
            # 偶数对角线，反转加入
            if k % 2 == 0:
                result.extend(temp[::-1])
            else:
                result.extend(temp)

        return result
"""
