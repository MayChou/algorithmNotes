# C++ STL：set

### 1. 定义

set 容器内的元素会被自动排序，set 与 map 不同，set 中的元素即是键值又是实值，set 不允许两个元素有相同的键值。不能通过 set 的迭代器去修改 set 元素，原因是修改元素会破坏 set 组织。当对容器中的元素进行插入或者删除时，操作之前的所有迭代器在操作之后依然有效。

set里面每个元素只存有一个key值，它支持高效的关键字查询操作，比如检查一个关键字是否在set中。如果这个key值之前存在的话就不插入。



### 2. 使用

使用前加入头文件：

```c++
#include <set>
using namespace std;
```

**创建set和初始化:**

```c++
set<string> myset;
set<int> b(a); // 定义并用集合a初始化集合b
set<int> b(a.begin(), a.end()); // 将集合a中的所有元素作为集合b的初始值
```

**插入函数：**

```c++
// 在容器中插入元素
	st.insert(4);
	// 任意位置插入一个元素
	set<int>::iterator it = st.begin();
	st.insert(it, 2);
```

**删除元素：**

```c++
st.pop_back(const T& elem);//删除容器中值为 elem 的元素
st.erase(it);//it为所需要删除元素的迭代器
st.erase(st.find(200));//就是利用迭代器，利用find()函数找到100，然后利用erase删除它
st.erase(value);//value为所需要删除元素的值
st.erase(iterator first, iterator last);//删除区间 [first,last] 之间的所有元素
st.clear();//清空所有元素：
```

**通过键值访问函数**

查找键 key 是否存在,若存在，返回该键的元素的迭代器；若不存在，返回`set.end()`

```c++
#include <iostream>
#include <set>

using namespace std;

int main(int argc, char* argv[])
{
	set<int> st;
	for (int i = 0; i < 6; i++)
		st.insert(i);

	// 通过find(key)查找键值
	set<int>::iterator it;
	it = st.find(2);
	cout << *it << endl; // 输出：2

	return 0;
}
```

**交换两个set的值：**

```c++
swap(set&, set&);或lst.swap(set&);
st1.swap(st2);
```

**迭代器和常用算法：**

- 开始迭代器指针：`st.begin();`
- 末尾迭代器指针：`st.end();` // 指向最后一个元素的下一个位置
- 指向常量的开始迭代器指针：`st.cbegin();` // 意思就是不能通过这个指针来修改所指的内容，但还是可以通过其他方式修改的，而且指针也是可以移动的。
- 指向常量的末尾迭代器指针：`lst.cend();`
- 反向迭代器指针，指向最后一个元素：`st.rbegin();`
- 反向迭代器指针，指向第一个元素的前一个元素：`st.rend();`
- 返回最后一个 key<=keyElem 元素的迭代器：`st.lower_bound(keyElem);`
- 返回第一个 key>keyElem 元素的迭代器： `st.upper_bound(keyElem);`
- 返回容器中 key 与 keyElem 相等的上下限的两个迭代器，这两个迭代器被放在对组（pair）中： `st.equal_range(keyElem);`

该方法返回一个 pair 对象（包含 2 个双向迭代器），其中 pair.first 和 lower_bound() 方法的返回值等价，pair.second 和 upper_bound() 方法的返回值等价。也就是说，该方法将返回一个范围，该范围中包含的值为 val 的元素（set 容器中各个元素是唯一的，因此该范围最多包含一个元素）。

**遍历元素：**

注意set只能通过迭代器（iterator）访问。

```c++
set<int>::iterator it;
for (it = st.begin(); it != st.end(); it++)
    cout << *it << endl;
```

### 3. 注意点

- set 不支持 resize() 函数；
- set 容器不提供下标操作符。为了通过键从 set 中获取元素，可使用 find 运算；
- set 只能使用insert的两种重载函数插入，不支持 push_back() 和 push_front() 函数；
- set 不支持 STL 里的 reverse 和 sort 算法；
- set 能不通过迭代器，只通过元素值来删除该元素；

