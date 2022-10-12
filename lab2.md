# getting started

![ ](./assets/Screenshot%20from%202022-10-08%2015-21-03.png)

- src: used for c++ source files .cpp
- include: used for c++ header files .h
- tests: used for tests and related files

## make CMakeLists
![ ](./assets/Screenshot%20from%202022-10-08%2016-28-21.png)

### 指定 cmake 的最小版本

```c++
cmake_minimum_required(VERSION 3.12)
```
这行命令是可选的，我们可以不写这句话，但在有些情况下，如果 CMakeLists.txt 文件中使用了一些高版本 cmake 特有的一些命令的时候，就需要加上这样一行，提醒用户升级到该版本之后再执行 cmake。

### 设置项目名称

```c++
project(demo) 
```
这个命令不是强制性的，但最好都加上。它会引入两个变量 demo_BINARY_DIR 和 demo_SOURCE_DIR，同时，cmake 自动定义了两个等价的变量 PROJECT_BINARY_DIR 和 PROJECT_SOURCE_DIR。

<https://blog.csdn.net/qq_28087491/article/details/125459993?ops_request_misc=&request_id=&biz_id=102&utm_term=CMakeLists&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-5-125459993.142^v52^pc_rank_34_2,201^v3^control_2&spm=1018.2226.3001.4187>

# gtests

