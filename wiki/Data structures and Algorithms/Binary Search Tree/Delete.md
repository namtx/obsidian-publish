
### Two steps
- Find the element we wish to remove (if it exists)
- Replace the node we want to remove with its successor (if any) to maintain the BST invariant

#### Find the element

[[Search And Insertion]]

#### Delete the element

Four cases:

![[delete bst four cases.png]]

- Case 1: leaf node
	- remove it immediately
- Case 2, 3: either the left/child node is substree
	- The successor of the node we are trying to remove ins these cases will be the root node of the left/rigth substree.
- Case 4: Node to remove has both the left subtree and a right subtree
	- In which subtree will the successor of the node we are trying to remove be?
	- The answer is both, the successor can either the largest value inf the left substree or the smallest value in the right subtree.

### Source code

```java
/**  
 * Remove the node from the Binary Search Tree
 */
public class DeleteInBST {  
	public static void main(String[] args) {  
		TreeNode root = new TreeNode(  
			50,  
			new TreeNode(30, new TreeNode(20), new TreeNode(40)),  
			new TreeNode(70, new TreeNode(60), new TreeNode(80))  
		);  
		root = new DeleteInBST().delete(root, 50);  
		System.out.println(root);  
	}
  
	public TreeNode delete(TreeNode root, int val) {  
		if (root == null) return null;  
	  
		if (root.val < val) {  
			// recursive to the right subtree  
			root.right = delete(root.right, val);  
		} else if (root.val > val) {  
			// recursive to the left subtree  
			root.left = delete(root.left, val);  
		} else {    
			if (root.left == null)  
				return root.right;  
			else if (root.right == null)  
				return root.left;  
			// both the smallest in right subtree and biggest in the left subtree would work  
			TreeNode smallestNodeFromRightSubtree = findTheSmallest(root.right);  
			root.val = smallestNodeFromRightSubtree.val;  
			root.right = delete(root.right, smallestNodeFromRightSubtree.val);  
		}  
	  
		return root;  
	}  
  
	public TreeNode findTheSmallest(TreeNode root) {  
		if (root.left == null) return root;  
	  
		return findTheSmallest(root.left);  
	}
}
```


### Optiomal version

```java
/**  
 * Optimal version of remove a TreeNode in BST 
 */
public class BSTNodeRemoval {  
	public TreeNode remove(TreeNode root, int val) {  
		if (root == null) return null;  

		if (root.val > val) {  
			root.left = remove(root.left, val);  
		} else if (root.val < val) {  
			root.right = remove(root.right, val);  
		} else {  
			if (root.left == null) {  
				return root.right;  
			} else if (root.right == null) {  
				return root.left;  
			} else {  
				TreeNode successorParent = root;  
				TreeNode successor = root.right;  

				while(successor.left != null) {  
					successorParent = successor;  
					successor = successor.left;  
				}  

				if (successorParent != root) {  
					successorParent.left = successor.right;  
				} else {  
					successorParent.right = successor.right;  
				}  

				root.val = successor.val;  
			}  
		}  

		return root;  
	}  
}
```

### References
- https://www.geeksforgeeks.org/binary-search-tree-set-2-delete/
- https://www.youtube.com/watch?v=8K7EO7s_iFE