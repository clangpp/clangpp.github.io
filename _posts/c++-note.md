___
2009.12.31

**问题描述**：是不是有什么东西一定隐藏在并发程序设计模式之下？这东西是C++机器模型可实现的且可以定义在语言特性里的？

**问题原因**：谁知道啊，就是一种感觉。

**解决方法**：跟朱建勋或其他程序设计高手请教和讨论一下，不断去寻找隐藏在并发之下的机器模型。一旦找到，就可以将其定义在C++语言之中，从而有更多的环境可以使用并发编程了。

___
2009.12.31

**问题描述**：如何找到最新的C++0x进展？

**解决方法**：一个可能的办法是，把下面这个URL改改，放到浏览器里去试试。

<http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2007/n2440.htm>

<http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2007/n2440.pdf>

<http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2009/>

___
2010.01.02

**问题描述**：当自己写一个类的时候，如何确定成员变量和成员函数的访问权限？

**解决方法**：根据《Effective C++》所说，所有成员变量都应声明为private，这样可以保证该类的public用户（类使用者）和protected用户（派生类撰写者）都可以不因你要修改类而修改他们的代码。

___
2010.01.02

**问题描述**：当自己写一个类的时候，有些功能只依赖于类的public接口函数。当需要用函数封装该功能时，是写成成员函数、友元函数还是普通函数？

**解决方法**：根据《Effective C++》所说，当然是普通函数。这样增强了类的封装性，实现新功能也更灵活。相关功能的普通函数还可以声明到一个namespace中作进一步打包封装。用namespace可以在很多文件中实现向同一个namespace添加功能函数，扩展灵活，编译依存度更低，使用起来语意像类的静态成员函数一样清晰。有百利而无一害。

___
2010.01.02

**问题描述**：为什么将自定义代码放在std命名空间里会出错？

**问题原因**：因为std的所有成员，都能且只能由C++标准委员会指定。

**解决方法**：1.没招儿，没法解决。
+ 2.将代码写在别的命名空间内，用的时候using对应的namespace。
+ 3.最根本的办法，你去成为C++标准委员会的一员，提交提案并说服其他委员在定C++标准的时候，把你这段代码加到std命名空间去。

___
2010.01.03

**问题描述**：如何评价和看待复杂性？

**解决方法**：Complexity will go somewhere: if not the language then the application code.
——by Bjarne Stroustrup

___
2010.01.08

**问题描述**：在类继承体系中，为什么会出现“鸟都会飞――企鹅是鸟――但企鹅不会飞”这样的悖论？

**问题原因**：因为软件世界和现实世界有一些不同。在软件世界中，类的继承表示派生类能拥有基类的所有行为，而且严格拥有。但在现实世界中，我们说“鸟都会飞”，是说“一般的鸟都会飞”，并不是很严格的继承关系。

**解决方法**：1.严格地使用抽象继承体系，对世界做贴近软件规则的抽象；
+ 2.根据软件的应用范围，灵活设计继承体系；（换句话说，也许你的应用中根本不会出现不会飞的鸟，那还操那个心干什么？）
+ 3.在运行时检查逻辑错误，抛出异常或提示错误等。
+ 4.在逻辑非法的操作中使用static_assert()，保证编译期查错，个别禁止非法行为；（也就是在企鹅的飞行函数中加入一个错的判断）

___
2010.03.27

**问题描述**：在Visual Studio 2005中，如何将代码转换为标准格式？

**解决方法**：选定需要格式化的范围，在菜单中选择“编辑”->“高级”->“设置选定内容的格式”即可。
+ 快捷键为：CTRL+K，CTRL+F

___
2010.03.27

**问题描述**：在Visual Studio 2005中，如何为主函数执行加入参数？

**解决方法**：在菜单中选择“项目”->“属性”->“配置属性”->“调试”->&quot;命令参数&quot;，加入参数即可。

___
2010.03.30

**问题描述**：如何在启动命令行界面(cmd.exe)运行程序时，程序执行完毕后命令行不退出？

**解决方法**：1. 在启动命令行的时候加入参数 /k 可以保持命令行不自动退出。如：cmd /k test.exe

___
2010.03.30

**问题描述**：对一个区间进行排序的标准算法有哪些？都完成什么功能？

**解决方法**：
&nbsp; &nbsp; 1.BidirectionalIterator partition(BidirectionalIterator first, BidirectionalIterator last, Predicate pred);
+ 完成区间[first,last)的不稳定二分，使满足pred(*iter)的元素都在左边，返回值是指向第一个不满足pred(*iter)==true的迭代器iter。
+ 2. BidirectionalIteratorstable_partition(BidirectionalIterator first, BidirectionalIterator last,Predicate pred);
+ 完成区间[first,last)的稳定二分，使满足pred(*iter)的元素都在左边，返回值是指向第一个不满足pred(*iter)==true的迭代器iter。
+ 3. void nth_element(RandomAccessIterator first, RandomAccessIterator middle, RandomAccessIterator last);
+ void nth_element(RandomAccessIterator first, RandomAccessIterator middle, RandomAccessIterator last, StrictWeakOrdering cmp);
+ 完成区间[first,last)上的不稳定二分，使区间[first,middle+1)内的任意元素i和区间[middle+1,last)内的任意元素j满足j<i==false(或cmp(j,i)==false)，
+ 而且，middle位置的元素恰好是区间[first,last)全排后middle位置的元素。
+ 4. void partial_sort(RandomAccessIterator first, RandomAccessIterator first_n, RandomAccessIterator last);
+ void partial_sort(RandomAccessIterator first,RandomAccessIterator first_n, RandomAccessIterator last, StrictWeakOrderingcmp);
+ 完成区间[first,last)上的不稳定二分，使区间[first,first_n)中的元素为[first,last)中的最小的(first_n-first)个元素，
+ 而且，[first,first_n)中的元素按升序排序(后一版本中，使用cmp为排序规则)，[first_n,last)中的元素不排序。
+ 5. void sort(RandomAccessIterator first, RandomAccessIterator last);
+ void sort(RandomAccessIterator first, RandomAccessIterator last, StrictWeakOrdering cmp);
+ 完成区间[first,last)的不稳定排序。（后一个版本使排序后的区间内相邻元素满足cmp(*(i+1),*i)==false（i为迭代器）。）
+ 6. void stable_sort(RandomAccessIterator first, RandomAccessIterator last);
+ void stable_sort(RandomAccessIterator first, RandomAccessIterator last, StrictWeakOrdering cmp);
+ 完成区间[first,last)的稳定排序。（后一个版本使排序后的区间内相邻元素满足cmp(*(i+1),*i)==false（i为迭代器）。）

___
2010.04.05

**问题描述**：为什么用私有继承不能实现运行时多态？

**问题原因**：人民邮电出版社.徐惠民.2005年.《C++大学基础教程》.P246有以下语句：
+ 要实现运行时的多态，需要以下条件：
+ 必须通过指向基类对象的指针访问和基类成员函数同名的派生类成员函数；
+ 或者用派生类对象初始化的基类对象的引用访问和基类成员函数同名的派生类成员函数；
+ 派生类的继承方式必须是公有继承；
+ 基类中的同名成员函数必须定义为虚函数。
+ 
**解决方法**：如上所述，私有继承和保护继承都不能实现运行时多态，要将继承方式改为公有继承，并将需要实现多态的成员函数修改为虚函数。

___
2010.04.07

**问题描述**：为什么#include <stdlib.h>后报错“std命名空间中没有名为long labs(long)的函数”？

**问题原因**：因为stdlib.h是C语言的函数，没有命名空间概念。

**解决方法**：改用#include <cstdlib>，long labs(long)在其中的std命名空间内。
+ （顺便说一句，全局命名空间中的labs仍然有效（long ::labs(long)），放心用您的。）

___
2010.04.09

**问题描述**：如何在Visual Studio 2010里面设置全局引用目录(include)和库目录(lib)？

**解决方法**：&quot;View&quot;->&quot;PropertyManager&quot;(没看到蹦出来对话框？没错。它在左边的边栏里)->&quot;Properties&quot;(可以按里面的按钮，也可以在空白处右键)->&quot;ConfigurationProperties&quot;->&quot;VC++ Directories&quot;

___
2010.08.26

**问题描述**：size_t是在哪个头文件中定义的？

**解决方法**：在<cstddef>中定义，该文件定义了若干个标识符：
+ 类型：ptrdiff_t, size_t
+ 宏：NULL, offsetof

___
2010.08.27

**问题描述**：system()函数是在哪个头文件中定义的？

**解决方法**：在<cstdlib>中定义，该文件定义了getenv()和system()函数。

___
2010.08.28

**问题描述**：<stdexcept>头文件中有哪些成员？

**解决方法**：成员如下：

+ domain_error Class
  + The class serves as the base class for all exceptions thrown to report a domain error.
+ invalid_argument Class
  + The class serves as the base class for all exceptions thrown to report an invalid argument.
+ length_error Class
  + The class serves as the base class for all exceptions thrown to report an attempt to generate an object too long to be specified.
+ logic_error Class
  + The class serves as the base class for all exceptions thrown to report errors presumably detectable before the program executes, such as violations of logical preconditions.
+ out_of_range Class
  + The class serves as the base class for all exceptions thrown to report an argument that is out of its valid range.
+ overflow_error Class
  + The class serves as the base class for all exceptions thrown to report an arithmetic overflow.
+ range_error Class
  + The class serves as the base class for all exceptions thrown to report a range error.
+ runtime_error Class
  + The class serves as the base class for all exceptions thrown to report errors presumably detectable only when the program executes.
+ underflow_error Class
  + The class serves as the base class for all exceptions thrown to report an arithmetic underflow.

___
2010.08.31

**问题描述**：在输入流中，如何把读到的一个字节放回到输入缓冲区中？

**解决方法**：istream& istream.putback(char c);

___
2010.08.31

**问题描述**：在输入流中，如何提取缓冲区第一个字符而不造成读取指针变化？

**解决方法**：int istream.peek();

___
2010.08.31

**问题描述**：在输入流中，如何读取一个以回车结尾的行字符串，而不读取回车？

**解决方法**：
+ istream& istream.get( char* buffer, streamsize num );
+ istream& istream.get( char* buffer, streamsizenum, char delim );

___
2010.08.31

**问题描述**：istream.getline(char* buf, streamsize size)最多读取多少字节？

**解决方法**：size-1。

___
2010.09.20

**问题描述**：如何处理double类型的NaN数据？

**解决方法**：

1.#include <limits>
+ using namespace std;
+ bool numeric_limits<double>::has_quiet_NaN
+ double numeric_limits<double>::quiet_NaN
+ bool numeric_limits<double>::has_signaling_NaN
+ double numeric_limits<double>::signaling_NaN

2.\#define NAN (0.0/0.0)
+ \#define IS_NAN(val) ((val)!=(val))

___
2010.09.23

**问题描述**：有没有比较搞笑的模板使用方法？

**解决方法**：有的是。

1. 方法一

   ```cpp
   template <typename T, template<typename> class Comp=greater>
   class Select {
     //没有实际作用，就是演示模板用法
    public:
     T operator () (T* first, T* last) {
       if (first>=last) return T();
       T val = *first++;
       Comp<T> comp;
       // 注意：亮点！
       while (first!=last) {
         if (!comp(val, *first))
           val = *first;
         return val;
       }
     }
   };
   ```

2. 跟刚才那个一样：

   ```cpp
   template <template <typename> class Comp>
   void test(const Comp<int>& c) {
     cout << c(1,2) << endl;
   }

   int main(int argc, char* argv[]){
     less<int> ls;
     greater<int> gr;
     test(ls);
     test(gr);
     return 0;
   }
   ```

___
2010.10.10_20'39'18

**问题描述**：如何使用C++实现通用的“字符串转为其他类型”函数？

**解决方法**：

```cpp
#include <sstream>

template <typename T>
T cast(const char* str) {
  std::stringstream ss;
  ss << str;
  T val;
  ss >> val;
  return val;
}
```

___
2010.10.14_10'39'09

**问题描述**：在C++中能否直接引用C风格头文件？

**解决方法**：在Linux下测试，可以直接引用<math.h>，内部函数位于全局命名空间。

___
2010.10.16_02'39'21

**问题描述**：如何安装boost库？

**解决方法**：
+ 在Windows上，根据文档向导所示：
  1. 启动Visual Studio 命令行，将文件夹cd到boost文件夹根目录
  2. 输入命令bootstrap，回车
  3. 输入命令bjam --prefix=D:\Libraries\boost --build-type=complete install，回车
  4. 耐心等待，卡住了也不要管，直至安装完成。

+ 在Linux上，根据文档向导所示：
  1. 开启一个终端，cd到boost文件夹根目录
  2. 输入命令./bootstrap.sh，回车
  3. 输入命令sudo ./bjam install，回车（需要系统权限）
  4. 耐心等待，直至安装完成

___
2010.10.17_15'39'23

**问题描述**：在Visual Studio 2005中，为什么空项目不能调试？如何解决？

**问题原因**：在空项目中不生成调试文件pdb，所以无法调试。

**解决方法**：
+ 项目->属性->配置属性->链接器->调试->生成调试信息->是
+ 项目->属性->配置属性->C/C++->常规->调试信息格式->C7兼容
+ 项目->属性->配置属性->C/C++->优化->优化->禁用

**参考资料**：http://blog.163.com/cjp19900228@126/blog/static/12016225720105514314590/

___
2010.11.13_18'39'41

**问题描述**：下面的语句，为什么第一行不会报错？为什么第二行会报错？
+ string string, str;
+ string str1;

**问题原因**：
1.  第一行不会报错，是因为局部变量string是在类型名string之后出现的，不会导致类型名解析为变量，不会出错；
2.  str在变量string之后出现，但因为这种声明语法表示str的类型是变量string出现之前的类型名string，所以也不会出错；
3.  str1的声明，试图使用类型名string，但此时变量string已经覆盖了str1所处的作用域中所有其他的与string同名的元素，所以编译器认为str1前面的string是变量名，而不是类型名，因此出现声明错误；

**解决方法**：
1.  尽量不要以类型名命名变量，这样看起来很帅气，实际很危险；
2.  在名称空间已经被污染之后，使用作用域操作符(::)来指明到底要用哪一个名称，如下所示：
  + string string,str;
  + std::string str1;
  + ::string str2;

___
2010.11.14_18'39'04

**问题描述**：使用`new int[10]`能否初始化？

**解决方法**：能，但只能进行默认初始化，语法为：`new int[10]()`;
+ 如果试图用初值初始化（`new int[10](3)`），则编译报错。

___
2010.11.14_21'39'04

**问题描述**：如何在Linux下使用boost库编写程序？

**解决方法**：在Linux下,使用库文件需要在编译选项中指明所使用的库，所以只把库所在文件夹给出是没有用的。
+ makefile中相关配置如下：

```makefile
# BOOST_INC_DIR: where the boost headers (ie. header directory &quot;boost/&quot;) are
BOOST_INC_DIR = /usr/local/include

# BOOST_LIB_DIR: where the boost binary libraries are
BOOST_LIB_DIR = /usr/local/lib

# INC_BOOST: used to add all boost headers to include path
INC_BOOST = -I$(BOOST_INC_DIR)

# LIB_BOOST: used to add all boost libraries to compile path
LIB_BOOST = -L$(BOOST_LIB_DIR) \
-lboost_date_time \
-lboost_filesystem \
-lboost_graph \
-lboost_math_c99 \
-lboost_math_c99f \
-lboost_math_c99l \
-lboost_math_tr1 \
-lboost_math_tr1f \
-lboost_math_tr1l \
-lboost_prg_exec_monitor \
-lboost_program_options \
-lboost_random \
-lboost_regex \
-lboost_serialization \
-lboost_signals \
-lboost_system \
-lboost_test_exec_monitor \
-lboost_thread \
-lboost_unit_test_framework \
-lboost_wave \
-lboost_wserialization \

exec : *.cpp
c++ *.cpp -o a $(INC_BOOST) $(LIB_BOOST)
```

___
2010.11.18_12'39'37

**问题描述**：如何在一个局部作用域内，强制使用一组重载函数中的某一个？

**解决方法**：使用函数的局部声明，根据C++的名字查找和作用域覆盖规则，将屏蔽掉重载函数名。
+ 具体实例如下：

  ```cpp
  void print(char*);
  void print(int);
  void print(double);
  int test() {
    void print(int);
    print(30);  // use void print(int)
    print(2.5);  // use void print(int)
  }
  ```

___
2010.11.18_13'39'29

**问题描述**：在`#include <iostream>`之后，如果需要使用istream或ostream，是否还需要单独`#include <istream>`或`<ostream>`？

**解决方法**：不用。iostream类继承自istream和ostream，即如果我们能看到iostream类，就一定能看到istream类和ostream类，不用单独引用这两个相应的头文件。

___
2010.11.19_16'39'36

**问题描述**：编译器如何确定拷贝构造函数和赋值运算符的选择？

**解决方法**：

```cpp
A a;
A b(a);  // 调用拷贝构造函数，或
A b = a;  // 仍然调用拷贝构造函数
 
A a;
A b;
b = a;  // 这样才能调用赋值运算符
```

___
2010.11.20_20'39'08

**问题描述**：如何编写工具代码，得到一个数组的大小？

**解决方法**：
1. 使用常规方法，sizeof：

   ```cpp
   #define ARRAY_LENGTH(arr) (sizeof(arr)/sizeof(arr[0]))
   ```

2. 使用模板函数：

   ```cpp
   template <typename T, size_t N>
   inline size_t ArrayLength(T (&arr)[N]) {return N;}
   ```

___
2010.11.21_14'39'21

**问题描述**：在位域定义中，可否将同一字节内的不同位赋予不同的访问权限？

**解决方法**：可以，示例如下：

```cpp
class BitField {
 public:
  unsigned char a:2;
 protected:
  unsigned char b:2;
 protected:
  unsigned char c:2;
};
// sizeof(BitField) == 1;
```

___
2010.11.23_19'39'13

**问题描述**：如何使用C++读取一个目录下的所有文件（夹）名？

**解决方法**：使用操作系统目录命令和C++ system()函数，代码如下（Windows为例）：

```cpp
system("dir /B > input.txt");
ifstream fin("input.txt");
cout << fin.rdbuf();
fin.close();
system("del input.txt");
```

___
2010.12.01_09'39'19

**问题描述**：在继承层次中，如果基类定义了重载的虚函数，在派生类中能否只覆盖其中一个重载，而复用其他重载？

**解决方法**：能。只要在派生类中public区块指定using Base::FuncName（没有括号），再重载需要的形式即可。

+ 代码如下：

  ```cpp
  class A {
   public:
    virtual void func() {
      cout << "A::func()" << endl;
    }
    virtual void func(int i) {
      cout << "A::func(" << i << ")" << endl;
    }
  };

  class B1: public A {
   public:
    void func() {
      cout << "B1::func()" << endl;
    }
  };

  class B2: public A {
   public:
    using A::func;
    void func() {
      cout << "B2::func()" << endl;
    }
  };

  int main() {
    A a;
    a.func();
    a.func(1);
    B1 b1;
    b1.func();
    // b1.func(2);  // error
    B2 b2;
    b2.func();
    b2.func(3);
  }
  ```

