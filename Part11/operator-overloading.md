# 运算符重载

运算符重载本质就是个语法糖，没有它也不是不可以，但是它的存在可以使得程序更加简洁直观。

运算符重载是多态的一种形式，它允许你重载运算符，使得运算符可以作用于各种各样不同的类型。



## 运算符本质

运算符的本质是一个函数，当出现一个运算符时，编译器会自动把它变成相应的函数调用形式。

如`a+b` 会变成 `a.operator+(b)` 或 `operator+(a,b)` ，前者的+重载为a的成员函数，后者+重载为全局函数。



## 基本语法

运算符本质是要重载函数，重载方式有两种：

1. **成员函数**

```c++
class Int 
{
    int m_val;
public:
    Int operator+(const Int& b) {
    	return Int(m_val + b.m_val);
    }  
}
```

Note:

- 所有运算符对应的函数名都形如`operator[符号]` ，要重载运算符时，重载对应函数即可。
- 返回值类型依据需要选取，如+号则应该返回值类型是和的类型，==号则应是一个bool类型，当然你可以重新定义这些符号的含义，但不推荐这么做。
- 参数列表即为运算符的操作数，重载为成员函数的话，对象自身为第一个操作数。
- 重载运算符一定要在公有部分。



2. **全局函数**

```c++
class Int
{
public:
    friend ostream& operator<<(const Int& a);
};

ostream& operator<<(const Int& a)
{
    //....
}
```

- 由于无法修改ostream类的定义，因此这里需要把`>>`重载为全局函数，并且为了使得能访问 `Int` 的私有成员，需要把该函数设为 `Int` 的友元。



## 注意事项

1. **操作数的顺序会影响重载运算符的使用**

由于重载成成员函数的本质是调用成员函数，所以以下的重载方式调用的时候会有所限制：

```c++
class Int 
{
    int m_val;
public:
    Int operator+(const int b) {	// method 1
    	return Int(m_val + b);
    }  
}
```

Note： 以这种方式重载的时候，只能够这样用：

```
Int a;
int b;
a+b;	// = a.operator+(b);
```

而不能这么用：

```c++
b+a
```

如果想要这么用，必须将+再重载一个全局函数，形如

```c++
Int operator+(const int b, const Int& a);
```



2. **重载运算符一样可以用`const`关键字修饰。**

如+不修改其操作数的值，则可以用const修饰

```c++
Int operator+(const int b, const Int& a) const;
```



## 限制

1. 重载运算符的操作数必须至少有一个是用户的自定义类型
2. 重载运算符的时候，运算符的操作数和优先级不能改变
3. 不能自己创造运算符
4. 有些运算符不能重载，具体如下

| 运算符           | 描述                           |
| ---------------- | ------------------------------ |
| sizeof           | The sizeof operator            |
| .                | The membership operator        |
| .*               | The pointer-to-member operator |
| ::               | The scope-resolution operator  |
| ?:               | The conditional operator       |
| typeid           | An RTTI operator               |
| const_cast       | A type cast operator           |
| dynamic_cast     | A type cast operator           |
| reinterpret_cast | A type cast operator           |
| static_cast      | A type cast operator           |

5. 有些运算符只能重载为成员函数，具体如下

| 运算符 | 描述                                    |
| ------ | --------------------------------------- |
| =      | Assignment operator                     |
| ()     | Function call operator                  |
| []     | Subscripting operator                   |
| ->     | Class member access by pointer operator |



