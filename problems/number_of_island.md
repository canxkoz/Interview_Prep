## Question

Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Source: https://leetcode.com/problems/number-of-islands/

## Solution

```python
class UnionFind():
    def __init__(self, values, lands):
        self.values = values
        self.parent = {i:i for i in values}
        self.size = {i:1 for i in values}
        self.groups = lands

    # Find with path compression
    def find(self, x):
        root = self.parent.get(x)
        while root != self.parent.get(root):
            root = self.parent.get(root)

        while x != root:
            x, self.parent[x] = self.parent[x], root
        return root

    # Union with size
    def union(self,x, y):
        x_root = self.find(x)
        y_root = self.find(y)
        if x_root == y_root: return False

        x_size = self.size[x_root]
        y_size = self.size[y_root]

        if x_size < y_size:
            self.parent[y_root] = x_root
            self.size[x_root] += y_size
        else:
            self.parent[x_root] = y_root
            self.size[y_root] += x_size

        self.groups -= 1

    def __len__(self):
        return self.groups

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        row,col = len(grid), len(grid[0])
        lands = sum([Counter(grid[i]).get("1",0) for i in range(row)])

        uf = UnionFind(list(range(row*col)), lands)

        def is_valid(nr,nc):
            return not(nr < 0 or nc < 0 or nr >= row or nc >= col)

        for r in range(row):
            for c in range(col):
                index = r * len(grid[0]) + c
                if grid[r][c] != '1': continue

                for x,y in [(0,1),(1,0),(-1,0),(0,-1)]:
                    nr,nc = r+x,c+y
                    if not is_valid(nr,nc):continue

                    nindex = nr * len(grid[0]) + nc
                    if grid[nr][nc] == grid[r][c]:
                        uf.union(index,nindex)
        return len(uf)

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid: return

        row, col = len(grid), len(grid[0])
        groups = 0
        queue = deque([[0]])
        visited = set()
        directions = [(0,1), (1,0), (-1,0), (0,-1)]

        def is_valid(r,c):
            return r >= 0 and \
                    c >= 0 and \
                    r < row and \
                    c < col and \
                    grid[r][c] == "1" and \
                    not (r,c) in visited

        for r in range(row):
            for c in range(col):
                if not is_valid(r, c): continue

                queue = deque([(r,c)])
                groups += 1
                while queue:
                    cur_row, cur_col = queue.popleft()
                    for x,y in directions:
                        new_row, new_col = cur_row + x, cur_col + y
                        if not is_valid(new_row, new_col): continue
                        queue.append((new_row, new_col))
                    visited.add((cur_row,cur_col))
        return groups

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid: return
        directions = [(0,1), (1,0), (-1,0), (0,-1)]
        row, col = len(grid), len(grid[0])

        def dfs(r, c):
            if r < 0 or c < 0 or r >= row or c >= col or grid[r][c] != "1": return
            grid[r][c] = "#"
            for x,y in directions:
                nr,nc = r + x, c + y
                dfs(nr,nc)

        count = 0
        for r in range(len(grid)):
            for c in range(len(grid[0])):
                if grid[r][c] != "1": continue
                dfs(r,c)
                count += 1
        return count





```