+ 输出如下：

  ```
  A::func()
  A::func(1)
  B1::func()
  B2::func()
  A::func(3)
  ```

___
2010.12.15

**问题描述**：C++流中，输入（输出）流的提取（插入）操作符接受哪几种类型的函数指针操作数？

**解决方法**：
1. 对`basic_istream<charT,traits>`，包括：

   ```cpp
   basic_istream<charT,traits>& operator >> (
   basic_istream<charT,traits>& (*pf) (basic_istream<charT,traits>&));
   basic_istream<charT,traits>& operator >> (
   basic_ios<charT,traits>& (*pf) (basic_ios<charT,traits>&));
   basic_istream<charT,traits>& operator >> (
   ios_base& (*pf) (ios_base&));
   ```

2. 对`basic_ostream<charT,traits>`，包括：

   ```
   basic_ostream<charT,traits>& operator << (
   basic_ostream<charT,traits>& (*pf) (basic_ostream<charT,traits>&));
   basic_ostream<charT,traits>& operator << (
   basic_ios<charT,traits>& (*pf) (basic_ios<charT,traits>&));
   basic_ostream<charT,traits>& operator << (
   ios_base& (*pf) (ios_base&));
   ```

3.  对于hex、dec、oct等流操作符，都是定义成为以上参数类型的函数，通过函数指针控制流的。

___
2010.12.15

**问题描述**：C++流中，每进行一次输入（输出）操作都清空缓存的选项是什么？

**解决方法**：
+ `unitbuf`，包括：

  ```cpp
  ios_base::unitbuf()
  ios_base& unitbuf(ios_base&)
  ```

+ 也即可以这样使用：

  ```cpp
  cout << setiosflags(ios::unitbuf);
  cout.setf(ios::unitbuf);
  cout << unitbuf;
  ```

___
2010.12.15

**问题描述**：`cout << setw(10)`的工作原理是什么？

**解决方法**：
1. `setw(int)`是`<iomanip>`中的函数，产生一个`smanip`(暂用名)类型对象；
2. `<iomanip>`中针对smanip类型对流的<<和>>运算符进行了重载，使得以下代码等价：
  + `smanip m=setw(10); cout << m;`
  + `cout.width(10);`

   达到这一目的，可选的方式之一就是使用函数指针，如下：

   ```cpp
   smanip m; m.m_func = ios_base::width; m.arg = 10;
   istream& operator >> (istream& is, const smanip& m) {
     (is.*(m.m_func))(m.arg);
   }
   ostream& operator << (ostream& os, const smanip& m) {
     (os.*(m.m_func))(m.arg);
   }
   ```

3. 这样，`cout << setw(10)`的代码就展开为：
   ```cpp
   smanip m; m.m_func=ios_base::width; m.arg=10;
   (cout.*(m.m_func))(m.arg);
   ```
4. 完成。

___
2010.12.15

**问题描述**：ends对输出流做了什么？

**解决方法**：追加了一个空字符：
```cpp
basic_ostream<charT,traits>& ends (basic_ostream<charT,traits>&) {
  os.put(charT());
}
```

___
2010.12.19

**问题描述**：为什么表达式“ch&0x80==0”总是为false？

**问题原因**：运算符“==”的优先级要高于“&”。因此先计算“0x80==0”，其值恒为false，然后计算“ch&false”，也即“ch&0”，当然结果是0了。

**解决方法**：加上小括号，即“(ch&0x80)==0”。

___
2010.12.19

**问题描述**：在基类中定义虚函数fcaller和fcalled，其中fcaller调用了fcalled，二者在派生类中均进行了覆盖。当派生类的fcaller调用基类的fcaller函数时，基类的fcaller却调用了派生类的fcalled，这是怎么回事？

**问题原因**：因为调用的是虚函数，虚函数是根据对象的动态类型进行绑定的。问题情形中，动态类型是派生类，因此调用了派生类的fcalled。

**解决方法**：
1.  如果想要让基类总是调用本类中的虚函数，不发生动态绑定，则在调用时应显式指定类名为作用域，即Base::fcalled();
2. 如果条件允许，只调用非虚成员函数即可；
3.  这个语言特性，可以用来设计模板函数，派生类指定细节，基类定义框架；（参见《设计模式》）
4.  **补充说明**：Java中所有的成员函数都是虚函数，因此也有这个问题，如不注意，将会非常难以解决，后患无穷。

___
2010.12.20

**问题描述**：函数void DoSth(int n=1) {if (n<=1) ... else ...}等价的宏怎么写？

**解决方法**：最难的地方在于默认实参，要求DoSth()也是合法的。论坛牛人给出解答：

```cpp
#define DoSth(n) {if ((n + 0) <= 1) ... else ...}
```

___
2011.01.10

**问题描述**：如何在模板类中定义友元模板函数？为何形如friend ostream& operator << (ostream& os, ClassName& c);的声明加类外定义会导致链接错误？

**问题原因**：因为如上的声明，编译器认为这是一个普通函数，不会为模板生成特化代码；

**解决方法**：

1.

```cpp
template <typename T>
class ClassName {
 public:
  friend ostream& operator << <T> (ostream& os, ClassName<T>& c);
};

template <typename T>
ostream& operator << (ostream& os, ClassName<T>& c) { return os; }
```

2.

```cpp
template <typename T>
class ClassName {
 public:
  template <typename T>
  friend ostream& operator << (ostream& os, ClassName<T>& c);
};

template <typename T>
ostream& operator << (ostream& os, ClassName<T>& c) { return os; }
```

3.

```cpp
template <typenameT>
class ClassName {
 public:
  friend ostream& operator << (ostream&os, ClassName& c) {
   return &nbsp;os;
  }
};
```

___
2011.01.14

**问题描述**：类模板中的静态成员变量应该如何初始化？

**解决方法**：在头文件中，类外初始化。例：

```cpp
template <typename T>
class A {
 public:
  static int num;
  static string str;
};

template <typename T>
int A<T>::num = 1;

template <typename T>
string A<T>::str = "hello";
int main() {
  cout << A<int>::num << " " << A<double>::num << endl;  // 1 1
  cout << A<int>::str << " " << A<double>::str << endl;  // hello hello
}
```

___
TODO(clangpp): continue format.
2011.03.05

**问题描述**：如何取得当前时间的字符串形式？（不要默认的那个ctime）

**解决方法**：
<pre class="prettyprint linenums prettyprinted" style="">string CurrentTime() {
time_t t=time(NULL);  char strt[30]={0};
strftime(strt,sizeof(strt),&quot;%Y.%m.%d %H:%M:%S&quot;,localtime(&t));
return string(strt);}</pre>

___
2011.03.21

**问题描述**：在vs2005中编译boost.python应用程序时，为什么报错：无法打开包括文件:“pyconfig.h”:No such file or directory？

**问题原因**：这个文件是python跨语言开发使用的文件，在“python安装目录/include”中。

**解决方法**：在VS2005中，项目上右击->“属性”->“配置属性”->“C/C++”->“常规”->“附加包含目录”中，将“python安装目录/include”加入进去即可。

___
2011.03.21

**问题描述**：在vs2005中编译boost.python应用程序时，为什么报错：无法打开文件“python26.lib”？

**问题原因**：这个文件是python跨语言开发使用的文件，在“python安装目录/libs”中。

**解决方法**：在VS2005中，项目上右击->“属性”->“配置属性”->“链接器”->“常规”->“附加库目录”中，将“python安装目录/libs”加入进去即可。

___
2011.03.21

**问题描述**：在VS2005中，如何生成动态链接库文件？

**解决方法**：新建项目->Win32->Win32项目->给项目命名->弹出向导->下一步->应用程序类型选择“DLL”->附加选项选择“空项目”->齐活。

___
2011.03.27

**问题描述**：定义operator=成员函数为如下形式（模板成员函数）时，在客户代码中调用operator=，没有编译错误，但为什么没有执行该函数？
+ 函数定义形式：
+ template <T>
+ class Foo
+ {
+ public:
+ template <U>
+ Foo& operator = (const Foo<U>& rhs);
+ };

**问题原因**：模板函数特点是，如果不调用，就不会编译；如果有特殊的，就不用通用的。
+ 编译器编译Foo时，检查没有自定义的Foo<T>operator = (constFoo<T>&)，就启动默认机制，生成了默认的浅拷贝赋值操作符函数。
+ 因此在客户代码中，编译器根据模板“有特殊的就不用一般的”原则，实际调用的是浅拷贝的赋值操作符函数，自定义的这个函数没有被调用。
+ 这也就解释了没有编译错误的原因。

**解决方法**：老老实实地写一个接受严格相同类型参数的赋值操作符函数，再写其他的通用赋值操作符函数。如下：
+ template <T>
+ class Foo
+ {
+ public:
+ Foo& operator = (const Foo& rhs);

+ template <U>
+ Foo& operator = (const Foo<U>& rhs);
+ };

___
2011.04.16

**问题描述**：为什么数字输入流中有逗号时，输入流会读取失败？

**问题原因**：不知道。猜想可能是因为逗号有可能是千位区分标志，导致流读取也不是，不读也不是，只好报错。//tbc

