### Algorithms
- Token bucket
- Leaking bucket
- Fixed window counter
- Sliding window log
- Sliding window counter

#### Token bucket

Pros:
- simple

- well understood

- commonly used by internet companies. Both Amazon and Stripe are using this algorithm to throttle their API request.


![[token bucket.png]]
- A token bucket is a container that has pre-defined capacity. Tokens are put in the bucket at preset rates periodically. Once the bucket is full, no more tokens are added.

- Each request consumes one token. When a request arrives, we check if there are enough tokens in the bucket.
	- If there are enough tokens, we take one token out for each request, and the request goes through.
	- If there are not enough tokens, the request are dropped.

![[token bucket algo.png]]

![[token bucket refill.png]]

The token bucket algorithm takes two parameters:

- Bucket size: the maximum number of tokens allowed in the bucket

- Refill rate: number of tkens put into the bucket every second

Cons:

- Two parameters in the algorithm are bucket size and refill rate. However, it might be challenging to tune them properly.
