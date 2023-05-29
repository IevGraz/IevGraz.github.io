---
title: Peak performance MySQL tuning training for operators
author: Aurimas Mikalauskas
date: 2023-05-29
---

The focus of this course was to get the best possible performance out of MySQL.The target audience - DBAs, SREs and alike. It was presented by Aurimas Mikalauskas at the Vinted office some 5 years ago. Aurimas was working as a consultant for [Percona](https://www.percona.com/) at the time. I’m not sure if the course is still available though. I got to watch a recording of the session at Vinted.  

### Contents of the course

* Hardware and OS (how it affects MySQL performance)
* MySQL server architecture
* MySQL configuration
* Schema optimisation
* Query optimisation
* Scaling with MySQL

### Why I watched it

Whenever I asked for recommendations on how to improve my technical skills our staff engineer would recommend me to watch the recording of this course. I agreed that it is a good idea, but kept postponing it. Then I switched domains, asked my new staff engineer how to improve my relevant technical skills - and got the same recommendation again.

### How I watched it

For the better half of the course I watched it and took vigorous notes, pausing the course whenever I needed to write more things down. This approach cost me about an hour to get through 15 minutes of the recording - while there were more than 8 hours of the recording in total. At some point I got frustrated enough and switched to taking additional notes on the printouts of the slides. This made me feel a bit uncomfortable at first - like I wasn’t able to focus on the content as much. But eventually I got used to it. 

After finishing the course I went through my notes, highlighting different things in different colors - the things that seemed interesting or useful in general, the things I would like to learn more about, the things I planned to mention in this post. So far this is more or less the same approach I usually take with [reading technical books](/2022/03/09/how_i_read-technical_books.html). However, there was one new thing I tried - discussing what I’ve read with Chat GPT. I asked about things like how concepts from different views (e.g. tablespaces vs B+ trees) relate to each other or requested additional resources for some topics.

### What I found the most valuable

As the course seems to have been aimed at DBAs and SREs, some parts (e.g. hardware and OS, MySQL configuration) flew right over my head. However things like schema and query optimisation seem invaluable for any backend engineer. MySQL server architecture was interesting for my general curiosity. 

I would like to have some of the learnings always at hand, so I’ll summarize them in this blog post. However I’m not sure if it is OK to share the information from the course, so I will focus on the things that are available in [official MySQL documentation](https://dev.mysql.com/doc/).

#### Usage of the EXPLAIN statement

I catch myself in a lot of self-conscious moments where someone from my colleagues says “a proper senior developer should definitely know X” and I panic that apparently I am not a proper senior developer yet. One of these X’es that stood out for me was using MySQL explain statements.  I guess the author of the talk agrees with this sentiment as there was quite a bit of course dedicated to explaining the EXPLAIN statement. There is also quite a bit on the topic in the official MySQL documentation. I think the best way to store this for a future reference is by organizing it into a table (I’ve omitted some fields that seemed less valuable):

<table>
  <tr>
   <td><strong>Output field</strong>
   </td>
   <td><strong>Possible values</strong>
   </td>
   <td><strong>Meaning</strong>
   </td>
  </tr>
  <tr>
   <td><strong>id</strong>
   </td>
   <td>
   </td>
   <td><a href="https://dev.mysql.com/doc/refman/5.7/en/explain.html">EXPLAIN</a> returns a row of information for each table used in the <a href="https://dev.mysql.com/doc/refman/5.7/en/select.html">SELECT</a> statement. It lists the tables in the output in the order that MySQL would read them while processing the statement. 
   </td>
  </tr>
  <tr>
   <td><strong>type</strong>
   </td>
   <td>
   </td>
   <td>describes how tables are joined.
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>system
   </td>
   <td>The table has only one row (= system table)
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>const
   </td>
   <td>The table has at most one matching row, which is read at the start of the query. Because there is only one row, values from the column in this row can be regarded as constants by the rest of the optimizer
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>eq_ref
   </td>
   <td>One row is read from this table for each combination of rows from the previous tables. It is used when all parts of an index are used by the join and the index is a PRIMARY KEY or UNIQUE NOT NULL index.
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>ref
   </td>
   <td>Is used if the join uses only a leftmost prefix of the key or if the key is not a PRIMARY KEY or UNIQUE index (in other words, if the join cannot select a single row based on the key value). If the key that is used matches only a few rows, this is a good join type.
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>ref_or_null
   </td>
   <td>This join type is like ref, but with the addition that MySQL does an extra search for rows that contain NULL values. 
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>index_merge
   </td>
   <td>Indicates that the Index Merge optimization is used.
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>range
   </td>
   <td>Only rows that are in a given range are retrieved, using an index to select the rows.
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>index
   </td>
   <td> The index tree is scanned. This occurs in two ways: if the index is a covering index for the queries only the index tree is scanned (in this case, the <strong>extra</strong> column says ‘Using index’);  A full table scan is performed using reads from the index to look up data rows in index order (uses index does not appear in the <strong>extra</strong> column)
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>ALL
   </td>
   <td>A full table scan is done.
   </td>
  </tr>
  <tr>
   <td><strong>possible_keys</strong>
   </td>
   <td>
   </td>
   <td>Indicates the indexes from which MySQL can choose to find the rows in this table. If this column is NULL there are no relevant indexes. 
   </td>
  </tr>
  <tr>
   <td><strong>key</strong>
   </td>
   <td>
   </td>
   <td>The key (index) that MySQL actually decided to use
   </td>
  </tr>
  <tr>
   <td><strong>key_len</strong>
   </td>
   <td>
   </td>
   <td>The key_len column indicates the length of the key that MySQL decided to use. The value of key_len enables you to determine how many parts of a multiple-part key MySQL actually uses.
   </td>
  </tr>
  <tr>
   <td><strong>rows</strong>
   </td>
   <td>
   </td>
   <td>The number of rows MySQL believes it must examine to execute the query (rough estimate)
   </td>
  </tr>
  <tr>
   <td><strong>extra</strong>
   </td>
   <td>
   </td>
   <td>This column contains additional information about how MySQL resolves the query. One example was given above when describing index join <strong>type</strong>. 
   </td>
  </tr>
</table>

#### Indices

A big part of the course was dedicated to how data is stored in InnoDB and why that is important when thinking about your schema and queries. As for the overall InnoDB architecture I think a picture speaks a thousand words and there is[ a good one ](https://dev.mysql.com/doc/refman/5.7/en/innodb-architecture.html)in the official documentation. 

The part I want to understand and remember the most are [indices](https://dev.mysql.com/doc/refman/5.7/en/innodb-index-types.html). 

**Clustered Index.** InnoDB stores row data in the leaf nodes of a special B+ tree index called clustered index. The index is called “clustered” because the rows are sorted by the primary key values - rows with related index values are clustered together. 

Let’s say I want to store the technical books I read in an InnoDB table. Here are the 5 most recent of them:

<table>
  <tr>
   <td><strong>Id</strong>
   </td>
   <td><strong>Tittle</strong>
   </td>
   <td><strong>Author</strong>
   </td>
   <td><strong>Rating</strong>
   </td>
  </tr>
  <tr>
   <td>1
   </td>
   <td>High Performance Browser Networking
   </td>
   <td>Ilya Grigorik
   </td>
   <td>5
   </td>
  </tr>
  <tr>
   <td>2
   </td>
   <td>Fundamentals of Software Architecture
   </td>
   <td>Mark Richards
   </td>
   <td>3
   </td>
  </tr>
  <tr>
   <td>3
   </td>
   <td>Database Reliability Engineering
   </td>
   <td>Charity Majors
   </td>
   <td>3
   </td>
  </tr>
  <tr>
   <td>4
   </td>
   <td>Staff Engineer
   </td>
   <td>Will Larson
   </td>
   <td>4
   </td>
  </tr>
  <tr>
   <td>5
   </td>
   <td>Kubernetes Up & Running
   </td>
   <td>Kelsey Hightower
   </td>
   <td>5
   </td>
  </tr>
</table>

To make things more interesting I would like to use the title as the primary key. The B+ tree (limited to 3 children per node) would look something like this: 

![Titles B+ tree index](/assets/images/clustered_index.drawio.svg){: width="800" }

The implications of storing data in such structure: 
* As a unique, non-null key is required to order the data, if you don't specify a primary key InnoDB will either choose a suitable one or generate one itself (this would take up additional storage space for each row).
* Accessing a row through the clustered index is fast because the index search leads directly to the page that contains the row data. 
* As data is inserted, it will be placed in the appropriate position according to the key value, not necessarily at the end of the table. This can lead to page splits if a page is full and a new row needs to be inserted in the middle.

 **Secondary Indices.** If I needed to add another index or few for my table (e.g. because there is a use case to also look up books by their rating or author) those would be secondary indexes. They would also be stored as B+ trees, but the leaf nodes would contain the value of the primary key, instead of the actual row data. 
The implications of this approach:
* In order to perform an index lookup by the secondary index, we actually need to do two lookups. The first lookup searches the table and finds the primary key for a record. Once the primary key is found, a second lookup searches the primary key index to find the row.
* If the primary key is long, the secondary indices use more space, so it is advantageous to have a short primary key. (Choosing the title as the primary key as I did in my example here might not actually be the best idea).

**Compound indices.** Both clustered and secondary indices can be composed of multiple columns. In such a case still a single B+ tree is used to store the index, but it is ordered by all the values comprising the index, starting from the leftmost one. 
This has some implications for the queries:
* If you have an index on columns A, B and C, it can also be used for queries on columns A and B and column A alone. This is also known as **the left-prefix rule**: “_a query can search an index efficiently if it provides search terms (such as values in a WHERE clause) that match the leading columns of the index, in left-to-right order_”.
* When you want to use 2 columns in an index and you are not sure which one to add first, go with the more selective one (or, in database terms, the one with higher cardinality). This way the database can eliminate non-matching rows more quickly when scanning the index. 

### Other impressions

The most valuable thing I got out of this course is the feeling that I have some understanding about how MySQL works. Not having it was becoming an issue for me as everytime I had to do a database related task I would get anxious that maybe there is some big and important nuance I’m oblivious about. I feel like I would at least know the keywords worth looking into.

### Book recommendations
I watched the course, took some notes and even summarized the most interesting things in this blog post. However, I would still like to have a good resource about MySQL query optimisation always at hand. I haven’t bought it yet, but [“High Performance MySQL”](https://www.goodreads.com/book/show/59700215-high-performance-mysql) looks like a good candidate for this as it is well rated (4.43/5 stars) and the last edition was published recently (2021) enough.  
