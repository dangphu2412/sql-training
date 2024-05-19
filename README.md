# What we practice in this notebook:

## Learn about what is indexing
- Indexing is provide hint to access data in our database
- It 's like a table of content in a book that provide way to find the page faster

## Attribute of index
- Access Types: This refers to the type of access such as value-based search, range access, etc.
- Access Time: It refers to the time needed to find a particular data element or set of elements.
- Insertion Time: It refers to the time taken to find the appropriate space and insert new data.
- Deletion Time: Time taken to find an item and delete it as well as update the index structure.
- Space Overhead: It refers to the additional space required by the index.


## In general, there are two types of file organization mechanisms:
### Sequential file organization
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

Index types:
- Unique Index: Ensures that the indexed columns do not contain duplicate values.
- Non-Unique Index: Allows duplicate values in the indexed columns.
- Composite Index: An index that is created on multiple columns.
- Clustered Index: Determines the physical order of data in a table. When a table has a clustered index, the rows are stored on disk in the order of the index key.
- Non-Clustered Index: A non-clustered index, on the other hand, does not alter the physical order of the rows in the table. Instead, it creates a separate structure within the table that contains a sorted list of key values and pointers to the corresponding rows.
- Bitmap Index: A bitmap index is a special type of index that stores the values of the indexed columns as bitmaps. Each bit in the bitmap represents a distinct value in the column, and the bit is set to 1 if the value is present in the row and 0 if it is not.

Advance index types:
- Function-Based Index: A function-based index is an index that is created based on the result of a function or expression applied to one or more columns in the table.
- Spatial Index: A spatial index is an index that is created on spatial data types, such as points, lines, or polygons. It is used to optimize queries that involve spatial operations, such as finding points within a certain distance of a given location.
- Full-Text Index: A full-text index is an index that is created on one or more columns that contain text data. It is used to optimize queries that involve full-text search operations, such as searching for specific words or phrases in a large body of text.
- Partial Index: A partial index is an index that is created on a subset of rows in a table that meet a specific condition. It is used to optimize queries that involve only a subset of the data in the table.
- Covering Index: A covering index is an index that includes all the columns required to satisfy a query, so the query can be resolved by looking only at the index without accessing the table data.
- Filtered Index: A filtered index is an index that is created on a subset of rows in a table that meet a specific condition. It is used to optimize queries that involve only a subset of the data in the table.
- Index-Organized Table: An index-organized table is a type of table that stores data in an index structure, rather than in a separate data structure. The index-organized table is organized based on the primary key, and the data rows are stored in the leaf nodes of the index.
- Reverse Key Index: A reverse key index is an index that is created by reversing the bytes of the indexed columns before storing them in the index. It is used to reduce index block contention and improve performance in high-concurrency environments.
- Descending Index: A descending index is an index that is created in descending order on the indexed columns. It is used to optimize queries that require sorting the results in descending order.
- Invisible Index: An invisible index is an index that is not visible to the optimizer when generating query plans. It is used to test the impact of dropping an index without actually dropping it.
- Global Index: A global index is an index that is created on a partitioned table, and it spans all partitions of the table. It is used to optimize queries that involve the entire table.
- Local Index: A local index is an index that is created on a partitioned table, and it is specific to a single partition of the table. It is used to optimize queries that involve only a subset of the data in the table.
- Partitioned Index: A partitioned index is an index that is created on a partitioned table, and it is partitioned in the same way as the table. It is used to optimize queries that involve only a subset of the data in the table.

## Features of Indexing
When building indexing, be consider on:
- The cardinality
- Selectivity
- Uniqueness of the indexing columns can be taken into account

When non-contiguous data blocks are stored in an index, it can result in index fragmentation, which makes the index less effective. Regular index maintenance, such as defragmentation and reorganization, can decrease fragmentation.
