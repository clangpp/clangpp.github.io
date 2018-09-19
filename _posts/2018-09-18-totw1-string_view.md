# C++贴士 #1: string_view

+ 最初发布于2012-04-20
+ 作者: Michael Chastain (mec.desktop@gmail.com)
+ 更新于2017-09-18

## 什么是string_view，以及为什么你该关心？

如果需要写一个函数接受（常量）字符串为输入参数，你有四个选项：其中两个你已经知道了，另外两个你也许还不知道：

```c++
void TakesCharStar(const char* s);             // C风格
void TakesString(const string& s);             // 旧标准(C++17以前) C++风格
void TakesStringView(absl::string_view s);     // Abseil C++风格
void TakesStringView(std::string_view s);      // C++17 C++风格
```
