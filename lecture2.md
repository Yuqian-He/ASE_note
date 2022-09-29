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

## Automating the Build process
