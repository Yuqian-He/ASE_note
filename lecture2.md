# C++ Programming “In the Large”

![ ](./assets/Screenshot%20from%202022-09-29%2011-56-07.png)
![ ](./assets/Screenshot%20from%202022-09-29%2012-04-27.png)
![ ](./assets/Screenshot%20from%202022-09-29%2012-05-03.png)

> header files define interfaces for functions, structures, unions and classes

> They may also define variables, however if this header file is then included in more than one module the **linker** will complain as the same variable is defined twice.

> should not be defined many times like this

![ ](./assets/Screenshot%20from%202022-09-29%2012-11-27.png)
![ ](./assets/Screenshot%20from%202022-09-29%2012-11-43.png)

> or like this, case redifination

![ ](./assets/Screenshot%20from%202022-09-29%2012-24-56.png)
![ ](./assets/Screenshot%20from%202022-09-29%2012-25-08.png) 

# Single File Inclusion (avoid not being include mang times)

## #pragma once
the same with #ifndef/#define

## #ifndef/#define

C++程序还会用到一项预处理功能的头文件保护符，头文件保护符依赖于预处理变量。

预处理变量有两种状态：已定义和末定义。

#define指令把一个名字设定为预处理变量。

#define和#ifndef这两个分别检查某个指定的预处理变量是否已定义：#ifdef当且仅当变量已定义时为真，#ifndef当且仅当变量末定义时为真。

一但上面检查为真，就会执行后续操作直到遇到#endif指令为止。

> avoid include many times 

![ ](./assets/Screenshot%20from%202022-09-29%2015-32-28.png)
![ ](./assets/Screenshot%20from%202022-09-29%2015-33-14.png)

## difference

- #ifndef和#pragma once都发生在预处理阶段，#ifndef的方式**依赖于宏名字不能冲突**，这不光可以保证同一个文件不会被包含多次，也能保证内容完全相同的两个文件不会被不小心同时包含。当然，缺点就是如果不同头文件的宏名不小心“撞车”。

- #ifndef是C/C++语言特性，而#pragma once是**编译器提供的指令**，同一个文件不会被包含多次。注意这里所说的“同一个文件”是指物理上的一个文件，而不是指内容相同的两个文件。带来的好处是，你不必再费劲想个宏名了，当然也就不会出现宏名碰撞引发的奇怪问题。对应的缺点就是如果某个头文件有多份拷贝，本方法不能保证他们不被重复包含。

- #pragma依赖于编译器，所以一些老的编译器不提供（比如说vc6之前），而#ifndef可移植性非常好。

# Program Libraries

> Program = set of modules (files)
> Function interfaces - defined using library files.
> Libraries give us code reuse across programs (good thing!)
> However we need to have available
>
> - Header Files & Implementation files
> - Compiled Library Files.

# Code as Modules

> With C++ we create classes which contain all the functionality required of the thing we are going to represent.

# build process

> create code like this

![ ](./assets/Screenshot%20from%202022-09-29%2019-55-45.png)

> should first compile .o file, that transfer programming language to machine language

![ ](./assets/Screenshot%20from%202022-09-29%2019-58-55.png)
![ ](./assets/Screenshot%20from%202022-09-29%2019-59-09.png)

>than build them all to create executable file

![ ](./assets/Screenshot%20from%202022-09-29%2020-02-18.png)
![ ](./assets/Screenshot%20from%202022-09-29%2020-02-50.png)

# makefile

makefile 指的是一个叫 makefile 的文件，里面提前写了一些指令。每次要自动化的完成一个比较复杂项目的自动编译用的时候，就在命令行输入“make”命令。使用Makefile可以 “智能” 的知道：

- 哪些文件需要先进行编译。
- 当某一文件在某次make命令之后发生了改变。再一次使用make命令的时候Makefile只会针对变化的部分相关文件进行重新编译，而其他的不做任何改变，所以在效率上比较高。

> The syntax and whitespace rules can be problematic

> Makefiles can be complicated to generate especially for large projects

> Best to use a meta language / tool to generate the Makefiles

> We will use two

## qmake

> Is a system which allows the automatic generation of Makefiles from within the Qt development environment

>In QT

## cmake

cmake is a tool that manages the build process for us in an operating system and compiler independent is credibly powerful and has a clunky language syntax.

why?
>  Make 工具:  GNU Make ，QT 的 qmake ，微软的 MS nmake，BSD Make（pmake），Makepp，等等. 如果软件想跨平台，必须要保证能够在不同平台编译。而如果使用上面的 Make 工具，就得为每一种标准写一次 Makefile.

> CMake 就是针对上面问题所设计的工具：它首先允许开发者编写一种平台无关的 CMakeList.txt 文件来定制整个编译流程，然后再根据目标用户的平台进一步生成所需的本地化 Makefile 和工程文件，如 Unix 的 Makefile 或 Windows 的 Visual Studio 工程。从而做到“Write once, run everywhere”。显然，CMake 是一个比上述几种 make 更高级的编译配置工具。

![ ](./assets/Screenshot%20from%202022-09-30%2015-17-21.png)

### single file

![ ](./assets/Screenshot%20from%202022-09-30%2015-42-05.png)

> then code **cmake .** to generate makefile and code **make** to generate excutable file.

![ ](./assets/Screenshot%20from%202022-09-30%2015-49-55.png)

### multiple file(in one root)

![ ](./assets/Screenshot%20from%202022-09-30%2016-03-32.png)

> we should change CMakeLists.txt a little bit

![ ](./assets/Screenshot%20from%202022-09-30%2016-06-24.png)

> or we can also change it like that

![ ](./assets/Screenshot%20from%202022-09-30%2016-08-08.png)

### multiple file (in different file)

![ ](./assets/Screenshot%20from%202022-09-30%2016-31-20.png)

>对于这种情况，需要分别在项目根目录**5**和**foo**目录里各编写一个 CMakeLists.txt 文件。为了方便，我们可以先将 foo 目录里的文件编译成静态库再由 main 函数调用。

![ ](./assets/Screenshot%20from%202022-09-30%2016-35-02.png)

>第3行，使用命令 add_subdirectory 指明本项目包含一个子目录 foo，这样 foo 目录下的 CMakeLists.txt 文件和源代码也会被处理 。第6行，使用命令 target_link_libraries 指明可执行文件 main 需要连接一个名为 foo 的链接库 。

![ ](./assets/Screenshot%20from%202022-09-30%2016-37-55.png)

> 在该文件中使用命令 add_library 将 src 目录中的源文件编译为静态链接库。

<https://www.hahack.com/codes/cmake/>

