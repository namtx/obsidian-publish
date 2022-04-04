[Leetcode - K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

### Priority Queue
We can easily solve this problem with [[Priority Queue]]

```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> o1[0]*o1[0] + o1[1]*o1[1] - o2[0]*o2[0] - o2[1]*o2[1]);
        Collections.addAll(pq, points);

        int[][] ans = new int[k][2];
        for (int i = 0; i < k; i++) {
            ans[i] = pq.poll();
        }
        return ans;
    }
}
```

- Time complexity: **`O(nlog(n))`**
- Space complexity: **`O(n)`**

### Binary Search

Algorithm:

1. Precompute the Euclidean distances of each point.
2. Define the initial binary search range by indentify the farthest computed distance.
3. Perform a Binary Search from `low` to `high` using the reference distances:
	- Calculate the mid point of the remaining range as target distance.
	- Split the remaining points into those closer and those farther than the target distance.
	- If the `closer` list has fewer than `k` points, add them to the `closest` array and add just the value of `k`.
	- Keep only the appropritate remaning array for the next interation and update the binary search range.
4. Once k elements added to `closest`, return that `k` closest points.


```java
class Solution {
	public int[][] kClosest(int[][] points, int k) {
        double[] distances = new double[points.length];
        double low = 0;
        double high = 0;
        List<Integer> remaining = new ArrayList<>();
        for (int i = 0; i < points.length; i++) {
            double d = distance(points[i]);
            distances[i] = d;
            high = Math.max(high, d);
            remaining.add(i);
        }

        List<Integer> closest = new ArrayList<>();

        while (k > 0) {
            double mid = low + (high - low) / 2;
            List<List<Integer>> result = splitDistances(remaining, distances, mid);
            List<Integer> closer = result.get(0);
            List<Integer> farther = result.get(1);
            if (closer.size() > k) {
                remaining = closer;
                high = mid;
            } else {
                k -= closer.size();
                closest.addAll(closer);
                remaining = farther;
                low = mid;
            }
        }

        k = closest.size();
        int[][] ans = new int[k][2];

        for (int i = 0; i < k; i++) {
            ans[i] = points[closest.get(i)];
        }
        return ans;
    }

    private List<List<Integer>> splitDistances(List<Integer> remaining, double[] distances, double mid) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> closer = new ArrayList<>();
        List<Integer> farther = new ArrayList<>();
        for (int pointIndex : remaining) {
            if (distances[pointIndex] > mid) {
                farther.add(pointIndex);
            } else {
                closer.add(pointIndex);
            }
        }

        result.add(closer);
        result.add(farther);

        return result;
    }

    private double distance(int[] point) {
        return point[0] * point[0] + point[1] * point[1];
    }
}
```

- Time complexity: **`O(n)`**
- Space complexity: **`O(n)`**

### References
- https://leetcode.com/problems/k-closest-points-to-origin/solution/