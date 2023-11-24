## RedRusDb

NOTE: This was my all time dream to build something complex from scratch to understand evrything from end to end.

A distributed in-memory k-v storage engine in Rust! [RedRusDB Repo](https://github.com/RedRusDB/redrus)


An attempt to write distributed in-memory k-v storage engine in Rust
to learn about database internals.

Building a database from scratch has its own thrill, and you can leverage this to

build a database from scratch
learn database internals, starting with Redis
learn about advanced data structures, algorithms, and event loops
collaborate with other engineers and contribute back to Open Source

While our B+ tree now support concurrent operations, it's still a single
threaded database system, as our frontend (network/cli layer) doesn't support
handling concurrent requests yet.

_This is by no mean an idiomatic Rust implementation as I'm learning Rust
along the way._

-----

The project is kind of slow phase coz i have job in parallel and am learning the things on the way. Hence, the progress will be slower.
Hopefully, I can regain my momentum after a couple of weeks._

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