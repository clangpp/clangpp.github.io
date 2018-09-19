# C++贴士 #1: string_view

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

一个`string_view`类型的变量可以被想象成一个“镜像”，映射了一段已经存在的字符列表。更明确地说，一个`string_view`仅仅包含一个指针和一个长度，用以定位一个字符数据区间。`string_view`既不拥有这些数据，又不能修改这段存储。因此，复制`string_view`是浅拷贝，字符串数据不会被复制。

`string_view`可以从`const char*`和`const string&`隐式构造而成。又因为`string_view`不会复制字符串，构造`string_view`不会有`O(n)`的内存代价。以`const string&`构造`string_view`时，构造函数时间复杂度为`O(1)`。以`const char*`构造`string_view`时，构造函数会自动调用`strlen()`（或者你可以用双参形式的`string_view`构造函数）。

```c++
void AlreadyHasString(const string& s) {
  TakesStringView(s); // 没有显式类型转换；方便！
}

void AlreadyHasCharStar(const char* s) {
  TakesStringView(s); // 没有复制；高效！
}
```
