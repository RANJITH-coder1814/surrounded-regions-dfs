# 🧩 Surrounded Regions (LeetCode 130)

## 📌 Problem Statement

Given an `m x n` matrix `board` containing `'X'` and `'O'`, capture all regions surrounded by `'X'`.

* A region is formed by connecting adjacent `'O'` cells (horizontal or vertical).
* A region is **surrounded** if it is completely enclosed by `'X'` and **not connected to the boundary**.

👉 Convert all such surrounded `'O'` into `'X'` **in-place**.

---

## 💡 Intuition

Instead of directly finding surrounded regions:

* Any `'O'` connected to the **boundary** is **safe** (cannot be flipped).
* So:

  1. Traverse boundary and mark connected `'O'` as safe.
  2. Flip remaining `'O'` → `'X'`.
  3. Restore safe cells.

---

## 🚀 Approach (DFS)

1. Run DFS from all boundary `'O'` cells.
2. Mark them as `'T'` (temporary safe).
3. Traverse the board:

   * `'O'` → `'X'` (captured)
   * `'T'` → `'O'` (restore)

---

## 💻 Code (C++)

```cpp
class Solution {
public:
    int m, n;

    void dfs(vector<vector<char>>& board, int i, int j) {
        if (i < 0 || j < 0 || i >= m || j >= n || board[i][j] != 'O')
            return;

        board[i][j] = 'T';

        dfs(board, i+1, j);
        dfs(board, i-1, j);
        dfs(board, i, j+1);
        dfs(board, i, j-1);
    }

    void solve(vector<vector<char>>& board) {
        if (board.empty()) return;

        m = board.size();
        n = board[0].size();

        // Traverse boundaries
        for (int i = 0; i < m; i++) {
            if (board[i][0] == 'O') dfs(board, i, 0);
            if (board[i][n-1] == 'O') dfs(board, i, n-1);
        }

        for (int j = 0; j < n; j++) {
            if (board[0][j] == 'O') dfs(board, 0, j);
            if (board[m-1][j] == 'O') dfs(board, m-1, j);
        }

        // Flip cells
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'O')
                    board[i][j] = 'X';
                else if (board[i][j] == 'T')
                    board[i][j] = 'O';
            }
        }
    }
};
```

---

## ⏱ Complexity

* **Time Complexity:** `O(m × n)`
* **Space Complexity:** `O(m × n)` (recursion stack)

---



---
