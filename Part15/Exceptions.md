# 异常处理

程序在运行过程中，难免出现各种各样的异常错误，通常我们会尽可能预测这些异常并对其进行处理，对不好处理的异常，我们有时候也以让程序直接崩溃。

## 在以前

在C++标准异常机制出现之前，我们通常有以下几种处理异常的方法。

1. **异常出现时让程序直接退出**

在程序遭遇异常时，让程序终止。这个方法通常有两个函数可以调用：

1. abort()
2. exit()

在程序中任何地方调用这些函数都会使得程序立刻终止。

**例：**

```c++
// TODO
```

2. **使用函数返回值**

想法很简单，利用函数返回值指示函数运行状态。如，返回值为bool类型，若为0表示函数运行出错。

3. **使用全局变量指示错误**

同样简单的想法，定义一个全局变量，通过改变它的值指示函数运行状态。

</br>

以上想法都很简单，有时候也很有效，但有时候也会出现问题。

## 全新的异常处理机制

这个机制主要有三个部分：

1. 抛出异常
2. 捕获异常
3. 处理异常

**例：**

```c++
try { // start of try block 
    z = hmean(x,y); 
} // end of try block 
catch (const char * s) // start of exception handler 
{
	std::cout << s << std::endl;
	std::cout << "Enter a new pair of numbers: ";
	continue; 
} // end of handler

...
double hmean(double a, double b) 
{
    if (a == -b)
    throw "bad hmean() arguments: a = -b not allowed";
    return 2.0 * a * b / (a + b); 
}
```

**Note：**在这个例子中，我们可以看到异常机制的三部是怎么结合在一起的。

- 首先在 `hmean()` 函数中，通过 `throw` 关键字抛出了一个异常（就是一个变量，可以是任何类型）。
- 然后我们把调用 `hmean()` 的部分用 try catch 包裹起来。
- 捕获异常的时候 `catch()` 括号里定义的变量要和抛出的变量类型相同。
- 然后在 `catch` 块进行异常的处理。

如果不catch这个异常，则程序会直接结束。

### 抛出一个对象的例子



```c++
class bad_hmean { 
private:
    double v1;
    double v2; 
public:
	bad_hmean(int a = 0, int b = 0) : v1(a), v2(b){}
    void mesg();
};
inline void bad_hmean::mesg() {
	std::cout << "hmean(" << v1 << ", " << v2 <<"): " << "invalid arguments: a = -b\n";
}
```

