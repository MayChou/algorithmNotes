# C++: 常用技巧

### fill函数：

fill函数可以为数组或者vector中的每个元素赋以相同的值，通常用于初始化。

```c++
#include <algorithm> //fill函数包含在这个头文件之中
fill(v,v+10,-1);//给数组元素赋值-1

std::vector<string> data {12}; // Container has 12 elements
std::fill (std::begin (data), std::end (data), "none"); // Set all elements to "none"
```

