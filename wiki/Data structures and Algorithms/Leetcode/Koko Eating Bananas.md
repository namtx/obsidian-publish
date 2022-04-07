[Leetcode - Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

#### Approach

[[Binary Search]]

The maximum `k` is the maximum bananas in `piles`, and the minimum is `1` (Koko eats one banana each hour).
Do a binary seach in range `1..max`
For each `mid`, and `total` as the number of hours Koko needs to eat all bananas:
- If `total > h`, it means Koko needs to eat faster, so `left = mid + 1`
- If `total <= h`, it means Koko can eat all bananas within `total` hours, and since Koko likes to eat slowly, we will assign `right = mid` to find better result.

#### Submission

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int left = 1;
        int max = 0;
        for (int pile : piles) {
            max = Math.max(max, pile);
        }
        int right = max;
        while (left < right) {
            int total = 0;
            int mid = (left + right) / 2;
            for (int pile : piles) {
                if (pile <= mid) {
                    total++;
                    continue;
                }
                if (pile % mid == 0) {
                    total += pile / mid;
                } else {
                    total += pile / mid + 1;
                }
            }
            if (total <= h) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```