# 类型判定(Runtime-Type-Identification)

RTTI提供了一种在程序运行时确认变量类型的方法。

1. 这是一个比较新的特性，不是所有的编译器都支持它，同时有的编译器默认选项是关闭这个特性（你需要手动开启，如果你需要用到它）。
2. RTTI只能用在含有虚函数的类

RTTI的主要内容有三部分：

1. `dynamic_cast` 对指针进行类型转换，如果转换是安全的则转换，否则返回空指针。
2. `typeid` 运算符：返回一个 type_info
3. `type_info`  一个类：存储与类型有关的信息

## dynamic_cast

**语法：**

```c++
Superb * pm = dynamic_cast<Superb *>(pg);
```

也可以用在引用上，但如果失败的话会抛出一个错误。

```c++
#include <typeinfo> // for bad_cast ...
try {
    Superb & rs = dynamic_cast<Superb &>(rg); 
    ...
} catch(bad_cast &){ 
    ...
};
```

**用法举例：**

1. 尝试转换指针，如果是空，表示这个指针指向的对象不是对应类型，反之则是。

## typeid && type_info

1. 判断两个变量是不是一个类型

```c++
typeid(Magnificent) == typeid(*pg)
```

2. 打印类型名称（通常是名称）

```c++
cout << "Now processing type " << typeid(*pg).name() << ".\n";
```

**Note：**

- type_info 里有类的信息，其中有很多方法，name()是其中一个。



## 注意

不要滥用RTTI，许多情况下虚函数足以实现你想要的效果。



