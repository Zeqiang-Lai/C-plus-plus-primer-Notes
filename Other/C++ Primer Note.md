# Chapter 2 : Setting Out to C++

1. 不要使用 `void main()` ，它不是C++标准， 在在某些操作系统不可行。请使用 `int main()`
2. 在 `main()` 中省略 `return` 语句是可行的，C++标准中，省略它与 `return 0` 等价，但仅在 `main()` 中有效。
3. `/* comment */` 是C风格的注释，c++采用 `//` 作为注释标识符。
4. C++的头文件 `iostream.h` 为C++旧的引用风格，新标准在 `include` 的时候不用加后缀 `.h`，而C的头文件要加后缀。除此之外，一些由C的头文件转换过来的C++头文件以 `cxx` 的方式命名，如 `cmath`。
5. `using` 关键字声明使用哪个 `namespace`。 
    - `using namespace std` 使std中的所有名称都可直接使用，但是在大型项目中，这种做法十分危险。
    - 你也可以使用 `using std::cout;` 来使特定的名称可直接使用。
6. `cout<<string` 可以理解为： `cout`为一个`object`，`<<`运算符代表`cout`中的一个运算，这个运算作用是将`string`加入到`outStream`当中。
7. `\n` 和 `endl` 的区别： `endl` 会立刻输出(flush), `\n` 在有些操作系统中会延迟输出
8. C++中以分号作为结束，回车不会影响语句合法性。
9. `main()`的返回值的含义取决于操作系统，一般来说0表示程序正确运行，非0表示程序出错。

10. `using namespace std` 可以用在文件开头使得所有函数都可以用std中的名称，或者用在函数开头，使得在函数中可以使用std中的名称。

# Chapter 3 : Dealing with Data

1. 变量命名：`_`单下划线和`__`双下划线开头的变量名没有语法错误，但这些名称一般被保留用作编译器，STL中使用。
2. 在变量命名的时候，有时候会在开头加一个前缀暗示这个变量的类型，如`n_apple`表示一个int型变量，`str`表示字符串，`b`表示布尔变量，`p`表示指针，`c`表示字符。
3. 关于`int`,`short`,`long`, `long long`长度的问题
    - short 最少 16位
    - int 最少和 short 一样长
    - long 最少 32位，并且至少和int一样长
    - long long 至少 64位，并且至少和long一样长
4. 在编写跨平台程序的时候要格外注意不同系统间基本数据类型字长的差异。
5. C++中`byte`的字长不一定是8位，它会随不同基本字符集不同，以美国英语基本字符集ascii为例，则`byte`为8位，而在其他语言中，`byte`可能为16位或32位。

6. `sizeof` 是一个运算符，当`sizeof`作用于具体的变量是，括号可以去掉。如`sizeof n_apple`，而`sizeof(int)`不行。
7. C++特有的初始化变量的方式。`int wrens(432);`, 而C,C++通用的是`int wrens = 432;`。另一种C++特有的初始化方式，`int apple = {24};`, `int apple{24};`。中括号里可以放空，默认初始化为0.
8. C++中不同进制的表示
    - 默认为十进制
    - 0开头为8进制
    - 0X或0x开头为16进制，16进制数字的字母大小写均可
9. 表示数字类型的后缀, 默认为int， 大小写的`L`表示long，以任意方式组合的`ul`,`lU`表示 `unsigned long`，C++11中还有`unsigned long long`，表示法类似。
10. 在C++源代码中使用unicode字符，`\u`接4个16进制数字, `\U`接8个16进制数字
11. 如果要用`char`来存数字，最好明确`signed`或是`unsigned`，因为单单`char`其范围是不确定的。
12. `wchar_t`一个更大的`char`，可以用来存诸如中文在内的字符。
    - 前缀L表示这类字符，字符串。如L"p"
    - 读入输出要用 `wcin` , `wcout`
13. 另两种国际化字符的表示方式：
    - `char16_t` ，前缀u
    - `char32_t` ，前缀U
