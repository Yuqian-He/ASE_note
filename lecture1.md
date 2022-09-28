# Animation Software Engineering
- Using C++ to develop Graphics application
- Develop 2D / 3D Applications and Tools
- Use OpenGL for Real-time applications
- Develop Algorithms for graphics simulations
- Output files to Renderman for High Quality production level graphics
- Write tools to help with the Graphics Production Pipeline

> you can wrap that up and have a Python binding for it so that you can use your **fast C++ code in Python**, sort of things like Numpy, CUDA and machine learing tools actually are all written in C++

# What we will use
- **C++** using the **clang++** compiler (and also g++) and other tools
- **Doxygen** for documenting our code
- **OpenGL**
- **QtCreator** IDE and Qt for GUI applications
- Loads of external libraries ( **OpenGL, Qt, Boost, Bullet**)
- **git** and **git-hub** for versions control and code submission

> Qt which is the standard GUI library within all the animation tools, virtually all of them use Qt as their sort of GUI and to extend it, that's written in **C++**, but there are bindings for other languages

# NCCA Graphics Library （ngl::）
https://nccastaff.bournemouth.ac.uk/jmacey/GraphicsLib/

# CPP Core Guidelines
http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines


# helloWorld.cpp

## It's bad version

```c++
#include<iostream>
using namespace std;
int main(){
    count<<"Hello World"<<endl;
    return 0;
}
```

![ ](./assets/Screenshot%20from%202022-09-28%2012-43-10.png)

> - store in large memery, cuz pre processing
>
> - using namespace imports all of std
>
> - return 0 means: return是C++预定义的语句，它提供了终止函数执行的一种方式。当return语句提供了一个值时，这个值就成为函数的返回值.

## It's better

```c++
#include <iostream>
#include <cstdlib>
int main()
{
  std::cout<<"Hello World\n";
  return EXIT_SUCCESS;
}
```

> EXIT_SUCCESS, EXIT_FAILURE
> - Defined in header <cstdlib> - 定义于头文件 <cstdlib>
> - EXIT_SUCCESS 与 EXIT_FAILURE 展开成整数常量表达式能用做 std::exit 函数的参数 (从而能用做从 main 函数返回的值)，并指示程序执行状态。
> - use this because it's readable
> http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#a-namerio-endlasl50-avoid-endl

![ ](./assets/Screenshot%20from%202022-09-28%2013-50-56.png)

# Compilation process

![ ](./assets/Screenshot%20from%202022-09-28%2014-25-19.png)

## compile

When I compile g++ like this, it comes out a **a.out** file

![ ](./assets/Screenshot%20from%202022-09-28%2014-06-39.png)

- should add **-o** rename this file or all the default name is **a**
- a.out = assembler output
- ![ ](./assets/Screenshot%20from%202022-09-28%2014-12-53.png)

编译器 g++ 通过检查命令行中指定的文件的后缀名可识别其为 C++ 源代码文件。编译器默认的动作：编译源代码文件生成**对象文件(object file)**，链接对象文件和libstdc++库中的函数得到可执行程序。然后删除对象文件。由于命令行中未指定可执行程序的文件名，编译器采用默认的 a.out。

![ ](./assets/Screenshot%20from%202022-09-28%2014-34-35.png)

- use **-o** to rename this file

<https://blog.csdn.net/weixin_33328213/article/details/116554724?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166437137916782417011764%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166437137916782417011764&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~pc_rank_34-1-116554724-null-null.142^v50^pc_rank_34_queryrelevant25,201^v3^control_2&utm_term=g%2B%2B%20-c%20hello.cpp&spm=1018.2226.3001.4187>

## flag

- flags control the compiler functio
  - **-g** turn on debug information
  - **-Wall** enable all warnings
  - **-std=c++1z** turn on c++ 17 (use c++11 or c++14 for other versions)
  - **-o** output name (default if not used a.out)
![ ](./assets/Screenshot%20from%202022-09-28%2015-43-45.png)

## clang++ vs g++

<https://blog.csdn.net/forcj/article/details/117531228?ops_request_misc=&request_id=&biz_id=102&utm_term=clang++%20g++&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-3-117531228.142^v50^pc_rank_34_queryrelevant25,201^v3^control_2&spm=1018.2226.3001.4187>
