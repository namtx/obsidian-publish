[Leetcode - Maximum Candies Allocated to K Children](https://leetcode.com/problems/maximum-candies-allocated-to-k-children/)

### Binary search

[[Binary Search]]

Assume we want to give `m` candies, for each pile of `candies[i]`,
we can divide out at most `candies[i]/m` sub piles with each pile `m` candies.
We can sum up to sub piles we can divide out, then compare with the `k` children.

If `k > sum`, we can not allocate to all children, since the pile of `m` candies is too big, so we assign `right = m-1`

If `k < sum`, we are able to allocate to every child, since the pile of `m` candies is small enough so we assign `left = m`.

We repeatly do this untile `left == right`, and that's the maxium number of candies each child can get.


```java
class Solution {
	public int maximumCandies(int[] candies, long k) {
		int left = 0;
		int right = 10_000_000;
		while(left < right) {
			long sum = 0;
			int mid = (left + right + 1) / 2;
			for (int candy: candies) {
				sum += candy / mid;
			}
			if (k > sum) {
				right = mid - 1;
			} else {
				left = mid;
			}
		}

		return left;
	}
}
```
