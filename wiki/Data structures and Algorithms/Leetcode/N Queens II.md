[Leetcode - N Queens II](https://leetcode.com/problems/n-queens-ii)

### Submission

```java
class Solution {
    int ans;
    public int totalNQueens(int n) {
        boolean[][] marked = new boolean[n][n];
        backtrack(n, 0, marked);
        return ans;
    }

    private void backtrack(int n, int r, boolean[][] marked) {
        if (r == n) {
            ans++;
            return;
        }

        for (int j = 0; j < n; j++) {
            if (!marked[r][j]) {
                boolean[][] copied = cp(marked);
                markCell(r, j, marked, true);
                backtrack(n, r + 1, marked);
                marked = copied;
            }
        }
    }

    private boolean[][] cp(boolean[][] original) {
        boolean[][] r = new boolean[original.length][original[0].length];
        for (int i = 0; i < original.length; i++) {
            r[i] = Arrays.copyOf(original[i], original[i].length);
        }

        return r;
    }

    private void markCell(int r, int c, boolean[][] marked, boolean isPlaced) {
        // row
        int n = marked.length;
        for (int i = 0; i < n; i++) {
            marked[r][i] = isPlaced;
        }
        // col
        for (int i = 0; i < n; i++) {
            marked[i][c] = isPlaced;
        }
        // /
        int i = r;
        int j = c;
        while (i >= 0 && j < n) {
            marked[i][j] = isPlaced;
            i--;
            j++;
        }
        // /
        i = r;
        j = c;
        while (i < n && j >= 0) {
            marked[i][j] = isPlaced;
            i++;
            j--;
        }
        // \
        i = r;
        j = c;
        while (i >= 0 && j >= 0) {
            marked[i][j] = isPlaced;
            i--;
            j--;
        }
        i = r;
        j = c;
        while (i < n && j < n) {
            marked[i][j] = isPlaced;
            i++;
            j++;
        }
    }
}
```