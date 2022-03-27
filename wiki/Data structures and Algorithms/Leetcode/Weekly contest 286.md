### Weekly contest 286

#### Find the difference of two arrays
Difficulty: Easy

Approach: `HashMap`

```java
class Solution {
    public List<List<Integer>> findDifference(int[] nums1, int[] nums2) {
        Map<Integer, Boolean> m1 = new HashMap<>();
        Map<Integer, Boolean> m2 = new HashMap<>();
        
        for (int num: nums1) {
            m1.put(num, true);
        }
        for(int num: nums2) {
            m2.put(num, true);
        }
        
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(new ArrayList<>());
        ans.add(new ArrayList<>());
        
        for (int num1: m1.keySet()) {
            if (!m2.containsKey(num1)) {
                ans.get(0).add(num1);
            }
        }
        
        for (int num2: m2.keySet()) {
            if (!m1.containsKey(num2)) {
                ans.get(1).add(num2);
            }
        }
        
        return ans;
    }
}
```

#### Minimum Deletions to Make Array Beautiful
Difficulty: Medium

Approach: Use a `offset` variable to determine when we have to delete a number from `nums`.

```java
class Solution {
    public int minDeletion(int[] nums) {
        int offset = 0;
        int ans = 0;

        for (int i = 0; i < nums.length-1; i++) {
            if (nums[i] == nums[i+1]) {
                if ((i + offset) % 2 == 0) {
                    offset = offset ^ 1;
                    ans++;
                }
            }
        }

        if ((nums.length + offset) % 2 != 0) ans++;

        return ans;
    }
}
```