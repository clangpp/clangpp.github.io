# C++贴士 #1: string_view

+ 原文链接: https://abseil.io/tips/1
+ 最初发布于2012-04-20
+ 作者: Michael Chastain (mec.desktop@gmail.com)
+ 更新于2017-09-18

## 什么是string_view，以及为什么你应该关心？

如果需要写一个函数接受（常量）字符串为输入参数，你有四个选项：其中两个你已经知道了，另外两个你也许还不知道：

```c++
void TakesCharStar(const char* s);             // C风格
void TakesString(const string& s);             // 旧标准(C++17以前) C++风格
void TakesStringView(absl::string_view s);     // Abseil C++风格
void TakesStringView(std::string_view s);      // C++17 C++风格
```

当函数调用时已经有对应格式的字符串存在，前两种方式最适合；但如果需要类型转换时怎么办（从`const char*`转换为`string`，或反之）？

将`string`转换为`const char*`需要（高效但不方便的）函数`c_str()`：

```c++
void AlreadyHasString(const string& s) {
  TakesCharStar(s.c_str());               // 显式转换
}
```

Callers needing to convert a const char* to a string don’t need to do anything additional (the good news) but will invoke the creation of a (convenient but inefficient) temporary string, copying the contents of that string (the bad news):

将`const char*`转换为`string`不需要额外操作（好消息），但会（方便但低效地）创建一个临时字符串，拷贝原来字符串的内容（坏消息）：

```c++
void AlreadyHasCharStar(const char* s) {
  TakesString(s); // 编译器会复制一份s
}
```

## 怎么解决？

Google推荐使用`string_view`来接受字符串参数。这个类型比C++17要早——在C++17环境中你应该使用`std::string_view`，在非C++17环境中你应该使用`absl::string_view`。

一个`string_view`类型的变量可以被想象成一个“镜像”，映射了一段已经存在的字符列表。更明确地说，一个`string_view`仅仅包含一个指针和一个长度，用以定位一个字符数据区间。`string_view`既不拥有这些数据，又不能修改这段存储。因此，复制`string_view`是浅拷贝，字符串内容不会被复制。

`string_view`可以从`const char*`和`const string&`隐式构造而成。又因为`string_view`不会复制字符串，构造`string_view`不会有`O(n)`的内存代价。以`const string&`构造`string_view`时，构造函数时间复杂度为`O(1)`。以`const char*`构造`string_view`时，构造函数会自动调用`strlen()`（或者你可以用双参形式的`string_view`构造函数）。

```c++
void AlreadyHasString(const string& s) {
  TakesStringView(s); // 没有显式类型转换；方便！
}

void AlreadyHasCharStar(const char* s) {
  TakesStringView(s); // 没有复制；高效！
}
```

因为`string_view`不拥有其指向的数据，所以`string_view`（就像`const char*`）指向的字符串需要有超出该`string_view`的生存期。这意味着存储`string_view`总是需要问个问题：你得证明`string_view`指向的数据的生存期超出`string_view`的生存期

如果你的API只需要在单次函数调用中使用字符串数据，且不需要修改该字符串数据，（让函数（译者注））接收一个`string_view`就足够了。如果你需要修改数据或在以后访问数据，那么你需要用`string(my_string_view)`将`string_view`显式转换为C++字符串。

向现有代码库中添加`string_view`并不总是正确的事：如果在函数内需要将字符串以`string`或以[`NULL`](https://baike.baidu.com/item/NULL/19660386)结尾的`const char*`传给下一级函数，那么将本级函数参数改为`string_view`可能会是低效的。对于`string_view`，推荐先在工具代码中采用，进而逐步向其调用端推广；或者在全新项目中统一使用`string_view`。

## 附加说明

+ 与其他字符串类型不同，`string_view`应该像`int`或`double`那样按值传递（相对于按引用、指针传递，译者注），因为`string_view`对象本身只占用很小的内存。

+ `string_view`指向的字符串未必以`NULL`字符结尾。因此，如下的写法是不安全的：
  ```c++
  printf("%s\n", sv.data()); // 别这样写
  ```
  然而，如下写法是可以的：
  ```c++
  printf("%.*s\n", static_cast<int>(sv.size()), sv.data());
  ```

+ 你可以像打印`string`或`const char*`一样直接打印`string_view`：
  ```c++
  std::cout << "Took '" << s << "'";
  ```

+ 在大部分情况下，你可以安全地将现有函数的`const string&`或`NULL`结尾的`const char*`类型的形参直接转换为`string_view`。我们见过的唯一例外是，如果将函数地址赋值给某函数指针，那么会遇到“函数指针类型不匹配”的编译错误。