**解决方法**：借用stringstream，代码如下：
+ string stuff;
+ getline(in,stuff,&#39;,&#39;);
+ unsigned int val=0;
+ stringstream(stuff) >> val;

___
2011.04.20

**问题描述**：在模板类声明中声明operator<<的流重载函数，在类外进行定义，为什么报链接错误？（operator>>流输出函数也有同样问题）

**问题原因**：在模板类中声明operator <<时，如果没有template <typenameU>，编译器会认为这是个非模板函数，不会到类外找同名的模板函数进行链接，因此报链接错误。

**解决方法**：
+ 方法一：将operator <<的函数体放到类声明中。
+ 方法二：在类声明中的函数头加上template <typenameU>，如下所示：
+ template <typename T>
+ class Class
+ {
+ public:
+ template <typename U>
+ friend std::ostream& operator <<(std::ostream& os, const Class<U>& obj);
+ };
+ （对operator >>原因和**解决方法**相同）

___
2011.04.28

**问题描述**：为什么普通函数在头文件里实现，在多个源文件中引用的时候，链接时报错“重定义的函数”？

**问题原因**：暂时还不知道。

**解决方法**：对这类函数，使用inline进行声明，即可绕过这个问题。

___
2011.04.30

**问题描述**：在非fstream的标准流中，能否使用seekg、seekp等成员函数？

**问题原因**：能，这些是在basic_istream和basic_ostream中定义的。

___
2011.05.01

**问题描述**：fstream不支持中文路径怎么办？

**问题原因**：不知道。

**解决方法**：
&nbsp; &nbsp; &nbsp;ofstream writefile;
+  string filename=(&quot;d:\我的文档\测试.txt&quot;);
&nbsp; &nbsp; &nbsp;locale loc = locale::global(locale(&quot;&quot;));//要打开的文件路径含中文，设置全局locale为本地环境
&nbsp; &nbsp; &nbsp;writefile.open(filename.c_str(),ios::out); //打开文件
&nbsp; &nbsp; &nbsp;locale::global(loc);//恢复全局locale

___
2011.05.19

**问题描述**：#pragma warning(disable : 4996)是什么意思？

**问题原因**：
+ 1. #pragmawarning(disable:n)是说编译的时候忽略编号为n的编译警告；
+ 2. 警告C4996：编译器遇到了标记有 deprecated的函数。 在未来版本中可能不再支持此函数；

___
2011.05.26

**问题描述**：可否使用函数内的类完成匿名函数功能？

**解决方法**：
+ 1.函数内可以进行类声明，定义仿函数，使作用域局部化到函数内部；
+ 2. 无法定义匿名类，每个类仍需指定名称；
+ 3. 类声明时直接定义匿名对象貌似不行，以后可再试；

___
2011.07.06

**问题描述**：delete 0;是否可行？

**问题原因**：不知道。

**解决方法**：在VS2005和g++4.4上测试，均可以，代码如下：
+ int* p=0;
+ delete p;

___
2011.07.12

**问题描述**：auto_ptr和unique_ptr有什么区别？

**解决方法**：
+ 1. unique_ptr不能拷贝，auto_ptr可以拷贝；
+ 2. unique_ptr能自定义指针释放函数，auto_ptr不能；
+ 3. unique_ptr能操作动态分配数组，auto_ptr不能；

附加说明：
+ unique_ptr cannot be copied while auto_ptr can.
+ unique_ptr provide user defined delete oprationwhile auto_ptr can&#39;t.
+ unique_ptr can manage array while auto_ptrcan&#39;t.

___
2011.07.12

**问题描述**：unique_ptr, auto_ptr与scoped_ptr三者有什么不同？

**解决方法**：
+ auto_ptr+ 具有拷贝语义，具有移动语义；
+ unique_ptr+ 没有拷贝语义，具有移动语义；
+ scoped_ptr+ 没有拷贝语义，没有移动语义；
+ 显然，任何时候，auto_ptr都是一个糟糕的选择；
+ 当你明确需要移动语义的时候，使用unique_ptr；
+ 当你明确禁止移动语义的时候，使用scoped_ptr；
+ 以上所有智能指针都具有交换语义（p.swap(q)）,如需禁止该语义，使用const..._ptr即可；

附加说明：
+ A auto_ptr is a pointer with copy and with movesemantics and ownership (=auto-delete).&nbsp;
+ A unique_ptr is a auto_ptr without copy but withmove semantics.&nbsp;
+ A scoped_ptr is a auto_ptr without copy and withoutmove semantics.

+ auto_ptrs are allways a bad choice – that isobvious.
+ Whenever you want to explicitely have movesemantics, use a unique_ptr.
+ Whenever you want to explicitely disallow movesemantics, use a scoped_ptr.
+ All pointers allow swap semantics, like p.swap(q).To disallow those, use any const …_ptr.

___
2011.07.12

**问题描述**：C++的四种编程范式是什么？

**解决方法**：
+ 1.按照我最近的理解，它们分别是：面向过程编程，使用对象编程，面向对象编程，泛型编程；
+ 2.《深入探索C++对象模型》中，提出C++支持三种编程范式：面向过程编程，抽象数据类型编程（ADT，也即基于对象编程，Object-Based），面向对象编程。加上后来出现的泛型编程，总共是四种范式；

___
2011.08.24

**问题描述**：如何用栈模拟递归实现深度优先搜索算法？

**解决方法**：
+ 1.模拟函数调用栈，在栈的每一个元素中，记录其子结点的访问顺序及状态。
+ 退栈压栈时判断状态，决定访问下一个子结点，还是当前结点访问退栈。

+ 2.不模拟函数调用栈，在栈中加入冗余占位符，兄弟结点按访问逆序同时入栈。
+ 访问时判断冗余占位符，决定是继续压栈子结点，还是当前结点访问退栈。
+ 代码如下：

+ // 以栈实现深度优先搜索算法
+ //原来我用栈实现深度优先搜索的时候，必须要记录状态，
+ //+ 用以表示一次退栈之后下一个压栈的兄弟结点的次序。
+ //如下方法的优点在于，每一次退栈之后，自然地转到下一个兄弟结点的压栈操作。
+ //+ 从而充分利用了压栈的先后顺序，表征了兄弟结点间的顺序信息，
+ //+ 同时自然记录了父结点的退栈顺序。
+ //原来我用的记录顺序信息的方法，完整地模拟了函数调用栈，
+ //+ 栈深度d与对应递归函数调用栈深度df完全相同。
+ //如下方法每次压栈都将栈顶结点的所有子节点一并压栈，设每个节点子节点数为c，
+ //+ 栈深度d与对应递归函数调用栈深度df满足：d=df*(c+1)，数量级仍相同。
+ //原来的栈数据结构中，由栈底到栈顶的所有结点，构成当前决策路径。
+ //如下方法的栈数据结构中，由栈底到栈顶所有的NULL占位符结点，构成当前决策路径。
+ void dfs(node* root)
+ {
+ stack<node*> s;
+ if (NULL!=root) &nbsp;// 只对非空树进行遍历
+ s.push(root);
+ while (!s.empty()) &nbsp;// 所有结点访问结束后栈空
+ {
+ if (NULL==s.top()) //栈顶元素的所有子结点（如果有的话）已访问完毕
+ {
+ // 访问栈顶结点，并将其退栈
+ s.pop(); &nbsp;//占位符退栈，逻辑上表示将栈顶元素退出决策路径
+ cout << s.top()->value << endl;
+ s.pop();
+ }
+ else &nbsp;// 还未访问栈顶元素的子结点
+ {
+ // 将栈顶结点的所有子结点压栈
+ node* curr = s.top();
+ s.push(NULL); &nbsp;//占位符压栈，逻辑上表示将栈顶结点加入决策路径
+ if (curr->right)
+ s.push(curr->right);
+ if (curr->left)
+ s.push(curr->left);
+ }
+ }
}

___
2011.08.25

**问题描述**：如何使用同样的逻辑重载operator << (T)和operator <<(ostream& (*pf) (ostream&))？

问题补充：只写一个operator << (T val)，当使用 obj << endl时会报错：没有接受该类型参数的重载；

**解决方法**：
<pre class="prettyprint linenums prettyprinted" style="">template <typename
T>Logger& operator << (const T& value) {  for
(SinkContainer::iterator sink=sinks_.begin();      sink!=sinks_.end(); ++sink) {
if (level_>=sink->second)      (*sink->first) << value;  }
return *this;}Logger& operator << (std::ostream& (*pf)
(std::ostream&)) {  return operator << <std::ostream& (*)
(std::ostream&)>(pf);}</pre>
+ 同理，需要重载的其他函数指针类型参数，可以定义如下：
<pre class="prettyprint linenums prettyprinted" style="">Logger& operator
<< (std::ios& (*pf) (std::ios&)) {  return operator <<
<std::ios& (*) (std::ios&)>(pf);}Logger& operator <<
(std::ios_base& (*pf) (std::ios_base&)) {  return operator <<
<std::ios_base& (*) (std::ios_base&)>(pf);}</pre>

___
2011.08.26

**问题描述**：C++里有什么缺德的语法陷阱吗？

**解决方法**：太多了，有专门的书来写。这里列举几个最变态的：
+ 1.最变态：在行注释的最后，如果有一个反斜线(\)，那这个反斜线会被当作续行符，下一行代码就莫名奇妙地成了注释了。
+ 追加说明：在VS2010中，这个问题依然存在，但是编译器会给出警告。这还让人欣慰点儿。
+ main.cpp(5): warning C4010: single-line commentcontains line-continuation character

+ 2. 可以忍受：如果有如下代码：
+ float result = num/*pInt;
+ ....
+ /* &nbsp;some comments */
+ -x<10 ? f(result):f(-result);

+ 本意是float result = num / (*pInt);
+ 结果编译器认成了 float result = num-x<10 ?f(result):f(-result);

+ 初看惊讶，再一想还是怪自己，编译器按最长标识符匹配原则解析，人家没错。

+ 3.C++11已经改了：牵套模板类型定义的时候，如果两个连续的右尖括号(>>)出现，会被解释成右移运算符。这还不算，还会有一大片编译器错误信息，但没有一句告诉我是这个问题。
+ 在C++11标准中，已经规定，将连续右尖括号解析为模板参数结束符。

___
2011.09.02

**问题描述**：在GOOGLE C++编程规范中，源文件扩展名使用什么？

**解决方法**：在Name这一章，File Names这一节中，有如下说明：
&nbsp; &nbsp; C++ files should end in .cc and header files should end in .h.
&nbsp; &nbsp; 所以应该使用.cc

___
2011.09.02

**问题描述**：在C/C++中，有没有文件重命名的库？

**解决方法**：在标准C库<stdio.h>中，有文件重命名库。其函数原型如下：
&nbsp; &nbsp; Syntax:
&nbsp; &nbsp; &nbsp; #include <stdio.h>
&nbsp; &nbsp; &nbsp; int rename( const char *oldfname, const char *newfname);

&nbsp; &nbsp; The function rename() changes the name of the file oldfname tonewfname. The return value of rename() is zero upon success, non-zero onerror.&nbsp;

**补充说明**：与此功能相关还有几个库函数，同样在<stdio.h>中：

&nbsp; &nbsp; 1. 删除文件：int remove( const char *fname );
&nbsp; &nbsp; &nbsp; &nbsp; Syntax:
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; #include <stdio.h>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; int remove( const char *fname );

&nbsp; &nbsp; &nbsp; &nbsp; The remove() function erases the file specifiedby fname. The return value of remove() is zero upon success, and non-zero ifthere is an error.&nbsp;

&nbsp; &nbsp; 2. 临时文件：FILE *tmpfile( void );
&nbsp; &nbsp; &nbsp; &nbsp; Syntax:
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; #include <stdio.h>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; FILE *tmpfile( void );

&nbsp; &nbsp; &nbsp; &nbsp; The function tempfile() opens a temporary filewith an unique filename and returns a pointer to that file. If there is anerror, null is returned.&nbsp;

&nbsp; &nbsp; 3. 临时文件名：char *tmpnam( char *name );
&nbsp; &nbsp; &nbsp; &nbsp; Syntax:
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; #include <stdio.h>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; char *tmpnam( char *name );
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;

&nbsp; &nbsp; &nbsp; &nbsp; The tmpnam() function creates an unique filenameand stores it in name. tmpnam() can be called up to TMP_MAX times.&nbsp;

___
2011.09.02

**问题描述**：C语言文件打开模式都有哪些，哪些会自动创建新文件？

**解决方法**：fopen() Description
&nbsp; &nbsp; The fopen function opens the file whose name is the stingpointed to by filename. and
&nbsp; &nbsp; associates a stream with it.
&nbsp; &nbsp; The argument mode points to a sting beginning with one of thefollowing sequences:115
&nbsp; &nbsp; &nbsp; &nbsp; r &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; open textfile for reading
&nbsp; &nbsp; &nbsp; &nbsp; w &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; truncate tozero length or create text file for writing
&nbsp; &nbsp; &nbsp; &nbsp; a &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; append;open or create text file for writing at end-of-file
&nbsp; &nbsp; &nbsp; &nbsp; rb &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;open binaryfile for reading
&nbsp; &nbsp; &nbsp; &nbsp; wb &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;truncate tozero length or create binary file for writing
&nbsp; &nbsp; &nbsp; &nbsp; ab &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;append;open or create binary file for writing at end-of-file
&nbsp; &nbsp; &nbsp; &nbsp; r+ &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;open textfile for update (reading and writing)
&nbsp; &nbsp; &nbsp; &nbsp; w+ &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;truncate tozero length or create text file for update
&nbsp; &nbsp; &nbsp; &nbsp; a+ &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;append;open a create text file for update, writing at end-of-file
&nbsp; &nbsp; &nbsp; &nbsp; r+b or rb+ &nbsp;open binary file for update(reading and writing)
&nbsp; &nbsp; &nbsp; &nbsp; r+b or wb+ &nbsp;truncate to zero length orcreate binary file for update
&nbsp; &nbsp; &nbsp; &nbsp; a+b or ab+ &nbsp;append; open or create binaryfile for update, writing at end-of-file
&nbsp; &nbsp; Opening a file with read mode (&#39; r&#39; as the firstcharacter in the mode argument) fails if the
&nbsp; &nbsp; file does not exist or cannot be read.
&nbsp; &nbsp; Opening a file with append mode (&#39; a&#39; as the firstcharacter in the mode argument) causes all
&nbsp; &nbsp; subsequent writes to the file to be forced to the then currentend-of-file, regardless of intervening
&nbsp; &nbsp; calls to the fseek function. In some implementations, openinga binary file with append mode
&nbsp; &nbsp; (&#39;b&#39; as the second or third character in the abovelist of mode argument values) may initially
&nbsp; &nbsp; position the file position indicator for the stream beyond thelast data written, because of null
&nbsp; &nbsp; character padding.
&nbsp; &nbsp; When a file is opened with update mode (&#39; +&#39; as thesecond or third character in the above list
&nbsp; &nbsp; of mode argument values), both input and output may beperformed on the associated stream.
&nbsp; &nbsp; However, output may not be directly followed by input withoutan intervening call to the f f lush
&nbsp; &nbsp; function or to a file positioning function (fseek, fsetpos, orrewind), and input may not
&nbsp; &nbsp; be directly followed by output without an intervening call toa file positioning function, unless
&nbsp; &nbsp; the input operation encounters end-of-file. Opening (orcreating) a text file with update mode may
&nbsp; &nbsp; instead open (or create) a binary stream in someimplementations.
&nbsp; &nbsp; When opened, a stream is fully buffered if and only if it canbe determined not to refer to an
&nbsp; &nbsp; interactive device. The error and end-of-file indicators forthe stream are cleared.

___
2011.09.02

**问题描述**：在C++的ostream中，如果seekp()到一个不存在的位置，会发生什么事情？

**解决方法**：
&nbsp; &nbsp; 1.在ofstream中，如果seekp到一个比较大的位置，然后输出数据，在vs2010中测试，结果是该位置之前填0，数据在该位置开始输出；
&nbsp; &nbsp; 2.在cout中，如果seekp到一个比较大的位置，fail()就变成了true，再输出数据直接没有显示；
&nbsp; &nbsp; 3. 其他情况及此中规定，还没找到资料；// TBD.

___
2011.09.02

**问题描述**：vector<bool>中的pointer是怎么实现的？

**解决方法**：
&nbsp; &nbsp; template <>
&nbsp; &nbsp; class vector<bool> {
&nbsp; &nbsp; public:
&nbsp; &nbsp; &nbsp; &nbsp; class reference;
&nbsp; &nbsp; &nbsp; &nbsp; class iterator {
&nbsp; &nbsp; &nbsp; &nbsp; public:
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; reference operator * () const;
&nbsp; &nbsp; &nbsp; &nbsp; };
&nbsp; &nbsp; &nbsp; &nbsp; typedef iterator pointer;
&nbsp; &nbsp; };

___
2011.10.12

**问题描述**：C++不支持函数模板偏特化，如何间接实现之？

**问题原因**：标准中不支持，就是不支持，没办法；但这难不倒我，我可以间接实现之；

**解决方法**：示例如下：
&nbsp; &nbsp; 欲实现：

&nbsp; &nbsp; &nbsp; &nbsp; template <typename ToType, typenameFromType>
&nbsp; &nbsp; &nbsp; &nbsp; inline ToType to(const FromType& from) {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; std::stringstream ss;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ss << from;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ToType result = ToType();
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ss >> result;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return result;
&nbsp; &nbsp; &nbsp; &nbsp; }

&nbsp; &nbsp; &nbsp; &nbsp; // error: c++ don&#39;t support functiontemplate partial specification
&nbsp; &nbsp; &nbsp; &nbsp; template <typename FromType>
&nbsp; &nbsp; &nbsp; &nbsp; inline std::string to<std::string>(constFromType& from) {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; std::stringstream ss;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ss << from;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return ss.str();
&nbsp; &nbsp; &nbsp; &nbsp; }

&nbsp; &nbsp; 可以使用普通模板函数，内嵌一个有全特化版本的模板函数即可：

&nbsp; &nbsp; &nbsp; &nbsp; template <typename ToType>
&nbsp; &nbsp; &nbsp; &nbsp; inline ToType to(std::stringstream& ss) {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ToType result = ToType();
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ss >> result;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return result;
&nbsp; &nbsp; &nbsp; &nbsp; }

&nbsp; &nbsp; &nbsp; &nbsp; template <>
&nbsp; &nbsp; &nbsp; &nbsp; inline std::stringto<std::string>(std::stringstream& ss) {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return ss.str();
&nbsp; &nbsp; &nbsp; &nbsp; }

&nbsp; &nbsp; &nbsp; &nbsp; template <typename ToType, typenameFromType>
&nbsp; &nbsp; &nbsp; &nbsp; inline ToType to(const FromType& from) {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; std::stringstream ss;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ss << from;
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return to<ToType>(ss);&nbsp;// bingo!
&nbsp; &nbsp; &nbsp; &nbsp; }

**补充说明**：当然，这种方法是有局限的，只适用在那些只有一部分逻辑需要特化的函数中。需要逻辑完全不同的偏特化函数，这种方法就不行了。期待着更好的解决方案；

___
2011.10.17

**问题描述**：关键字__func__是什么来头？

**解决方法**：
&nbsp; &nbsp; 1.__func__是C99引入的新关键字，是在每一个函数中由编译器定义的字符串常量：
&nbsp; &nbsp; &nbsp; &nbsp; static char __fun__[] =&quot;function-name&quot;;
&nbsp; &nbsp; &nbsp; &nbsp; 在C中为不包含返回类型和参数类型的函数名字符串；
&nbsp; &nbsp; 2.__func__在C++98和C++03中都不支持，但各编译器都有类似的功能：
&nbsp; &nbsp; &nbsp; &nbsp; VS2005中，使用__FUNCTION__支持之；
&nbsp; &nbsp; &nbsp; &nbsp;g++中，提供C兼容的__func__支持，也提供__PRETTY_FUNCTION__为C++支持更丰富的打印格式；
&nbsp; &nbsp; 3.__func__在C++11中得到了支持，但与C不同的是，C++11规定__func__的值由实现决定，只要便于表现出函数的信息就好；

___
2011.10.17

**问题描述**：assert宏以哪个调试宏为编译开关？

**解决方法**：NDEBUG

**补充说明**：如果要让assert编译为空，则需要在#include<cassert>之前定义NDEBUG。这是因为assert宏的定义类似如下形式：

&nbsp; &nbsp; // cassert
&nbsp; &nbsp; #ifdef NDEBUG
&nbsp; &nbsp; # &nbsp;define assert(ignore) ((void)0)
&nbsp; &nbsp; #else
&nbsp; &nbsp; # &nbsp;define assert(expression) ASSERT_FUNCTION(expression)
&nbsp; &nbsp; #endif &nbsp;// NDEBUG

&nbsp; &nbsp; 所以比较稳妥的使用方式是，在编译命令选项中，加入-DNDEBUG。

___
2011.10.23

**问题描述**：main函数的标准形式是什么？

**解决方法**：int main() 或 int main(int argc, char* argv[])；

**补充说明**：argv[argc] == 0；

___
2011.10.26

**问题描述**：能否使用一个区间初始化set或map？

**解决方法**：能，set和map都有一个构造函数，接受一对InputIterator；

**补充说明**：unordered_set和unordered_map也行；

___
2011.10.26

**问题描述**：set和map有没有assign(InputIterator, InputIterator)接口？

**解决方法**：没有，但是它们都提供了insert(InputIterator,InputIterator)。所以可以先clear()，再insert(first, last)；

**补充说明**：unordered_set和unordered_map也一样；

___
2011.10.28

**问题描述**：标准迭代器都有默认构造函数吗？

**解决方法**：根据ISO-IEC14882-1998，InputIterator和OutputIterator可以没有默认构造函数，ForwardIterator,BidirectionalIterator和RandomAccessIterator必须要有默认构造函数；

**补充说明**：所有类型的迭代器，都有拷贝构造函数和赋值运算符，都有前置/后置++运算符，都有解引用(*)操作符。输出迭代器可以没有->操作符，输入迭代器可以没有*iter=value操作；

___
2011.11.28

**问题描述**：子类的友元（友元类、友元函数）能否访问父类的私有成员？

**解决方法**：不能。

**补充说明**：子类的友元可以访问父类的保护成员。

___
2011.10.28

**问题描述**：模板函数支持默认模板参数吗？

**解决方法**：不支持。

**补充说明**：只有模板类支持默认模板参数。

___
2011.11.01

**问题描述**：C++编译预处理中有defined关键字吗？

**解决方法**：有，也没有。defined 不是C++关键字，只是在编译预处理语句中有意义：

&nbsp; &nbsp; 在 #if defined(ABC) 或 #if defined ABC中，如果宏ABC被定义过了，那么defined(ABC) 或 definedABC在此处的值为1，该预处理语句判断为真。

&nbsp; &nbsp; 在程序运行时，defined 不是关键字，可以随意使用。

**补充说明**：对define, elif,endif等编译预处理命令，在前面没有#的时候，也不是关键字，可以被随意使用。

___
2011.11.04

**问题描述**：C++中类的拷贝构造函数有什么条件？

**解决方法**：对于类X：
&nbsp; &nbsp; 1. 第一个参数必须是X&, const X&, volatile X&,const volatile X&其中之一；
&nbsp; &nbsp; 2. 没有其他参数，或者其他参数均有默认值；

**补充说明**：参考《ISO-IEC-14882-1998》 12.1 和12.8。

___
2011.11.30

**问题描述**：C++ string类型有reserve(size_type)函数吗？

**解决方法**：有；

**补充说明**：
&nbsp; &nbsp; 1. 与reserve相对应，也有size_typecapacity();函数，跟vector的意义一样，表示不新申请空间的情况下，能盛下多少个字符；
&nbsp; &nbsp; 2. 有push_back(const value_type&), 但是没有pop_back(),push_front(const value_type&), pop_front()；
&nbsp; &nbsp; 3. 有append系列函数，都返回增长之后的字符串自身引用；
&nbsp; &nbsp; &nbsp; &nbsp; #include <string>
&nbsp; &nbsp; &nbsp; &nbsp; string& append( const string& str );
&nbsp; &nbsp; &nbsp; &nbsp; string& append( const char* str );
&nbsp; &nbsp; &nbsp; &nbsp; string& append( const string& str,size_type index, size_type len );
&nbsp; &nbsp; &nbsp; &nbsp; string& append( const char* str, size_typenum );
&nbsp; &nbsp; &nbsp; &nbsp; string& append( size_type num, char ch );
&nbsp; &nbsp; &nbsp; &nbsp; string& append( input_iterator start,input_iterator end );
&nbsp; &nbsp; 4. 有const char* data()函数，返回首个字符的地址；
&nbsp; &nbsp; 5. 有int compare(const string& rhs)函数，跟strcmp类似；
&nbsp; &nbsp; 6.有replace系列函数，完成指定位置处的指定数量字符替换；比较厉害的是，待替换字符个数与替换字符个数可以不一样；
&nbsp; &nbsp; &nbsp; &nbsp; #include <string>
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( size_type index, size_typenum, const string& str );
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( size_type index1, size_typenum1,
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; const string&str, size_type index2, size_type num2 );
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( size_type index, size_typenum, const char* str );
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( size_type index, size_typenum1, const char* str, size_type num2 );
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( size_type index, size_typenum1, size_type num2, char ch );
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( iterator start, iteratorend, const string& str );
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( iterator start, iteratorend, const char* str );
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( iterator start, iteratorend, const char* str, size_type num );
&nbsp; &nbsp; &nbsp; &nbsp; string& replace( iterator start, iteratorend, size_type num, char ch );
&nbsp; &nbsp; 7.有copy函数，从当前字符串中拷贝指定数量的字符到一个字符数组中；
&nbsp; &nbsp; &nbsp; &nbsp; #include <string>
&nbsp; &nbsp; &nbsp; &nbsp; size_type copy( char* str, size_type num,size_type index = 0 ); &nbsp; &nbsp;
&nbsp; &nbsp; 8. 有size_type length() const { return size();}，字符串的长度概念，想用就用吧；

___
2011.12.13

**问题描述**：类模板成员函数是否能够偏特化？

**问题原因**：类（普通类/模板类/模板类偏特化/模板类全特化） --模板成员函数（全特化/偏特化）
&nbsp; &nbsp; 0. 所有模板函数（普通函数/类成员函数）都不支持偏特化；
&nbsp; &nbsp; 1. 普通类模板成员函数支持全特化；
&nbsp; &nbsp; 2. 模板类模板成员函数不支持全特化；
&nbsp; &nbsp; 3. 全特化模板类的模板成员函数支持全特化；（理解为普通类）
&nbsp; &nbsp; 4. 偏特化模板类的模板成员函数不支持全特化；

___
2011.12.13
&nbsp;
**问题描述**：类的拷贝构造函数参数other是常引用时，other的成员变为常类型，成员赋值时为什么不报错？
&nbsp;
问题补充：示例代码：
&nbsp; &nbsp; struct TestConst {&nbsp;
&nbsp; &nbsp; &nbsp; &nbsp; int a;
&nbsp; &nbsp; &nbsp; &nbsp; int* p;
&nbsp; &nbsp; &nbsp; &nbsp; TestConst(int aa=0, int* pp=NULL): a(aa), p(pp){}
&nbsp; &nbsp; &nbsp; &nbsp; TestConst(const TestConst& other):a(other.a), p(other.p) {}
&nbsp; &nbsp; };
&nbsp; &nbsp; &nbsp;
&nbsp; &nbsp; int main() {
&nbsp; &nbsp; &nbsp; &nbsp; TestConst t1;
&nbsp; &nbsp; &nbsp; &nbsp; TestConst t2(t1); // 为什么不报错？
&nbsp; &nbsp; &nbsp; &nbsp; return 0;
&nbsp; &nbsp; }
&nbsp;
**问题原因**：在这种情况下，other的成员类型都视为常量。而常量可以用来初始化对应类型的变量，故不会报错。对于指针类型，其对应常量类型是指针常量，而不是常指针，使用指针常量初始化指针变量完全合法。
&nbsp;
答案补充：代码说明：
&nbsp; &nbsp; struct TestConst {&nbsp;
&nbsp; &nbsp; &nbsp; &nbsp; int a;
&nbsp; &nbsp; &nbsp; &nbsp; int* p;
&nbsp; &nbsp; &nbsp; &nbsp; TestConst(int aa=0, int* pp=NULL): a(aa), p(pp){}
&nbsp; &nbsp; &nbsp; &nbsp; TestConst(const TestConst& other):
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; a(other.a), &nbsp;// int = (constint)
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; p(other.p) &nbsp;// int* = (int*const)
&nbsp; &nbsp; &nbsp; &nbsp; {}
&nbsp; &nbsp; };
&nbsp;
&nbsp; &nbsp; int main() {
&nbsp; &nbsp; &nbsp; &nbsp; TestConst t1;
&nbsp; &nbsp; &nbsp; &nbsp; TestConst t2(t1);
&nbsp; &nbsp; &nbsp; &nbsp; return 0;
&nbsp; &nbsp; }

___
2011.12.16

**问题描述**：引用指向的临时变量，具有什么样的生存期？

**解决方法**：具有与引用相同的生存期。标准中有说明《ISO-IEC-14882-2003》 12.2.4,12.2.5：

12.2.4
There are two contexts in which temporaries are destroyed at a differentpoint than the end of the fullexpression.&nbsp;
The first context is when an expression appears as an initializer for adeclarator defining an
object. In that context, the temporary that holds the result of theexpression shall persist until the object’s
initialization is complete. The object is initialized from a copy of thetemporary; during this copying, an
implementation can call the copy constructor many times; the temporary isdestroyed after it has been
copied, before or when the initialization completes. If many temporaries arecreated by the evaluation of
the initializer, the temporaries are destroyed in reverse order of thecompletion of their construction.

12.2.5
The second context is when a reference is bound to a temporary. Thetemporary to which the reference is&nbsp;
bound or the temporary that is the complete object to a subobject of whichthe temporary is bound persists
for the lifetime of the reference except as specified below. A temporarybound to a reference member in a
constructor’s ctor-initializer (12.6.2) persists until the constructorexits. A temporary bound to a reference
parameter in a function call (5.2.2) persists until the completion of thefull expression containing the call.
A temporary bound to the returned value in a function return statement(6.6.3) persists until the function
exits. In all these cases, the temporaries created during the evaluation ofthe expression initializing the reference,
except the temporary to which the reference is bound, are destroyed at theend of the full-expression
in which they are created and in the reverse order of the completion oftheir construction. If the lifetime of
two or more temporaries to which references are bound ends at the samepoint, these temporaries are
destroyed at that point in the reverse order of the completion of theirconstruction. In addition, the
destruction of temporaries bound to references shall take into account theordering of destruction of objects
with static or automatic storage duration (3.7.1, 3.7.2); that is, if obj1is an object with static or automatic
storage duration created before the temporary is created, the temporaryshall be destroyed before obj1 is
destroyed; if obj2 is an object with static or automatic storage durationcreated after the temporary is created,
the temporary shall be destroyed after obj2 is destroyed. [Example:
&nbsp; &nbsp; class C {
&nbsp; &nbsp; &nbsp; &nbsp; // ...
&nbsp; &nbsp; public:
&nbsp; &nbsp; &nbsp; &nbsp; C();
&nbsp; &nbsp; &nbsp; &nbsp; C(int);
&nbsp; &nbsp; &nbsp; &nbsp; friend C operator+(const C&, const C&);
&nbsp; &nbsp; &nbsp; &nbsp; ~C();
&nbsp; &nbsp; };
&nbsp; &nbsp; C obj1;
&nbsp; &nbsp; const C& cr = C(16)+C(23);
&nbsp; &nbsp; C obj2;
the expression C(16)+C(23) creates three temporaries. A first temporary T1to hold the result of the
expression C(16), a second temporary T2 to hold the result of the expressionC(23), and a third temporary
T3 to hold the result of the addition of these two expressions. Thetemporary T3 is then bound to the
reference cr. It is unspecified whether T1 or T2 is created first. On animplementation where T1 is created
before T2, it is guaranteed that T2 is destroyed before T1. The temporariesT1 and T2 are bound to
the reference parameters of operator+; these temporaries are destroyed atthe end of the full expression
containing the call to operator+. The temporary T3 bound to the reference cris destroyed at the end of
cr’s lifetime, that is, at the end of the program. In addition, the order inwhich T3 is destroyed takes into
account the destruction order of other objects with static storage duration.That is, because obj1 is constructed
before T3, and T3 is constructed before obj2, it is guaranteed that obj2 isdestroyed before T3,
and that T3 is destroyed before obj1. ]

**补充说明**：

代码：
&nbsp; &nbsp; class TestTempObject {
&nbsp; &nbsp; public:
&nbsp; &nbsp; &nbsp; &nbsp; TestTempObject() {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cout <<&quot;TestTempObject::TestTempObject()&quot; << endl;
&nbsp; &nbsp; &nbsp; &nbsp; }
&nbsp; &nbsp; &nbsp; &nbsp; TestTempObject(const TestTempObject& other){
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cout <<&quot;TestTempObject::TestTempObject(const TestTempObject&)&quot; <<endl;
&nbsp; &nbsp; &nbsp; &nbsp; }
&nbsp; &nbsp; &nbsp; &nbsp; ~TestTempObject() {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cout <<&quot;TestTempObject::~TestTempObject()&quot; << endl;
&nbsp; &nbsp; &nbsp; &nbsp; }
&nbsp; &nbsp; &nbsp; &nbsp; static TestTempObject Create() {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return TestTempObject();
&nbsp; &nbsp; &nbsp; &nbsp; }
&nbsp; &nbsp; };
&nbsp; &nbsp; int main() {
&nbsp; &nbsp; &nbsp; &nbsp; cout << &quot;before creating&quot;<< endl;
&nbsp; &nbsp; &nbsp; &nbsp; TestTempObject& r =TestTempObject::Create();
&nbsp; &nbsp; &nbsp; &nbsp; cout << &quot;after creating&quot;<< endl;
&nbsp; &nbsp; &nbsp; &nbsp; return 0;
&nbsp; &nbsp; }

运行结果：
&nbsp; &nbsp; before creating&nbsp;
&nbsp; &nbsp; TestTempObject::TestTempObject()
&nbsp; &nbsp; after creating
&nbsp; &nbsp; TestTempObject::~TestTempObject()

___
2011.12.21
&nbsp;
**问题描述**：对于一个类类型的typedef，如何调用其构造和析构函数？
&nbsp;
**解决方法**：既可以用原类型名做函数名，又可以用新类型名作函数名；
&nbsp;
**补充说明**：代码：
&nbsp; &nbsp; typedef TestTempObject T1;
&nbsp; &nbsp; T1 t2 = TestTempObject();
&nbsp; &nbsp; t2.~TestTempObject();
&nbsp; &nbsp; T1 t3 = T1();
&nbsp; &nbsp; t3.~T1();

___
2011.12.21
&nbsp;
**问题描述**：C++的#include，解析规则是什么？
&nbsp;
**解决方法**：
&nbsp; &nbsp; 1. #include <h-char-sequence>new-line，由编译器指定查找路径，将h-char-sequence代表的源文件内容展开在当前行；
&nbsp; &nbsp; 2. #include &quot;q-char-sequence&quot;new-line，查找由q-char-sequence确定的文件名，将其全部内容展开在当前行。如果查找失败，则按规则#include<q-char-sequence> new-line继续查找；
&nbsp; &nbsp; 3. #include MACROnew-line，先完成宏展开，再按照以上规则进行解析；
&nbsp;
**参考资料**：《ISO-IEC-14882-1998》 16.2 source file inclusion

___
2011.12.29
&nbsp;
**问题描述**：为什么我重载了istream& operator >> (istream&,pair<T1,T2>&)，调用cin>>a_pair也正常，可定义istream_iterator<pair<T1,T2> > is_iter(cin)就失败了呢？
&nbsp;
问题补充：
&nbsp; &nbsp; 编译错误：找不到重载的operator>>，接受pair<T1,T2>类型的参数；
&nbsp; &nbsp; 错误原文：compile error: rror C2678: binary &#39;>>&#39;: no operator found which takes a left-hand operand of type&#39;std::basic_istream<_Elem,_Traits>&#39; (or there is no acceptableconversion)
&nbsp;
**问题原因**：因为istream_iterator<pair<T1, T2>>在模板特化的时候，是在命名空间std中。std中有很多重载的operator >>(参见<istream>)，而我自定义的重载函数不在std命名空间中。因此，由于发生了**命名覆盖**，std::operator>>覆盖了我自定义的重载函数，std::istream_iterator<pair<T1, T2>>编译时自然就找不到合适的重载函数了，所以报这个错误。
&nbsp;
**解决方法**：将我自己的重载版本用namespace std{}扩起来，就通过了。但我不确定这是不是通用手段，因为我记得std命名空间不允许自己往里写东西。
&nbsp;
问题补充：对于自定义类型，重载istream& operator >> (istream&,MyClass<T>&)后，std::istream_iterator<MyClass<T>>工作一切正常，为什么没有遇到上面的问题？
&nbsp;
**解决方法**：C++规定，当一个类实例被使用时，这个类所在的命名空间中，参数列表包含该类的所有当前可见的函数，都会被引入到当前命名空间。因此，自定义类型MyClass版本的operator>>重载，是参与到std::operator>>的推导过程的，不会发生找不到的错误。

___
2012.01.02

**问题描述**：一个类可以作为自己的友元类吗？

**解决方法**：可以。
&nbsp; &nbsp; class TestFriendClass {
&nbsp; &nbsp; public:
&nbsp; &nbsp; &nbsp; &nbsp; friend class TestFriendClass;
&nbsp; &nbsp; };

___
2012.01.10

**问题描述**：两个ifstream可以同时打开同一个文件吗？

**解决方法**：经测试，可以；

___
2012.01.15

**问题描述**：引用可以运行期绑定吗？

**解决方法**：可以；

示例代码：
&nbsp; &nbsp; int a=1, b=2;
&nbsp; &nbsp; int& r=a>b ? a : b;
&nbsp; &nbsp; cout << r << endl;

&nbsp; &nbsp; 输出：2

___
2012.03.20

**问题描述**：有什么比较变态的模板参数声明吗？

**解决方法**：有。

示例代码：

template <typename FloatT>
class Filter {
public:
&nbsp; &nbsp; typedef FloatT float_type;
&nbsp; &nbsp; typedef std::size_t size_type;
&nbsp; &nbsp; typedef std::complex<float_type> value_type;

public:
&nbsp; &nbsp; // RandomAccessContainer can be vector or deque
&nbsp; &nbsp; template <template <class T,
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;classA=std::allocator<T> > class RandomAccessContainer>
&nbsp; &nbsp; RandomAccessContainer<value_type>& filter(
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;RandomAccessContainer<value_type>& seq) const;
};

template <typename FloatT>
template <template <class T,
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;class A=std::allocator<T> > classRandomAccessContainer>
RandomAccessContainer<typename Filter<FloatT>::value_type>&
Filter<FloatT>::filter(RandomAccessContainer<value_type>&seq) const {
&nbsp; &nbsp; return seq;
}

___
2012.03.31

**问题描述**：C++的类中，静态成员可以怎样访问？

**解决方法**：对于静态数据成员和静态成员函数，都可以通过类名加::访问，也可以通过对象名加.访问。

___
2012.04.01

**问题描述**：C++中有没有什么办法，可以防止为类写很多冗余的比较逻辑？比如有了<和==，还得写>,<=, >=, !=，都是简单的重复模式。

**解决方法**：有办法，C++的<utility>标准库头文件，提供了一个子命名空间rel_ops，提供了根据<和==完成余下四种比较操作的运算符重载模板函数：

namespace std {
namespace rel_ops {
template <typename T> bool operator != (const T& lhs, const T&rhs) { return !(lhs==rhs); }
template <typename T> bool operator > (const T& lhs, constT& rhs) { return rhs<lhs; }
template <typename T> bool operator <= (const T& lhs, constT& rhs) { return !(rhs<lhs); }
template <typename T> bool operator >= (const T& lhs, constT& rhs) { return !(lhs<rhs); }
}
}

示例代码：
#include <iostream>
#include <utility>

namespace aa {

class A {
public:
&nbsp; &nbsp; A(int value=0): value_(value) {}
&nbsp; &nbsp; bool operator < (const A& rhs) const {
&nbsp; &nbsp; &nbsp; &nbsp; return this->value_ < rhs.value_;
&nbsp; &nbsp; }
&nbsp; &nbsp; friend bool operator == (const A& lhs, const A& rhs){
&nbsp; &nbsp; &nbsp; &nbsp; return lhs.value_ == rhs.value_;
&nbsp; &nbsp; }
&nbsp; &nbsp; // friend bool std::rel_ops::operator > <A>(constA&, const A&); &nbsp;// not ok
&nbsp; &nbsp; // friend std::rel_ops::operator > ; &nbsp;// error
&nbsp; &nbsp; // using std::rel_ops::operator > ; &nbsp;// error
private:
&nbsp; &nbsp; int value_;
};

// using namespace std::rel_ops; &nbsp;// not ok
// using std::rel_ops::operator > ; &nbsp;// ok

using std::rel_ops::operator > ;
using std::rel_ops::operator <= ;
using std::rel_ops::operator >= ;
using std::rel_ops::operator != ;

} &nbsp;// namespace aa

int main(int argc, char* argv[]) {

&nbsp; &nbsp; aa::A x(5), y(6), z(6);
&nbsp; &nbsp; bool pass = true;
&nbsp; &nbsp; pass = x<y && !(y<x) && !(y<z)&& !(z<y);
&nbsp; &nbsp; clog << &quot;test operator <: &quot; << (pass? &quot;pass&quot;: &quot;FAILED&quot;) << endl;

&nbsp; &nbsp; pass = !(x==y) && !(y==x) && (y==z);
&nbsp; &nbsp; clog << &quot;test operator ==: &quot; << (pass ?&quot;pass&quot;: &quot;FAILED&quot;) << endl;

&nbsp; &nbsp; pass = !(x>y) && (y>x) && !(y>z)&& !(z>y);
&nbsp; &nbsp; clog << &quot;test operator >: &quot; << (pass? &quot;pass&quot;: &quot;FAILED&quot;) << endl;

&nbsp; &nbsp; return 0;
}

___
2012.04.02

**问题描述**：浮点数取模函数fmod和modf怎样使用，有什么区别？

**解决方法**：
&nbsp; &nbsp; double fmod(double x, double y); &nbsp;// return x % y;
&nbsp; &nbsp; double modf(double value, double* iptr); &nbsp;//*iptr存value整数部分，返回值是value小数部分

___
2012.04.06

**问题描述**：C++头文件中定义常量，会不会引起链接时的重复定义错误？

**问题原因**：不会的。
&nbsp; &nbsp; 在 C++（但不是在 C 语言）中，const限定符对默认存储类型稍有影响。在默认情况下，全局变量的链接性为外部的，但 const全局变量的链接性为内部的。也就是说，在 C++ 看来，全局 const 定义就像使用了static 说明符一样。
&nbsp; &nbsp; 因此，可以将 const常量定义在头文件中供工程中的多个其它文件包含引用，并且编译时不会产生变量重复定义的错误。当然，也可以用#define 宏定义。
&nbsp;
注意事项：
&nbsp; &nbsp; 一般常量定义并无问题，但是，如果 const要限定的是指针就须特别注意。例如：
&nbsp; &nbsp; const char* STRING1 = &quot;aaaa&quot;; &nbsp;// error:常指针不是常量，而是变量；
&nbsp; &nbsp; char* const STRING2 = &quot;bbbb&quot;; &nbsp;// ok:指针常量是常量；

___
2012.04.06

**问题描述**：std::priority_queue取队头的元素，使用top()还是用front()？

**解决方法**：priority_queue.top()。

___
2012.04.06

**问题描述**：std::queue中，能够取队尾元素吗？

**解决方法**：能，queue.back()。

___
2012.04.10

**问题描述**：C++中如何知道一个基础数据类型是浮点数类型还是整数类型？

**解决方法**：
&nbsp; &nbsp; #include <limits>
&nbsp; &nbsp; cout << std::numeric_limits<T>::is_integer<< endl;

___
2012.04.10

**问题描述**：如何获得一个基础数据类型的数轴最左端的值和最右端的值？

**解决方法**：
&nbsp; &nbsp; 1. 获得最大值：std::numeric_limits<T>::max()；
&nbsp; &nbsp; 2.std::numeric_limits<T>::min()能够获取整数类型的最小值；对于浮点类型，它获得的是距离0最近的最小正数值；
&nbsp; &nbsp; 3.C++11中，解决了2.中的问题，用std::numeric_limits<T>::lowest()表示类型在数轴最左端的值；
&nbsp; &nbsp; 4. 经测试（VS11），C++11中，对于浮点类型（float, double, longdouble），std::numeric_limits<T>::lowest()恰好是std::numeric_limits<T>::max()的相反数；
&nbsp; &nbsp; 5.在C++98中，对于浮点数，需要结合std::numeric_limits<T>::is_integer来获得最小值：
&nbsp; &nbsp; &nbsp; &nbsp; T lowest =std::numeric_limits<T>::is_integer ? std::numeric_limits<T>::min() :-std::numeric_limits<T>::max();

___
2012.04.10

**问题描述**：complex<T>如何取得模值？如何获得角度？

**解决方法**：
&nbsp; &nbsp; #include <complex>
&nbsp; &nbsp; std::complex<double> c(3,4);
&nbsp; &nbsp; cout << abs(c) << endl; &nbsp;//sqrt(real(c)*real(c) + imag(c)*imag(c))
&nbsp; &nbsp; cout << arg(c) << endl; &nbsp;// atan(imag(c),real(c))
&nbsp; &nbsp; cout << norm(c) << endl; &nbsp;// real(c)*real(c)+ imag(c)*imag(c)

___
2012.04.11

**问题描述**：如何用一个参数向函数传递数组（包括数组名和数组大小）？

**解决方法**：
&nbsp; &nbsp; 1. 向函数传递元素可修改的数组
&nbsp; &nbsp; template <typename T, int N>
&nbsp; &nbsp; void func(T (&A)[N]);
&nbsp; &nbsp; &nbsp;
&nbsp; &nbsp; 2. 向函数传递元素不可修改的数组（常数组）
&nbsp; &nbsp; template <typename T, int N>
&nbsp; &nbsp; void func(const T (&A)[N]);
&nbsp; &nbsp; 或
&nbsp; &nbsp; template <typename T, int N>
&nbsp; &nbsp; void func(T const (&A)[N]);
&nbsp; &nbsp; &nbsp;
&nbsp; &nbsp; 3. 向函数传递本身地址不可修改的数组（数组常量）
&nbsp; &nbsp; template <typename T, int N>
&nbsp; &nbsp; void func(T (&A)[N]);
&nbsp; &nbsp; note：数组地址都是不可改变的，不需要const限定！！！

___
2012.04.23

**问题描述**：char* strncpy(char* dst, char* src, size_tn)各种不同情形是怎么处理的？

**解决方法**：
&nbsp; &nbsp; 1.当strlen(src)>=n时，拷贝n个普通字符，&#39;\0&#39;字符不会被自动追加到dst；
&nbsp; &nbsp; 2.当strlen(src)<n时，拷贝src所有的字符到dst，dst其余n-strlen(src)个位置都以&#39;\0&#39;填充；

___
2012.04.23

**问题描述**：memcpy, memmove, strcpy, strncpy中，是否考虑区间重叠？

**解决方法**：
&nbsp; &nbsp; 1. memmove考虑区间重叠，保证对重叠的区间也有正确的行为；
&nbsp; &nbsp; 2. memcpy, strcpy,strncpy不考虑区间重叠，当区间重叠时，行为未定义；

___
2012.04.25
&nbsp;
**问题描述**：tellg, seekg, tellp, seekp这四个IO流函数最早是在哪一级定义的？
&nbsp;
**解决方法**：
&nbsp; &nbsp; &nbsp; &nbsp; 1. tellg, seekg: class basic_istream<charT,traits>
&nbsp; &nbsp; &nbsp; &nbsp; 2. tellp, seekp: class basic_ostream<charT,traits>

___
2012.05.14

**问题描述**：在定义宏Fatal(...)的时候，为什么应避免定义为语句块（{}）？

**补充说明**：

#define Fatal(...) \
{ \
&nbsp; &nbsp; std::fprintf(stderr, &quot;Fatal: %d: %d: &quot;, __FILE__,__LINE__); \
&nbsp; &nbsp; std::fprintf(stderr, ...); \
&nbsp; &nbsp; std::fflush(stderr); \
&nbsp; &nbsp; std::exit(1); \
}

**问题原因**：如果这样定义的话，在如下调用情形中，将会出错：

if (cond)
&nbsp; &nbsp; Fatal(&quot;fatal error&quot;);
else &nbsp;//宏展开后，此处的else将报错：没有匹配的if。因为前面的if会被“;”终止。
&nbsp; &nbsp; Warning(&quot;warning #1&quot;);

**解决方法**：在以上的调用语句中，Fatal须为单语句表达式，故可用逗号表达式替换之。代码如下：

#define Fatal(...) \
( \
&nbsp; &nbsp; std::fprintf(stderr, &quot;Fatal: %d: %d: &quot;, __FILE__,__LINE__), \
&nbsp; &nbsp; std::fprintf(stderr, ...), \
&nbsp; &nbsp; std::fflush(stderr), \
&nbsp; &nbsp; std::exit(1) \
)

___
2012.06.11

**问题描述**：namespace作用域内的全局变量能否放在头文件内？

**问题原因**：不能。
&nbsp; &nbsp; 1.如果声明为普通变量，则在每个编译实体内都会生成一个变量实体，链接时报重定义错误；
&nbsp; &nbsp; 2.如果声明为静态变量，则在每个编译实体内都会生成一个文件作用域静态变量，虽然没有错误，但是变量无法共享；
&nbsp; &nbsp; 3.所以，我只有一个办法了，声明为模板类的静态变量，然后在该头文件中写定义式；

___
2012.04.25 （已记录）

**问题描述**：tellg, seekg, tellp, seekp这四个IO流函数最早是在哪一级定义的？

**解决方法**：
&nbsp; &nbsp; &nbsp; &nbsp;1. tellg, seekg: class basic_istream<charT,traits>
&nbsp; &nbsp; &nbsp; &nbsp;2. tellp, seekp: class basic_ostream<charT,traits>

___
2012.06.14

**问题描述**：为什么rand()函数的随机性不好？

**解决方法**：rand()实现算法是线性求余法，速度快，但是有个缺陷，低比特的随机性不好，很容易就遇到环了。所以如果对随机性要求比较高，可以取rand()的较高位重新组合，可以获得不错的随机性。

___
2012.07.03

**问题描述**：如何为一个序列填充初值？

**解决方法**：std::generate(ForwardIterator first, ForwardIterator last,Generator gen);

___
2012.07.12

**问题描述**：如何快速生成一个指定大小的空白文件（全0）？

**解决方法**：
#include <fstream>

std::size_t size = 1000000;
std::ofstream fout(&quot;fname&quot;);
fout.seekp(size-1);
fout << &#39;\0&#39;;
fout.close();

___
2012.07.17

**问题描述**：如何设置输出流每一次输出操作都清空缓冲区，直接到目标对象？

**解决方法**：
&nbsp; &nbsp; &nbsp; &nbsp;# include <ostream>
&nbsp; &nbsp; &nbsp; &nbsp;std::ostream out;
&nbsp; &nbsp; &nbsp; &nbsp;out << std::unitbuf; &nbsp;//设置每一次输出动作都清空缓冲区
&nbsp; &nbsp; &nbsp; &nbsp;out << std::nounitbuf; &nbsp;// 取消设置

___
2012.07.18

**问题描述**：std::move()在哪个头文件里？

**解决方法**：<utility>

___
2012.07.24

**问题描述**：可以为某个大小的某类型数组定义别名吗？

**解决方法**：可以。
&nbsp; &nbsp; &nbsp; &nbsp;typedef int ArrayType[100];
&nbsp; &nbsp; &nbsp; &nbsp;ArrayType arr;
&nbsp; &nbsp; &nbsp; &nbsp;cout << sizeof(arr)/sizeof(int) <<endl; &nbsp;// 100

___
2012.07.27

**问题描述**：函数参数是数组类型时，数组大小起作用吗？

**解决方法**：
&nbsp; &nbsp; &nbsp; &nbsp;1.最外层的大小会直接被忽略，函数体内只能得到一个非常指针；
&nbsp; &nbsp; &nbsp; &nbsp;2.多维数组次维度的大小都有用，其实是用来指示主维度指针的数据类型；

___
2012.08.06

**问题描述**：类内的静态函数可以访问该类实例的私有变量吗？

**解决方法**：可以。在VS2010下和g++下都测试通过；

测试代码：

<p>
    <code>#<span style="color:#0000ff"><strong>include</strong></span><span
style="color:#333399"><</span>iostream<span
style="color:#333399">></span><br/><br/><span
style="color:#0000ff"><strong>using</strong></span><span
style="color:#0000ff"><strong>namespace</strong></span> std;<br/><br/><span
style="color:#0000ff"><strong>class</strong></span> Test {<br/><span
style="color:#0000ff"><strong>public</strong></span><span
style="color:#333399">:</span><br/><span
style="color:#0000ff"><strong>static</strong></span><span
style="color:#0000ff"><strong>void</strong></span> test() {<br/> &nbsp; &nbsp;
&nbsp; &nbsp;Test t;<br/> &nbsp; &nbsp; &nbsp; &nbsp;t.a <span
style="color:#333399">=</span><span style="color:#6e00aa">5</span>;<br/> &nbsp;
&nbsp; &nbsp; &nbsp;cout <span style="color:#333399"><<</span> t.a <span
style="color:#333399"><<</span> endl;<br/> &nbsp; &nbsp;}<br/><br/><span
style="color:#0000ff"><strong>private</strong></span><span
style="color:#333399">:</span><br/><span
style="color:#0000ff"><strong>int</strong></span> a;<br/>};<br/><br/><span
style="color:#0000ff"><strong>int</strong></span> main() {<br/><br/> &nbsp;
&nbsp;Test<span style="color:#333399">:</span><span
style="color:#333399">:</span>test();<br/><span
style="color:#0000ff"><strong>return</strong></span><span
style="color:#6e00aa">0</span>;<br/>}</code>
</p>

___
2012.08.30

**问题描述**：在类作用域内，可不可以在定义内嵌枚举类型时同时定义枚举变量？

**解决方法**：可以。而且这样枚举常量直接被圈在类作用域之下，方便直接；

示例代码：
&nbsp; &nbsp;struct ItemEntry{
&nbsp; &nbsp; &nbsp; &nbsp;UInt32 id;
&nbsp; &nbsp; &nbsp; &nbsp;enum {SOME_ARRAY_SIZE = 1000};
&nbsp; &nbsp; &nbsp; &nbsp;enum {NORMAL, RETAIN, NONE} in_queue_state;
&nbsp; &nbsp;};

___
2012.09.18

**问题描述**：在C++11中，Function template generate_canonical是干什么的？

**补充说明**：
&nbsp; &nbsp; &nbsp; &nbsp;#include <random>
&nbsp; &nbsp; &nbsp; &nbsp;template<class RealType, size_t bits, classURNG>
&nbsp; &nbsp; &nbsp; &nbsp;RealType generate_canonical(URNG& g);

**解决方法**：根据Uniform Random Number Generator(URNG)产生的随机整数，通过多次调用g()进行高低位组合，生成一个[0.0,1.0]之间均匀分布的随机浮点数。

___
2012.09.28

**问题描述**：cout的缓冲区可以用其他输出流缓冲区替换吗？

**解决方法**：可以；

示例代码：
&nbsp; &nbsp; &nbsp; &nbsp;ofstream fout(&quot;output.txt&quot;);
&nbsp; &nbsp; &nbsp; &nbsp;streambuf* oldbuf = cout.rdbuf(fout.rdbuf());
&nbsp; &nbsp; &nbsp; &nbsp;cout << &quot;str1&quot;; &nbsp;// write&quot;str1&quot; to file &quot;output.txt&quot;
&nbsp; &nbsp; &nbsp; &nbsp;cout.rdbuf(oldbuf);

&nbsp; &nbsp; &nbsp; &nbsp;ostringstream oss;
&nbsp; &nbsp; &nbsp; &nbsp;oldbuf = cout.rdbuf(oss.rdbuf());
&nbsp; &nbsp; &nbsp; &nbsp;cout << &quot;str2&quot;; &nbsp;// write&quot;str2&quot; to string stream oss
&nbsp; &nbsp; &nbsp; &nbsp;cout.rdbuf(oldbuf);
&nbsp; &nbsp; &nbsp; &nbsp;cerr << oss.str(); &nbsp;// write&quot;str2&quot; to screen, as a validation

**补充说明**：查标准发现，cout有cout.rdbuf(streambuf*sb)成员函数，但是ofstream和ostringstream却没有这个函数，意味着后面二者无法改变自己的缓冲区对象；

___
2012.11.13

**问题描述**：当类成员函数在类外定义的时候，哪些保留字必须既要在声明时指定，又要在定义时指定？

**解决方法**：
&nbsp; &nbsp; &nbsp; &nbsp;1. const内外必须都写,这是函数类型的一部分,表明隐式形参this的常量性
&nbsp; &nbsp; &nbsp; &nbsp;2. inline内外均可,一处标明即可(最好写在外面,使用者不关心也不必了解该函数是否为内联函数)
&nbsp; &nbsp; &nbsp; &nbsp;3. 以下必须只能写在内部 static friend explicitvirtual

**参考资料**：<ahref="http://bbs.byr.cn/#!article/CPP/66438">http://bbs.byr.cn/#!article/CPP/66438</a>

___
2012.12.14

**问题描述**：查名字查找规则，是先父类还是先全局？

**解决方法**：先父类；

**补充说明**：标准规定：对于依赖模版参数的父类，名字查找时默认不查找父类成员，需要程序员显式加上this->才行；

___
2013.08.08


**问题描述**：在variadic template编译时，报错“no match function forcall”是怎么回事？

**解决方法**：
&nbsp; &nbsp; &nbsp; &nbsp;1.
template <typename... Args>
void func(Args... args, int a, double b) {}
这种情况下，Args... args必须函数的最后一个参数，修改如下：
<p style="margin:5px 0px;">
    template <typename... Args>
</p>
<p style="margin:5px 0px;">
    void func(int a, double b, Args... args) {}
</p>
<p style="margin:5px 0px;">
    <br/>
</p>
<p style="margin:5px 0px;">
    &nbsp; &nbsp; &nbsp; &nbsp;2.
</p>
void test_impl(const string& a, const string& b) {
}

void test_impl(int a, double b) {
}

template <typename Arg0, typename... Args>
void test_impl(const string& a, const string& b, Arg0 arg0, Args...args) {
&nbsp;cout << a << b << arg0 << &quot; &quot;;
&nbsp;test_impl(a, b, args...);
}

template <typename... Args>
void test(const string& a, const string& b, Args... args) {
&nbsp;test_impl(a, b, args...);
}

int main(int argc, char* argv[]) {
&nbsp;test(&quot;a&quot;, &quot;aa&quot;, 1, 2, 3.5, test_impl);
&nbsp;return 0;
}

报错：
main.cc:279:3: error: no matching function for call to &#39;test&#39;
&nbsp;test(&quot;a&quot;, &quot;aa&quot;, 1, 2, 3.5, test_impl);
&nbsp;^~~~
main.cc:271:6: note: candidate function not viable: requires 5 arguments,but 6 were provided
void test(const string& a, const string& b, Args... args) {
&nbsp; &nbsp; ^
1 error generated.
这报错挺诡异的，其实是因为test_impl有重载，传递给它这个函数地址时没法决定选哪个。
**解决方法**是，把要作为参数传进函数的重载函数换个没重载的名字。比如套个namespace。

___
2013.09.24

**问题描述**：C++11中根据第一个模板参数选择::type是第二个还是第三个模板参数的模板元是什么？

**解决方法**：#include <type_traits> &nbsp;std::conditional<bool,TrueType, FalseType>::type;

___
2014.02.19

**问题描述**: C++11 <memory>中shared_ptr的aliasing构造函数怎么用?

**解决方法**:
<pre style="margin-top: 0px; margin-bottom: 0px; font-size: 12px;">
structC {int* data;};</pre>
<pre style="margin-top: 0px; margin-bottom: 0px; font-size: 12px;">
std::shared_ptr<C> obj (newC);
  std::shared_ptr<int> p9 (obj, obj->data);</pre>
&nbsp; &nbsp; &nbsp; &nbsp;&nbsp;
**信息来源**:&nbsp;<ahref="http://www.cplusplus.com/reference/memory/shared_ptr/"_src="http://www.cplusplus.com/reference/memory/shared_ptr/">http://www.cplusplus.com/reference/memory/shared_ptr/</a>

___
2014.04.20

**问题描述**：C++11中，是否允许对任意类型数据成员使用in-class初始化？

**补充说明**：in-class初始化示例：
class A {
&nbsp; &nbsp; int i = 1;
&nbsp; &nbsp; double d = 1.0;
&nbsp; &nbsp; string s = &quot;abc&quot;;
};

**解决方法**：
&nbsp; &nbsp; &nbsp; &nbsp; 1. 对非静态数据成员，是。
C++11标准文档：12.6.2 Initializing bases and members


8 In a non-delegating constructor, if a given non-static data member or baseclass is not designated by a mem-initializer-id (including the case where thereis no mem-initializer-list because the constructor has no ctor-initializer) andthe entity is not a virtual base class of an abstract class (10.4), then
— if the entity is a non-static data member that has abrace-or-equal-initializer, the entity is initialized as speciﬁed in 8.5;
— otherwise, if the entity is a variant member (9.5), no initialization isperformed;
— otherwise, the entity is default-initialized (8.5).
<p>
    [ Note: An abstract class (10.4) is never a most derived class, thus its
constructors never initialize virtual base classes, therefore the corresponding
mem-initializers may be omitted. — end note ] An attempt to initialize more than
one non-static data member of a union renders the program ill-formed. After the
call to a constructor for class X has completed, if a member of X is neither
initialized nor given a value during execution of the compound-statement of the
body of the constructor, the member has indeterminate value.
</p>
[Example:
struct A {
&nbsp; A();
};
struct B {
&nbsp; B(int);
};
struct C {
&nbsp; C() { } // initializes members as follows:
&nbsp; A a; // OK: calls A::A()
&nbsp; const B b; // error: B has no default constructor
&nbsp; int i; // OK: i has indeterminate value
&nbsp; int j = 5; // OK: j has the value 5
};
— end example ]

9 If a given non-static data member has both a brace-or-equal-initializerand a mem-initializer, the initialization speciﬁed by the mem-initializer isperformed, and the non-static data member’s brace-or-equal-initializer isignored. [Example: Given<br/>
struct A {
&nbsp; int i = /* some integer expression with side eﬀects */ ;
&nbsp; A(int arg) : i(arg) { }
&nbsp; // ...
};
the A(int) constructor will simply initialize i to the value of arg, and theside eﬀects in i’s brace-or-equal-initializer will not take place. — end example]

&nbsp; &nbsp; &nbsp; &nbsp; 2.对静态数据成员，只有整数类型和枚举类型的常量，可以使用in-class被常量表达式初始化。
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
C++11标准文档：9.4.2 Static data members [class.static.data]

<p>
    3 If a non-volatile const static data member is of integral or enumeration
type, its declaration in the class deﬁnition can specify a
brace-or-equal-initializer in which every initializer-clause that is an
assignment-expression is a constant expression (5.19). A static data member of
literal type can be declared in the class deﬁnition with the constexpr speciﬁer;
if so, its declaration shall specify a brace-or-equal-initializer in which every
initializer-clause that is an assignment-expression is a constant expression. [
Note: In both these cases, the member may appear in constant expressions. — end
note ] The member shall still be deﬁned in a namespace scope if it is odr-used
(3.2) in the program and the namespace scope deﬁnition shall not contain an
initializer.
</p>



**参考资料**：
&nbsp; &nbsp; &nbsp; &nbsp; 1. mem-initializer-id, mem-initializer-list:
ctor-initializer:
&nbsp; &nbsp; : mem-initializer-list
mem-initializer-list:
&nbsp; &nbsp; mem-initializer ...opt
&nbsp; &nbsp; mem-initializer , mem-initializer-list ...opt
mem-initializer:
&nbsp; &nbsp; mem-initializer-id ( expression-listopt)
&nbsp; &nbsp; mem-initializer-id braced-init-list
mem-initializer-id:
&nbsp; &nbsp; class-or-decltype
&nbsp; &nbsp; identiﬁer

&nbsp; &nbsp; &nbsp; &nbsp; 2. (8.5) means&nbsp;8.5 Initializers [dcl.init]

___
2014.04.20

**问题描述**：有什么办法可以快速记忆copy-elision和move-semantics是怎么工作的？

**解决方法**：distinct-names rule:
For copy-elision: The rule of thumb here is that something that lookslike&nbsp;a copy operation only actually invokes the copy constructor&nbsp;if itresults in two distinct names for the value (hereinafter the&quot;distinct-names rule&quot;).
For move-semantics: You can&#39;t have two names for the same value of amove-only type,&nbsp;so if you&#39;re creating a new name for thatvalue,&nbsp;you have to give up the old name by passing it to std::move().
独名原则：发生拷贝省略或移动语义的时候，一个数值不能有两个变量名；
拷贝省略：拷贝操作不会调用拷贝构造函数，除非它造成同一个数值有了两个不同的变量名；
移动语义：对于可移动不可拷贝的类型，同一个数值不能同时有两个变量名，因此需要对旧变量名调用std::move()，来表明你希望放弃旧的变量名；

___
2014.04.30

**问题描述**：std::set_intersection(first1, last1, first2, last2,result)是否保证输出的元素来自哪一个输入集合？

**解决方法**：保证，返回[first1, last1)里的元素；

**信息来源**：<ahref="http://www.cplusplus.com/reference/algorithm/set_intersection/"_src="http://www.cplusplus.com/reference/algorithm/set_intersection/">http://www.cplusplus.com/reference/algorithm/set_intersection/</a>

___
2014.05.05

**问题描述**：如何获取一组重载函数中某一个重载的函数地址？

**解决方法**：将函数名强制转换为需要的函数类型。
int func(int) {}
double func(double) {}
int (*ptr)(int) = static_cast<int (*)(int)>(&func);

**信息来源**：<ahref="http://stackoverflow.com/questions/17874489/disambiguate-overloaded-member-function-pointer-being-passed-as-template-paramet"_src="http://stackoverflow.com/questions/17874489/disambiguate-overloaded-member-function-pointer-being-passed-as-template-paramet">http://stackoverflow.com/questions/17874489/disambiguate-overloaded-member-function-pointer-being-passed-as-template-paramet</a>

___
2014.05.06

**问题描述**：有没有算集合不对称差的STL算法？（SetA-SetB，不是std::set_symmetric_difference）

**解决方法**：
#include <algorithm>
OutputIterator set_difference (InputIterator1 first1, InputIterator1last1,&nbsp;InputIterator2 first2, InputIterator2 last2,&nbsp;OutputIteratorresult);
结果为Set1 - Set2

**信息来源**：<ahref="http://www.cplusplus.com/reference/algorithm/set_difference/"_src="http://www.cplusplus.com/reference/algorithm/set_difference/">http://www.cplusplus.com/reference/algorithm/set_difference/</a>

___
2014.05.06

**问题描述**：u8&quot;some_characters&quot;中的u8是什么意思？

**解决方法**：这是C++11新加入的字符串字面值引导符，跟L&quot;some_characters&quot;表示字符串元素是wchar_t类似，u8&quot;some_characters&quot;表示这是一个UTF-8字符串，类型为constchar[]；

**信息来源**：<a href="http://en.cppreference.com/w/cpp/language/string_literal"_src="http://en.cppreference.com/w/cpp/language/string_literal">http://en.cppreference.com/w/cpp/language/string_literal</a>

**补充说明**：C++11标准中所有的字符串字面值引导符：

摘抄以上链接中部分原文（关于R&quot;()&quot;原生字符串字面值，请直接略过本节看下面的C++11标准文档摘录）：
<meta charset="utf-8"/>
<h3 style="color: rgb(0, 0, 0); font-weight: bold; margin: 0px 0px 0.3em;
overflow: hidden; padding: 1.1em 0px 0.2em 0.75em; border-bottom-style: none;
width: auto; font-size: 17px; font-family: DejaVuSans, &#39;DejaVu Sans&#39;,
arial, sans-serif; font-style: normal; font-variant: normal; letter-spacing:
normal; line-height: 15.360000610351563px; orphans: auto; text-align: start;
text-indent: 0px; text-transform: none; white-space: normal; widows: auto;
word-spacing: 0px; -webkit-text-stroke-width: 0px; background: none rgb(255,
255, 255);">
    <span class="mw-headline" id="Syntax">Syntax</span>
</h3>
<table class="t-sdsc-begin" style="font-size: 13px; color: rgb(0, 0, 0);
font-family: DejaVuSans, &#39;DejaVu Sans&#39;, arial, sans-serif; font-style:
normal; font-variant: normal; font-weight: normal; letter-spacing: normal;
line-height: 15.360000610351563px; orphans: auto; text-align: start;
text-indent: 0px; text-transform: none; white-space: normal; widows: auto;
word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255,
255, 255);">
    <tbody>
        <tr class="firstRow">
            <td colspan="10" class="t-sdsc-sep" style="border-top-width: 1px;
border-top-style: solid; border-top-color: rgb(204, 204, 204); padding:
0px;"></td>
        </tr>
        <tr class="t-sdsc">
            <td style="padding: 0.5em 0px 0.5em 1em; font-size: 1em;">
                <code style="font-family: DejaVuSansMono, &#39;DejaVu Sans
Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight:
bold;">&quot;</strong></code>&nbsp;(<span class="t-spar" style="color: rgb(128,
128, 128); font-style: italic; line-height:
1.1em;">unescaped_character</span>|<span class="t-spar" style="color: rgb(128,
128, 128); font-style: italic; line-height:
1.1em;">escaped_character</span>)*&nbsp;<code style="font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace !important;
background-color: transparent;"><strong style="font-weight:
bold;">&quot;</strong></code>
            </td>
            <td style="padding-left: 3em;">
                (1)
            </td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
        </tr>
        <tr>
            <td colspan="10" class="t-sdsc-sep" style="border-top-width: 1px;
border-top-style: solid; border-top-color: rgb(204, 204, 204); padding:
0px;"></td>
        </tr>
        <tr class="t-sdsc">
            <td style="padding: 0.5em 0px 0.5em 1em; font-size: 1em;">
                <code style="font-family: DejaVuSansMono, &#39;DejaVu Sans
Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight: bold;">L</strong></code>&nbsp;<code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">&quot;</strong></code>&nbsp;(<span class="t-spar"
style="color: rgb(128, 128, 128); font-style: italic; line-height:
1.1em;">unescaped_character</span>|<span class="t-spar" style="color: rgb(128,
128, 128); font-style: italic; line-height:
1.1em;">escaped_character</span>)*&nbsp;<code style="font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace !important;
background-color: transparent;"><strong style="font-weight:
bold;">&quot;</strong></code>
            </td>
            <td style="padding-left: 3em;">
                (2)
            </td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
            <td class="t-sdsc-nopad" style="padding-left: 2em;"></td>
        </tr>
        <tr>
            <td colspan="10" class="t-sdsc-sep" style="border-top-width: 1px;
border-top-style: solid; border-top-color: rgb(204, 204, 204); padding:
0px;"></td>
        </tr>
        <tr class="t-sdsc">
            <td style="padding: 0.5em 0px 0.5em 1em; font-size: 1em;">
                <code style="font-family: DejaVuSansMono, &#39;DejaVu Sans
Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight: bold;">u8</strong></code>&nbsp;<code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">&quot;</strong></code>&nbsp;(<span class="t-spar"
style="color: rgb(128, 128, 128); font-style: italic; line-height:
1.1em;">unescaped_character</span>|<span class="t-spar" style="color: rgb(128,
128, 128); font-style: italic; line-height:
1.1em;">escaped_character</span>)*&nbsp;<code style="font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace !important;
background-color: transparent;"><strong style="font-weight:
bold;">&quot;</strong></code>
            </td>
            <td style="padding-left: 3em;">
                (3)
            </td>
            <td style="padding-left: 2em;">
                <span class="t-mark-rev t-since-cxx11" style="color: rgb(0, 128,
0); font-size: 0.8em; line-height: 1.1em;">(since C++11)</span>
            </td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
        </tr>
        <tr>
            <td colspan="10" class="t-sdsc-sep" style="border-top-width: 1px;
border-top-style: solid; border-top-color: rgb(204, 204, 204); padding:
0px;"></td>
        </tr>
        <tr class="t-sdsc">
            <td style="padding: 0.5em 0px 0.5em 1em; font-size: 1em;">
                <code style="font-family: DejaVuSansMono, &#39;DejaVu Sans
Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight: bold;">u</strong></code>&nbsp;<code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">&quot;</strong></code>&nbsp;(<span class="t-spar"
style="color: rgb(128, 128, 128); font-style: italic; line-height:
1.1em;">unescaped_character</span>|<span class="t-spar" style="color: rgb(128,
128, 128); font-style: italic; line-height:
1.1em;">escaped_character</span>)*&nbsp;<code style="font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace !important;
background-color: transparent;"><strong style="font-weight:
bold;">&quot;</strong></code>
            </td>
            <td style="padding-left: 3em;">
                (4)
            </td>
            <td style="padding-left: 2em;">
                <span class="t-mark-rev t-since-cxx11" style="color: rgb(0, 128,
0); font-size: 0.8em; line-height: 1.1em;">(since C++11)</span>
            </td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
        </tr>
        <tr>
            <td colspan="10" class="t-sdsc-sep" style="border-top-width: 1px;
border-top-style: solid; border-top-color: rgb(204, 204, 204); padding:
0px;"></td>
        </tr>
        <tr class="t-sdsc">
            <td style="padding: 0.5em 0px 0.5em 1em; font-size: 1em;">
                <code style="font-family: DejaVuSansMono, &#39;DejaVu Sans
Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight: bold;">U</strong></code>&nbsp;<code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">&quot;</strong></code>&nbsp;(<span class="t-spar"
style="color: rgb(128, 128, 128); font-style: italic; line-height:
1.1em;">unescaped_character</span>|<span class="t-spar" style="color: rgb(128,
128, 128); font-style: italic; line-height:
1.1em;">escaped_character</span>)*&nbsp;<code style="font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace !important;
background-color: transparent;"><strong style="font-weight:
bold;">&quot;</strong></code>
            </td>
            <td style="padding-left: 3em;">
                (5)
            </td>
            <td style="padding-left: 2em;">
                <span class="t-mark-rev t-since-cxx11" style="color: rgb(0, 128,
0); font-size: 0.8em; line-height: 1.1em;">(since C++11)</span>
            </td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
        </tr>
        <tr>
            <td colspan="10" class="t-sdsc-sep" style="border-top-width: 1px;
border-top-style: solid; border-top-color: rgb(204, 204, 204); padding:
0px;"></td>
        </tr>
        <tr class="t-sdsc">
            <td style="padding: 0.5em 0px 0.5em 1em; font-size: 1em;">
                <span class="t-spar" style="color: rgb(128, 128, 128);
font-style: italic; line-height: 1.1em;">prefix</span><span class="t-mark"
style="color: rgb(0, 128, 0); font-size: 0.8em; line-height:
1.1em;">(optional)</span>&nbsp;<code style="font-family: DejaVuSansMono,
&#39;DejaVu Sans Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight: bold;">R</strong></code>&nbsp;<code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">&quot;</strong></code><span class="t-spar"
style="color: rgb(128, 128, 128); font-style: italic; line-height:
1.1em;">delimiter</span><code style="font-family: DejaVuSansMono, &#39;DejaVu
Sans Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight: bold;">(</strong></code>&nbsp;<span
class="t-spar" style="color: rgb(128, 128, 128); font-style: italic;
line-height: 1.1em;">raw_character</span>*&nbsp;<code style="font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace !important;
background-color: transparent;"><strong style="font-weight:
bold;">)</strong></code><span class="t-spar" style="color: rgb(128, 128, 128);
font-style: italic; line-height: 1.1em;">delimiter</span><code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">&quot;</strong></code>
            </td>
            <td style="padding-left: 3em;">
                (6)
            </td>
            <td style="padding-left: 2em;">
                <span class="t-mark-rev t-since-cxx11" style="color: rgb(0, 128,
0); font-size: 0.8em; line-height: 1.1em;">(since C++11)</span>
            </td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
            <td style="padding-left: 2em;"></td>
        </tr>
        <tr>
            <td colspan="10" class="t-sdsc-sep" style="border-top-width: 1px;
border-top-style: solid; border-top-color: rgb(204, 204, 204); padding:
0px;"></td>
        </tr>
    </tbody>
</table>
<h3 style="color: rgb(0, 0, 0); font-weight: bold; margin: 0px 0px 0.3em;
overflow: hidden; padding: 1.1em 0px 0.2em 0.75em; border-bottom-style: none;
width: auto; font-size: 17px; font-family: DejaVuSans, &#39;DejaVu Sans&#39;,
arial, sans-serif; font-style: normal; font-variant: normal; letter-spacing:
normal; line-height: 15.360000610351563px; orphans: auto; text-align: start;
text-indent: 0px; text-transform: none; white-space: normal; widows: auto;
word-spacing: 0px; -webkit-text-stroke-width: 0px; background: none rgb(255,
255, 255);">
    <span class="mw-headline" id="Explanation">Explanation</span>
</h3>
<table class="t-par-begin" style="font-size: 13px; border-spacing: 0px; color:
rgb(0, 0, 0); font-family: DejaVuSans, &#39;DejaVu Sans&#39;, arial, sans-serif;
font-style: normal; font-variant: normal; font-weight: normal; letter-spacing:
normal; line-height: 15.360000610351563px; orphans: auto; text-align: start;
text-indent: 0px; text-transform: none; white-space: normal; widows: auto;
word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255,
255, 255);">
    <tbody>
        <tr class="t-par firstRow">
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;
white-space: nowrap; text-align: right; font-weight: bold; font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace;">
                unescaped_character
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;">
                -
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top; width:
570.203125px;">
                Any valid character
            </td>
        </tr>
        <tr class="t-par">
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;
white-space: nowrap; text-align: right; font-weight: bold; font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace;">
                escaped_character
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;">
                -
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top; width:
570.203125px;">
                See&nbsp;<a
href="http://en.cppreference.com/w/cpp/language/escape"
title="cpp/language/escape" style="text-decoration: none; color: rgb(11, 0,
128); background: none;">escape sequences</a>
            </td>
        </tr>
        <tr class="t-par">
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;
white-space: nowrap; text-align: right; font-weight: bold; font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace;">
                prefix
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;">
                -
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top; width:
570.203125px;">
                One of&nbsp;<code style="font-family: DejaVuSansMono,
&#39;DejaVu Sans Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight: bold;">L</strong></code>,&nbsp;<code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">u8</strong></code>,&nbsp;<code style="font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace !important;
background-color: transparent;"><strong style="font-weight:
bold;">u</strong></code>,&nbsp;<code style="font-family: DejaVuSansMono,
&#39;DejaVu Sans Mono&#39;, courier, monospace !important; background-color:
transparent;"><strong style="font-weight: bold;">U</strong></code>
            </td>
        </tr>
        <tr class="t-par">
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;
white-space: nowrap; text-align: right; font-weight: bold; font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace;">
                delimiter
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;">
                -
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top; width:
570.203125px;">
                A string made of any source character but parentheses, backslash
and&nbsp;<a href="http://en.cppreference.com/w/cpp/string/byte/isspace"
title="cpp/string/byte/isspace" style="text-decoration: none; color: rgb(11, 0,
128); background: none;">spaces</a>&nbsp;(can be empty)
            </td>
        </tr>
        <tr class="t-par">
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;
white-space: nowrap; text-align: right; font-weight: bold; font-family:
DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier, monospace;">
                raw_character
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top;">
                -
            </td>
            <td style="padding: 0.5em 1em 0px 0px; vertical-align: top; width:
570.203125px;">
                Must not contain the closing sequence&nbsp;<code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">)</strong></code><span class="t-spar" style="color:
rgb(128, 128, 128); font-style: italic;">delimiter</span><code
style="font-family: DejaVuSansMono, &#39;DejaVu Sans Mono&#39;, courier,
monospace !important; background-color: transparent;"><strong
style="font-weight: bold;">&quot;</strong></code>
            </td>
        </tr>
    </tbody>
</table>
<p style="margin: 0.4em 0px 0.5em; line-height: 15.360000610351563px; color:
rgb(0, 0, 0); font-family: DejaVuSans, &#39;DejaVu Sans&#39;, arial, sans-serif;
font-size: 13px; font-style: normal; font-variant: normal; font-weight: normal;
letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px;
text-transform: none; white-space: normal; widows: auto; word-spacing: 0px;
-webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255);">
    <br/>
</p>
<p>
    <span class="t-li" style="text-indent: 0em; display: inline-block; width:
5em; text-align: right;">1)</span>&nbsp;Narrow multibyte string literal. The
type of an unprefixed string literal is&nbsp;<span class="t-c" style="border:
1px solid rgb(214, 214, 214); border-top-left-radius: 3px;
border-top-right-radius: 3px; border-bottom-right-radius: 3px;
border-bottom-left-radius: 3px; margin: 0px 2px; padding: 0px 2px; display:
inline-block; text-indent: 0em; background-color: rgba(0, 0, 0,
0.027451);"><span class="mw-geshi cpp source-cpp" style="font-family: monospace;
line-height: normal;"><span class="kw4" style="color: rgb(0, 0,
255);">const</span>&nbsp;<span class="kw4" style="color: rgb(0, 0,
255);">char</span><span class="br0" style="color: rgb(0, 128, 0);">[</span><span
class="br0" style="color: rgb(0, 128, 0);">]</span></span></span>
</p>
<p>
    <span class="t-li" style="text-indent: 0em; display: inline-block; width:
