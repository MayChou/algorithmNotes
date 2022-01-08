

# C++ STL：vector

### 1. 定义

向量（Vector）是一个封装了动态大小数组的顺序容器（Sequence Container）。跟任意其它类型容器一样，它能够存放各种类型的对象。可以简单的认为，向量是一个能够存放任意类型的动态数组。

### 2. 特点

（1）顺序序列，可以通过元素在序列中的位置访问对应的元素

（2）动态数组  支持对序列中的任意元素进行快速直接访问，甚至可以通过指针算述进行该操作。**提供了在序列末尾相对快速地添加/删除元素的操作**。

（3）能够感知内存分配器的（Allocator-aware）容器使用一个内存分配器对象来动态地处理它的存储需求。

### 3. 使用

*先引入头文件*：

```c++
#include <vector>
using namespace std;
```

```c++
vector<double> values;//创建double类型的空vector容器
vector<double> values(20);//创建时指定元素个数，所有的元素的默认初始值为0
vector<double> values(20, 1.0);//设置默认初始值1.0

vector<int> primes {2, 3, 5, 7, 11, 13, 17, 19};//创建容器时指定初始值和元素个数
```

注意，这是一个空的 vector 容器，因为容器中没有元素，所以没有为其分配空间。当添加第一个元素（比如使用 push_back() 函数）时，vector 会自动分配内存。

*reserve()函数增加容量：*

```c++
values.reserve(20);//容器至少可以容纳20个元素
```

*push_back()函数尾部插入数据：*

```c++
string word; 
while ( cin >> word ) { 
values.push_back( word ); 
// ... 
}
```

*访问vector元素：*

典型的做法是使用vector 操作集中的begin()和 end()所返回的迭代器 iterator 
对 ：

```c++
cout << "words read are: \n"; 
 
for ( vector<string>::iterator it = text.begin(); 
    it != text.end(); ++it ) 
           cout << *it<< ' '; 
 
cout << endl;
```

iterator 是标准库中的类，它具有指针的功能 

*it;对迭代器解引用，并访问其指向的实际对象 

++it向前移动迭代器 it 使其指向下一个元素 

*插入元素：*

```c++
   values.insert(vec.begin()+i,a);//在第i+1个元素前面插入a;
```

*删除元素：*

```c++
 vec.erase(vec.begin()+2);//删除第3个元素
vec.erase(vec.begin()+i,vec.begin()+j);//删除区间[i,j-1];区间从0开始
void pop_back()://删除向量中最后一个元素
```

遍历函数：

```c++
value.at(int pos)//返回pos位置元素的引用
value.front()//返回首元素的引用
value.back()//返回末尾位置的元素
```



其他：

```c++
vec.size();//向量大小
vec.clear();//清空向量
void swap(vector&)//交换两个同类型向量的数据
a.swap(b);//a和b中数据进行整体交换
```



### 4. 注意点

**Vector作为函数的参数或者返回值时，需要注意它的写法：**

  **double Distance(vector<int>&a, vector<int>&b) 其中的“&”绝对不能少！！！**



**c++不同容器的使用场景和特性的区别：**

[(11条消息) STL中list,vector,deque,map,set区别、联系和使用场景原理_从零开始学习的ZHL的博客-CSDN博客_vector和map的原理及区别](https://blog.csdn.net/qq_22080999/article/details/81199904)



