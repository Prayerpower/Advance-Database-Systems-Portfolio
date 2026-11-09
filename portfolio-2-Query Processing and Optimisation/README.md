Brief Performance Analysis
EXPLAIN ANALYZE was used to compare the transaction query for James John's account (account_id = 1) before and after creating an index on the account_id column.

Before indexing, PostgreSQL used a sequential scan on the transactions table. It returned 2 rows and removed 4 rows by filter, with an estimated cost of 18.88, a planning time of 0.008 ms and an execution time of 0.004 ms.

After indexing, PostgreSQL still used a sequential scan. It returned the same 2 rows, and the estimated cost dropped to 1.07, because creating the index updated the planner's statistics on the table size. The planning time rose to 0.062 ms because the planner now had the new index to consider, and the execution time was 0.011 ms.

The index was not used because the Dove Bank test database holds only six transaction records, all stored in a single data page (shared hit=1). Reading that one page directly is cheaper than looking up the index first. The small differences in time are normal variation at this scale. As the number of transaction records grows, PostgreSQL would switch to an index scan, and the index would greatly reduce the time needed to find a customer's transactions.
