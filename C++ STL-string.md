# C++ STL:string

### 1. 定义

之所以抛弃char*的字符串而选用C++标准程序库中的string类，是因为他和前者比较起来，不必担心内存是否足够、字符串长度等等，而且作为一个泛型类出现，他集成的操作函数足以完成我们大多数情况下(甚至是100%)的需要。我们可以用 = 进行赋值操作，== 进行比较，+ 做串联。



### 2. 使用

**引入头文件**

```c++
#include <iostream>
#include <string>
using namespace std;
```

**创建string和初始化：**

```c++
int main(){
    string s1;//默认为空字符串
    string s2 = "c plus plus";//注意string结尾没有结束标志\0
    string s3 = s2;//利用另外的字符串对其初始化
    string s4 (5, 's');//初始化为5个s
    return 0;
}
```

**字符串长度：**

```c++
string s = "http://c.biancheng.net";
int len = s.length();
```

**转换为C风格的字符串：**

然 C++ 提供了 string 类来替代C语言中的字符串，但是在实际编程中，有时候必须要使用C风格的字符串（例如打开文件时的路径），为此，string 类为我们提供了一个转换函数 c_str()，该函数能够将 string 字符串转换为C风格的字符串，并返回该字符串的 const 指针（const char*）。请看下面的代码：

```c++
string path = "D:\\demo.txt";
FILE *fp = fopen(path.c_str(), "rt");
```

注：为了使用C语言中的 fopen() 函数打开文件，必须将 string 字符串转换为C风格的字符串。

**插入字符串：**

insert() 函数可以在 string 字符串中指定的位置插入另一个字符串，它的一种原型为：

```c++
string& insert (size_t pos, const string& str);
s1.insert(5, s3);

insert(it,it2,it3)//it为原字符串的预插入位置，it2和it3为待插入字符串的首尾迭代器，用来表示串[it2,it3)将被插入在it的位置上
string str="abcxyz",str2="opq";
str.insert(str.begin()+3,str2.begin(),str2.end());
```

如果insert函数插入位置越界会产生运行异常。

**删除字符串：**

erase() 函数可以删除 string 中的一个子字符串。它的一种原型为：

```c++
string& erase (size_t pos = 0, size_t len = npos);
```

pos 表示要删除的子字符串的起始下标，len 表示要删除子字符串的长度。如果不指明 len 的话，那么直接删除从 pos 到字符串结束处的所有字符（此时 len = str.length - pos）。

有读者担心，在 pos 参数没有越界的情况下， len 参数也可能会导致要删除的子字符串越界。但实际上这种情况不会发生，erase() 函数会从以下两个值中取出最小的一个作为待删除子字符串的长度：

- len 的值；
- 字符串长度减去 pos 的值。

**提取字符串：**

substr() 函数用于从 string 字符串中提取子字符串，它的原型为：

```c++
string substr (size_t pos = 0, size_t len = npos) const;
```

pos 为要提取的子字符串的起始下标，len 为要提取的子字符串的长度。

```c++
    string s1 = "first second third";
    string s2;
    s2 = s1.substr(6, 6);
```

**字符串查找**：

find()函数：

find() 函数用于在 string 字符串中查找子字符串出现的位置，它其中的两种原型为：

```c++
size_t find (const string& str, size_t pos = 0) const;
size_t find (const char* s, size_t pos = 0) const;

if(str.find(str2)!=string::npos){
    cout<<str.find(str2)<<endl;
}
```

第一个参数为待查找的子字符串，它可以是 string 字符串，也可以是C风格的字符串。第二个参数为开始查找的位置（下标）；如果不指明，则从第0个字符开始查找。

find() 函数最终返回的是子字符串第一次出现在字符串中的起始下标。

rfind()函数：

rfind() 和 find() 很类似，同样是在字符串中查找子字符串，不同的是 find() 函数从第二个参数开始往后查找，而 rfind() 函数则最多查找到第二个参数处，如果到了第二个参数所指定的下标还没有找到子字符串，则返回一个无穷大值4294967295。

***string::npos***

string::npos是一个常数，其本身的值为-1，但是由于是unsigned_int类型，因此实际上也认为是unsigned_int类型的最大值，string::npos作为find函数失配时的返回值。

find_first_of() 函数：

find_first_of() 函数用于查找子字符串和字符串共同具有的字符在字符串中首次出现的位置。

```c++
 string s1 = "first second second third";
 string s2 = "asecond";
 int index = s1.find_first_of(s2);
```

**string 访问：**

1）通过下标访问，即直接像数组那样去访问string

```c++
string str="abcd";
for(int i=0;i<str.length();i++){
	printf("%c",str[i]);
}
```

2)通过迭代器访问

```c++
string str="abcd";
for(string::iterator it=str.begin();it!=str.end();it++){
	printf("%c",*it);
}
```

**assign函数：**

C++ string 类的成员函数，用于拷贝、赋值操作，它们允许我们顺次地把一个 string 对象的部分内容拷贝到另一个 string 对象上。

```c++
string &operator=(const string &s);　　  　　　　　　　　　　　把字符串s赋给当前字符串
string &assign(const char *s);　　　　　　　　　　　　　　　　　用c类型字符串s赋值
string &assign(const char *s,int n);　　　　　　　　　　　　　 用c字符串s开始的n个字符赋值
string &assign(const string &s);　　　　　　　　　　　　　　　  把字符串s赋给当前字符串
string &assign(int n,char c);　　　　　　　　　　　　　　　　　 用n个字符c赋值给当前字符串
string &assign(const string &s,int start,int n);　　　　　　 把字符串s中从start开始的n个字符赋给当前字符串
string &assign(const_iterator first,const_itertor last);　　把first和last迭代器之间的部分赋给字符串

v2.assign(v1.begin(), v1.end());
```

