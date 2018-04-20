# 访问权限控制

这里的权限控制，指的是对类的成员使用的权限的控制。

## Public

所有public内的成员函数，成员变量都可以被内外界直接访问。

例：

```c++
// TODO
```



## Private

Private内的成员函数，成员变量只能被类内的函数访问。

例：

```c++
// TODO
```



## Protected

Protected 与继承有关，对于本类与Private无异，但对于派生类，派生类可以直接访问Protected中的内容，但不能直接访问Private中的内容。

例：

```c++
// TODO
```



## Friend

友元管的是两个类直接的访问权限。

详见：