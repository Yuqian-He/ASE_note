# Storage Areas
When a program is executed three storage areas are created called segments.
- Text / Code Segment :- used for the machine code / program instructions including functions.
- Data Segment (Data + Block Started Symbol + Heap)
- The Stack Segment :- used for all variables / function variables executed in main

# core dump文件
core dump 又叫核心转储,是一个程序运行时的环境一个集合包，包含崩溃时的堆栈信息，是一个二进制文件，没法使用记事本打开，通常会在指定目录下生成一个core文件。core文件仅仅是一个内存映象，主要用来调试。

# stack and heap