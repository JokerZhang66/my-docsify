![文章图片](https://gitee.com/Barneys/myfiles/raw/master/img/20220302180231.png)
# c++基础用法

##  输入输出

```c
#include <iostream>
using namespace std;
//c++输入输出
int main()
{
    string str = "hello world!";
    int a;
    //endl有换行的功能
    cout << str << endl;
    cin >> a;
    cout << a << "\n";
    cout << a;
    return 0;
}
```

**using namespace std** ,它声明了命名空间 **std**,后续如果有未指定命名空间的符号,那么默认使用 **std**,这样就可以使用 **cin,cout,vector** 等。

**cin** 用于从控制台获取用户输入,**cout** 用于将数据输出到控制台

**cin** 是输入流对象,**cout** 是输出流对象,它们分别可以用 **>>** 和 **<<**,是因为分别在其类中对相应运算符进行了重载。

## 数据类型及范围

```c
#include <limits>
#include <iostream>
using namespace std;

int main()
{
    cout << boolalpha;
    cout << "max(unsigned char): " << (int)(numeric_limits<unsigned char>::max()) << endl;
    cout << "min(unsigned char): " << (int)(numeric_limits<unsigned char>::min()) << endl;

    cout << "max(signed char): " << (int)(numeric_limits<signed char>::max()) << endl;
    cout << "min(signed char): " << (int)(numeric_limits<signed char>::min()) << endl;

    cout << "max(short): " << numeric_limits<short>::max() << endl;
    cout << "min(short): " << numeric_limits<short>::min() << endl;

    cout << "max(int): " << numeric_limits<int>::max() << endl;
    cout << "min(int): " << numeric_limits<int>::min() << endl;

    cout << "max(long): " << numeric_limits<long>::max() << endl;
    cout << "min(long): " << numeric_limits<long>::min() << endl;

    cout << "max(float): " << numeric_limits<float>::max() << endl;
    cout << "min(float): " << numeric_limits<float>::min() << endl;

    cout << "max(double): " << numeric_limits<double>::max() << endl;
    cout << "min(double): " << numeric_limits<double>::min() << endl;

    cout << "max(long double): " << numeric_limits<long double>::max() << endl;
    cout << "min(long double): " << numeric_limits<long double>::min() << endl;

    cout << endl;
}
```

**运行结果:**

```c
max(unsigned char): 255 
min(unsigned char): 0   
max(signed char): 127   
min(signed char): -128  
max(short): 32767       
min(short): -32768      
max(int): 2147483647    
min(int): -2147483648   
max(long): 2147483647   
min(long): -2147483648  
max(float): 3.40282e+038
min(float): 1.17549e-038
max(double): 1.79769e+308
min(double): 2.22507e-308
max(long double): 1.18973e+4932
min(long double): 3.3621e-4932
```

## 枚举

```c
#include <iostream>
using namespace std;

int main()
{
    /**
     * 枚举变量 
     * 元素都是常量,默认从0开始,递增+1
     * 每个常量都有一个值,里面的值递增,可以自己定义常量的值,该值后面的值也是递增
     */
    enum color
    {
        green,  //0 
        blue = 4,   //1
        yellow, //2
    } ;
    cout << yellow << endl;
    cout << size_t(yellow) << endl;
    return 0;
}
```

## C++ 中的左值和右值

C++ 中有两种类型的表达式：

- **左值（lvalue）：**指向内存位置的表达式被称为左值（lvalue）表达式。左值可以出现在赋值号的左边或右边。
- **右值（rvalue）：**术语右值（rvalue）指的是存储在内存中某些地址的数值。右值是不能对其进行赋值的表达式，也就是说，右值可以出现在赋值号的右边，但不能出现在赋值号的左边

变量是左值，因此可以出现在赋值号的左边。数值型的字面值是右值，因此不能被赋值，不能出现在赋值号的左边。下面是一个有效的语句：

```
int g = 20;
```

但是下面这个就不是一个有效的语句，会生成编译时错误：

```
10 = 20;
```

## c++变量(函数)的声明和定义

```c
#include <iostream>

using namespace std;
extern int a;//声明有a这个变量

void func(); //函数声明
void func()
{
    cout << "func" << endl;
}

int main()
{
    int a = 15; //定义变量a,同时包含了声明
    func();
    cout << a << endl;
}
```

## c++变量

全局变量:在所有函数外部声明的变量，称为全局变量。

局部变量:在函数或一个代码块内部声明的变量，称为局部变量。

形式参数:在函数参数的定义中声明的变量，称为形式参数。

**注:**全局变量和局部变量的值相同时,局部变量的值会覆盖全局变量的值,即作用域小的会覆盖作用域大的变量

```c
#include <iostream>

using namespace std;
int  a = 20;
void func()
{
    int a = 15;
    cout << a << endl;
}

int main(int argv,char **__argc)
{
    int a = 15;
    cout << a << endl; //15
    func(); //15
    return 0;
}
```

如果现在函数中访问同名的全局变量,需要配加上域名解析`::`

```c
cout << ::a << endl; //20
```

**输出结果: 15 15**

## static关键字

**static** 存储类指示编译器在程序的生命周期内保持局部变量的存在，而不需要在每次它进入和离开作用域时进行创建和销毁。因此，使用 static 修饰局部变量可以在函数调用之间保持局部变量的值

static 修饰符也可以应用于全局变量。当 static 修饰全局变量时，会使变量的作用域限制在声明它的文件内

```c
#include <iostream>

using namespace std;
int func(){
    static int a=11;
    return a--;

}
int main(int argv,char **__argc)
{
    cout << func() << endl; //11
    return 0;
}
```

## 常量

在 C++ 中，有两种简单的定义常量的方式：

- 使用 **#define** 预处理器。
- 使用 **const** 关键字。

```C
#define MAX_NUM 50
const int MAX_NUM = 50;
```

整数常量可以是十进制、八进制或十六进制的常量。前缀指定基数：0x 或 0X 表示十六进制，0 表示八进制，不带前缀则默认表示十进制。

整数常量也可以带一个后缀，后缀是 U 和 L 的组合，U 表示无符号整数（unsigned），L 表示长整数（long）。后缀可以是大写，也可以是小写，U 和 L 的顺序任意

宏定义可以使用 `#undef `来取消

```C
#undef  MAX_NUM;
```

## const小补充

```c
#include<stdio.h>
#include<stdlib.h>
/**
 * 指针问题
 * 
 */
int main() 
{
    //指针指向的数据不可改变,只读状态
    //p所指向的字符串不可改变
    const char *p="zhang";
    char *q= "abc";
    q= (char *)malloc(sizeof(char)*10);
    *q='1';
    //输出十六进制地址
    printf("%p,%p\n",p,q);
    //无符号十进制表示
    printf("%u,%u\n",p,q);
    char s[]="new string";
    char *b;
    b = (char *)malloc(sizeof(char)*20);
    b = "new string";
    printf("%p\n",s);
    printf("%p\n","new string");
    printf("%p\n",b);

    const int * const m1= (const int *)b;//指针指向不可修改,指针指向的数据也不可修改
    const int * m2;//指针指向的数据不可修改
    int *p1;
    int *q1;
    m2=p1;//可以将char * 指向 const char *
    return 0;
}
```

## 赋值运算符

下表列出了 C++ 支持的赋值运算符：

| 运算符 | 描述                                                         | 实例                            |
| :----- | :----------------------------------------------------------- | :------------------------------ |
| =      | 简单的赋值运算符，把右边操作数的值赋给左边操作数             | C = A + B 将把 A + B 的值赋给 C |
| +=     | 加且赋值运算符，把右边操作数加上左边操作数的结果赋值给左边操作数 | C += A 相当于 C = C + A         |
| -=     | 减且赋值运算符，把左边操作数减去右边操作数的结果赋值给左边操作数 | C -= A 相当于 C = C - A         |
| *=     | 乘且赋值运算符，把右边操作数乘以左边操作数的结果赋值给左边操作数 | C *= A 相当于 C = C * A         |
| /=     | 除且赋值运算符，把左边操作数除以右边操作数的结果赋值给左边操作数 | C /= A 相当于 C = C / A         |
| %=     | 求模且赋值运算符，求两个操作数的模赋值给左边操作数           | C %= A 相当于 C = C % A         |
| <<=    | 左移且赋值运算符                                             | C <<= 2 等同于 C = C << 2       |
| >>=    | 右移且赋值运算符                                             | C >>= 2 等同于 C = C >> 2       |
| &=     | 按位与且赋值运算符                                           | C &= 2 等同于 C = C & 2         |
| ^=     | 按位异或且赋值运算符                                         | C ^= 2 等同于 C = C ^ 2         |
| \|=    | 按位或且赋值运算符                                           | C \|= 2 等同于 C = C \| 2       |

## 函数

形参有默认值时如果没有在调用时给出具体值,会采用默认值

```c
#include <iostream>
using namespace std;

void add_sum(int a,int b=20)
{
    cout << a+b << endl;
}

int main() 
{
        int a = 15;
        int b = 200;
        add_sum(a,b);//215
        add_sum(a);//35
        return 0;
}
```

| 调用类型 | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| 传值调用 | 该方法把参数的实际值复制给函数的形式参数。在这种情况下，修改函数内的形式参数对实际参数没有影响。 |
| 指针调用 | 该方法把参数的地址复制给形式参数。在函数内，该地址用于访问调用中要用到的实际参数。这意味着，修改形式参数会影响实际参数。 |
| 引用调用 | 该方法把参数的引用复制给形式参数。在函数内，该引用用于访问调用中要用到的实际参数。这意味着，修改形式参数会影响实际参数。 |

### 函数占位

**给函数一个类型但是没有变量名**

```c
#include <iostream>

using namespace std;

//占位参数也可以有默认参数
void func(int a,int = 10)
{
	cout << a << endl;
} 
int main(int argc, char const *argv[])
{
	func(10);
	return 0;
}
```

### 函数重载

作用：函数名可以相同，提高复用性函数

重载满足条件:

- 同一个作用域下
- 函数名称相同
- 函数参数类型不同或者个数不同或者顺序不同

```c
#include <iostream>

using namespace std;

int func(int a, int b)
{
	return a + b;
}
int func(float a, int b)
{
	return 22;
}
int func(int a, double b)
{
	return a + (int)(b);
}

int func(double a, int b)
{
	return (int)(a) + b;
}
//错误情况


/*
void func(int a,int b)
{
	cout << a + b << endl;
}
*/
int main(int argc, char const *argv[])
{
	cout << func(10, 10.55) << endl;//20
	cout << func((float)10.2, 10) << endl;//22
	cout << func(10.2,10) << endl;//20
	return 0;
}
```

**注意事项**

```c
#include <iostream>

using namespace std;

void func(int &a)
{
	cout << "aaa" << endl;
}
//会出现模糊调用
/*void func(const int &a)
{
	cout << "bbb" << endl;
}*/

void func(int a)
{
	cout << a << endl;
}
int main(int argc, char const *argv[])
{
	func(10);
	return 0;
}
```

## C++ 随机数

需要加上`ctime`头文件

C/C++产生随机数用到两个函数`rand()` 和 `srand()`

1. 产生[0,x)的随机数
2. 产生[m,n]的随机数
3. 产生不指定范围的随机数(rand()即可)

```c
#include <iostream>
#include <ctime>

#define random_x(x) (rand() % x) //生成[0,x)之间的随机数
using namespace std;

//产生[m,n]之间的随机数
int Random(int m, int n)
{
        int pos, dis;
        if(m == n)
        {
            return m;
        }
        else if(m > n)
        {
            pos = n;
            dis = m - n + 1;
            return rand() % dis + pos;
        }
        else
        {
            pos = m;
            dis = n - m + 1;
            return rand() % dis + pos;
        }
}

int main()
{
    //每次执行种子不同，生成不同的随机数
    srand((int)time(NULL));
    int ra;
    for (size_t i = 0; i < 10; i++)
    {
        //生成随机数
        ra = Random(0,5);
        cout << "随机数为: " << ra << endl;
    }
    return 0;
}
```

## c++数组

```c
#include <iostream>
#include <vector>

using namespace std;

int main()
{
    int b[5] = {1,2,3,4,5};
    int c[] = {1,2,3,4,5}; 
    int d[10] = {1,4};//其余元素为0
    //一个可变大小的数组
    vector<int> a;
    for (size_t i = 0; i < 5; i++)
    {
        a.push_back(i);
        cout << a[i] << " "; 
        cout << b[i] << " ";
        cout << c[i] << " ";
        cout << d[i] << endl;
    }
    //向量数组大小
    cout << a.size() << endl;
    return 0;
}
```

**数组和向量之间的相互转换**

```c
#include<iostream>
#include <vector>

using namespace std;

int main(int argc, char const *argv[])
{
    int array[10] = {1,2,3,4,5,6,7,8,9,10};
    //数组转向量
    vector<int> vec(array, array + sizeof(array)/sizeof(array[0]));
    for (int i = 0; i < 10 ; ++i)
    {
        cout << vec[i] << endl;
    }
    //向量转数组
    int *arr = new int[vec.size()];
    if(!vec.empty())
    {
        memcpy(arr,&vec[0],vec.size()*sizeof(int));
    }
    for (int i = 0; i < 10; ++i)
    {
        cout << arr[i] << endl;
    }
    return 0;
}

```

## c++ string字符串

**部分函数如下:**[详见这篇博客](https://www.cnblogs.com/this-543273659/archive/2011/07/21/2113172.html)

- append() -- 在字符串的末尾添加字符
- find() -- 在字符串中查找字符串
- insert() -- 插入字符
- length() -- 返回字符串的长度
- replace() -- 替换字符串
- substr() -- 返回某个子字符串

```c
#include <iostream>
#include <string>
 
using namespace std;
 
int main ()
{
   string str1 = "Hello";
   string str2 = "World";
   string str;
   //获取一段字符串
   getline(cin,str);
   //拷贝字符串
   string s(str1,0,3);
   string s1(str1);
   cout << s << endl;
   cout << s1 << endl;
   string str3;

   // 复制 str1 到 str3
   str3 = str1;
   cout << "str3 : " << str3 << endl;
 
   // 连接 str1 和 str2
   str3 = str1 + str2;
   cout << "str1 + str2 : " << str3 << endl;
 
   // 连接后，str3 的总长度
   int len = str3.size();
   cout << "str3.size() :  " << len << endl;

   //使用部分函数
   //拼接
   cout << str1.append(str2) << endl;
   //查找子串出现的首字母位置,从0开始
   cout << str1.find("lo") << endl;
   //返回[0,2)子串
   cout << str1.substr(0,2) << endl;
   //返回长度,也可以使用size()
   cout << str1.size() << endl;
   cout << str1.length() << endl;
   //replace(start,num,str)
   cout << str1.replace(0,1,"") <<endl;//相当于删除
   //insert(index,str)
   cout << str1.insert(0,"H") << endl;
   return 0;
}
```

## c++指针

**最基础操作:**

`&`符号的意思是取地址，也就是返回一个对象在内存中的地址。

`*` 符号的意思是取得一个指针所指向的对象。 也就是如果一个指针保存着一个内存地址，那么它就返回在那个地址的对象。

```c
#include <iostream>
 
using namespace std;
 
int main ()
{
   int  var = 20;   // 实际变量的声明
   int  *ip;        // 指针变量的声明

   ip = &var;       // 在指针变量中存储 var 的地址
   
   cout << "Value of var variable: ";
   cout << var << endl;
 
   // 输出在指针变量中存储的地址
   cout << "Address stored in ip variable: ";
   cout << ip << endl;

   // 访问指针中地址的值
   cout << "Value of *ip variable: ";
   cout << *ip << endl;
 
   return 0;
}
```

## C++ 引用 vs 指针

引用容易与指针混淆，它们之间有三个主要的不同：

- 不存在空引用。引用必须连接到一块合法的内存。
- 一旦引用被初始化为一个对象，就不能被指向到另一个对象。指针可以在任何时候指向到另一个对象。
- 引用必须在创建时被初始化。指针可以在任何时间被初始化。

| 概念           | 描述                                                     |
| :------------- | :------------------------------------------------------- |
| 引用作为参数   | C++ 支持把引用作为参数传给函数，这比传一般的参数更安全。 |
| 引用作为返回值 | 可以从 C++ 函数中返回引用，就像返回其他数据类型一样。    |

```c
#include <iostream>
 
using namespace std;
 
int main ()
{
   int i=15;
   int &p = i;
   cout << "引用的变量的值: " << p << endl;
   cout << "原变量的值: " << i << endl;
   return 0;
}
```

## c++ 日期 & 时间

```c
#include <iostream>
#include <ctime>
 
using namespace std;
 
int main( )
{
   // 基于当前系统的当前日期/时间
   time_t now = time(0);
   
   // 把 now 转换为字符串形式
   char* dt = ctime(&now);
 
   cout << "本地日期和时间：" << dt << endl;
 
   // 把 now 转换为 tm 结构
   tm *gmtm = gmtime(&now);
   dt = asctime(gmtm);
   cout << "UTC 日期和时间："<< dt << endl;
   return 0;
}
```

## c++结构体

{{< image src="https://cdn.jsdelivr.net/gh/CorPython/images@master/img/20200108203103.png" caption="">}}

C 语言的 struct 定义了一组变量的集合，C 编译器并不认为这是一种新的类型。

C++ 中的 struct 是一个新类型的定义声明, 所以可以省略 typedef, 定义变量的时候也可以省略 struct, 而不用向c语言那样没用 typedef 取新名字, 就需要用 **struct 结构体名** 这种形式定义变量。

```c
#include <iostream>
#include <cstring>
 
using namespace std;
 
typedef struct
{
   int age;
   bool sex;
   char name[10];
}student;

int main(int argc, char const *argv[])
{
   student a1;
   student *p = &a1;
   a1.age = 15;
   a1.sex = false;
   strcpy(a1.name,"zhang");
   cout << "姓名: " << a1.name << endl;
   cout << "年龄: " <<a1.age << endl;
   cout << "性别:";
   if (a1.sex)
   {
      cout << "男";
   }
   else
   {
      cout << "女" << endl;
   }
   /*
   cout << "姓名: " << p->name << endl;
   cout << "年龄: " << p->age << endl;
   cout << "性别:";
   if (p->sex)
   {
      cout << "男";
   }
   else
   {
      cout << "女" << endl;
   }
   */
   return 0;
}
```

## c++文件

要在 C++ 中进行文件处理，必须在 C++ 源代码文件中包含头文件 `<iostream>` 和 `<fstream>`

```c++
#include <fstream>
#include <iostream>
#include <string>
using namespace std;

int main ()
{

   char data[100];
   string a;

   //写入文件

   ofstream fout;
   fout.open("a.txt");
   cout << "input what you want: " << endl;
   //cin.getline(data, 100);
   getline(cin,a);
   fout << a;
   fout.close();

   //读文件
   ifstream fin;
   fin.open("a.txt");
   fin >> data;
   cout << data << endl;
   return 0;
}
```

`cin.getline()`会从外部读取一行!

对于 **cin** 的操作 使用 **getline(cin，str)**往往可以实现更加简单以及安全的字符串操作,不同于**cin.getline(char*, int a)**，前者可以直接对字符串进行操作。

## 异常处理

C++ 异常处理涉及到三个关键字：**try、catch、throw**。

- **throw:** 当问题出现时，程序会抛出一个异常。这是通过使用 **throw** 关键字来完成的。
- **catch:** 在您想要处理问题的地方，通过异常处理程序捕获异常。**catch** 关键字用于捕获异常。
- **try:** **try** 块中的代码标识将被激活的特定异常。它后面通常跟着一个或多个 catch 块。

```c
#include <iostream>
using namespace std;

double division(int a, int b)
{
   if( b == 0 )
   {
      throw "Division by zero condition!";
   }
   return (a/b);
}

int getNum(int a)
{
	if(a > 10)
	{
		throw "the number is more than 10!";
	}
	return a;
}

int main(int argc, char const *argv[])
{
	try{
		division(15,0);
	}catch(const char * msg){
		cout << msg << endl;
	}
	try{
		getNum(15);
	}
	catch(const char *error){
		cout << error << endl;
	}
	return 0;
}
```

## c++动态内存

C++ 程序中的内存分为两个部分：

- **栈：**在函数内部声明的所有变量都将占用栈内存。
- **堆：**这是程序中未使用的内存，在程序运行时可用于动态分配内存。

很多时候，无法提前预知需要多少内存来存储某个定义变量中的特定信息，所需内存的大小需要在运行时才能确定。

在 C++ 中，您可以使用特殊的运算符为给定类型的变量在运行时分配堆内的内存，这会返回所分配的空间地址。这种运算符即 **new** 运算符。

如果您不再需要动态分配的内存空间，可以使用 **delete** 运算符，删除之前由 new 运算符分配的内存。

```c
#include <iostream>
using namespace std;

int main ()
{
    //基本数据类型的内存分配
    double *value = NULL;
    value = new double;
    *value = 15.50;
    cout << *value << endl;
    delete value;

    //一维数组的动态内存分配
    int *array = new int[10];
    for (int i = 0; i < 10; i++)
    {
        cin >> array[i];
    }
    for (int i = 0; i < 10; i++)
    {
        cout << array[i] << endl;
    }
    delete []array;

    //二维数组的动态分配
    int **array_two, m, n;
    // 假定数组第一维长度为 m， 第二维长度为 n
    // 动态分配空间
    cout << "请输入行(m)和列(n)的值:" << endl;
    cin >> m >> n;
    array_two = new int *[m];
    for ( int i = 0; i < m; i++ )
    {
        array_two[i] = new int [n]  ;
    }
    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < n; j++)
        {
            cin >> array_two[i][j];
        }
    }
    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < n; j++)
        {
            cout << array_two[i][j] << endl;
        }
    }
    //释放
    for ( int i = 0; i < m; i++ )
    {
        delete [] array_two[i];
    }
    delete [] array_two;
    return 0;
}
```

### 三维数组

```c
#include <iostream>
using namespace std;

int main ()
{
    //a[2][3][4]
    int ***a;
    a = new int **[2];
    for (int i = 0; i < 2; i++)
    {
        a[i] = new int *[3];
        for (int j = 0; j < 3; j++)
        {
            a[i][j] = new int[4];
        }
    }
    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            for (int n = 0; n < 4; n++)
            {
                a[i][j][n] = i + j + n;
            }
        }
    }
    for (int i = 0; i < 2; ++i)
    {
        for (int j = 0; j < 3; ++j)
        {
            for (int n = 0; n < 4; ++n)
            {
                cout << a[i][j][n] << endl;
            }
        }
    }
    //释放内存
    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            delete [] a[i][j];
        }
    }
    for (int i = 0; i < 2; i++)
    {
        delete [] a[i];
    }
    delete [] a;
    return 0;

}
```

### 对象的动态内存分配

使用`new`关键字的对象会调用对象的构造函数,并且使用`delete`关键字时会调用析构函数

但是使用`malloc`函数不会调用构造函数,使用`free`关键字也不会调用析构函数

```c
#include <iostream>
#include <malloc.h>

class TEST
{
private:
    int num1;
    int num2;

public:
    TEST()
    {
        num1 = 10;
        num2 = 20;
    }
    void Print()
    {
        std::cout << num1 << " " << num2 << std::endl;
    }
};

int main(void)
{
    // 用malloc()函数在堆区分配一块内存空间，然后用强制类型转换将该块内存空间
    // 解释为是一个TEST类对象，这不会调用TEST的默认构造函数
    TEST *pObj1 = (TEST *)malloc(sizeof(TEST));
    pObj1->Print();

    // 用new在堆区创建一个TEST类的对象，这会调用TEST类的默认构造函数
    TEST *pObj2 = new TEST;
    pObj2->Print();
    delete pObj1;
    delete pObj2;
    return 0;
}
```

**运行结果:**

```
6957200 0
10 20
69572000
1020
```

## 命名空间

举一个计算机系统中的例子，一个文件夹(目录)中可以包含多个文件夹，每个文件夹中不能有相同的文件名，但不同文件夹中的文件可以重名。为了让不同库中的同名函数,变量可以共存,所以引入了命名空间这个概念

如下图中的例子

```C
#include <iostream>
using namespace std;
 
// 第一个命名空间
namespace first_space{
   void func(){
      cout << "Inside first_space" << endl;
   }
}
// 第二个命名空间
namespace second_space{
   void func(){
      cout << "Inside second_space" << endl;
   }
}
int main ()
{
   // 调用第一个命名空间中的函数
   first_space::func();

   // 调用第二个命名空间中的函数
   second_space::func(); 
   
   return 0;
}
```

### using指令

您可以使用 **using namespace** 指令，这样在使用命名空间时就可以不用在前面加上命名空间的名称。这个指令会告诉编译器，后续的代码将使用指定的命名空间中的名称,<span style= 'color:red'>`using`必须使用已经存在的命名空间.</span>

```c
#include <iostream>
using namespace std;

// 第一个命名空间
namespace first_space{
   void func(){
      cout << "Inside first_space" << endl;
   }
}
// 第二个命名空间
namespace second_space{
   void func(){
      cout << "Inside second_space" << endl;
   }
}
namespace third_space{
   void func(){
      cout << "Inside third_space" << endl;
   }
}
using namespace second_space;
int main ()
{
 
   func();
   return 0;
}
```

### 嵌套的命名空间

命名空间可以嵌套，您可以在一个命名空间中定义另一个命名空间，如下所示：

```c
namespace namespace_name1 {   
		// 代码
	namespace namespace_name2{      
		// 代码   
	} 
}
```

您可以通过使用 `::` 运算符来访问嵌套的命名空间中的成员：

```c
// 访问 namespace_name2 中的成员 using namespace namespace_name1::namespace_name2;  
// 访问 namespace:name1 中的成员 using namespace namespace_name1;
```

在上面的语句中，如果使用的是 `namespace_name1`，那么在该范围内`namespace_name2`中的元素也是可用的，

全局变量 `a` 表达为 **::a**,用于当有同名的局部变量时来区别两者!

如下所示：

```c
#include <iostream>
using namespace std;

int a = 300;//全局变量

// 第一个命名空间
namespace first_space{
   int a = 15;
   void func(){
      
      cout << "Inside first_space" << endl;
   }
   namespace second_space{
      int a = 30;
      void func()
      {
         cout << "Inside second_space" << endl;
      }
   }
}

using namespace first_space;//必须在定义之后
int main ()
{
   func();
   int a = 100;//局部变量
   cout << "局部变量a: "<< a << endl;
   cout << "全局变量a: "<< ::a << endl;
   cout << "第一个命名空间变量a: "<< first_space::a <<endl;
   cout << "第二个命令空间变量a: "<< second_space::a<<endl;
   return 0;
}
```
