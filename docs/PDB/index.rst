PDB (Program Database) is a file format invented by Microsoft and which contains debug information that can be consumed by debuggers and other tools. Since officially supported APIs exist on Windows for querying debug information from PDBs even without the user understanding the internals of the file format, a large ecosystem of tools has been built for Windows to consume this format. In order for Clang to be able to generate programs that can interoperate with these tools, it is necessary for us to generate PDB files ourselves.

At the same time, LLVM has a long history of being able to cross-compile from any platform to any platform, and we wish for the same to be true here. So it is necessary for us to understand the PDB file format at the byte-level so that we can generate PDB files entirely on our own.

This manual describes what we know about the PDB file format today. The layout of the file, the various streams contained within, the format of individual records within, and more.

We would like to extend our heartfelt gratitude to Microsoft, without whom we would not be where we are today. Much of the knowledge contained within this manual was learned through reading code published by Microsoft on their GitHub repo
