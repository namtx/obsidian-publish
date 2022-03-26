### Search
```java
public TreeNode search(TreeNode root, int key) {
	if (root == null || root.val == key) return root;

	if (root.val > key) {
		return search(root.right, key);
	}

	return search(root.left, key);
}
```

### Insertion
```java
public TreeNode insert(TreeNode root, int val) {
	if (root == null) {
		root = new TreeNode(val);
		return root;
	}

	if (root.val < val) {
		root.right = insert(root.right, val);
	} else if (root.val > val) {
		root.left = insert(root.left, val);
	}

	return root;
}
```

### Time complexity
- The worst-case time complexity of search and insert operation is `O(h)` where h is the height of the BST.

### Insertion using loop

```java
class BinarySearchTree {
	TreeNode root;

	public void insert(int val) {
		TreeNode node = new TreeNode(val);
		if (root == null) {
			root = node;
			return;
		}

		TreeNode prev = null;
		TreeNode tmp = root;
		while(tmp != null) {
			if (tmp.val > key) {
				prev = tmp;
				tmp = tmp.left;
			} else if (tmp.val < key) {
				prev = tmp;
				tmp = tmp.right;
			}
		}

		if (prev.val > val) {
			prev.left = node;
		} else prev.right = node;
	}
}
```

### Leetcode Problems
- [https://leetcode.com/problems/insert-into-a-binary-search-tree/](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

### References
- [Geeks for Geeks](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)