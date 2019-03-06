# A C++ List:

1. Memory Models for C++ Programmers
   This paper introduces the C++ multithreaded memory access modes.
   It's surprised the x86 memory model is weaker than the sequentially consistent model.
   An interesting concept is `inter-thread happens before` that describes the order
   between two evalations from different threads.
   `Release` and `acquire` are two matching synchronize operations.
   They limit reorders of other reads or writes.
   The key to understand the model is to observe how `acquire` matches with `release`.
    
2. [Clarifying Direct IO's Semantics](https://ext4.wiki.kernel.org/index.php/Clarifying_Direct_IO%27s_Semantics)
