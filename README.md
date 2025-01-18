# Leetcode---1368
Minimum Cost To Make at Least One Valid Path in a Grid
// code in java
import java.util.*;

class Solution {
    private static final int[][] DIRECTIONS = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    private static final int[] COST = {0, 1, 1, 1};

    public int minCost(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] cost = new int[m][n];
        for (int[] row : cost) Arrays.fill(row, Integer.MAX_VALUE);
        cost[0][0] = 0;

        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[2]));
        pq.offer(new int[]{0, 0, 0});

        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int x = curr[0], y = curr[1], c = curr[2];

            if (x == m - 1 && y == n - 1) return c;

            for (int i = 0; i < 4; i++) {
                int nx = x + DIRECTIONS[i][0], ny = y + DIRECTIONS[i][1];
                if (nx >= 0 && ny >= 0 && nx < m && ny < n) {
                    int newCost = c + (grid[x][y] == i + 1 ? 0 : 1);
                    if (newCost < cost[nx][ny]) {
                        cost[nx][ny] = newCost;
                        pq.offer(new int[]{nx, ny, newCost});
                    }
                }
            }
        }

        return -1;
    }
}
