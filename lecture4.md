- [enum](#enum)
  - [use enum class](#use-enum-class)
  - [conver deftype to int](#conver-deftype-to-int)
  - [define enum class](#define-enum-class)
  - [use enum class](#use-enum-class-1)
- [cstdint](#cstdint)
- [nullptr](#nullptr)
- [constexpr](#constexpr)
  - [limitation](#limitation)
- [lambda](#lambda)

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

# constexpr
> constexpr allows for computation to now take place at compile time rather than runtime

> This means that code using this will not need to do the computation at runtime (for example evaluating a cos or sine function on a know value)

when add constexpr, this function conculate in compile
![ ](./assets/Screenshot%20from%202022-10-07%2020-11-22.png)

![ ](./assets/Screenshot%20from%202022-10-07%2020-11-59.png)

<https://www.youtube.com/watch?v=PJwd4JLYJJY>

## limitation
- It must consist of single return statement (with a few exceptions)
- It can call only other constexpr functions
- It can reference only constexpr global variables

# lambda
another expression of the function

![ ](./assets/Screenshot%20from%202022-10-07%2020-54-20.png)

<https://en.cppreference.com/w/cpp/language/lambda>
