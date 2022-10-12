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
  - [Lambda表达式定义](#lambda表达式定义)
  - [Lambda表达式工作原理](#lambda表达式工作原理)
  - [Lamdba表达式适用场景](#lamdba表达式适用场景)
    - [Lamdba表达式应用于STL算法库](#lamdba表达式应用于stl算法库)
    - [短小不需要复用函数场景](#短小不需要复用函数场景)
    - [Lamdba表达式应用于函数指针与function](#lamdba表达式应用于函数指针与function)
    - [Lamdba表达式作为函数的入参](#lamdba表达式作为函数的入参)

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

## Lambda表达式定义
 ISO C ++标准官网展示了一个简单的lambda 表示式实例:

 ```c++
 #include <algorithm>
#include <cmath>

void abssort(float* x, unsigned n) {
    std::sort(x, x + n,
        // Lambda expression begins
        [](float a, float b) {
            return (std::abs(a) < std::abs(b));
        } // end of lambda expression
    );
}
```
在上面的实例中std::sort函数第三个参数应该是传递一个排序规则的函数，但是这个实例中直接将排序函数的实现写在应该传递函数的位置，省去了定义排序函数的过程，对于这种不需要复用，且短小的函数，直接传递函数体可以增加代码的可读性。

## Lambda表达式工作原理
编译器会把一个lambda表达式生成一个匿名类的匿名对象，并在类中重载函数调用运算符,实现了一个operator()方法。

```c++
auto print = []{cout << "Hello World!" << endl; };
```
编译器会把上面这一句翻译为下面的代码:
```c++
class print_class
{
public:
	void operator()(void) const
	{
		cout << "Hello World！" << endl;
	}
};
//用构造的类创建对象，print此时就是一个函数对象
auto print = print_class();
```

## Lamdba表达式适用场景
### Lamdba表达式应用于STL算法库
```c++
// for_each应用实例
int a[4] = {11, 2, 33, 4};
sort(a, a+4, [=](int x, int y) -> bool { return x%10 < y%10; } );
for_each(a, a+4, [=](int x) { cout << x << " ";} );
```
```c++
// find_if应用实例
int x = 5;
int y = 10;
deque<int> coll = { 1, 3, 19, 5, 13, 7, 11, 2, 17 };
auto pos = find_if(coll.cbegin(), coll.cend(), [=](int i) {                 
    return i > x && i < y;
});
```
```c++
// remove_if应用实例
std::vector<int> vec_data = {1, 2, 3, 4, 5, 6, 7, 8, 9};
int x = 5;
vec_data.erase(std::remove_if(vec.date.begin(), vec_data.end(), [](int i) { 
    return n < x;}), vec_data.end());

std::for_each(vec.date.begin(), vec_data.end(), [](int i) { 
    std::cout << i << std::endl;});
```
### 短小不需要复用函数场景
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main(void)
{
    int data[6] = { 3, 4, 12, 2, 1, 6 };
    vector<int> testdata;
    testdata.insert(testdata.begin(), data, data + 6);

    // 对于比较大小的逻辑，使用lamdba不需要在重新定义一个函数
    sort(testdata.begin(), testdata.end(), [](int a, int b){ 
        return a > b; });

    return 0;
}
```
### Lamdba表达式应用于函数指针与function
```c++
#include <iostream>
#include <functional>
using namespace std;

int main(void)
{
    int x = 8, y = 9;
    auto add = [](int a, int b) { return a + b; };
    std::function<int(int, int)> Add = [=](int a, int b) { return a + b; };

    cout << "add: " << add(x, y) << endl;
    cout << "Add: " << Add(x, y) << endl;

    return 0;
}
```

### Lamdba表达式作为函数的入参
```c++
using FuncCallback = std::function<void(void)>;

void DataCallback(FuncCallback callback)
{
	std::cout << "Start FuncCallback!" << std::endl;
	callback();
	std::cout << "End FuncCallback!" << std::endl;
}

auto callback_handler = [&](){
	std::cout << "This is callback_handler";
};

DataCallback(callback_handler);
```