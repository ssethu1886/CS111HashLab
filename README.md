# Hash Hash Hash
This lab includes two hash table implemenations. One is only concerned with correctness and the other with correctness and performance. Both are safe to use concurrently.

## Building
Run the command "make" in the shell.

```

## Running
Run "./hash-table-tester -t 8 -s 50000" in the shell. 8 is the argument for the number of cores and 50000 is the number of entries.

```

## First Implementation
In the `hash_table_v1_add_entry` function, I added a lock at the very beginning and unlocked at the very end.
### Performance
This version is slower than the base hash table implementation because in addition to running serielly, overhead time is added for context switching between threads. 

```

This time version 1 is 1,352,817 usec.

## Second Implementation
In the `hash_table_v2_add_entry` function, I locked before the new SLIST head is inserted and unlocked after. 

### Performance
This version is faster than the base implementation because the threads can run concurrently in most cases. A lock is created for each hash table bucket/entry, and is only locked when multiple threads are at the same bucket. 

```

This time the speed up is 359,104 usec.

## Cleaning up
In the 'hash_table_v1_destroy' function add 'pthread_mutex_destory(&lock)' right before freeing the hash table. Do the same for v2.

```
