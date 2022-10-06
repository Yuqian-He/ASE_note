# namespace

## 为什么使用命名空间

两个同名的人在同一个班里。当我们需要对它们进行区分我们必须使用一些额外的信息.比如区域或者它们的母亲或父亲的名字

在C++应用程序中也会出现同样的情况。例如，编写一些具有名为xyz（）函数的代码，并且还有另一个可用的库，它也具有相同的xyz（）函数。现在编译器无法知道代码中引用的xyz（）函数的哪个版本。

名称空间（namespace）被设计来克服这个困难，并被用作额外的信息来区分类似的函数、类、变量等等，它们在不同的库中具有相同的名称。使用名称空间，可以定义名称的上下文。本质上，名称空间定义了一个范围。

## 命名空间的定义
 ![ ](./assets/Screenshot%20from%202022-10-05%2014-43-51.png)

> should be specific

![ ](./assets/Screenshot%20from%202022-10-05%2014-46-04.png)
![ ](./assets/Screenshot%20from%202022-10-05%2014-46-26.png)

# sizeof()

![ ](./assets/Screenshot%20from%202022-10-05%2015-04-16.png)
![ ](./assets/Screenshot%20from%202022-10-05%2015-04-48.png)

> as we shall see many graphics API's work by passing around chunks of raw memory.

> knowing how big our data is will become important when using lower level languages and API's

## special sizeof

![ ](./assets/Screenshot%20from%202022-10-05%2015-41-22.png)
> the output is:
![ ](./assets/Screenshot%20from%202022-10-05%2015-42-23.png)

one reason:
> 每个特定平台上的编译器都有自己的默认“对齐系数”(也叫对齐模数)。程序员可以通过预编译命令#pragma pack(n)，n=1,2,4,8,16来改变这一系数，其中的n就是你要指定的“对齐系数”。

![ ](./assets/Screenshot%20from%202022-10-05%2015-48-41.png)

another reason
> n 字节的对齐方式 VC 对结构的存储的特殊处理确实提高 CPU 存储变量的速度，但是有时候也带来了一些麻烦，我们也屏蔽掉变量默认的对齐方式，自己可以设定变量的对齐方式。 VC 中提供了#pragma pack(n)来设定变量以 n 字节对齐方式。n 字节对齐就是说 变量存放的起始地址的偏移量有两种情况：
> - 如果 n 大于等于该变量所占用的字节数，那么偏移量必须满足默认的对齐方式。
> - 如果 n 小于该变量的类型所占用 的字节数，那么偏移量为 n 的倍数，不用满足默认的对齐方式。结构的总大小也有个 约束条件，分下面两种情况：如果 n 大于所有成员变量类型所占用的字节数，那么结 构的总大小必须为占用空间最大的变量占用的空间数的倍数； 否则必须为 n 的倍数。

![ ](./assets/Screenshot%20from%202022-10-05%2015-55-33.png)

> when use default alignment rules

![ ](./assets/Screenshot%20from%202022-10-05%2016-02-12.png)


## openGL Buffer Object

> 缓存对象,是OpenGL管理的一段内存，为了与我们CPU的内存区分开，一般叫OpenGL管理的内存，叫显存。

> 那为什么需要Buffer Object呢？这个，主要就是我们的显卡，访问显存，比访问内存要快很多。

![ ](./assets/Screenshot%20from%202022-10-05%2015-20-17.png)

## cuda memory models

<https://www.3dgep.com/cuda-memory-model/>

<https://blog.csdn.net/weixin_30912051/article/details/96973452?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166497966416800182147281%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166497966416800182147281&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-1-96973452-null-null.142^v51^pc_rank_34_2,201^v3^control_2&utm_term=CUDA%20Memory%20Model&spm=1018.2226.3001.4187>

# arrays
> It is sometimes more efficient to group data items together in main memory than to allocate an individual memory cell block for each variable.

problems with arrays

> one of the main issues with using arrays is we don't know the ammount of elements

> the previous code showed how we can determine the array elements by using: 
```
int sizeOfArray=sizeof(primesLT100)/sizeof(int);
```
> however this can cause issues with pointers

![ ](./assets/Screenshot%20from%202022-10-05%2016-48-54.png)

## about array a/ a[0]/*a/&a

![ ](./assets/Screenshot%20from%202022-10-05%2017-53-50.png)
![ ](./assets/Screenshot%20from%202022-10-05%2017-54-00.png)

- a[0]is the first element of an array
- *a is the element which pointed by address
- &a is the address of array but also the address of first element

## C++中int a[10]和int* a=new int[10]有什么区别

![ ](./assets/Screenshot%20from%202022-10-05%2018-16-19.png)

![ ](./assets/Screenshot%20from%202022-10-05%2018-16-33.png)

> the different thing between them is the way memory allocation
int* a=new int[10] : 

- a is the address of new array
- a* is the first element of new array
- &a is the address of a
- if you want to change the element of new array,you should :

![ ](./assets/Screenshot%20from%202022-10-05%2018-29-25.png)
![ ](./assets/Screenshot%20from%202022-10-05%2018-29-37.png)

so the reason why pointers cause sizeof didn't work is **(sizeof(p)/sizeof(*p))** is wrong. 
- sizeof(*p) still point to the first element of new array
- sizeof(p) just the address of p which store the address of new array.

## std::array
more in a later lecture

# auto

![ ](./assets/Screenshot%20from%202022-10-06%2011-31-37.png)

## 用在哪

auto用于推断类型，具体可用于声明变量时根据初始化表达式自动推断该变量的类型，也就是可用在for循环。
也可以用于声明函数返回值的占位符。

## auto and 原数组
![ ](./assets/Screenshot%20from%202022-10-06%2011-50-23.png)

## auto &
![ ](./assets/Screenshot%20from%202022-10-06%2011-51-41.png)

## different
- **auto** open a new memery to store the data, it's a copy of the original data
![ ](./assets/Screenshot%20from%202022-10-06%2011-54-12.png)

- **auto &** points to the address of original store and change it directely
![ ](./assets/Screenshot%20from%202022-10-06%2011-56-22.png)

<https://pythontutor.com/>

# unions
> In a union, every member is allocated the same piece of storage

## difference between unions and structure
 ![ ](./assets/Screenshot%20from%202022-10-06%2019-39-53.png)
 




