[Leetcode - Unique Binary Search Tree II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

### Approach
- Dynamic programming
- DFS

### Submission

```java
class Solution {
    public List<TreeNode> generateTrees(int n) {
        List<TreeNode>[][] memo = new List[n + 1][n + 1];
        return dfs(1, n, memo);
    }

    private List<TreeNode> dfs(int min, int max, List<TreeNode>[][] memo) {
        if (min > max) {
            List<TreeNode> base = new ArrayList<>();
            base.add(null);
            return base;
        }
        if (min == max) {
            List<TreeNode> base = new ArrayList<>();
            base.add(new TreeNode(min));
            memo[min][max] = base;
            return base;
        }
        if (memo[min][max] != null) {
            return memo[min][max];
        }

        List<TreeNode> trees = new ArrayList<>();

        for (int i = min; i <= max; i++) {
            for (TreeNode left : dfs(min, i - 1, memo)) {
                for (TreeNode right : dfs(i + 1, max, memo)) {
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    trees.add(root);
                }
            }
        }

        return trees;
    }
}
```