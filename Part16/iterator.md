# 迭代器

迭代器（iterator）和模版（template）的使用是为了更好的实现泛型编程（generic programming)。

- 模版（template）的出现是为了类，函数的实现与数据类型无关。
- 迭代器（iterator）的出现则是为了类，函数的实现与容器的数据结构无关。



## 基本结构

迭代器通常是一个指针，并且用一个类进行封装，同时通常作为某个数据类型的嵌套类存在。

作为一个迭代器，它应该有以下属性：

1. 可以用 `*p` 取内容。
2. 可以互相赋值 `p = q`
3. 可以判等 `p == q` ， `p != q`
4. 可以迭代 `++p` ， `p++`

**接口定义例子：**

```c++
class iterator
{
    Node * pt;
public:
    iterator();
    iterator(Node * pn); // 性质2
    double operator*();	// 性质1
    iterator& operator++();	// 性质4 ++p
    iterator operator++(int);	// 性质4 p++
    bool operator==(const iterator& p);	// 性质3 ==
    bool operator!=(const iterator& p);	// 性质3 !=
}
```

## 基本用法

通常在迭代器所处的容器中定义两个方法：

1. begin() 返回容器中第一个元素
2. end() 返回容器中最后一个元素之后的一个元素（用于判定结尾）

**例：**

```c++
list<double>::iterator pr; 
for (pr = scores.begin(); pr != scores.end(); pr++) 
    	cout << *pr << endl;
```

STL用迭代器封装的更为简洁的用法：

```c++
for (auto x : scores) cout << x << endl;
```