14. C++中常量定义用`const` 更好
15. `cout`设置浮点数输出方式的办法 `cout.setf(ios_base::fixed, ios_base::floatfield)`
16. `float` `double` `long double` 的后缀, f/F (float), l/L (long double), double 不需要后缀（默认double）。
15. C++中强制类型转换有两种：
    - C方式 `(type name) variable` 如 `(int)a`
    - C++方式 `type name(variable)` 如 `int(a)`

# Chapter 4 : Compound Types

1. 数组在定义时，其大小必须为一个值 `const value` 或者一个常量`const int` (任何在编译时能确定的值)。用`new`的话 **@todo**

2. 数组可以在定义的时候用`{ }`初始化
    -  但只能在定义的时候用
    -  可以初始化部分元素，剩下元素被置为0
    -  不初始化的数组其元素值不确定
    -  若要将数组元素全部置为0，可以使用`int a[100] = {0}`
3. 在C++11，数组初始化的时候可以不要`=`等号，并且可以用空括号`{}`将数组初始化为0
4. 在C++中，任何中间只有空格，tab字符，换行符的两个字符串会被自动连接在一起。
```c++
cout<< "Hello"
" World!";
// output: Hello World!
```
5. `cin`是有一个输入缓冲区的，`cin`识别字符串的方式是 空格，tab，换行。

6. 要一次读一行的话，C++的`cin`提供了一个`getline()`成员函数。`getline()`有两个参数，第一个为存放字符串的数组，第二个为读入字符数量限制。
7. `cin.get()`使用要注意的
    - 参数与`cin.getline()`一样
    - `cin.get()`会把回车留在缓冲区，要去掉它可以调用一次`cin.get()`（无参数）, 或者用更简洁的方法，`cin.get(xx,xx).get()`
8. 为什么要使用`cin.get()` ? 它使得我们能够得知读入是因为什么结束的，如果最后有一个换行符，则表示读入完成，否则是因为数量限制读入结束。
9. `cin.geline()`,`cin.get()` 会遇到的问题，读入空行，超出字符限制。
10. 读一整行字符到`string`中的方法是 `getline(cin, str);`
11. `wchar_t`, `char16_t`, `char32_t` 的字符串前缀和`raw string`的用法（page 154）
12. C++中`structure`可以用`{}`初始化，可以加等号也可以不加（C++11）。
13. 数组指针和指针数组: `short (*pas)[20] = &tell` 是数组指针，去掉括号即为指针数组。
14. 对数组名进行`sizeof`返回的是整个数组的大小
15. 记时相关函数: 头文件`ctime`
```c++
#include<ctime>
clock_t delay = secs * CLOCKS_PER_SEC;
clock_t start = clock();

// clock()返回的是系统时钟的值,它是一个long 或unsigned long
// clock_t 是long, unsigned long 的一个别名(编译器会选择代表哪种类型)
// CLOCKS_PER_SEC是一个常量表示当前环境下每秒的clock数
```
16. `cin>>`读入有一个缓冲区，读入一长串如果没处理完会留给下一次`cin`处理
17. `cin.get(ch)`会读入空格，回车结束，仍有缓冲区。
18. `cin.get()`有三个版本，两参数（字符数组首地址，最长长度），单参数（char&)，无参数`ch = cin.get()`。
19. `istream`中有一个可以把`cin`变为`bool`值的函数，所有读入字符到EOF有很多写法
```c++
// 1
while(cin.fail() == false){}
// 2
while(!cin.fail()){}
// 3
while(cin){}
// 4
while(cin.get()){} // cin.get() return a cin
```
20. EOF的值随操作系统可能会变，`char ch = cin.get()`可能要换成`int ch = cin.get()`

# Chapter 6 : Branching Statements and Logical Operators

