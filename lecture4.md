# enum
枚举类型 (enumeration)，是C++中的一种派生数据类型，是用户创建的一个集合，可以增加程序的可读性，在一些需要重复用到一些元素时颇有益处。 

## use enum class

![ ](./assets/Screenshot%20from%202022-10-07%2018-45-13.png)
![ ](./assets/Screenshot%20from%202022-10-07%2018-45-29.png)

## conver deftype to int

```c++
static_cast<int>;
```
## define enum class

```c++
enum class Mesh {SPHERE,BOX,TORUS};
enum class Shapes {CUBE,CYLINDER,SPHERE};
```

## use enum class

```c++
Shapes::CUBE;
```
make the code more readable

# cstdint
This header was originally in the C standard library as <stdint.h>.

This header is part of the type support library, providing fixed width integer types and part of C numeric limits interface.

# nullptr
C++ 11 introduces the nullptr type. It should replace NULL and you should just use it wherever you used to use NULL

