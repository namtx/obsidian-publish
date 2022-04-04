[Leetcode - Maximum Score From Removing Stones](https://leetcode.com/problems/maximum-score-from-removing-stones/)

### Approach - PQ
[[Priority Queue]]
To maximize the score, we have to choose two piles with most of stones first.
For each turn, we choose two piles with most of stones, reduce the numer of stone for chose piles and increase `score` by 1.

```java
public int maximumScore(int a, int b, int c) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(Comparator.reverseOrder());
        pq.add(a);
        pq.add(b);
        pq.add(c);
        int ans = 0;
        while (pq.size() > 1) {
            int first = pq.poll();
            int second = pq.poll();
            first--;
            second--;
            ans++;
            if (first > 0) {
                pq.add(first);
            }
            if (second > 0) {
                pq.add(second);
            }
        }

        return ans;
    }
```

### Approach - Math
Firstly, find the largest number of the three, let it be `hi`, and the other two be `lo1` and `lo2` (`hi` >= `lo1`, `hi` >= `lo2`)
There are two situations:

1. `hi >= lo1 + lo2`
	- We can take all stones from `lo1` and `lo2`, take `lo1+lo2` from `hi`
	- It's impossible to take more
	- The maximum score we can get is **`lo1 + lo2`**
2. `hi < lo1 + lo2`
	- Conclusion (see proof below): **it is possible to:**
		- Either take all stones (if number of stones is even)
		- Or leave only ONE stone left (if number of stones is odd)
	- No matter of total number of stones, the maximum score we can get is `sum(a, b, c)/2`

#### Proof

```
lo1 + lo2 > hi

In each turn we take 1 stone from hi, and 1 stone from the HIGHER pile of the other two (or any pile if lo1 and lo2 have the same amount)
Until hi reaches 0.

Now we have hi is 0, lo1 and lo2 are either the same, or one pile is 1 stone more than the other.
	We can prove this by contradiction:
	Suppose we are left with:
	hi:  0
	lo1: x
	lo2: y
	x - y >= 2
	Then we must have taken stones ONLY from lo1. Because we never take stone from the lower pile, if at any step number of stones in lo2 is >= lo1, it would be impossible to make the difference be > 1.
	So at the beginning lo1 had (x + hi) stones.
	x >= 2 + y >= 2 > 0  =>  x + hi > hi  =>  lo1 > hi
	This contradicts the condition hi >= lo1. Thus the assumption is incorrect, and
		abs(x - y) <= 1

Then each ture we take 1 stone from lo1 and 1 from lo2, until one pile or both reach 0. We are left with at most 1 stone.

Q.E.D.
```

```java
int maximumScore(int a, int b, int c) {
	int largest = max({a, b, c}), total = a + b + c, sumOfOtherTwo = total - largest;
	return largest >= sumOfOtherTwo ? sumOfOtherTwo : total/2;
}
```
