## Question

You are given a graph that started as a tree with n nodes labeled from 1 to n, with one additional edge added. The added edge has two different vertices chosen from 1 to n, and was not an edge that already existed. The graph is represented as an array edges of length n where edges[i] = [ai, bi] indicates that there is an edge between nodes ai and bi in the graph.

Return an edge that can be removed so that the resulting graph is a tree of n nodes. If there are multiple answers, return the answer that occurs last in the input.

## Solution
Always prefer the Iterative DFS approach because Recursive can make 1000 calls at maximum in Python Language. Iterative approach is limited with the RAM which is a lot more than the 1000 calls that the recursive one can make.

The solution below uses defaultdict(list) ours.
```python
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        graph = defaultdict(list)
        
        def dfs(src, target):
            if src in visited: return
            if src == target: return True
            visited.add(src)
            for n in graph[src]:
                if dfs(n, target):
                    return True
            return False
        
        for src, dest in edges:
            visited = set()
            if dfs(src, dest): 
                return [src, dest]
            
            graph[src].append(dest)
            graph[dest].append(src)
```

Our solution uses graphs - w.o. defaultdict. - will be fixed.
```python
class Solution:
    def findRedundantConnection(self, edges):
        graph = {}
        for src, dest in edges:
            if dfs(graph, src, dest):
                return[src, dest]
            else:
                if src in graph:
                    graph[src].append(dest)
                else:
                    graph[src] = [dest]

            if dest in graph:
                graph[dest].append(src)
            else:
                graph[dest] = [src]
```


The solution below uses defaultdict(set). - On leet code
```python
class Solution(object):
    def findRedundantConnection(self, edges):
        graph = collections.defaultdict(set)

        def dfs(source, target):
            if source not in seen:
                seen.add(source)
                if source == target: return True
                return any(dfs(nei, target) for nei in graph[source])

        for u, v in edges:
            seen = set()
            if u in graph and v in graph and dfs(u, v):
                return u, v
            graph[u].add(v)
            graph[v].add(u)
```

https://www.youtube.com/watch?v=wU6udHRIkcc&t=69s
Kruskal Algo detects a cycle in a graph.
Disjoint sets are different than normal sets than Mathematical sets.

The solution below uses disjoit sets. - On leet code

```python
class DSU(object):
    def __init__(self):
        self.par = range(1001)
        self.rnk = [0] * 1001

    def find(self, x):
        if self.par[x] != x:
            self.par[x] = self.find(self.par[x])
        return self.par[x]

    def union(self, x, y):
        xr, yr = self.find(x), self.find(y)
        if xr == yr:
            return False
        elif self.rnk[xr] < self.rnk[yr]:
            self.par[xr] = yr
        elif self.rnk[xr] > self.rnk[yr]:
            self.par[yr] = xr
        else:
            self.par[yr] = xr
            self.rnk[xr] += 1
        return True

class Solution(object):
    def findRedundantConnection(self, edges):
        dsu = DSU()
        for edge in edges:
            if not dsu.union(*edge):
                return edge
```





