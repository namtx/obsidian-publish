[Leetcode - Increasing Order Search Tree](https://leetcode.com/problems/increasing-order-search-tree)

### Submission

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode increasingBST(TreeNode root) {
        if (root == null) return null;

        if (root.left == null) {
            root.right = increasingBST(root.right);
            return root;
        } else {
            TreeNode node = increasingBST(root.left);
            root.right = increasingBST(root.right);
            root.left = null;
            TreeNode current = node;
            while(current.right != null) {
                current = current.right;
            }
            current.right = root;
            return node;
        }
    }
}
```

### Better Submission

```java
public TreeNode increasingBST(TreeNode root, TreeNode tail) {  
	if (root == null) return tail;  
  
	TreeNode res = increasingBST(root.left, root);  
	root.left = null;  
	root.right = increasingBST(root.right, tail);  
	return res;  
}
```

![[Pasted image 20220327153712.png]]