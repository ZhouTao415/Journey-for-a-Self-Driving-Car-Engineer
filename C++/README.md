<div align="center">
📖 Github
</div> 
<br>

<div align="center">
简体中文
&emsp;&emsp; | &emsp;&emsp;
<a href="https://github.com/ZhouTao415/Journey-for-a-Self-Driving-Car-Engineer/blob/main/C%2B%2B/Cpp_Interview_EN.md">English</a>
</div> 
<br>


# ➕ C++ Interview for Autonomous Driving
  
## 1. 开始
The purpose of this text is to organize commonly asked questions in interviews. For specific details, it is necessary to refer to books for study, such as 
- "C++ Primer"
- "Effective C++"
- "Inside the C++ Object Model"
The title, consistent with the book "C++ Primer."

### 1.1. C 和 C++ 的区别
  
设计思想上:
- C++ 是面向对象的语言, C 是面向过程的语言. [Case](https://www.zhihu.com/question/24425316)

语法上:
- C++ 具有封装/继承/多态三种特性.
- C++ 相比 C, 增加了类型安全的功能, 比如强制类型转换.
- C++ 支持范式编程, 比如模板类/函数模板等.

## 2. 变量和基本类型
### 2.1. 复合类型
复合类型(compound type)是指基于其他类型定义的类型. 最常见的是引用(references)和指针(pointers).

**引用(references):**

引用即别名: 引用(reference)为对象起了另外一个名字, 引用类型引用(refers to)另外一种类型.
- 定义引用时, 程序把引用和它的初始值绑定在一起, 而不是将初始值拷贝给引用. 一旦初始化完成, 引用将和它的初始值对象一直绑定在一起. 因为无法令引用重新绑定到另外一个对象, 因此引用必须初始化.
```cpp
int ival = 1024;
int &refVal = ival; // refVal refers to (is another name for) ival
int &refVal2; // error: a reference must be initialized
```
- 因为引用不是一个对象, 所以不能定义引用的引用.
- const reference
```cpp
  int a = 1;
  const &b = a;
  a = 2;
  std::cout << b << "= 2"<< std::endl;
  ```

**指针(pointers):**

指针(pointer)是指向(point to)另外一种类型的复合类型.
- 指针无需在定义时赋初值.
- 指针本身就是一个对象, 允许对指针赋值和拷贝, 而且在指针的生命周期内它可以先后指向几个不同的对象.

| 指针  | 数组 |
|-------|----|
|保存数据的地址. |保存数据.|
|间接访问数据, 首先获得指针的内容, 然后将其作为地址, 从该地址中提取数据. |直接访问数据.|
|通常用于动态的数据结构. |通常用于固定数目且数据类型相同的元素. |
|通过malloc分配内存, free释放内存. |隐式的分配和删除. |
|通常指向匿名数据, 操作匿名函数. |自身即为数据名. |
|指针取地址得到的是指针变量自身的地址. |数组名取地址得到的是数组名所指元素的地址(数组的第一个元素的地址). |
|指针能更改名字 |数组是固定大小, 数组一经定义, 就不能改变数组名. |

### 2.2. const限定符
#### 2.2.1. 作用
- 修饰变量: 表明该变量的值不可以被改变.
- 修饰指针: 区分指向常量的指针和常量指针.
- 修饰引用: 用于形参, 既避免了拷贝, 又避免了函数对值的修改.
- 修饰成员函数: 表示函数不能修改成员变量(实际上是修饰this指针)

补充:

- 对于局部对象,常量存放在栈区;
- 对于全局对象, 常量存放在全局/静态存储区;
-对于字面值常量, 常量存放在常量存储区(代码段).

#### 2.2.2. 指向常量的指针 VS 常量指针
参考 C++ Primer 2.4.2 指针和const:

- 指向常量的指针(pointer to const):
  - 具有只能够读取内存中数据, 却不能够修改内存中数据的属性的指针(底层 const).
  - ``` const int * p;或者int const * p; ```
- 常量指针(const pointer):
  - 常量指针是指指针所指向的位置不能改变, 即指针本身是一个常量(顶层 const), 但是指针所指向的内容可以改变.
  - 常量指针必须在声明的同时对其初始化, 不允许先声明一个指针常量随后再对其赋值, 这和声明一般的常量是一样的.
  - ``` int * const p = &a;```

#### 2.2.3. cosntexpr
- 常量表达式(const expression)是**指值不会改变**并且在**编译过程就能得到计算结果**的表达式.
- 一般来说, 如果认定变量是一个常量表达式, 那就把它声明成constexpr类型.
- 一个constexpr指针的初始值必须是nullptr或者0, 或者是存储于某个固定地址中的对象.
- constexpr函数是指能用于常量表达式的函数.
  - 函数的返回类型及所有的形参的类型都得是字面值类型.
  - 函数体中必须有且只有一条return语句.
```cpp
const int max_files = 20; // max_files is a constant expression
const int limit = max_files + 1; // limit is a constant expression
int staff_size = 27; // staff_size is not a constant expression
const int sz = get_size(); // sz is not a constant expression
```

```cpp
constexpr int mf = 20; // 20 is a constant expression
constexpr int limit = mf + 1; // mf + 1 is a constant expression
constexpr int sz = size(); // ok only if size is a constexpr function
```
```cpp
const int *p = nullptr; // p is a pointer to a const int
constexpr int *q = nullptr; // q is a const pointer to int
```
```cpp
constexpr int *np = nullptr; // np is a constant pointer to int that is null
int j = 0;
constexpr int i = 42; // type of i is const int
// i and j must be defined outside any function
constexpr const int *p = &i; // p is a constant pointer to the const int i
constexpr int *p1 = &j; // p1 is a constant pointer to the int j
```
- static constexpr
```cpp 
static constexpr int period = 30;// period is a constant expression
constexpr static char const* name = "Dog"
```
#### 2.2.4. #define VS const

|#define |	const|
|-------|----|
|宏定义, 相当于字符替换	| 常量声明|
|预处理器处理	| 编译器处理|
|无类型安全检查	| 有类型安全检查|
|不分配内存	| 要分配内存|
|存储在代码段(.text)	| 存储在数据段(.data, .bbs)|
|可通过#undef取消	| 不可取消|

- #define
  - 定义了一个宏#define PI 3.14，每当代码中出现PI，预处理器就会将其替换为3.14，然后编译器处理替换后的代码。

- 关于数据段
  - .data段：用于存储初始化的全局变量、静态变量等。
  - .bss段（Block Started by Symbol）：用于存储未初始化的全局变量和静态变量。
  - .text段：包含程序的执行代码。

## 3. 字符串、向量和数组

## 4. 表达式

### 4.1. 右值 & 左值
C++的表达式要不然是右值(rvalue), 要不然是左值(lvalue). 这两个名词是从 C 语言继承过来的, 原本是为了帮助记忆: 左值可以位于赋值语句的左侧, 右值则不能.

当一个对象被用做右值的时候, 用的是对象的值(内容); 当对象被用做左值的时候, 用的是对象的身份(在内存中的位置).

### 4.2. 自增和自减运算符
Increment and Decrement Operators
**++i/i++**
前置版本++i: 首先将运算对象加 1, 然后将改变后的对象作为求值结果.

后置版本i++: 也会将运算对象加 1, 但是求解结果是运算对象改变之前的那个值的副本.
```cpp
int i = 0, j;
j = ++i; // j = 1, i = 1: prefix yields the incremented value
j = i++; // j = 1, i = 2: postfix yields the unincremented value
```
以下摘录自 More Effective C++ Item 6:
```cpp
// prefix form(++i): increment and fetch
UPInt&  UPInt::operator++()
{
    *this +=1；        // increment
    return *this；     // fetch
}
// postfix form(i++): fetch and increment
const UPInt UPInt::operator++(int)
{
    const UpInt oldValue = *this; // fetch
    ++(*this);                    // increment
    return oldValue；             // return what was fetched
}
```

### 4.3. sizeof运算符

sizeof运算符的结果部分地依赖于其作用的类型:

- 对char或者类型为char的表达式执行sizeof运算, 结果得 1.
- 对引用类型执行sizeof运算得到被引用对象所占空间的大小.
- 对指针执行sizeof运算得到指针本身所占空间的大小.
- 对解引用指针执行sizeof运算得到指针指向的对象所占空间的大小.
- 对数组执行sizeof运算得到整个数组所占空间的大小, 等价于对数组中所有元素各执行一次sizeof运算并将所得结果求和.
- 对string对象或vector对象执行sizeof运算只返回该类型固定部分的大小.

### 4.3.2. 类执行sizeof

```cpp
class A {};
class B { B(); ~B() {} };
class C { C(); virtual ~C() {} };
class D { D(); ~D() {} int d; };
class E { E(); ~E() {} static int e; };
int main(int argc, char* argv[]) {
    std::cout << sizeof(A) << std::endl; // 输出结果为1
    std::cout << sizeof(B) << std::endl; // 输出结果为1
    std::cout << sizeof(C) << std::endl; // 输出结果为8,实例中有一个指向虚函数表的指针
    std::cout << sizeof(D) << std::endl; // 输出结果为4,int占4个字节
    std::cout << sizeof(E) << std::endl; // 输出结果为1,static不算
    return 0;
}
```
- 定义一个空类型, 里面没有成员变量和成员函数, 求sizeof结果为 1. 空类型的实例中不包括任何信息, 本来求sizeof得到0, 但是当我们声明该类型的实例的时候, 它必须在内存中占有一定的空间, 否则则无法使用这些实例, 至于占用多少内存, 由编译器决定, 一般有一个char类新的内存.
- 如果在该类型中添加一个构造函数和析构函数, 再对该类型求sizeof结果仍为 1. 调用构造函数和析构函数只需要知道函数的地址即可, 而这些函数的类型只与类型相关, 而与类型的实例无关, 编译器也不会因为这两个函数在实例内添加任何额外的信息.
- 如果把析构函数标记为虚函数, 就会为该类型生成虚函数表, 并在该类型的每一个实例中添加一个指向虚函数表的指针. 在 32 位的机器上, 一个指针占 4 字节的空间, 因此求sizeof得到 4; 在 64 位机器上, 一个指针占 8 字节的空间, 因此求sizeof得到 8.
- 成员函数是与类相关联的，而不是与类的每个实例相关联。因此，每个对象不需要存储成员函数的额外信息，所有对象共享同一份成员函数的实现。这种设计旨在提高内存效率和执行效率，因为它避免了在每个对象实例中重复存储相同的函数代码。

### 4.4. 显式转换
Explicit Conversions

有时候，我们希望显式地强制一个对象转换成不同的类型。例如，在以下代码中，我们可能想要使用浮点数除法：
```cpp
int i, j;
double slope = i/j;
```
为此，我们需要一种方法来显式地将i和/或j转换为double。我们使用**cast**请求一个显式的转换。
```cpp
cast-name<type>(expression);
```

- static_cast: 任何具有明确定义的类型转换, 只要不包含底层const, 都可以使用static_cast.
- dynamic_cast: 用于(动态)多态类型转换. 只能用于含有虚函数的类, 用于类层次间的向上向下转化.
- const_cast: 去除"指向常量的指针"的const性质.
- reinterpret_cast: 为运算对象的位模式提供较低层次的重新解释, 常用于函数指针的转换.

```cpp
double slope = static_cast<double>(j) / i; // cast used to force floating-point division
void* p = &d; // ok: address of any nonconst object can be stored in a void*
double *dp = static_cast<double*>(p); // ok: converts void* back to the original pointer type
```
```cpp
dynamic_cast<type*>(e)
dynamic_cast<type&>(e)
dynamic_cast<type&&>(e)
{
 (Derived *dp = dynamic_cast<Derived*>(bp))
 // use the Derived object to which dp points
} else { // bp points at a Base object
 // use the Base object to which bp points
}
void f(const Base &b)
{
 try { const Derived &d = dynamic_cast<const Derived&>(b);
 // use the Derived object to which b referred
 } catch (bad_cast) {
 // handle the fact that the cast failed
}
```
```cpp
const char *cp;
char *q = static_cast<char*>(cp); // error: static_cast can't cast away const
static_cast<string>(cp); // ok: converts string literal to string
const_cast<string>(cp); // error: const_cast only changes constness
```
```cpp
int *ip;
char *pc = reinterpret_cast<char*>(ip);
```

## 5. 语句
## 6. 函数
### 6.1. 函数基础
#### 6.1.1. 形参和实参 (Parameter & Argument)
- The arguments are used to initialize the function’s parameters.
- 实参是形参的初始值.
#### 6.1.2. static

- 修饰局部变量: 使得被修饰的变量成为静态变量, 存储在静态区. 存储在静态区的数据生命周期与程序相同, 在main函数之前初始化, 在程序退出时销毁. 默认初始化为 0.
- 修饰全局变量: 限制了链接属性, 使得全局变量只能在声明它的源文件中访问.
- 修饰普通函数: 使得函数只能在声明它的源文件中访问.
- 修饰类的成员变量和成员函数: 使其只属于类而不是属于某个对象. 对多个对象来说, 静态数据成员只存储一处, 供所有对象共用.
  - 静态成员调用格式<类名>::<静态成员>
  - 静态成员函数调用格式<类名>::<静态成员函数名>(<参数表>)
```cpp
size_t count_calls() {
 static size_t ctr = 0; // value will persist across calls
 return ++ctr;
}
int main() {
 for (size_t i = 0; i != 10; ++i) cout << count_calls() << endl; return 0;
}
/*
- This program will print the numbers from 1 through 10 inclusive.
- Before control flows through the definition of ctr for the first time, ctr is created and given an initial value of 0. 
- Each call increments ctr and returns its new value. 
- Whenever count_calls is executed, the variable ctr already exists and has whatever value was in that variable the last time the function exited. 
- Thus, on the second invocation, the value of ctr is 1, on the third it is 2, and so on.
*/
```
```cpp
class Account {
public:
    void calculate() { amount += amount * interestRate; }
    static double rate() { return interestRate; }
    static void rate(double);
private:
    std::string owner;
    double amount;
    // The static members of a class exist outside any object.
    // Objects do not contain data associated with static data members.
    // There is only one interestRate object that will be shared by all the Account objects.
    static double interestRate;
    static double initRate();
};
```
```cpp
double r;
r = Account::rate(); // access a static member using the scope operator(::)

Account ac1;
Account *ac2 = &ac1;
// equivalent ways to call the static member rate function
r = ac1.rate(); // through an Account object or reference
r = ac2->rate(); // through a pointer to an Account object

// define and initialize a static class member
double Account::interestRate = initRate();
```
- we can use a static member as a default argument


### 6.2. 参数传递 Argument Passing
- passed by value
- passed by value
- 指针参数传递本质上是值传递, 它所传递的是一个地址值.
- 一般情况下, 输入用传值或者传const reference. 输出传引用(或者指针).

### 6.3. 内联函数
#### 6.3.1. 使用

将函数指定为内联函数(inline), 通常就是将它在每个调用点上"内联地 (in line)"展开.

一般来说, 内联机制用于优化规模较小(Google C++ Style 建议 10 行以下)、流程直接、频繁调用的函数.

在类声明中定义的函数, 除了虚函数的其他函数都会自动隐式地当成内联函数.
```cpp
inline int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(5, 3);
}
// 在编译时，编译器会将main函数中的add(5, 3)调用直接替换为：
int main() {
// 这样，程序运行时就没有了函数调用的开销，因为它直接执行了相加的操作，而不是跳转到函数然后再返回。
    int result = 5 + 3; 
}
```
#### 6.3.2. 编译器对inline函数的处理步骤

1. 将inline函数体复制到inline函数调用点处;
2. 为所用inline函数中的局部变量分配内存空间;
3. 将inline函数的的输入参数和返回值映射到调用方法的局部变量空间中;
4. 如果inline函数有多个返回点, 将其转变为inline函数代码块末尾的分支(使用 GOTO).

#### 6.3.3. 优缺点

优点:

1. 内联函数同宏函数一样将在被调用处进行代码展开, 省去了参数压栈、栈帧开辟与回收, 结果返回等, 从而提高程序运行速度.
2. 内联函数相比宏函数来说, 在代码展开时, 会做安全检查或自动类型转换(同普通函数), 而宏定义则不会.
3. 在类中声明同时定义的成员函数, 自动转化为内联函数, 因此内联函数可以访问类的成员变量, 宏定义则不能.
4. 内联函数在运行时可调试, 而宏定义不可以.

缺点:

1. 代码膨胀. 内联是以代码膨胀(复制)为代价, 消除函数调用带来的开销. 如果执行函数体内代码的时间, 相比于函数调用的开销较大, 那么效率的收获会很少. 另一方面, 每一处内联函数的调用都要复制代码, 将使程序的总代码量增大, 消耗更多的内存空间.
2. inline函数无法随着函数库升级而升级. inline函数的改变需要重新编译, 不像non-inline可以直接链接.
3. 是否内联, 程序员不可控. 内联函数只是对编译器的建议, 是否对函数内联, 决定权在于编译器.
   
## 6.4. 返回类型和return语句
调用一个返回引用的函数得到左值, 其他返回类型得到右值.
```cpp
int x = 10;
int& getRef() {
    return x; // 返回全局变量x的引用
}
getRef() = 20; // 由于getRef()返回了一个引用，我们可以将它用作左值

//-------------------------------------------------------------
int getValue() {
    return 5; // 返回一个值
}
int main() {
    int y = getValue(); // 正确：右值可以用来初始化变量
    getValue() = 10;    // 错误：不能将值赋给一个右值
}
```
## 6.5. 特殊用途语言特性
### 6.5.1. 调试帮助

assert是一种预处理器宏 (preprocessor macro). 使用一个表达式作为它的条件:
```cpp
assert(expr);
```
首先对expr求值, 如果表达式为false. assert输出信息并终止程序的执行. 如果表达式为true. assert什么也不做

## 6.6. 函数指针
函数指针指向的是函数而非对象. 和其他指针一样, 函数指针指向某种特定类型. 函数的类型由它的返回类新和形参共同决定, 与函数名无关.

C 在编译时, 每一个函数都有一个入口地址, 该入口地址就是函数指针所指向的地址.

有了指向函数的指针变量后,可用该指针变量调用函数,就如同用指针变量可引用其他类型变量一样

用途: 调用函数和做函数的参数, 比如回调函数.
```cpp
char * fun(char * p)  {…}  // 函数fun
char * (*pf)(char * p);    // 函数指针pf
pf = fun;                  // 函数指针pf指向函数fun
pf(p);                     // 通过函数指针pf调用函数fun
```
```cpp
// compares lengths of two strings
bool lengthCompare(const string &, const string &);

// pf points to a function returning bool that takes two const string references
bool (*pf)(const string &, const string &); // uninitialized

// The parentheses around *pf are necessary. If we omit the parentheses,
   then we declare pf as a function that returns a pointer to bool:
// declares a function named pf that returns a bool*
bool *pf(const string &, const string &);

pf = lengthCompare; // pf now points to the function named lengthCompare
pf = &lengthCompare; // equivalent assignment: address-of operator is optional

bool b1 = pf("hello", "goodbye"); // calls lengthCompare
bool b2 = (*pf)("hello", "goodbye"); // equivalent call
bool b3 = lengthCompare("hello", "goodbye"); // equivalent call
```

<details>
  <summary>Callback 回调函数 案列</summary>

    #include <iostream>
    #include <algorithm> // for std::sort
    
    // 定义比较函数的类型
    typedef bool (*Compare)(int, int);
    
    // 升序比较
    bool ascending(int a, int b) {
        return a < b;
    }
    
    // 降序比较
    bool descending(int a, int b) {
        return a > b;
    }
    
    // 排序函数，接受数组、数组大小和比较函数作为参数
    void sortArray(int* array, int size, Compare compFunc) {
        std::sort(array, array + size, compFunc);
    }
    
    // 主函数
    int main() {
        int myArray[] = {3, 1, 4, 1, 5, 9, 2, 6};
        int size = sizeof(myArray) / sizeof(myArray[0]);
    
        // 使用升序排序
        sortArray(myArray, size, ascending);
        std::cout << "Ascending order: ";
        for(int i = 0; i < size; ++i) {
            std::cout << myArray[i] << ' ';
        }
        std::cout << '\n';
    
        // 使用降序排序
        sortArray(myArray, size, descending);
        std::cout << "Descending order: ";
        for(int i = 0; i < size; ++i) {
            std::cout << myArray[i] << ' ';
        }
        std::cout << '\n';
    
        return 0;
    }

</details>


## Bibliography: 
- [C++ 面经](https://zhuanlan.zhihu.com/p/675399586)
- [C++ Interview](https://github.com/huihut/interview)

  

