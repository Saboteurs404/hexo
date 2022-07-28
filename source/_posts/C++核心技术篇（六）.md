## 运算符的重载

**_算术运算符的重载_**
在前面的内容中曾介绍过 string 类型的数据，它是 C++标准模板库提供的一个类。string 类支持使用加号“+”连接两个 string 对象。但是使用两个 string 对象相减却是非法的，其中的原理是 C++所提供类中重载运算符的功能。在 string 类中定义了运算符“+”和“+=”两个符号的使用方法，这种方法的实质是一种成员函数。
关键字 operator 是专门实现类算符重载的关键字。在类成员中，定义一个这样形式的函数：

```cpp
返回值类型 operator 重载的运算符（参数列表）
```

一=以 box 类为例，我们可以将加号“+”重载，之后获得一个更大的盒子。
**_重载加号运算符_**
box.h 的代码如下：

```cpp
class box{
public:
  //类成员变量
  float m_lenth;
  float m_width;
  float m_hight;
  int Number;
  //类成员函数
  box(float lenth,float width,float hight);
  box();
  box(const box& b);
  bool Compare(const box b) const;
  void ToCheck();
  void Rebuild (float lenth,float width,float hight);
  box operator+();
  };

```

在 box,cpp 中添加实现部分的代码如下；

```java
box::operator+(const box b) const{
   box box1(
   this->m_lenth+b.m_lenth;
   this->m_width+b.m_width;
   this->m_hight+b.m_hight;
   );
return box1;
}
box::box(const box& b){
this->Rebuild(b.m_lenth,b.m_width,b.m_hight);
cout<<"盒子的复制品创建"<<endl;
}
```

main.cpp 程序入口的代码如下：

```java
#include"stdafx.h"
#include"box.h"
#include<iostream>
usng std::cout;
using std::endl;
using std::cin;
int main(){
const box boxA(3.2f,3.3f,3.4f);
const box boxB(4.1f,7.132f,6.094f);
box boxC=boxA+boxB;
boxC.ToCheck();

}
```

首先创建两个 box 对象，使用 box 类定义的重载运算符加号将 boxB 作为参数传到函数中。这是产生复制对象，函数返回一个 box 对象，他的长宽高是 boxA,boxB 的和。boxC 以这个返回值初始化，调用复制构造函数，最后输出的是 boxC 的长、宽、高。

## 比较运算符的重载

除了加减乘除运算符外，比较运算符也可以被重载。根据比较运算符的运算规则，在重载时最好贴近他们的定义
**_重载比较运算符_**
box.h 的代码如下：

````java
class box{
public :
//类成员变量
float m_lenth;
float m_width;
float m_hight;
int Number;
//类成员函数：
box(float lenth,float width,float hight);
box();
box(const box& b);
bool Compare(const box b) const;
void ToCheck();
void Bebuild(float lenth,float width,float hight);
box operator+();
bool operator>(const box b) const;
bool operator <(const box b) const;
};
在box.cpp中添加实现部分的代码如下:

```java
bool box::operator>(const box b) const{
return (m_lenth>b.m_lenth)&(m_width>b.m_width)&(m_hight>b.m_hight);
}
bool box::operator<(const box b) const{
return (m_lenth<b.m_lenth)&(m_width<b.m_width)&(m_hight<b.m_hight);
}
````

程序入口 main.cpp 的代码如下：

```java
#include"stdafx.h"
#include"box.h"
#include<iostream>
using std::cout;
using std::cin;
using std::endl;
int main(){
box boxA(4.44f,3.33f,5.55f);
box boxB(14.44f,13.33f,15.55f);
box boxC(24.44f,3.33f,1.55f);
if(boxA>boxB){
cout<<"盒子A能够完全容纳盒子B"<<endl;
}
else if(boxA<boxB)
   cout<<"盒子B能够完全容纳下盒子A"<<endl;
else
cout<<"这两个盒子不能相互容纳"endl;
if(boxC>boD){
cout<<"盒子C能够完全容纳盒子D"<<endl;
}
else if(boxA<boxB)
   cout<<"盒子D能够完全容纳下盒子C"<<endl;
else
cout<<"这两个盒子不能相互容纳"endl;
return 0;
}
```

依据比较运算符的重载定义，程序共执行了 4 次比较。
除此之外，逻辑运算符、位运算符、赋值运算符（=,+=)调用运算符（即（））等都可以被重载。
赋值运算符被重载会失去原来的定义，转为重载运算符函数。在重载算符时，最好贴近将算符应用于参数、成员变量等，使算符的意义与重载的意义相近。
