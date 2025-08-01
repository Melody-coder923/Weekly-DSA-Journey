#Common Matrix Flip Types
###1. 🔁 Horizontal Flip (Left-Right Mirror)
![alt text](image.png)

**Solution1:**
```
def flip_horizontal(matrix):
    n = len(matrix)
    for i in range(n):
        left, right = 0, n - 1
        while left < right:
            matrix[i][left], matrix[i][right] = matrix[i][right], matrix[i][left]
            left += 1
            right -= 1
```

**Solution2:**
🎯 Tip: Use reverse() or two pointers to swap elements in each row.
```
def flip_horizontal_v2(matrix):
    for row in matrix:
        row.reverse()
```

###2. 🔁 Vertical Flip (Top-Bottom Mirror)
![alt text](image-1.png)

**Solution1:**
```
def flip_vertical(matrix):
    n = len(matrix)
    top, bottom = 0, n - 1
    while top < bottom:
        matrix[top], matrix[bottom] = matrix[bottom], matrix[top]
        top += 1
        bottom -= 1
```

**Solution2:**
🎯 Tip: Use matrix.reverse() to flip the entire matrix vertically.
```
def flip_vertical_v2(matrix):
    matrix.reverse()
```

###3. 🔁 Main Diagonal Flip (Top-Left to Bottom-Right)
Transpose the matrix (mirror over main diagonal).
![alt text](image-2.png)

🎯 Tip: Swap (i, j) with (j, i) for all i < j (upper triangle only).
```
def transpose_main_diagonal(matrix):
    n = len(matrix)
    for i in range(n):
        for j in range(i + 1, n): #upper triangle
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
```
###4. 🔁 Anti-Diagonal Flip (Top-Right to Bottom-Left)
Mirror the matrix over the anti-diagonal.
![alt text](image-3.png)

🎯 Tip: Use the formula: matrix[i][j] ↔ matrix[n-1-j][n-1-i]. Only swap elements above the anti-diagonal.

```
def flip_anti_diagonal(matrix):
    n = len(matrix)
    for i in range(n):
        for j in range(n - i - 1):
            matrix[i][j], matrix[n - 1 - j][n - 1 - i] = matrix[n - 1 - j][n - 1 - i], matrix[i][j]
```

###5. 🔁 Rotate 90° Clockwise
Rotate the matrix 90 degrees to the right.
![alt text](image-4.png)

🎯 Tip:
- Step 1: Transpose (main diagonal)
- Step 2: Horizontal flip

```
def rotate_90_clockwise(matrix):
    n = len(matrix)
    for i in range(n):
        for j in range(i + 1, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    for row in matrix:
        row.reverse()
```
```
def rotate_90_clockwise_v2(matrix):
    n = len(matrix)
    # 从外层到内层处理
    for layer in range(n // 2):
        first, last = layer, n - 1 - layer
        for i in range(first, last):
            offset = i - first
            # 保存top
            top = matrix[first][i]
            # left → top
            matrix[first][i] = matrix[last-offset][first]
            # bottom → left
            matrix[last-offset][first] = matrix[last][last-offset]
            # right → bottom
            matrix[last][last-offset] = matrix[i][last]
            # top → right
            matrix[i][last] = top
```


###6. 🔁 Rotate 90° Counterclockwise
Rotate the matrix 90 degrees to the left.
![alt text](image-5.png)

🎯 Tip:
- Step 1: Transpose (main diagonal)
- Step 2: Vertical flip
```
def rotate_90_counterclockwise(matrix):
    n = len(matrix)
    for i in range(n):
        for j in range(i + 1, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    matrix.reverse()
```

```
def rotate_90_counterclockwise_v2(matrix):
    n = len(matrix)
    for layer in range(n // 2):
        first, last = layer, n - 1 - layer
        for i in range(first, last):
            offset = i - first
            # 保存top
            top = matrix[first][i]
            # right → top
            matrix[first][i] = matrix[i][last]
            # bottom → right
            matrix[i][last] = matrix[last][last-offset]
            # left → bottom
            matrix[last][last-offset] = matrix[last-offset][first]
            # top → left
            matrix[last-offset][first] = top
```

###7. 🔁Rotate 180°
Rotate the matrix 180 degrees (flip both horizontally and vertically).
This is equivalent to rotating the matrix twice by 90°, or flipping it around its center.
![alt text](image-6.png)

🎯 Tip:
- 180° rotation = horizontal flip + vertical flip (order doesn't matter).
- Can be done in-place for square matrices.
- Alternatively, reverse both row and column indices manually: matrix[i][j] ↔ matrix[n-1-i][n-1-j]

**In-place for square matrix**
This code carefully avoids double-swapping when (i, j) and (n-1-i, n-1-j) meet in the center.
```
def rotate_180(matrix):
    n = len(matrix)
    for i in range(n // 2 + n % 2):
        for j in range(n):
            ni, nj = n - 1 - i, n - 1 - j
            # Swap (i, j) with (ni, nj)
            matrix[i][j], matrix[ni][nj] = matrix[ni][nj], matrix[i][j]
```

**Simple version using flips**
Works for both square and rectangular matrices.
```
def rotate_180(matrix):
    # Vertical flip
    matrix.reverse()
    # Horizontal flip each row
    for row in matrix:
        row.reverse()
```
###🌀 Rotation and Flip Equivalences

✅ 90° Clockwise = Transpose + Horizontal Flip

✅ 90° Counterclockwise = Transpose + Vertical Flip = Horizontal Flip + Transpose

✅ 180° Rotation = Horizontal Flip + Vertical Flip = 90° Clockwise + 90° Clockwise

🧠 Memory Aids
Transpose: Flip across the main diagonal
→ "Diagonal fold"

Horizontal Flip: Mirror left to right
→ "Left-right symmetry"

Vertical Flip: Mirror top to bottom
→ "Up-down symmetry"

90° Clockwise: Transpose then horizontal flip
→ "Transpose, then mirror left-right"

90° Counterclockwise: Transpose then vertical flip
→ "Transpose, then mirror top-bottom"
→ Alternatively: mirror left-right, then transpose