# const关键字

const 关键字主要用于修饰变量，同时它也可以用来修饰函数。

1. 修饰变量时，其含义为该变量的值不会改变。
2. 修饰函数时，表示该函数不会改变其传入参数（引用，指针指向的内容）。


> const的使用准则是：能用const就尽量用const

## 修饰变量

> const 可以完全替代 C 中的宏定义来定义符号常量

const使用方法

`const type name = value;`

或者

`type const name = value;`

### 修饰指针

1. 放在 * 号后面表示指针不会指向别的内容。

```c++
int * const pr = &a;
pr = &b;	// error
```





2. 放在 * 号前面表示不能通过这个指针修改指向的内容。

```c++
const int * pr = &a;
int const * pr2 = &a;	// 等价形式
*pr = 20;	// error
```

要用指针指向一个const常量必须使用这种形式的指针。



### 修饰引用

1. const 修饰的引用表示不能通过引用修改其指向的内容

```c++
const int &s = b;
int const &s = b;	// 等价
int & const s = b;	// error, 无意义
```

2. 如果要用引用指向一个const变量，则必须用const修饰引用



## 修饰函数

在类中，一个被const修饰的函数，不会改变类的成员变量。

如下所示，print不会改变data。

```c++
class Example
{
    int data;
public:
    void print() const;
}
```

因此，当定义一个常对象时仍能调用print

```c++
const Example a;
Example b;
a.print()	// allowed
b.print()	// not allowed    
```