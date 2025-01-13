Oracle Database uses a combination of physical and logical storage structures to manage and store data efficiently. Here's an overview of how it works:

### Physical Storage Structures
1. **Data Files**: These files store the actual data, such as tables and indexes. Each data file is associated with only one database[1](https://docs.oracle.com/en/database/oracle///oracle-database/21/cncpt/physical-storage-structures.html).
2. **Control Files**: These files contain metadata about the database, including the structure and state of the database[1](https://docs.oracle.com/en/database/oracle///oracle-database/21/cncpt/physical-storage-structures.html).
3. **Redo Log Files**: These files record all changes made to the data, which are crucial for recovery purposes[1](https://docs.oracle.com/en/database/oracle///oracle-database/21/cncpt/physical-storage-structures.html).

### Logical Storage Structures
1. **Tablespaces**: Logical storage units that group related data files. Each tablespace can contain multiple data files[2](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/).
2. **Segments**: Space allocated for database objects like tables and indexes within a tablespace[2](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/).
3. **Extents**: Contiguous blocks of storage within a segment[2](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/).
4. **Data Blocks**: The smallest unit of storage in Oracle Database, corresponding to a specific number of bytes on disk[2](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/).

### Data Storage Process
- **Data Blocks**: Oracle stores data in data blocks, which are also referred to as logical blocks or pages[2](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/).
- **Extents and Segments**: Data blocks are grouped into extents, and extents are grouped into segments. Each segment is used to store a specific type of database object, such as a table or an index[2](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/).

### Example of Data Storage
When you create a table, Oracle allocates a segment for that table. The segment is made up of extents, which in turn are made up of data blocks. As data is inserted into the table, Oracle writes the data to the data blocks within the extents of the segment.

This architecture ensures efficient data management, high performance, and scalability[1](https://docs.oracle.com/en/database/oracle///oracle-database/21/cncpt/physical-storage-structures.html)[2](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/).

Is there a specific aspect of Oracle's data storage you'd like to dive deeper into?

[1](https://docs.oracle.com/en/database/oracle///oracle-database/21/cncpt/physical-storage-structures.html): Oracle Database Physical Storage Structures
[2](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/): [Oracle Database Logical Storage Structures](https://www.oracletutorial.com/oracle-administration/oracle-database-architecture/)