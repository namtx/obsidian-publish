### Indexes

###### Index types
- B-tree
- Adaptive Hash Indexes
The InnoDB storage engines has a special feature call _adaptive hash indexes_. When InnoDB notices that some index values being accessed with very high frequently. it builds a hash index for them in memory on top of B-tree indexes.
This gives its B-tree indexes some properties of hash indexes, such as very fast lookups.
This process is completely automatic.

###### Types of queries that can use a B-tree index
- Match the full value
- Match the left most prefix
- Math a column prefix 
- Match a range of values
- Match one part exactly and match a range on another part
- Index-only queries (which are queries that access only the index, not the row storage)

###### Limitation of B-tree
- lookup does not start from the `leftmost` side of the indexed columns.
- can't skip columns in the index
- can't optimize accesses with any columns to the right of the first range condition.

```sql
WHERE last_name="Smith" AND first_name LIKE 'J%' AND dob='1976-12-23
```

the index access will only the first two columns in the index because the `LIKE` is range condition. For a column that has a limited number of values, you can work round by specifying equality conditions instead of range conditions.

> You may need to create indexes with the same columns in different orders to satisfy your queries.

###### FULLTEXT Index

- finds keywords in the text instead of comparing values directly to the values in the index.
- Full-text indexes are for `MATCH AGAINST` operations, not ordinary `WHERE` clause operations.

###### Benefits of Indexes
- Indexes reduce the amount of data the server has to examine.
- Indexes help the server avoid sorting and temporary tables.
- Indexes turn random I/O into sequential I/O.

##### Indexing Strategies for High Performance

###### Prefix Indexes and Index Selectivity
- Index selectivity is the ratio of the number of distinct indexed values to the total number of rows in the table.
- The highly selectivity is good because it lets MySQL filter out more rows when it looks for the matches.
- A unique index has a selectivity of 1, which is as good as it gets.
- If you are indexing `BLOB` or `TEXT` columns, or very long `VARCHAR` columns, you _must_ define prefix indexes because MySQL disallows indexing their full length.
- Choose a prefix that's long enough to give good selectivity but short enough to save space.
