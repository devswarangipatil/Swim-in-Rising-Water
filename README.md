# Swim-in-Rising-Water

You are given an n x n integer matrix grid where each value grid[i][j] represents the elevation at that point (i, j).
It starts raining, and water gradually rises over time. At time t, the water level is t, meaning any cell with elevation less than equal to t is submerged or reachable.
You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares individually are at most t. You can swim infinite distances in zero time. Of course, you must stay within the boundaries of the grid during your swim.
Return the minimum time until you can reach the bottom right square (n - 1, n - 1) if you start at the top left square (0, 0).

import heapq

class Solution:
    def swimInWater(self, grid):
        n = len(grid)
        m = len(grid[0])
        directions = [(0,1), (0,-1), (1,0), (-1,0)]
        
        pq = [(grid[0][0], 0, 0)]
        visited = [[False]*m for _ in range(n)]
        
        while pq:
            time, x, y = heapq.heappop(pq)
            if visited[x][y]:
                continue
            visited[x][y] = True
            if x == n - 1 and y == m - 1:
                return time
            for dx, dy in directions:
                cx, cy = x + dx, y + dy
                if 0 <= cx < n and 0 <= cy < m and not visited[cx][cy]:
                    heapq.heappush(pq, (max(time, grid[cx][cy]), cx, cy))
        return -1