5em; text-align: right;">2)</span>&nbsp;Wide string literal. The type of
a&nbsp;<span class="t-c" style="border: 1px solid rgb(214, 214, 214);
border-top-left-radius: 3px; border-top-right-radius: 3px;
border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; margin: 0px
2px; padding: 0px 2px; display: inline-block; text-indent: 0em;
background-color: rgba(0, 0, 0, 0.027451);"><span class="mw-geshi cpp
source-cpp" style="font-family: monospace; line-height: normal;">L<span
class="st0" style="color: rgb(0, 128,
0);">&quot;...&quot;</span></span></span>&nbsp;string literal is&nbsp;<span
class="t-c" style="border: 1px solid rgb(214, 214, 214); border-top-left-radius:
3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px;
border-bottom-left-radius: 3px; margin: 0px 2px; padding: 0px 2px; display:
inline-block; text-indent: 0em; background-color: rgba(0, 0, 0,
0.027451);"><span class="mw-geshi cpp source-cpp" style="font-family: monospace;
line-height: normal;"><span class="kw4" style="color: rgb(0, 0,
255);">const</span>&nbsp;<span class="kw4" style="color: rgb(0, 0,
255);">wchar_t</span><span class="br0" style="color: rgb(0, 128,
0);">[</span><span class="br0" style="color: rgb(0, 128,
0);">]</span></span></span>
</p>
<p>
    <span class="t-li" style="text-indent: 0em; display: inline-block; width:
