

# C++ 技巧和知识点

### 1. 结构体构造函数：

默认构造函数：不用特地写构造函数，直接整体赋值。

```c++
#include <stdio.h>
//使用默认构造函数 
struct student {
	int id;
	char gender;
        student(){} //默认构造函数一般不可见，此处专门写出
}pig;  //能不经初始化就定义变量 

int main(){
	pig = {23,'F'};//使用该语句必须整体赋值，不能单独赋值
	printf("pig ID = %d\npig Gender = %c",pig.id,pig.gender);
	return 0;
}
```

```cpp
#include <stdio.h>
//使用自定义构造函数 
struct student {
	int id;
	char gender;

	//自定义构造函数 
	//可以同时初始化id和gender 
	student(int _id, char _gender) : id(_id), gender(_gender){} 
	//也可以单独初始化gender
	student(char _gender) : gender(_gender){} 
};  //不能不经初始化就定义变量 

int main(){
	student pig = student(23,'F');//定义变量，同时赋值
	student Pig = student('M'); //定义变量，单独赋值 
	printf("pig ID = %d\npig Gender = %c\n\n",pig.id,pig.gender);
	printf("Pig ID = %d\nPig Gender = %c",Pig.id,Pig.gender);
	return 0;
}
```

