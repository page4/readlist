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
   
   The O_DIRECT write can fall back to buffered I/O when allocating write.
   Even in the preallocating write, the data is not guaranteed to be present after a system crash unless the application uses an explicit fsync(2) call.

3. [Type Erasure as the Glue between OO and Generic Programming](https://www.artima.com/cppsource/type_erasure.html)

   Type plays a different role in OO programming and in generic programming.
   OO runtime polymorphism will pay a performance penalty, while GP compile time polymorphism introduces a compile-time dependency.
   On C++ template metaprogramming, Dave Abrahams and Aleksey Gurtovoy define type erasure as "the process of turning a wide variety of types with a common interface into one type with that same interface."


4. [Minimizing Dependencies within Generic Classesfor Faster and Smaller Programs](http://www.stroustrup.com/SCARY.pdf)

   > SCARY describes assignments and initializations that are Seemingly erroneous (appearing Constrained by conflicting generic param-eters), but Actually work with the Right implementation (unconstrained bY the conflict due to minimized dependencies). An Example:
   
   ```
   set<int, C1, A1>::iterator i1;
   set<int, C2, A1>::iterator i2 = i1;
   set<int, C1, A2>::iterator i3 = i1;
   ```
   The iterator of a set is defined by the structure of the underlying rbtree. 

5. [Detecting and handling split locks (misaligned memory access)](https://lwn.net/Articles/790464/)

The misaligned memory access that crosses two cache lines gets worse 
because of locking the whole memory bus to solve the coherency problem.
The split lock blocks not only the CPU performing the access, but also all others in the system.

6. [Curiously recurring template pattern (Static polymorphism)](https://en.wikipedia.org/wiki/Curiously_recurring_template_pattern)

Typically, the base class template will take advantage of the fact that member function bodies (definitions) are not instantiated until long after their declarations, and will use members of the derived class within its own member functions, via the use of a cast.

7. [Order of dynamic linking paths, RPATH, LD_LIBRARY_PATH, RUNPATH](https://wiki.debian.org/RpathIssue) 

> 1. the DT_RPATH dynamic section attribute of the library causing the lookup
> 2. the DT_RPATH dynamic section attribute of the executable
> 3. the LD_LIBRARY_PATH environment variable, unless the executable is setuid/setgid.
> 4. the DT_RUNPATH dynamic section attribute of the executable
> 5. /etc/ld.so.cache
> 6. base library directories (/lib and /usr/lib) 

The order can be changed. For example,
> Regarding steps 1 and 2: The DT_RPATH attribute is ignored if the DT_RUNPATH attribute is found. Then, LD_LIBRARY_PATH is searched first! 

Thus, `-Wl,-rpath` is ignored on Gentoo due to DT_RUNPATH.
