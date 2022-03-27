[Geeks for Geeks](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/?ref=lbp)

### Recursive - O(n^2)

```java
// Time complexity: O(n^2)  
private TreeNode helper(int[] nums, int start, int end) {  
	if (start > end) return null;  
	if (start == end) return new TreeNode(nums[start]);  
	TreeNode root = new TreeNode(nums[start]);  
	int i;
	// find the first node greater than current
	for (i = start + 1; i <= end; i++) {  
		if (nums[i] > nums[start]) break;  
	}  
	root.right = helper(nums, i, end);  
	root.left = helper(nums, start + 1, i - 1);
	
	return root;  
}
```

### Recursive with O(n)

```java
// Time complexity: O(n)  
private TreeNode helper2(int[] nums, int max, int min, Index preIndex) {  
	if (preIndex.index >= nums.length) return null;  
	int val = nums[preIndex.index];  
	
	TreeNode root = null;  
	if (val > min && val < max) {  
		root = new TreeNode(val);  
		preIndex.index = preIndex.index + 1;  
		if (preIndex.index < nums.length) {  
			root.left = helper2(nums, val, min, preIndex);  
		}  
		if (preIndex.index < nums.length) {  
			root.right = helper2(nums, max, val, preIndex);  
		}  
	}  
	return root;  
}  
  
static class Index {  
 int index = 0;  
}

```

### Stack - O(n)

1. Create a empty stack
2. Make the first value as the root, push it to the stack
3. Keep on popping while the stack is not empty and the next value is greater than stack's top value. Make this value as the right node child of the last popped node. Push the new node to the stack.
4. If the next lvau is less than the stack's top value, make this value as the left child of the stack's top node. Push the new node to the stack.
5. Repeat steps 2 and 3 until there a items remaining in `nums`

```java

private TreeNode helper3(int[] nums) {  
	Stack<TreeNode> stack = new Stack<>();  
	TreeNode root = new TreeNode(nums[0]);  
	stack.push(root);  

	for (int i = 1; i < nums.length; i++) {  
		TreeNode node = new TreeNode(nums[i]);  
		if (stack.peek().val > nums[i]) {  
			stack.peek().left = node;  
			stack.push(node);  
		} else {  
			TreeNode current = stack.peek();  
			while (!stack.isEmpty() && stack.peek().val < nums[i]) {  
				current = stack.pop();  
			}  
			current.right = node;  
		}  
		stack.push(node);  
	}  

	return root;  
}
```