# Things every developer absolutely, positively needs to know about database indexing

[Link to Tech Talk](https://www.youtube.com/watch?v=HubezKbFL7E)

An index is an **ordered** representaiton of indexed data, ordering is important as it is much faster than searching an unordered input, think about binary search

## What is a B-Tree

B-Tree is a balanced tree, meaning it has the same number of hierachial nodes on each side of the split, the **leaf nodes will always be on the same level**. So traversing a B-tree should take the same amount of time regardless of the branch we take

![B-Tree](images\2021-10-30-10-11-40.png)
_Note : how the numbers are ordered in the image below_

![B-Tree with Doubly Linked list](images\2021-10-30-10-16-53.png)
_Note : how the the leaves are doubly linked, this is improve performance, or else each leaf would have to go back to the leaf node and then go back to each leaf_

> B-Tree is a self-balancing search tree. In most of the other self-balancing search trees (like AVL and Red-Black Trees), it is assumed that everything is in main memory. To understand the use of B-Trees, we must think of the huge amount of data that cannot fit in main memory. When the number of keys is high, the data is read from disk in the form of blocks. Disk access time is very high compared to the main memory access time. The main idea of using B-Trees is to reduce the number of disk accesses. Most of the tree operations (search, insert, delete, max, min, ..etc ) require O(h) disk accesses where h is the height of the tree. B-tree is a fat tree. The height of B-Trees is kept low by putting maximum possible keys in a B-Tree node. Generally, the B-Tree node size is kept equal to the disk block size. Since the height of the B-tree is low so total disk accesses for most of the operations are reduced significantly compared to balanced Binary Search Trees like AVL Tree, Red-Black Tree, ..etc.

More on [b-trees](https://www.geeksforgeeks.org/introduction-of-b-tree-2/)

## What gets stored in an index

Consider the table which has an index on the `name` column
![What gets stored in the database](images\2021-10-30-14-23-02.png)

the index would look something like this, where the keys to the index are the ROWID not the primary key

![Index up](images\2021-10-30-14-25-35.png)

Benefits

- Seach for a value is fast in logirathamic scalability, meaning the increase in input will not be a problem to the index.

## Cost of an Index

![Cost of an Index](images\2021-10-30-14-30-10.png)

The tree will have to re-balanced on each and every DML query to the table.

## Understanding he execution Plan

Steps the db engine needs to perfrom to execute the query.

![Sample Query Plan](images\2021-10-31-00-11-45.png)
_A sample query plan_

### **Type**

or Join type is just really actually the access type the query is going to use to access the data in the table.

Possible values being

- Const/EQ_REF
If you see thig stop optimizing, there is nothing much you can do.
![Const EQ Ref](images\2021-10-31-00-14-49.png)
- REF/RANGE
Works on a subset of the index, finds a starting point and then traverses from that point on till it meets the end clause.
![Ref Range Scan](images\2021-10-31-00-17-23.png)
- INDEX
![Index](images\2021-10-31-00-19-52.png)
