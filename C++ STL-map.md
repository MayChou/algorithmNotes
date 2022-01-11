# C++ STL:map

### 1. 定义

C++ 中 map 提供的是一种键值对容器，里面的数据都是成对出现的,如下图：每一对中的第一个值称之为关键字(key)，每个关键字只能在 map 中出现一次；第二个称之为该关键字的对应值。

### 2. 特性

自动建立key － value的对应。key 和 value可以是任意你需要的类型，包括自定义类型。

### 3. 使用

**引入头文件：**

```c++
#include <map>
using namespace std;
```

**创建：**

```c++
map<int ,string> person;
```

可以对模版进行类型定义使其使用方便

```c++
typedef map<int , string> MAP_INI_STRING;
MAP_INI_STRING person;
```

**插入数据：**

1) insert 函数插入 pair 数据

```c++
mapPerson.insert(pair < int,string > (1,"Jim"));
```

pair是将2个数据组合成一组数据，当需要这样的需求时就可以使用pair，如stl中的map就是将key和value放在一起来保存。另一个应用是，当一个函数需要返回2个数据的时候，可以选择pair。 

2)insert 函数插入 value_type 数据

```c++
mapPerson.insert(map < int, string > ::value_type (2, "Tom"));
```

每个STL中的类都有value_type这种东西，通俗的说value_type 就是stl容器盛装的数据的数据类型

3)用数组方式插入数据

```c++
mapPerson[3] = "Jerry";
```

**遍历数据：**

三种常见迭代方法：

1）前向迭代器

```c++
map < int ,string > ::iterator it;
    map < int ,string > ::iterator itEnd;
    it = mapPerson.begin();
    itEnd = mapPerson.end();
    while (it != itEnd) {
	cout<<it->first<<' '<<it->second<<endl;  
	it++;
}
```

2）反向迭代器

反向迭代器是一种反向遍历容器的迭代器。也就是，从最后一个元素到第一个元素遍历容器。反向迭代器将自增（和自减）的含义反过来了：对于反向迭代器，++ 运算将访问前一个元素，而 -- 运算则访问下一个元素。

回想一下，所有容器都定义了 begin 和 end 成员，分别返回指向容器首元素和尾元素下一位置的迭代器。容器还定义了 rbegin 和 rend 成员，分别返回指向容器尾元素和首元素前一位置的反向迭代器。

![](https://github.com/MayChou/algorithmNotes/tree/main/pictures/1.jpg)

