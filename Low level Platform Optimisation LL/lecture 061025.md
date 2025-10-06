"mem'ry mem'ry mem'ry, you can't do much without it" - david

memory is a bottleneck, its slow to access and involves IO (as far as the CPU is concerned). its also slow to allocate.

but we have lots of power with memory in C. which also means lots of bugs.

we need to make a memory manager apparently:
- track memory usage
- check the integrity
- return memory from a pool (NOT directly allocating more)