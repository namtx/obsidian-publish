[Leetcode - Minimum Limit of Balls in a Bag](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag/)

#### Approach

[[Binary Search]]

The maximum penalty is `max(nums)` and the minimum is `1`.
Do a Binary Search in range `1..max(nums)` to find the lowest penalty, with the constraint that total `operations` is lower than `maxOperations`.

This problem is the same with [[Koko Eating Bananas]]
 and [[Maximum Candies Allocated to K Children]]

To optimize, we can find the `min(nums)` and do a Binary Search in range `min..max` instead.

But we have to care the case when all values in `nums` are the same, so `min === max`.

#### Submission

```java
class Solution {
    public int minimumSize(int[] nums, int maxOperations) {
        int min = Integer.MAX_VALUE;
        int max = 0;
        for (int num: nums) {
            min = Math.min(min, num);
            max = Math.max(max, num);
        }

        if (nums.length == 1) {
            return (int) Math.ceil((float)max/(maxOperations+1));
        }
        int left = max == min ? 1 : min;
        int right = max;
        while(left < right) {
            int operations = 0;
            int mid = (left + right)/2;
            for (int num: nums) {
                if (num > mid) {
                    if (num % mid == 0) {
                        operations += (num/mid)-1;
                    } else {
                        operations += (num / mid);
                    }
                }
            }
            if (operations > maxOperations) {
                left = mid+1;
            } else {
                right = mid;
            }
        }

        return left;
    }
}
```