1. 当你要在if中使用诸如 `3 == number` 的时候，请尽量使用 `3 == number`, 不要用 `number == 3` 因为如果你不小心写错（只写了一个`=`）则程序不会报错，而且很难发现）。
2. 逻辑运算符 `||`， `&&` 在运算的时候如果左边单边能确定结果，则不会再计算右边。
3. 不要用`17 < age < 35`这种判断（这语法正确但可能并不是你想要的），应该使用`age > 17 && age < 35)`
4. C++中可以用 `and`, `or`, `not` 来代替逻辑运算符 `&&`, `||`, `!`。
5. `cctype` : `isalpha()` 判断是否为字母，是则返回非0 / `ispunct()` 判断是否为标点，如果是返回true。
6. C++中在switch中，直接跳到匹配的label，然后一直往下执行，如果要让它在下一个label停下来，需要显式break;
7. `cin>>` error handle
```c++
while (!(cin >> golf[i])) 
{ 
    cin.clear(); // reset input 
    while (cin.get() != '\n') 
      continue; // get rid of bad input 
    cout << "Please enter a number: "; 
}
```
8. C++文件读取机制page293

# Chapter 7 : Functions: C++'s Programming Modules

# Chapter 8 : Adventures in Functions

1. 返回值是reference的话，这个语句是允许的 `accumulate(dup,five) = four;`
2. A function that returns a reference is actually an alias for the referred-to variable.
3. 不要返回一个指向函数中定义的变量的引用，除非是new出来的变量。
4. 在函数返回值中使用 const 引用 使得不能对返回值赋值。
5. 函数重载，变量和变量引用视为同一签名。
6. 函数重载 不允许不同返回类型的重载。]
7. `void stove(double && r3);` // matches rvalue
8. 函数模版的用法，在function prototype and definition 前都要声明 `template <typename T>` 
    - `template` 是关键字
    - `typename` 可与 `class` 互换
    - `T` 为类型名，可任意取
9. More typically, templates are placed in a header file that is then included in the file using the
10. The explicit specialization declaration has <> after the keyword template, whereas the explicit instantiation omits the <>.

# Chapter 9 : Memory Models and Namespaces

1. You can divide the original program into three parts:
    - A header file that contains the structure declarations and prototypes for functions that use those structures
    - A source code file that contains the code for the structure-related functions
    - A source code file that contains the code that calls the structure-related functions
2. Here are some things commonly found in header files:
    - Function prototypes
    - Symbolic constants defined using #define or const
    - Structure declarations
    - Class declarations
    - Template declarations
    - Inline functions
3. `Linkage`决定变量是否能在文件间共享，`scope`决定变量的可见范围以及生命周期。
4. 变量的生命周期取决与与它最近的{}大括号。
5. 静态变量的三种定义方式
    - 定义在函数外，不加`static`。所有文件可见
    - 定义在函数外，加`static`。文件内可见
    - 定义在函数内或block内加`static`，函数内或block内可见
6. 如果要用别的文件的外部变量，在本文件中得用`extern`关键字声明这个变量，并且不能初始化。否则将会变为定义这个变量。
7. static variable without linkage keep their value during function calls. It is only initilize once at the begining.
8. `volativle` 关键字定义的变量，表示这个变量可能会被程序以外的东西改变。p473
9. `mutable`
10. `new`的时候可以用`{}`初始化。`double * pdo = new double {99.99};`

# Chapter 10 : Objects and Classes

1. C++ structure 和 class 基本一样，除了class中默认为private，structure 默认为public
2. 成员变量通常用 加下划线的方式避免与构造函数参数名冲突 `string company_; long shares_;`
3. const加在函数后面，表示这个函数不会修改成员变量。const对象只能调用带const的成员函数。
4. 在类内定义常量请使用`static const`
5. C++11中新增的枚举类型：`enum class A {a, b, c, d}`，这个类型的枚举值不会被隐式转换。

# Chapter 11 : Working with Classes

1. 运算符重载本质： `total = coding.operator+(fixing);`
2. 运算符重载的参数至少有一个类型是自定义类型。
3. 友元分为友元函数，友元类，友元成员函数。
4. 友元函数可以访问友元函数所在类的私有成员。
5. 函数实现时不需要`friend`关键字。
6. 除了重载`cout<<`，你还可以重载`fout<<`
7. 自动类型转换(automatic conversion)，强制类型转换（type cast）
8. 所有单参数的构造函数都可以被用勒进行自动类型转换，在函数前加`explicit`将会屏蔽隐式类型转换。
9. 将类类型转换为基本类型，在类中定义类型转换函数，格式为`operator typeName()`，没有返回值，没有参数。



