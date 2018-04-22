# 函数重载

函数重载（function overloading）使得我们可以创建多个不同功能的**同名**函数。在通过名字调用时，根据具体情况选择执行哪一个。

## 规则

- 名字相同才叫函数重载
- 名字相同的函数的函数签名必须不同
- 仅返回值类型不同不能重载

**函数签名：** 即函数的参数

函数调用的时候，具体使用重载的哪个函数是在**编译**的时候就确定了的。

**例子：** 源自wikipedia [Function overloading](https://en.wikipedia.org/wiki/Function_overloading)

```c++
#include <iostream>

// volume of a cube
int volume(const int s)
{
    return s*s*s;
}

// volume of a cylinder
double volume(const double r, const int h)
{
    return 3.1415926*r*r*static_cast<double>(h);
}

// volume of a cuboid
long volume(const long l, const int b, const int h)
{
    return l*b*h;
}

int main()
{
    std::cout << volume(10);
    std::cout << volume(2.5, 8);
    std::cout << volume(100, 75, 15);

    return 0;
}
```



## Note

函数重载(function overloading) 与 函数重写(function overriding) 和多态（polymorphism）容易弄混淆，请多加注意。