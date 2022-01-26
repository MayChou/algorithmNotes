# C++: 常用技巧

### fill函数：

fill函数可以为数组或者vector中的每个元素赋以相同的值，通常用于初始化。

```c++
#include <algorithm> //fill函数包含在这个头文件之中
fill(v,v+10,-1);//给数组元素赋值-1

std::vector<string> data {12}; // Container has 12 elements
std::fill (std::begin (data), std::end (data), "none"); // Set all elements to "none"
```

### c++11新特性：循环

正常我们想要输出一个数组的全部元素时，需要采用以下的方法：

```c++
//随机定义的数组
int array[10] = { 54, 23, 78, 9, 15, 18, 63, 33, 87, 66 };

for (int i = 0; i < 10; i++) {
	cout << array[i] << " ";		//输出：54 23 78 9 15 18 63 33 87 66
}
```

在C++11中，我们可以在for循环**填加冒号 :** 来简化这一过程：

```c++
//随机定义的数组
int array[10] = { 54, 23, 78, 9, 15, 18, 63, 33, 87, 66 };
	
for (auto a : array) {
	cout << a << " ";		//输出：54 23 78 9 15 18 63 33 87 66
}
```

