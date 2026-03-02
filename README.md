# The cheapest way

This repository contains my solution for the **"The cheapest way"** problem from Yandex CodeRun.

## Problem Statement

You are given an `N x M` grid. Each cell contains a number (the "food cost" or "penalty"). A player starts at the top-left cell `(0, 0)` and wants to reach the bottom-right cell `(N-1, M-1)`. The player can only move **right** or **down**. The total cost is the sum of the numbers in all visited cells, including the first and the last one.

**Goal:** Find the **minimum possible total cost** to reach the destination.

### Input Format
*   The first line contains two integers `N` and `M` (1 ≤ N, M ≤ 20).
*   The next `N` lines each contain `M` integers (from 0 to 100) representing the grid.

### Output Format
*   Print a single integer — the minimum total cost.

## Solution Approach

This problem is solved using **Dynamic Programming (DP)** .

We create a DP table `dp` of the same size as the grid, where `dp[i][j]` represents the minimum cost to reach cell `(i, j)` from `(0, 0)`.

**Recurrence relation:**
Since we can only come from the top `(i-1, j)` or from the left `(i, j-1)`, the cost is calculated as:
`dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`

**Base Cases:**
*   `dp[0][0] = grid[0][0]` (starting point).
*   The first row `(i = 0)` can only be reached from the left.
*   The first column `(j = 0)` can only be reached from the top.

The answer is stored in `dp[N-1][M-1]`.

### Complexity
*   **Time complexity:** O(N * M) — we iterate through each cell once.
*   **Space complexity:** O(N * M) — for the DP table.

## Code (Python)

```python
n, m = map(int, input().split())
grid = [list(map(int, input().split())) for _ in range(n)]

dp = [[0] * m for _ in range(n)]

dp[0][0] = grid[0][0]

# Fill the first column
for i in range(1, n):
    dp[i][0] = dp[i-1][0] + grid[i][0]

# Fill the first row
for j in range(1, m):
    dp[0][j] = dp[0][j-1] + grid[0][j]

# Fill the rest of the table
for i in range(1, n):
    for j in range(1, m):
        dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])

print(dp[n-1][m-1])