5em; text-align: right;">3)</span>&nbsp;UTF-8 encoded string literal. The type
of a&nbsp;<span class="t-c" style="border: 1px solid rgb(214, 214, 214);
border-top-left-radius: 3px; border-top-right-radius: 3px;
border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; margin: 0px
2px; padding: 0px 2px; display: inline-block; text-indent: 0em;
background-color: rgba(0, 0, 0, 0.027451);"><span class="mw-geshi cpp
source-cpp" style="font-family: monospace; line-height: normal;">u8<span
class="st0" style="color: rgb(0, 128,
0);">&quot;...&quot;</span></span></span>&nbsp;string literal is&nbsp;<span
class="t-c" style="border: 1px solid rgb(214, 214, 214); border-top-left-radius:
3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px;
border-bottom-left-radius: 3px; margin: 0px 2px; padding: 0px 2px; display:
inline-block; text-indent: 0em; background-color: rgba(0, 0, 0,
0.027451);"><span class="mw-geshi cpp source-cpp" style="font-family: monospace;
line-height: normal;"><span class="kw4" style="color: rgb(0, 0,
255);">const</span>&nbsp;<span class="kw4" style="color: rgb(0, 0,
255);">char</span><span class="br0" style="color: rgb(0, 128, 0);">[</span><span
class="br0" style="color: rgb(0, 128, 0);">]</span></span></span>
</p>
<p>
    <span class="t-li" style="text-indent: 0em; display: inline-block; width:
