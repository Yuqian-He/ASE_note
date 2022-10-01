# vcpkg

vcpkg 是微软 C++ 团队开发的在 Windows 上运行的 C/C++ 项目包管理工具,可以帮助您在 Windows 平台上获取 C 和 C++ 库.

vcpkg 自身也是使用 C++ 开发的 (而其他的 C++ 包管理大多并不是 C++ 开发的),并且 vcpkg 能够帮助用户在 Visual Studio 中,更好的使用这些安装好的库.

vcpkg 整合了 git,构建系统整合的 CMake,而绝大多数的 C++ 项目都可以直接或者间接的方式使用 CMake创建原生项目文件并构建.

# fmt

> start this project

![ ](./assets/Screenshot%20from%202022-10-01%2015-15-09.png)

> this code using the **fmt:: library**, which contains an implementation of the new c++20 f**ormat library** amongst other things

format library: <https://en.cppreference.com/w/cpp/utility/format>

![ ](./assets/Screenshot%20from%202022-10-01%2015-23-24.png)

> if we want to use this library, we should tell the compiler it's address

> g++ -Wall -g -std=c++17 -I /public/devel/2022/vcpkg/installed/x64-linux/include/ fmt.cpp -o fmt

![ ](./assets/Screenshot%20from%202022-10-01%2015-25-57.png)

> but only the address is not enough. Because the header contains lots of defination of functions which not in the header but in other .cpp file.

> not the compiler but the linker

![ ](./assets/Screenshot%20from%202022-10-01%2015-30-11.png)

![ ](./assets/Screenshot%20from%202022-10-01%2015-30-27.png)

> first include the search path, find **include<fmt/format.h>**, than add the library search path, allow the function defination in this header can find the function.

# library

> lib include lots of .a file

![ ](./assets/Screenshot%20from%202022-10-01%2015-36-45.png)

> it's static library. By default vcpkg builds **static libraries** under linux.By default the linker will use a **.so** file if found else will search for the **.a** version. 

![ ](./assets/Screenshot%20from%202022-10-01%2015-56-46.png)

# Header Only Libraries

fmt use **-DFMT_HEADER_ONLY**, so we do not need use the -L/-l flag

![ ](./assets/Screenshot%20from%202022-10-01%2016-03-08.png)

# using cmake to automating the build

>First we will create a CMakeLists.txt file in the root of the project directory.

![ ](./assets/Screenshot%20from%202022-10-01%2016-21-50.png)

