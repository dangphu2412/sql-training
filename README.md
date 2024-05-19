# What we practice in this notebook:

## Learn about what is indexing
- Indexing is provide hint to access data in our database
- It 's like a table of content in a book that provide way to find the page faster

# Attribute of index
- Access Types: This refers to the type of access such as value-based search, range access, etc.
- Access Time: It refers to the time needed to find a particular data element or set of elements.
- Insertion Time: It refers to the time taken to find the appropriate space and insert new data.
- Deletion Time: Time taken to find an item and delete it as well as update the index structure.
- Space Overhead: It refers to the additional space required by the index.


In general, there are two types of file organization mechanisms:
#### Sequential file organization
- the indices are based on a sorted ordering of the values.
- Might store the data in a dense or sparse format.
Dense index:
- For every search key value in the data file, there is an index record.
- This record contains the search key and also a reference to the first data record with that search key value.

Sparse index:
- Each index records contains a search key references to a blocks of related records.
- To find a record, we find it with the largest search key, and the process along with the pointers in the file sequentially.
- Number of access required log2(n) +1
### Hash file organization
- Indices are distributed to a range of buckets in which the key is determined by a hash function.
- There are 3 methods of indexing:
    - Clustered Indexing
      - Determines the physical order of data in a table. When a table has a clustered index, the rows are stored on disk in the order of the index key.
      - Performance: Clustered indexes are very efficient for range queries and queries that return a large portion of the table. This is because the rows are stored in contiguous blocks, reducing the number of disk I/O operations.
      - Single per Table: A table can have only one clustered index because the data rows can be sorted in only one order.
      - Physical Order: The data rows are stored in the order specified by the clustered index. This means the index is the table.
    - Primary Indexing
      - A type of Clustered Indexing
      - It induces sequential file organization, unique and stored in sorted manner.
    - Non-clustered or Secondary Indexing
      - A non-clustered index, on the other hand, does not alter the physical order of the rows in the table. Instead, it creates a separate structure within the table that contains a sorted list of key values and pointers to the corresponding rows.
      - Multiple per Table: A table can have multiple non-clustered indexes.
      - Logical Order: The data rows are not stored in the order of the non-clustered index. The index contains pointers to the data rows.
      - Index Structure: The non-clustered index is a separate structure that holds the indexed column values and a pointer (row locator) to the actual data row. In a clustered table, this pointer is the clustered index key; otherwise, it's the row's physical address.
    - Multilevel Indexing
      - Multilevel indexing is a technique used to manage large indexes efficiently, especially when the index itself cannot fit entirely into memory. It extends the concept of indexing by creating a hierarchical structure, where an index is built on top of another index, allowing faster access to data. Here’s how it works:
      - Primary Index: The first level of the index, which may still be too large to fit in memory.
      - Secondary Index: An index on the primary index, reducing the number of entries that need to be scanned at the first level.
      - Additional Levels: More levels of indexing can be added as needed, each pointing to the index at the lower level, until the top-level index fits into memory.
      - This structure creates a tree-like hierarchy of indexes, similar to a B-tree or B+ tree, which balances the trade-off between index size and search efficiency.
      - Advantages:
        - Reduced Disk Access: By dividing the index into multiple levels, the number of disk accesses required to find an entry is significantly reduced.
        - Efficient Search: Each level of the index narrows down the search space, leading to faster query performance.
        - Scalability: Multilevel indexing scales well with very large datasets because it organizes the index entries in a hierarchical manner.

## Features of Indexing