5em; text-align: right;">4)</span>&nbsp;UTF-16 encoded string literal. The type
of a&nbsp;<span class="t-c" style="border: 1px solid rgb(214, 214, 214);
border-top-left-radius: 3px; border-top-right-radius: 3px;
border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; margin: 0px
2px; padding: 0px 2px; display: inline-block; text-indent: 0em;
background-color: rgba(0, 0, 0, 0.027451);"><span class="mw-geshi cpp
source-cpp" style="font-family: monospace; line-height: normal;">u<span
class="st0" style="color: rgb(0, 128,
0);">&quot;...&quot;</span></span></span>&nbsp;string literal is&nbsp;<span
class="t-c" style="border: 1px solid rgb(214, 214, 214); border-top-left-radius:
3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px;
border-bottom-left-radius: 3px; margin: 0px 2px; padding: 0px 2px; display:
inline-block; text-indent: 0em; background-color: rgba(0, 0, 0,
0.027451);"><span class="mw-geshi cpp source-cpp" style="font-family: monospace;
line-height: normal;"><span class="kw4" style="color: rgb(0, 0,
255);">const</span>&nbsp;<span class="kw4" style="color: rgb(0, 0,
255);">char16_t</span><span class="br0" style="color: rgb(0, 128,
0);">[</span><span class="br0" style="color: rgb(0, 128,
0);">]</span></span></span>
</p>
<p>
    <span class="t-li" style="text-indent: 0em; display: inline-block; width:
