## RedRusDb

```sql

NOTE: CURRENTY AM EXPLORING ABOUT THE LOCK-LESS AND WAIT-FREE DATA STRUCTURES

```


NOTE: This was my all time dream to build something complex from scratch to understand evrything from end to end.

Hi! I am Siddharth, a Software Engineer(Backend). I am currently learning Rust am primarily interested in algorithms, data structures, design principles, databases, large-scale systems, and distributed systems.

For the past few months, I have been exploring Rust, storage engines, distributed systems, and networking. I will use all this learning to build a small in-memory storage engine which will be distributed in nature, for learning and fun.

A distributed in-memory k-v storage engine in Rust! [RedRusDB Repo](https://github.com/RedRusDB/redrus)


An attempt to write distributed in-memory k-v storage engine in Rust
to learn about database internals.

Building a database from scratch has its own thrill, and you can leverage this to

build a database from scratch
learn database internals, starting with Redis
learn about advanced data structures, algorithms, and event loops
collaborate with other engineers and contribute back to Open Source

The rest of the work is continue based on multiple [references](#references).
One of the most important one is [CMU Intro to Database Systems projects][5]
_(including previous years archive, since each year they have students
implement different structure)_.

As am not a frontend enginner 

_This is by no mean an idiomatic Rust implementation as I'm learning Rust
along the way._

-----

The project is kind of slow phase coz i have job in parallel and am learning the things on the way. Hence, the progress will be slower.
Hopefully, I can regain my momentum after a couple of weeks._


## Progress

Since we have completed through the tutorial of Let's Build a Simple Database,
we will have to come up with our own checklist for this project. Here's a
quick breakdown of my journey and what I'm going to implement next:

- [ ] Add test case for splitting node and updating parent, where the new node is not the most right child.
- [ ] Implement split on internal node.
- [ ] Extend test cases to make sure insertion is working as intended and fix
      bugs along the way...
  - [ ] Add property-based testing for insertion test.
  - [ ] Fix all the bugs found through property based test.
- [ ] Implement find by id operation. This would be helpful when testing
      deletion.
- [ ] Implement delete operation for `sqlite`.
- [ ] Implement deletion for B+ Tree.
  - [ ] Implement deletion on leaf node.
  - [ ] Implement deletion on internal node.
  - [ ] Implement merging after the neighbouring nodes pointers/key-values < N.
  - [ ] Implement mergeing for internal nodes.
  - [ ] Implement rebalancing to reduce the number of merges need.
    - [ ] Implement steal from siblings if can't merge both nodes together.
    - [ ] Check if there's still other rebalancing optimisation technique
      available...
  - [ ] Replace hardcoded max internal node count of 3 with the actual internal
    node count supported by our data format.
      - This require us to generate a larger datasets to tests the
        behaviour.
- [ ] Implement buffer pool for our database. _([Reference][1])_
  - [ ] Implement least recently used (LRU) replacement policies.
  - [ ] Implement Buffer Pool Manager.
  - [ ] Integrated Buffer Pool manager into the rest of the system.
  - [ ] Make buffer pool page size configurable.
- [ ] Multi threaded index concurrency control. _([Reference][2], [Reference, see Task 4][3])_
    - [ ] Support concurrent insert to B+ Tree.
    - [ ] Support concurrent select to B+ Tree.
    - [ ] Support concurrent delete to B+ Tree.
    - [ ] Test concurrent insert + select;
    - [ ] Test concurrent delete + select;
    - [ ] Test concurrent insert + delete;
    - [ ] Test concurrent insert + select + delete;
    - [ ] Optimize latch crabbing by holding read lock and only swap to write
      lock when there's a split/merge.
    - [ ] Refactor tree operation out of `Pager`.
- [ ] Implement concurrency control at row/tuple level. _([Reference][4])_
  - [ ] Implement a transaction manager first.
  - [ ] Implement lock manager.
    - It currently doesn't support different locking behaviour based on
      different isolation levels.
    - While is completed, I can't really guarantee the correctness of the
      implementation for the time being. See the comments in code for more.
    - Testing for read and write anomalies are not included yet. This will
    require implementation of update operation and integration of lock manager
    into the query/table code, which is what I plan to do next.
  - [ ] Implement a query executor.
    - Implemented both sequence scan and delete executor and plan node.
    - It is not integrated into the other part of the systems yet.
  - [ ] Support update operation. This is important as it allow us to produce
  test case that can lead to read/write anomalies.
    - [ ] Implement update plan node.
    - [ ] Implement update executor.
    - [ ] Support usage of index scan in update plan node.
  - [ ] Write test to ensure that two phase locking works on all read and write
    anomolies.
    - [ ] Update query executor, table to ensure lock is acquired correctly so the
      tests for read/write anomolies passed.
    - Currently, the test is only available for index scan executor. To
      ensure, we can test the read/write anomolies with sequence scan, we need
      to first support where expression evaluation in our query engine.
      Which would be a task for another day.
  - [ ] Implement concurrent query execution.
  - [ ] Implement dead lock detection.
  - [ ] Implement dead lock prevention. (Wound Wait algorithm)
    _([Reference](https://15445.courses.cs.cmu.edu/fall2021/project4/#deadlock_prevention))_
- [ ] Implement recovery mechanism for our database. ([Reference][6])
  - [ ] Implement basic log manager and log record.
  - [ ] Update page struct to contain additional information required for
    recovery. E.g. LSN.
  - [ ] Implement WAL in other subsystems, such as buffer pool (pager) and transaction
    manager.
  - [ ] Implement ARIES.
  - [ ] Implement a stop the world checkpointing.
- [ ] Update our query parser to integrate with our new query executor. This will allow us to
  easily test things by using SQL statement instead of manually writing our query plan.
  - [ ] Implement insert executor.
  - [ ] Parse query into query plan.
  - [ ] Replace the query engine with the new onw in `main.rs`.

_(subject to changes as we progress)_

----

## End Goal

The main focus to write a distributed in-memory k-v storage engine from scratch. This project will
includes it's own:
- [ ] B+ Tree data structure
- [ ] Buffer pool
- [ ] LRU replacement policy
- [ ] Transaction manager
- [ ] Lock manager
- [ ] Vector support
- [ ] Persistence storage