### Tips
- Always use `left < right`
- `mid = (left + right + 1)/2` VS `mid = (left + right)/2`
	- `mid = (left + right)/2` to find **`first`** valid element
	- `mid = (left + right + 1)/2` to find **`last`** valid element

### Valid Triangle Number

[Leetcode - Valid Triangle Number](https://leetcode.com/problems/valid-triangle-number/)

```java
package dev.namtx.leetcode;  
  
import java.util.Arrays;  
  
public class ValidTriangleNumber {
    public int triangleNumber(int[] nums) {  
        Arrays.sort(nums);  
        int ans = 0;  
  
        for (int i = nums.length - 1; i >= 0; i--) {  
            int left = 0;  
            int right = i - 1;  
            while (left < right) {  
                if (nums[left] + nums[right] > nums[i]) {  
                    ans += right - left;  
                    right--;  
                } else {  
                    left++;  
                }  
            }  
        }  
  
        return ans;  
    }  
}
```