5em; text-align: right;">5)</span>&nbsp;UTF-32 encoded string literal. The type
of a&nbsp;<span class="t-c" style="border: 1px solid rgb(214, 214, 214);
border-top-left-radius: 3px; border-top-right-radius: 3px;
border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; margin: 0px
2px; padding: 0px 2px; display: inline-block; text-indent: 0em;
background-color: rgba(0, 0, 0, 0.027451);"><span class="mw-geshi cpp
source-cpp" style="font-family: monospace; line-height: normal;">U<span
class="st0" style="color: rgb(0, 128,
0);">&quot;...&quot;</span></span></span>&nbsp;string literal is&nbsp;<span
class="t-c" style="border: 1px solid rgb(214, 214, 214); border-top-left-radius:
3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px;
border-bottom-left-radius: 3px; margin: 0px 2px; padding: 0px 2px; display:
inline-block; text-indent: 0em; background-color: rgba(0, 0, 0,
0.027451);"><span class="mw-geshi cpp source-cpp" style="font-family: monospace;
line-height: normal;"><span class="kw4" style="color: rgb(0, 0,
255);">const</span>&nbsp;<span class="kw4" style="color: rgb(0, 0,
255);">char32_t</span><span class="br0" style="color: rgb(0, 128,
0);">[</span><span class="br0" style="color: rgb(0, 128,
0);">]</span></span></span>
</p>
<p>
    <span class="t-li" style="text-indent: 0em; display: inline-block; width:
5em; text-align: right;">6)</span>&nbsp;Raw string literal. Used to avoid
escaping of any character, anything between the delimiters becomes part of the
string, if&nbsp;<span class="t-spar" style="text-indent: 0em; color: rgb(128,
128, 128); font-style: italic;">prefix</span>&nbsp;is present has the same
meaning as described above.
</p>

摘录部分C++11标准文档（标准文档对R“()”原生字符串字面值的解释更透彻，还有好几个简单易懂的例子）：

2.14.5 String literals [lex.string]
string-literal:
&nbsp; &nbsp; encoding-preﬁx_opt&quot; s-char-sequence_opt&quot;
&nbsp; &nbsp; encoding-preﬁx_opt<strong>R</strong> raw-string
encoding-preﬁx:
&nbsp; &nbsp; u8
&nbsp; &nbsp; u
&nbsp; &nbsp; U
&nbsp; &nbsp; L
s-char-sequence:
&nbsp; &nbsp; s-char
&nbsp; &nbsp; s-char-sequence s-char
s-char:
&nbsp; &nbsp; any member of the source character set except&nbsp;thedouble-quote &quot;, backslash \, or new-line character
&nbsp; &nbsp; escape-sequence
&nbsp; &nbsp; universal-character-name
raw-string:
&nbsp; &nbsp; &quot; d-char-sequence_opt( r-char-sequence_opt)d-char-sequence_opt&quot;
r-char-sequence:
&nbsp; &nbsp; r-char
&nbsp; &nbsp; r-char-sequence r-char
r-char:
&nbsp; &nbsp; any member of the source character set, except&nbsp;a rightparenthesis ) followed by the initial d-char-sequence&nbsp;(which may be empty)followed by a double quote &quot;.
d-char-sequence:
&nbsp; &nbsp; d-char
&nbsp; &nbsp; d-char-sequence d-char
d-char:
&nbsp; &nbsp; any member of the basic source character setexcept:&nbsp;space, the left parenthesis (, the right parenthesis ), thebackslash \,&nbsp;and the control characters representing horizontaltab,&nbsp;vertical tab, form feed, and newline.


<p>
    1 A string literal is a sequence of characters (as deﬁned in 2.14.3)
surrounded by double quotes, optionally&nbsp;preﬁxed by R, u8, u8R, u, uR, U,
UR, L, or LR, as in &quot;...&quot;, R&quot;(...)&quot;, u8&quot;...&quot;,
u8R&quot;**(...)**&quot;, u&quot;...&quot;,&nbsp;uR&quot;*˜(...)*˜&quot;,
U&quot;...&quot;, UR&quot;zzz(...)zzz&quot;, L&quot;...&quot;, or
LR&quot;(...)&quot;, respectively.
</p>

2 A string literal that has an R in the preﬁx is a raw string literal. Thed-char-sequence serves as a delimiter.&nbsp;The terminating d-char-sequence of araw-string is the same sequence of characters as theinitial&nbsp;d-char-sequence. A d-char-sequence shall consist of at most 16characters.

3 [ Note: The characters ’(’ and ’)’ are permitted in a raw-string. Thus,R&quot;delimiter((a|b))delimiter&quot;&nbsp;is equivalent to &quot;(a|b)&quot;.— end note ]

4 [ Note: A source-ﬁle new-line in a raw string literal results in anew-line in the resulting execution string-literal. Assuming no whitespace atthe beginning of lines in the following example, the assert will succeed:<br/>
const char *p = R&quot;(a\
b
c)&quot;;
assert(std::strcmp(p, &quot;a\\\nb\nc&quot;) == 0);
— end note ]

5 [Example: The raw string
R&quot;a(
)\
a&quot;
)a&quot;
is equivalent to &quot;\n)\\\na\&quot;\n&quot;. The raw string
R&quot;(??)&quot;
is equivalent to &quot;\?\?&quot;. The raw string
R&quot;#(
)??=&quot;
)#&quot;
is equivalent to &quot;\n)\?\?=\&quot;\n&quot;. — end example ]

**参考资料**：[Raw string literals]&nbsp;<ahref="http://www.stroustrup.com/C++11FAQ.html#raw-strings"_src="http://www.stroustrup.com/C++11FAQ.html#raw-strings">http://www.stroustrup.com/C++11FAQ.html#raw-strings</a>

___
2014.05.07

**问题描述**：为什么我发现没有capture-list的lambda表达式可以直接赋值给相同签名的函数指针？

**问题原因**：C++11标准规定，lambda表达式是一个函数对象（特指闭包对象），实现了operator()的重载。如果capture-list为空，编译器必须为该对象实现一个公有非虚非显式声明的常量运算符转换函数（publicnon-virtual non-explicit const conversion function），该转换函数返回一个与lambda表达式函数签名一致的普通函数指针，当通过该函数指针调用函数时，调用过程中发生的效果必须与直接调用函数对象的operator()一致；

**信息来源**：C++11标准文档：
5.1.2 Lambda expressions [expr.prim.lambda]

<p>
    6 The closure type for a lambda-expression with no lambda-capture has a
public non-virtual non-explicit const&nbsp;conversion function to pointer to
function having the same parameter and return types as the closure
type’s&nbsp;function call operator. The value returned by this conversion
function shall be the address of a function&nbsp;that, when invoked, has the
same eﬀect as invoking the closure type’s function call operator.
</p>

___
2014.05.07

**问题描述**：为什么在全局空间里没法定义有capture-list的lambda表达式？

**问题原因**：C++11标准规定，非块作用域内的lambda表达式不能有capture-list；

**信息来源**：C++11标准文档：
5.1.2 Lambda expressions [expr.prim.lambda]

<p>
    9 A lambda-expression whose smallest enclosing scope is a block scope
(3.3.3) is a local lambda expression; any&nbsp;other lambda-expression shall not
have a capture-list in its lambda-introducer. The reaching scope of a
local&nbsp;lambda expression is the set of enclosing scopes up to and including
the innermost enclosing function and&nbsp;its parameters. [ Note: This reaching
scope includes any intervening lambda-expressions. — end note ]
</p>

___
2014.05.07

**问题描述**：Lambda表达式对capture-list中变量的生存期有什么要求？

**解决方法**：必须是自动变量生存期；（变量生存期：auto(该关键字在c++11中已移作他用),register, static, extern, thread_local）

**信息来源**：C++11标准文档：
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<p style="margin-top: 5px; margin-right: 0px; margin-bottom: 5px; margin-left:
0px; ">
    5.1.2 Lambda expressions [expr.prim.lambda]
</p>
<p style="margin-top: 5px; margin-right: 0px; margin-bottom: 5px; margin-left:
0px; ">
    <br/>
</p>
<p style="margin-top: 5px; margin-right: 0px; margin-bottom: 5px; margin-left:
0px; ">
    10 The identiﬁers in a capture-list are looked up using the usual rules for
unqualiﬁed name lookup (3.4.1); each&nbsp;such lookup shall ﬁnd a variable with
automatic storage duration declared in the reaching scope of the
local&nbsp;lambda expression.
</p>

___
2014.05.07

**问题描述**：所有编译器都用函数对象实现Lambda表达式吗？

**解决方法**：是，这是C++11标准；

**信息来源**：C++11标准文档：

5.1.2 Lambda expressions [expr.prim.lambda]

3 The type of the lambda-expression (which is also the type of the closureobject) is a unique, unnamed non-union class type — called the closure type —whose properties are described below.<br/>


5 The closure type for a lambda-expression has a public inline function calloperator (13.5.4) whose parameters and return type are described by thelambda-expression’s parameter-declaration-clause and trailing-return-typerespectively.

___
2014.05.07

**问题描述**：在Lambda表达式中，为什么按值capture的变量，无法对其赋值？

**问题原因**：因为实现Lambda表达式的函数对象中，operator()默认是const的，即return-typeoperator () (parameter-list) const;

**解决方法**：在定义Lambda表达式时，在参数列表后加上mutable，即[capture-list](parameter-list) mutable { function-body; }

**信息来源**：C++11标准文档：
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>5.1.2Lambda expressions [expr.prim.lambda]<br/>

5 /* ... */&nbsp;This function call operator is declared const (9.3.1) ifand only if the lambda-expression’s parameter-declaration-clause is not followedby mutable.&nbsp;It is neither virtual nor declared&nbsp;volatile.

___
2014.05.07

**问题描述**：Lambda表达式的参数列表中可以有默认实参吗？

**解决方法**：不可以。

**信息来源**：C++11标准文档：
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<p style="margin-top: 5px; margin-right: 0px; margin-bottom: 5px; margin-left:
0px; ">
    5.1.2 Lambda expressions [expr.prim.lambda]<br/>
</p>
<p style="margin-top: 5px; margin-right: 0px; margin-bottom: 5px; margin-left:
0px; ">
    <br/>
</p>
<p style="margin-top: 5px; margin-right: 0px; margin-bottom: 5px; margin-left:
0px; ">
    5 /* ... */&nbsp;Default arguments (8.3.6) shall not be speciﬁed in the
parameter-declaration-clause of a lambda-declarator.
</p>

___
2014.05.30

**问题描述**：有没有办法干掉remove_if,copy_if这样带_if尾巴的算法调用？因为有些算法没有_if版本，不好记。

**解决方法**：boost range adaptors；

**信息来源**：<ahref="http://www.boost.org/doc/libs/1_46_1/libs/range/doc/html/range/reference/adaptors/introduction.html"_src="http://www.boost.org/doc/libs/1_46_1/libs/range/doc/html/range/reference/adaptors/introduction.html">http://www.boost.org/doc/libs/1_46_1/libs/range/doc/html/range/reference/adaptors/introduction.html</a>&nbsp;(RangeAdaptors are to algorithms what algorithms are to containers)

___
2014.08.13

**问题描述**：临时变量生存期只有表达式结束吗？

**解决方法**：不是。
<p>
    <span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">12.2 Temporary objects
[class.temporary]&nbsp;</span><br style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">&nbsp;&nbsp;</span><br
style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;,
Verdana, Arial, sans-serif; line-height: 18.2000007629395px; white-space:
normal; background-color: rgb(255, 255, 255);"/><span style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; background-color: rgb(255, 255, 255);">5 The
second context is when a reference is bound to a temporary. The temporary to
which the reference is&nbsp;</span><span style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">bound or the
temporary that is the complete object of a subobject to which the reference is
bound&nbsp;</span>persists&nbsp;for the lifetime of the reference<span
style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;,
Verdana, Arial, sans-serif; line-height: 18.2000007629395px; background-color:
rgb(255, 255, 255);">&nbsp;except:&nbsp;</span><br style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; white-space: normal; background-color: rgb(255,
255, 255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">— A temporary bound
to a reference member in a constructor’s ctor-initializer (12.6.2) persists
until the&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">constructor
exits.&nbsp;</span><br style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">— A temporary bound to a reference
parameter in a function call (5.2.2) persists until the completion
of&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">the full-expression
containing the call.&nbsp;</span><br style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">— The lifetime of a temporary bound to
the returned value in a function return statement (6.6.3) is
not&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">extended; the
temporary is destroyed at the end of the full-expression in the return
statement.&nbsp;</span><br style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">— A temporary bound to a reference in a
new-initializer (5.3.4) persists until the completion of the&nbsp;</span><span
style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;,
Verdana, Arial, sans-serif; line-height: 18.2000007629395px; background-color:
rgb(255, 255, 255);">full-expression containing the new-initializer.
[Example:&nbsp;</span><br style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">struct S { int mi; const
std::pair<int,int>& mp; };&nbsp;</span><br style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; white-space: normal; background-color: rgb(255,
255, 255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">S a { 1, {2,3}
};&nbsp;</span><br style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">S* p = new S{ 1, {2,3} }; // Creates
dangling reference&nbsp;</span><br style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">— end example ] [ Note: This may
introduce a dangling reference, and implementations are
encouraged&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">to issue a warning in
such a case. — end note ]&nbsp;</span><br style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">The destruction of a temporary whose
lifetime is not extended by being bound to a reference is
sequenced&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">before the
destruction of every temporary which is constructed earlier in the same
full-expression. If the&nbsp;</span><span style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">lifetime of two or
more temporaries to which references are bound ends at the same point, these
temporaries&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">are destroyed at that
point in the reverse order of the completion of their construction. In addition,
the&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">destruction of
temporaries bound to references shall take into account the ordering of
destruction of objects&nbsp;</span><span style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">with static, thread,
or automatic storage duration (3.7.1, 3.7.2, 3.7.3); that is, if obj1 is an
object with the&nbsp;</span><span style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">same storage duration
as the temporary and created before the temporary is created the temporary shall
be&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">destroyed before obj1
is destroyed; if obj2 is an object with the same storage duration as the
temporary and&nbsp;</span><span style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">created after the
temporary is created the temporary shall be destroyed after obj2 is destroyed.
[Example:&nbsp;</span><br style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">struct S {&nbsp;</span><br
style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;,
Verdana, Arial, sans-serif; line-height: 18.2000007629395px; white-space:
normal; background-color: rgb(255, 255, 255);"/><span style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; background-color: rgb(255, 255,
255);">S();&nbsp;</span><br style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">S(int);&nbsp;</span><br
style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;,
Verdana, Arial, sans-serif; line-height: 18.2000007629395px; white-space:
normal; background-color: rgb(255, 255, 255);"/><span style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; background-color: rgb(255, 255, 255);">friend S
operator+(const S&, const S&);&nbsp;</span><br style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; white-space: normal; background-color: rgb(255,
255, 255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">~S();&nbsp;</span><br
style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;,
Verdana, Arial, sans-serif; line-height: 18.2000007629395px; white-space:
normal; background-color: rgb(255, 255, 255);"/><span style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; background-color: rgb(255, 255,
255);">};&nbsp;</span><br style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">S obj1;&nbsp;</span><br
style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;,
Verdana, Arial, sans-serif; line-height: 18.2000007629395px; white-space:
normal; background-color: rgb(255, 255, 255);"/><span style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; background-color: rgb(255, 255, 255);">const
S& cr = S(16)+S(23);&nbsp;</span><br style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; white-space: normal; background-color: rgb(255, 255,
255);"/><span style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida
Sans&#39;, Verdana, Arial, sans-serif; line-height: 18.2000007629395px;
background-color: rgb(255, 255, 255);">S obj2;&nbsp;</span><br
style="font-family: 宋体, &#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;,
Verdana, Arial, sans-serif; line-height: 18.2000007629395px; white-space:
normal; background-color: rgb(255, 255, 255);"/><span style="font-family: 宋体,
&#39;Lucida Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif;
line-height: 18.2000007629395px; background-color: rgb(255, 255, 255);">the
expression S(16) + S(23) creates three temporaries: a first temporary T1 to hold
the result of the&nbsp;</span><span style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">expression S(16), a
second temporary T2 to hold the result of the expression S(23), and a third
temporary&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">T3 to hold the result
of the addition of these two expressions. The temporary T3 is then bound to the
reference&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">cr. It is unspecified
whether T1 or T2 is created first. On an implementation where T1 is created
before&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">T2, it is guaranteed
that T2 is destroyed before T1. The temporaries T1 and T2 are bound to the
reference&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">parameters of
operator+; these temporaries are destroyed at the end of the full-expression
containing the&nbsp;</span><span style="font-family: 宋体, &#39;Lucida
Grande&#39;, &#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">call to operator+.
The temporary T3 bound to the reference cr is destroyed at the end of cr’s
lifetime,&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">that is, at the end
of the program. In addition, the order in which T3 is destroyed takes into
account the&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">destruction order of
other objects with static storage duration. That is, because obj1 is constructed
before&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">T3, and T3 is
constructed before obj2, it is guaranteed that obj2 is destroyed before T3, and
that T3 is&nbsp;</span><span style="font-family: 宋体, &#39;Lucida Grande&#39;,
&#39;Lucida Sans&#39;, Verdana, Arial, sans-serif; line-height:
18.2000007629395px; background-color: rgb(255, 255, 255);">destroyed before
obj1. — end example ]</span>
</p>

**信息来源**：C++11标准文档；

___
2014.08.19

**问题描述**：std::unique(ForwardIterator first, ForwardIterator last,BinaryPredicate p)中p是“相等”还是“小于”？

**解决方法**：相等；

**信息来源**：<a href="http://en.cppreference.com/w/cpp/algorithm/unique"_src="http://en.cppreference.com/w/cpp/algorithm/unique">http://en.cppreference.com/w/cpp/algorithm/unique</a>

___
2014.08.22

**问题描述**：GoogleC++编程风格指南里，重载operator是否需要在操作符前后加空格？

**补充说明**：T operator + (const T&, const T&)还是T operator+(constT&, const T&)？

**解决方法**：不知道，没找到相关说明，Google代码里两种方式都有，但是后者数量是前者数量的8倍左右，以后都用不加空格的方式（后者）；

___
2014.08.22

**问题描述**：在ubuntu中用g++编译代码futue.get()，会报运行时错误，为什么，怎么解决？

**补充说明**：g++版本为：
<p>
    $ g++ -v<br/>Using built-in
