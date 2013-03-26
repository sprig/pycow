             .=     ,        =.
     _  _   /'/    )\,/,/(_   \ \
      `//-.|  (  ,\\)\//\)\/_  ) |
      //___\   `\\\/\\/\/\\///'  /
   ,-"~`-._ `"--'_   `"""`  _ \`'"~-,_
   \       `-.  '_`.      .'_` \ ,-"~`/
    `.__.-'`/   (-\        /-) |-.__,'
      ||   |     \O)  /^\ (O/  |
      `\\  |         /   `\    /
        \\  \       /      `\ /
         `\\ `-.  /' .---.--.\
           `\\/`~(, '()      ('
            /(O) \\   _,.-.,_)
           //  \\ `\'`      /
     jgs  / |  ||   `""""~"`
        /'  |__||
              `o 


pycow
=====

Copy-on-write for Python

Python has support for shallow copying and deep copying functionality via its copy module. However it does not provide for copy-on-write
semantics. This project aims to remedy this shortcoming. The need for this sort of a functionality was felt when I was implementing a
symbolic execution engine in Python using PyPy (called SyPy). 

In a symbolic execution engine, the executor conceptually "forks" whenever it hits a decision point in the application. In SyPy, instead
of forking, we simply remember the decision point and move back to that point when we are done exploring a given choice in the execution
path. However, this also means reverting the heap (object space) to its original state. Creating a separate deep copy of the heap at each
fork point is an extremely heavy operation and the need was felt to have some sort of a COW functionality in place. Note that in modern OSes
this is automatic. Forking a child process creates a shallow copy of the parent process' memory space which is marked as read only. When
the child process attempts to write to the memory space, it triggers a fault that is intercepted by the kernel and recognized as a COW fault.
Then the OS creates a fresh copy of the parent's memory space and writes whatever was supposed to have been written to it.

The current implementation of pycow is very simplistic and naive but still potentially useful.

TODO:

1) Object rollback (rollback an object to its original state)

2) Versioned object (maintain all the deltas applied to the object and be able to go back and forth in history)


Contributors:
-------------

Nikhil Sarda


Cow ascii art from http://www.chris.com/ascii/?art=animals/cows
