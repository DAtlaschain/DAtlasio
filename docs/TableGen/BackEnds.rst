ableGen backends are at the core of TableGen's functionality. The source files provide the semantics to a generated (in memory) structure, but it's up to the backend to print this out in a way that is meaningful to the user (normally a C program including a file or a textual list of warnings, options and error messages).

TableGen is used by both LLVM and Clang with very different goals. LLVM uses it as a way to automate the generation of massive amounts of information regarding instructions, schedules, cores and architecture features. Some backends generate output that is consumed by more than one source file, so they need to be created in a way that is easy to use pre-processor tricks. Some backends can also print C code structures, so that they can be directly included as-is.

Clang, on the other hand, uses it mainly for diagnostic messages (errors, warnings, tips) and attributes, so more on the textual end of the scale.