specs.<br/>COLLECT_GCC=g++<br/>COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/4.6/lto-wrapper<br/>Target:
x86_64-linux-gnu<br/>Configured with: ../src/configure -v
--with-pkgversion=&#39;Ubuntu/Linaro 4.6.3-1ubuntu5&#39;
--with-bugurl=file:///usr/share/doc/gcc-4.6/README.Bugs
--enable-languages=c,c++,fortran,objc,obj-c++ --prefix=/usr
--program-suffix=-4.6 --enable-shared --enable-linker-build-id
--with-system-zlib --libexecdir=/usr/lib --without-included-gettext
--enable-threads=posix --with-gxx-include-dir=/usr/include/c++/4.6
--libdir=/usr/lib --enable-nls --with-sysroot=/ --enable-clocale=gnu
--enable-libstdcxx-debug --enable-libstdcxx-time=yes --enable-gnu-unique-object
--enable-plugin --enable-objc-gc --disable-werror --with-arch-32=i686
--with-tune=generic --enable-checking=release --build=x86_64-linux-gnu
--host=x86_64-linux-gnu --target=x86_64-linux-gnu<br/>Thread model:
posix<br/>gcc version 4.6.3 (Ubuntu/Linaro 4.6.3-1ubuntu5)
</p>

**补充说明**：报错信息：
terminate called after throwing an instance of&#39;std::system_error&#39;<br/> &nbsp;what(): &nbsp;Unknown error -1

**问题原因**：不知道；

**解决方法**：编译时加上-pthread就行了；

**信息来源**：<a href="https://gcc.gnu.org/ml/gcc-bugs/2010-12/msg01694.html"_src="https://gcc.gnu.org/ml/gcc-bugs/2010-12/msg01694.html">https://gcc.gnu.org/ml/gcc-bugs/2010-12/msg01694.html</a>

___
2014.08.24

**问题描述**：在写std::initializer_list<T>接口时，是该用值传递还是引用传递？

**解决方法**：值传递就行；
Initializer lists may be implemented as a pair of pointers or pointer andlength.
Copying a&nbsp;std::initializer_list does not copy the underlying objects.

**信息来源**：<ahref="http://en.cppreference.com/w/cpp/utility/initializer_list"_src="http://en.cppreference.com/w/cpp/utility/initializer_list">http://en.cppreference.com/w/cpp/utility/initializer_list</a>

___
2014.08.27

**问题描述**：在构造函数里如何使用enable_if？

**解决方法**：template <typename V, typename = typename Impl::templateEnableIfConvertibleFrom<V>> SomeCtor(const V& v);

___
2014.08.30

**问题描述**：std::future缺什么接口？

**解决方法**：std::future<int> f = std::async(...); f.then([](int a) {std::cout << a << std::endl; });

___
2014.09.10

**问题描述**：在gMock中，如何让函数有默认返回值，而不是每次都要写一遍？

**解决方法**：在Mocker类的构造函数里，写ON_Call(*this,Callable(testing::A<Param1Type>(),testing::A<Param2Type>())).WillByDefault(Return(true));

___
2014.10.08

**问题描述**：如何让std::ostream输出整数时，根据std::dec, std::oct,std::hex自动加上前缀（无、0、0x）？

**解决方法**: (#include <ios> 或 <iostream>) out <<std::showbase; out << std::hex << 15; &nbsp;// 0xf

**补充说明**：
&nbsp; &nbsp; &nbsp; &nbsp; 1. 取消可以用out << std::noshowbase;
&nbsp; &nbsp; &nbsp; &nbsp; 2. 标准流默认不显示前缀；

___
2014.12.12

**问题描述**：union类型中，如果有类类型成员变量，那该成员变量的析构函数会被调用吗？

**解决方法**：不会。

**信息来源**：C++11标准文档 >&nbsp;9.5 Unions
2(摘录) If any non-static data member of a union has a non-trivial defaultconstructor (12.1), copy constructor (12.8), move constructor (12.8), copyassignment operator (12.8), move assignment operator (12.8), or destructor(12.4), the corresponding member function of the union must be user-provided orit will be implicitly deleted (8.4.3) for the union.
4 In general, one must use explicit destructor calls and placement newoperators to change the active member of a union.

___
2014.12.12


**问题描述**：如何简单判断C++的拷贝和移动？

**解决方法**：在一行代码中为同一份数据数名字，如果有两个名字就是复制，如果有一个名字就是移动。（注：1.std::move()算做清除名字；2. 如果没有名字就是临时对象）；

___
2015.01.28

**问题描述**：C++类（默认、拷贝、移动）构造函数的自动生成规则是什么？

**解决方法**：
&nbsp; &nbsp; 1. 一个构造函数都不定义时，C() = default, C(const C&) =default, C(C&&) = delete；
&nbsp; &nbsp; 2. 定义了任何一个构造函数，其他所有构造函数都不会自动生成；

___
2015.01.28

**问题描述**：C++11中，右值引用接收函数返回的临时对象，函数调用表达式结束后，该临时对象会被立即析构吗？

**解决方法**：不会。C++11标准规定，临时对象绑定到引用（没有区分左值引用和右值引用），临时对象的生存期就都跟该引用生存期保持一致；

**参考资料**：12.2 Temporary objects
&nbsp; &nbsp; 5&nbsp;The second context is when a reference is bound to atemporary. The temporary to which the reference isbound or the temporary that is the complete object of a subobject to which thereference is bound persistsfor the lifetime of the reference except:
&nbsp; &nbsp; &nbsp; &nbsp; — A temporary bound to a reference member in aconstructor’s ctor-initializer (12.6.2) persists until theconstructor exits.
&nbsp; &nbsp; &nbsp; &nbsp; — A temporary bound to a reference parameter ina function call (5.2.2) persists until the completion ofthe full-expression containing the call.
&nbsp; &nbsp; &nbsp; &nbsp; — The lifetime of a temporary bound to thereturned value in a function return statement (6.6.3) is notextended; the temporary is destroyed at the end of the full-expression in thereturn statement.
&nbsp; &nbsp; &nbsp; &nbsp; — A temporary bound to a reference in anew-initializer (5.3.4) persists until the completion of thefull-expression containing the new-initializer. [Example:
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; struct S { int mi; conststd::pair& mp; };
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; S a { 1, {2,3} };
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; S* p = new S{ 1, {2,3} }; //Creates dangling reference— end example ] [ Note: This may introduce a dangling reference, andimplementations are encouragedto issue a warning in such a case. — end note ]

___
2015.02.13

**问题描述**：Initialization: =, (), and {}如何选择？

**解决方法**：
&nbsp; &nbsp; rule1: Use copy-initialization whenever possible:&nbsp;T var =expr. The expr can be a brace expression:&nbsp;{1, 2, 3}.
&nbsp; &nbsp; rule2: Prefer direct-initialization&nbsp;--&nbsp;T var(x, y,z)&nbsp;--&nbsp;over brace initialization&nbsp;--T var{x, y, z}.
&nbsp; &nbsp; rule3: Write your code as if most multi-argument constructorswere explicit.

**信息来源**：Roman&nbsp;Perepelitsa (Google)

___
2015.02.16

**问题描述**：C++怎么定义可变参数宏#define MACRO(...)？

**解决方法**：
#define MACRO_NAME(...) SOME_OP __VA_ARGS__

___
2015.02.16

**问题描述**：为什么想用__LINE__拼变量名name_123，结果却拼成name___LINE__？

问题代码：#define UNIQUE_NAME Type name_##__LINE__

**问题原因**：当宏定义中有#或##时，编译预处理器不会执行递归展开。而__LINE__本身是一个宏，遇到##就不会进行递归宏展开了；

**信息来源**：<ahref="http://stackoverflow.com/questions/1597007/creating-c-macro-with-and-line-token-concatenation-with-positioning-macr"_src="http://stackoverflow.com/questions/1597007/creating-c-macro-with-and-line-token-concatenation-with-positioning-macr">http://stackoverflow.com/questions/1597007/creating-c-macro-with-and-line-token-concatenation-with-positioning-macr</a>

___
2015.02.16

**问题描述**：在C++中如何实现类似其他语言中defer的功能？

**解决方法**：利用析构函数，参见刘未鹏ON_SCOPE_EXIT；

示例代码：
实现1：

#include <functional>
#include <utility>
class Defer {
&nbsp;public:
&nbsp; Defer(std::function<void()> deferred):deferred_(std::move(deferred)) {}
&nbsp; ~Defer() { deferred_(); }
&nbsp;private:
&nbsp; std::function<void()> deferred_;
};

#define DEFER_LINED_NAME(name, line) name##line
#define DEFER_OBJECT(name, line) DEFER_LINED_NAME(name, line)
#define DEFER(...) Defer DEFER_OBJECT(deferred_, __LINE__)([&]()__VA_ARGS__)

void Test3() {
&nbsp; cout << &quot;I&#39;m in.&quot; << endl;
&nbsp; DEFER({
&nbsp; &nbsp; cout << &quot;I&#39;m out.&quot; << endl;
&nbsp; });
&nbsp; DEFER({
&nbsp; &nbsp; cout << &quot;I&#39;m out, too.&quot; << endl;
&nbsp; });
&nbsp; cout << &quot;I&#39;m running.&quot; << endl;
}

实现2：Borrowed from&nbsp;Roman&nbsp;Perepelitsa (Google)

// On top of Defer defined before.

**参考资料**：<a href="http://mindhacks.cn/2012/08/27/modern-cpp-practices/"_src="http://mindhacks.cn/2012/08/27/modern-cpp-practices/">http://mindhacks.cn/2012/08/27/modern-cpp-practices/</a>

___
2015.03.03

**问题描述**：C++11中如何判断类B是类A的子类？

**解决方法**：
#include <type_traits>
static_assert(std::is_base_of<A, B>::value, &quot;error&quot;);
static_assert(std::is_base_of<A, B>(), &quot;error&quot;);

___
2015.05.12

**问题描述**：在C++11里如何模拟scoped_ptr？

**解决方法**：const std::unique_ptr；

**参考资料**：<a href="http://en.cppreference.com/w/cpp/memory/unique_ptr"_src="http://en.cppreference.com/w/cpp/memory/unique_ptr">http://en.cppreference.com/w/cpp/memory/unique_ptr</a>

___
2015.05.12

**问题描述**：如何向map<Key,UncopyableUnmovable>里插入一个不能复制、不能移动的值对象呢？

**解决方法**：m.emplace(std::piecewise_construct, std::forward_as_tuple(a),std::forward_as_tuple(b, c)));

**信息来源**：C++11培训的练习题（Justin）；

**参考资料**：<a href="http://en.cppreference.com/w/cpp/utility/pair/pair"_src="http://en.cppreference.com/w/cpp/utility/pair/pair">http://en.cppreference.com/w/cpp/utility/pair/pair</a>

___
2015.05.12

**问题描述**：在lambda中，如何以move的方式capture一个变量？

**解决方法**：
1. 在C++14中，将会被官方支持；
2. 在C++11中，
std::function<const string&()> GetStringFn(string str) {<br/>&nbsp;std::shared_ptr<string> r(new string(std::move(str)));<br/>&nbsp;return [r]() -> const string& {<br/> &nbsp; &nbsp;return*r.get();<br/> &nbsp;};<br/>}

**信息来源**：C++11培训的练习题（Justin）；

___
2015.05.29

**问题描述**：在gmock中，如何表述两个对象是同一个对象？

**解决方法**：gmock matcher: testing::Ref

___
2015.06.15

**问题描述**：如何向基类的构造函数传递一个子类的数据成员？

**解决方法**：
<pre class="prettyprint linenums prettyprinted" style="">class Derived : public
Base { public:  Derived(std::unique_ptr<SomeResource> some_resource) :
Base(some_resource.get()), some_resource_(std::move(some_resource)) {}
Derived() : Derived(std::make_unique<SomeResource>()) {} private:
SomeResource some_resource_;};</pre><br/>
**信息来源**：何子杰；

___
2015.07.01

**问题描述**：为什么C++里可以在.h文件中给定义常量而不会导致多个编译单元命名冲突？

**解决方法**：C++11 standard,&nbsp;Appendix C,&nbsp;C.1.2 Clause 3: basicconcepts,&nbsp;3.5 [also 7.1.6]
Change: A name of file scope that is explicitly declared const, and notexplicitly declared extern, hasinternal linkage, while in C it would have external linkage
Rationale: Because const objects can be used as compile-time values in C++,this feature urges programmersto provide explicit initializer values for each const. This feature allows theuser to put constobjectsin header files that are included in many compilation units.
Effect on original feature: Change to semantics of well-defined feature.
Difficulty of converting: Semantic transformation
How widely used: Seldom

**信息来源**：同事讨论；

**参考资料**：
&nbsp; &nbsp; 1. C++11 standard,&nbsp;Appendix C,&nbsp;C.1.2 Clause 3: basicconcepts,&nbsp;3.5 [also 7.1.6]
&nbsp; &nbsp; 2.&nbsp;<ahref="http://stackoverflow.com/questions/998425/why-does-const-imply-internal-linkage-in-c-when-it-doesnt-in-c"_src="http://stackoverflow.com/questions/998425/why-does-const-imply-internal-linkage-in-c-when-it-doesnt-in-c">http://stackoverflow.com/questions/998425/why-does-const-imply-internal-linkage-in-c-when-it-doesnt-in-c</a> 

___
2015.07.11

**问题描述**：C++11里有哪几种生存期（Storage Duration）？

**解决方法**：
— static storage duration
— thread storage duration
— automatic storage duration
— dynamic storage duration

**参考资料**：
&nbsp; &nbsp; 1. C++11 standard，3 Basic concepts，3.7 Storage duration；

___
2015.07.14

**问题描述**：在C++中如何应用不定长宏参数？

**解决方法**：#define SOME(...) __VA_ARGS__；

**参考资料**：<a href="https://en.wikipedia.org/wiki/Variadic_macro"_src="https://en.wikipedia.org/wiki/Variadic_macro">https://en.wikipedia.org/wiki/Variadic_macro</a>；

___
2015.07.14

**问题描述**：C++11标准中关于类特殊成员函数的生成和不生成是怎么说的？

**解决方法**：
§ 12.4.4 If a class has no user-declared destructor, a destructor isimplicitly declared as defaulted (8.4). An implicitlydeclareddestructor is an inline public member of its class.
<p>
    § 12.8.7 If the class definition does not explicitly declare a copy
constructor, one is declared implicitly. If the class
definition declares a move constructor or move assignment operator, the
implicitly declared copy constructor
is defined as deleted; otherwise, it is defined as defaulted (8.4). The latter
case is deprecated if the class has
a user-declared copy assignment operator or a user-declared destructor.
</p>
§ 12.8.9 If the definition of a class X does not explicitly declare a moveconstructor, one will be implicitly declaredas defaulted if and only if
— X does not have a user-declared copy constructor,
— X does not have a user-declared copy assignment operator,
— X does not have a user-declared move assignment operator,
— X does not have a user-declared destructor, and
— the move constructor would not be implicitly defined as deleted.
[ Note: When the move constructor is not implicitly declared or explicitlysupplied, expressions that otherwisewould have invoked the move constructor may instead invoke a copy constructor. —end note ]
<p>
    § 12.8.18 If the class definition does not explicitly declare a copy
assignment operator, one is declared implicitly. If
the class definition declares a move constructor or move assignment operator,
the implicitly declared copy
assignment operator is defined as deleted; otherwise, it is defined as defaulted
(8.4). The latter case is
deprecated if the class has a user-declared copy constructor or a user-declared
destructor.
</p>
<span style="white-space: normal;">§ 12.8.</span>20 If the definition of aclass X does not explicitly declare a move assignment operator, one will beimplicitlydeclared as defaulted if and only if
— X does not have a user-declared copy constructor,
— X does not have a user-declared move constructor,
— X does not have a user-declared copy assignment operator,
— X does not have a user-declared destructor, and
— the move assignment operator would not be implicitly defined as deleted.
<span style="white-space: normal;">§ 12.8.</span>23 A defaulted copy/moveassignment operator for class X is defined as deleted if X has:
— a variant member with a non-trivial corresponding assignment operator andX is a union-like class, or
— a non-static data member of const non-class type (or array thereof), or
— a non-static data member of reference type, or
<p>
    — a non-static data member of class type M (or array thereof) that cannot be
copied/moved because
overload resolution (13.3), as applied to M’s corresponding assignment operator,
results in an ambiguity
or a function that is deleted or inaccessible from the defaulted assignment
operator, or
</p>
— a direct or virtual base class B that cannot be copied/moved becauseoverload resolution (13.3), asapplied to B’s corresponding assignment operator, results in an ambiguity or afunction that is deletedor inaccessible from the defaulted assignment operator, or
— for the move assignment operator, a non-static data member or direct baseclass with a type that doesnot have a move assignment operator and is not trivially copyable, or any director indirect virtualbase class.

**参考资料**：C++11标准文档；

___
2015.07.26

**问题描述**：protobuf里enum类型field的default值是什么？

**解决方法**：the first value listed in the enum&#39;s type definition；

**信息来源**：protobuf文档；

___
2015.07.31

**问题描述**：在C++98中，register关键字和auto关键字作用相同？

**解决方法**：是的。register、auto和什么都不写，都表示变量有自动生存期；

**参考资料**：C++98 standard,&nbsp;3.7.2 Automatic storage duration:
1 Local objects explicitly declared auto or register or not explicitlydeclared static or extern haveautomatic storage duration. The storage for these objects lasts until the blockin which they are createdexits.

___
2015.08.06

**问题描述**：在gmock中，有没有类成员变量和无参类成员函数对应的matcher？

**解决方法**：
// Usage: Field(&Foo::number, Ge(5))
template <typename Class, typename FieldType, typename FieldMatcher>
NewFieldMatcher Field(FieldType Class::*field, const FieldMatcher&matcher);

// Usage: Property(&Foo::str, StartsWith(&quot;hi&quot;))
template <typename Class, typename PropertyTy0e, typenamePropertyMatcher>
NewPropertyMatcher Property(PropertyType (Class::*property)() const, constPropertyMatcher& matcher);

___
2015.09.22

**问题描述**：在C++11中，继承基类的构造函数时，能否改变其访问属性？

**解决方法**：不能。
class A {
public:
&nbsp; A(int) {}
};
class B : public A {
private:
&nbsp; using A::A; &nbsp;// still public.
};

**参考资料**：<ahref="http://en.cppreference.com/w/cpp/language/using_declaration"_src="http://en.cppreference.com/w/cpp/language/using_declaration">http://en.cppreference.com/w/cpp/language/using_declaration</a>:&quot;It has the same&nbsp;access&nbsp;as the corresponding baseconstructor.&quot;

___
2015.12.11

**问题描述**：在C++11中，一个右值引用为什么不能直接传给接收右值引用的函数？

**问题原因**：&quot;rvalue&quot; isn&#39;t an attribute of a type. It&#39;s anattribute of an expression.所以右值引用可以绑定到一个右值表达式上，但右值引用本身是左值。想要传给接收右值引用的函数，就要用std::move()将左值强制转换为右值；

**信息来源**：<span style="line-height: 1.6;">Billy Donahue,Google内部讨论组；</span>


___

