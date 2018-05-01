# 静态变量（Static）

C++提供三种静态变量

1. 外部链接型（external linkage）：不同文件间可访问。
2. 内部链接型（internal linkage）：同一文件不同函数内可访问。
3. 无链接型（no linkage）：只能在函数或块内访问。

静态变量存储在编译器分配的固定的内存空间中，并且在程序执行过程中一直存在。同时所有静态变量默认会被初始化为0（所以位为0）。

**静态的含义：** 变量存储在一个静态的空间。



## 创建静态变量的方法

例：

```c++
...
int global = 1000; // static duration, external linkage
static int one_file = 50; // static duration, internal linkage
int main() 
{
    ...
} 
void funct1(int n) 
{
	static int count = 0;	// static duration, no linkage
	int llama = 0; 
    ...
} 
void funct2(int q) 
{ 
    ...
}
```

- global 在当前文件所有位置均可访问，也可在其他文件访问。
- one_file 只能在当前文件所有位置访问。
- count 只能在 funct1 中访问（其值在函数调用结束后不消失）。



## 外部链接

   