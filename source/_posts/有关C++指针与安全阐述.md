**文件目录**

# 一、内存的分配方式

## 1、堆与栈

在程序中定义一个变量，他的值会被放入内存中，如果没有申请动态分配，它的值将会被放入栈中。栈中的变量所属的内存大小是无法改变的，他们的产生与消亡也与变量定义的位置和存储方式有关.堆是一种与栈相对应的动态分配方式的内存。当我们申请使用动态分配方式存储某个变量时，这个变量就会被放入堆中，根据需要，这个变量的内存大小可以发生改变，内存申请和销毁的时机则由编程者来操作。

## 2、关键字 new 与 dalete

在获取变量之前，编译器并没有获取到变量的名称，而只是具有指向该变量的指针。这时申请变量的堆内存即是申请自身指向堆。new 是 c++语言中申请动态内存的关键字，形如：

```csharp
int* PI=new int;
```

这样，PI 指针就申请了动态方式，使用它在堆内申请内存存储 int 型的值。
**_例;动态分配空间_**

```csharp
#include"stdafx.h"
#include<iostream>
using namespace std;
int main(){
int* PI1=NULL;
PI1=new int;   //申请动态分配
*PI=111；  //动态分配内存存储的内容变成111的整型变量
cout<<"PI内存的内容"<<*PI<<",PI所指向的地址"<<PI1<<endl;
int* PI2;
//*PI2=222;  //直接赋值会导致错误！！！
int k;   //栈中的变量
PI2=&k;  //分配栈内存
*PI2=222;   //分配内存后方可赋值
cout<<"PI内存的内容"<<*PI2<<",PI所指向的地址"<<PI2<<endl;
return 0;
}
```

从程序中可以看出，指针 PI1 被创建后就申请了动态分配，程序自动给它分配了一块堆内存。而指针 PI2 则是获取了栈中的内存地址，属于静态分配。
动态分配方式虽然很灵活，但是也带来了新的问题。当申请一块堆内存后，系统不会在程序执行时依据情况自动销毁它，若想释放该内存空间，则需要使用关键字 delete。
**_例：动态内存的销毁_**

```cpp
#include"stdafx.h"
#include<iostrteam>
using std::cout;
using std::endl;
int* newPointerGet(int* p1){
int k1=55;
p1=new int ;
*p1=k1;
return p1;
}
int* PointerGet(int *p2){
int k2=55;
p2=&k2;
return p2;
}
int main(){
cout<<"输出函数各自返回指针所指向的内存的值"<<endl;
int* p=NHLL;
p=newPointerGet(p);
int* i=NULL;
i=PointerGet(i);
cout<<"newGet:"<<*P<<",get:"<<*i<<endl;
cout<<"i所指向的内存没有被立即销毁，执行一个输出语句后：”<<endl;
cout<<"newGet:"<<*P<<",get:"<<*i<<endl;
delete p;
cout<<"销毁堆内存后："<<endl;
cout<<"*p:"<<*p<<endl;
return 0;
}

```

从程序可知，变量 p 接收 newGet 返回指针的堆内存地址，所以内存的内容并没被销毁，而栈内存则由系统控制。程序最后使用 delete 语句释放堆内存。

# 内存安全

指针是 c++提供的强大而又灵活的工具，如何安全地使用它们是编程者必须掌握的技能之一。前面我们已讨论过指针所指向内存的销毁问题，当一块内存被销毁时，该区域不可复用。若有指针指向该区域，则需要该指针置为空值（NULL）或者之相未被销毁的内存。
内存销毁实质上是系统判定该内存不是编程人员正常使用的空间，系统也会将他分配给别的任务，若擅自使用被销毁内存的指针更改该内存的数据，则可能会造成意想不到的后果。
**_例：被销毁的内存_**

```cpp
#include"stdafx.h"
#include<iostream>
using std::cout;
using std::endl;
int* sum(int a,int b){
int* ps=NULL;
int c=a+b;
ps=&c;
return ps;
}
int main(){
int* pi=NULL;
int k1=3;
int k2=5;
pi=sum(k1,k2);
cout<<"*pi的值："<<*pi<<endl;
cout<<"也许*pi还保留着i的值，但它已经被程序认定为销毁"<<endl;
cout<<"*pi的值："<<*pi<<endl;
cout<<"尝试修改*pi"<<endl;
*pi=3;
for(int i=0;i<3;i++){
cout<<"修改被销毁的内存后*pi的值："<<*pi<<endl;
}
}
```

从程序可知，指针 PI 从 sum 函数中得到了一个临时指针，该指针是指针 ps 的临时复制品，操作完成后就消失，而它做保留的地址交给了 pi。在函数 sum 执行完毕后，该域使用栈内存会被系统销毁或者挪用。本程序尝试通过 pi 继续使用、修改它，结果是系统会再次销毁它。在某些场合下，该程序也会引起内存报错，甚至造成多个系统崩溃。所以对于栈内存的指针一定要明白其何时被销毁，不再重复利用它。
于此相对应的另一个安全问题是内存泄漏。如我们所知，在申请动态分配内存后，系统不会主动销毁该堆内存，而需要编程者使用 delete 关键字通知系统销毁。如果不这样做，系统将浪费很多资源，是程序执行时变得臃肿，如只需占用数十 MB 内存的程序可能为此占用上百 MB 的内存。可见，回收堆内存空间是很有必要的。销毁内存时，需要保留指向该堆内存的指针。当没有指针指向一块没被回收的堆内存时，此块内存犹如丢失一般，我们称之为内存
**_例：丢失的内存_**

```cpp
//******这是一个反例，它会造成内存泄漏**********//
#include"stdafx.h"
#include<iostream>
using namespace std;
int main(){
float* pf=NULL;
pf=new float;
*pf=4.321f;
float f2=5.321f;
cout<<"pf指向的地址"<<pf<<endl;
cout<<"*pf的值："<<*pf<<endl;
pf=&pf;
cout>>"pf指向了f2的地址："<<pf<<endl;
if(*pf>5){
cout<<"*pf的值："<<*pf<<endl;
}
return 0;
}
```

程序中动态分配的内存开始有 pf 指向，当 pf 改变指向后，此块内存就再也无法回收了。
一般情况下，我们无法通过调试程序发现内存泄漏。所以，使用动态分配时一定要注意形成良好习惯
**_例：回收动态内存的一般处理步骤_**

```cpp
#include"stdafx.h"
#include<iostream>
void swap(int* a,int* b){
   int temp=*a;
   *a=*b;
   *b=temp;
}
int main(){
int* pi=new int;
*pi=3;
int k=5;
swap(pi,&k);
std::cout<<"*pi:"<<*pi<<std::end;   //使用std命名空间
std::cout<<"k:"<<k<<std::endl;
delete pi;    //回收动态内存
pi=NULL;   //将pi置空，防止使用已销毁的内存。不可与上一语句颠倒，否者将造成内存泄漏
return 0;
}
```
