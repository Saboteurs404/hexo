## 类的继承和派生
***继承***
  继承是面向对象的主要特征（此外还有封装和多态）之一，它使得一个类可以从现有类中派生，而不必重新定义一个新类。继承的实质就是用已有的数据类型创建新的数据类型，并保留已有的数据类型的特点，以旧类为基础创建新类，新类包含了旧类的数据成员和成员函数，并且可以在新类中添加新的数据成员和成员函数。旧类被称为基类或父类，新类被称为派生类或子类
  ***类的继承***
  类的继承形式如下：
```cpp
class 派生类的形式如下：[继承方式] 基类名标识符
{
[访问控制修饰符：]
[成员声明列表]
};
```
继承方式有3种派生类型，分别为public ,protected,private,访问控制修饰符也是这三种类型，成员声明列表中包含类的成员变量及成员函数，是派生类新增的成员。“：”是一个运算符，表示基类和派生类之间的继承关系
例如：定义一个继承员工类的操作员类：
定义一个员工类，它包含员工ID、工姓名、所属部门等信息。

```cpp
class CEmployee    //定义员工类
{
public:
   int m_ID;
   char m_Name[128];
   char m_Depart[128];
   
};
```
定义一个操作员类，通常操作员属于公司的员工，它包含员工ID、员工姓名、所属部门等信息，此外还包含密码信息、登录方法等

```cpp
class COperator:public CEmployee  //定义一个操作员类
{
public:
   char m_Password[128];
   bool Login();
   };
```
操作员类是从员工类派生的一个新类，新类增加了密码信息、登陆方法等，员工ID、员工姓名等信息直接从员工类中继承得到
*类的继承*

```cpp
#include<iosteram>
using namespace std;
class CEmployee{
public :
int m_ID;
char m_Name[128];
char m_Depart[128];
CEployee(){
memset(m_Name,0,128);
memset(m_Depart,0,128);
}
void OutputName(){
cout<<"员工姓名"<<m_Name<<endl;
}
};
class COperator:public CEmployee{
public:
 char m_Password[128];
 bool Login(){
 if(strcmp(m_Name,"MR"))==0&&strcmp(m_password,"KJ")==0)//比较用户名和密码

 {
 cout<<"登录成功！"<<endl;
 return true;
 }
 else {
 cout<<"登录失败！"<<endl;
 return false;
     }
   }
 };
int main(int argc,char* argv[]){
 COprator optr;
 strcpy(optr.m_Name,"MR");
 strcpy(optr.m_Password,"KJ" );
 optr.Login();
 optr.OutputName();
 return 0;
 }
```
用户在父类中派生子类时，可能存在一种情况，即在子类中定义了一个与父类同名的成员函数，此时称为子类隐藏了父类的成员函数。例如，重新定义COperator类，添加一个OutputName成员函数。
***类的可访问性***
类的特点之一就是具有封装性，封装在类里面的数据可以设置成对外可见或不可见，通过关键字public、private、protected说明可以设置数据成员对外是否可见，也就是其他类是否可以访问该数据成员。
***public属性的成员对外可见对内可见
private属性成员对外不可见，对内可见
protected属性成员对外可见，对内可见，且对派生类是可见的
如果在类的定义的时候没有加任何关键字，那么默认状态类成员都在private区域***
例如：在头文件person.h 中，有如下代码：

```cpp
class CPerson{
int m_iIndex;
int getIndex(){
return m_iIndex;}
int setIndex(int iIndex){
m_iIndex=iIndex;
return 0;
}
};
```
实现文件person.cpp的代码如下：

```cpp
#include<iostream.h>
#include"person.h"
void main(){
CPerson p;
p.m_iIndex=100;  //错误
cout<<"m_iIndex is:"<<p.getIndex()<<endl;  //错误
//如果在类的定义的时候没有加任何关键字，那么默认状态类成员都在private区域
```
有了不同的区域，开发人员便可以根据需求来进行封装，将不想让其他类访问和调用的类成员定义在private和protected区域，
这就保证了类成员的隐蔽性，需要注意的是，如果将成员的属性设置为protected，那么继承类也可以访问父类的保护成员，但是不能访问类中的私有成员。
关键字的作用范围是直到下一次出现另一个关键字为止，例如：

```cpp
class CPerson {
private:
int m_iIndex;
public :
int getIndex(){return m_iIndex;}
int setIndex(int iIndex){
    m_iIndex=iIndex;
    return 0;
    }
 };
    
```
在上面的代码中，使用private访问权限控制符设置m_iIndex成员变量为私有，使用public关键字将其下面的成员函数设置为公有，从中可以看出private的作用域到public出现时为止。
***继承后可访问性***
继承有public、private、protected这三种继承方式，其说明如下：
（一）共有型派生
共有型派生表示对于基类中的数据成员和成员函数，在派生类中任然是public，对于基类中的private数据成员和成员函数，在派生类中仍然是private。

```cpp
class CEmployee{
public :
   void Output(){
   cout<<m_ID<<endl;
   cout<<m_Name<<endl;
   cout<<m_Depart<<endl;
   }
private:
   int m_ID;
   char m_Name[128];
   char m_Depart[128];
   };
   class COperator:public CEmployee{
      void Output(){
        cout<<m_ID<<endl;    //引用基类私有成员，错误
        cout<<m_Name<<endl;   //引用基类私有成员，错误
        cout<<m_Depart<<endl;   //引用基类私有成员，错误
        cout<<m_Password<<endl;
        }
private:
     char m_Password[128];
     bool Login();
     };
     
```
CEmployee类无法继续访问COperator类中的private数据成员m_ID、m_Name和m_Depart,如果将COperator类中的所有程序都设置为public后，CEmployee类才能访问COperator类中所有成员。
（二）、私有型派生
私有型派生表示对于基类中的public、protected数据成员和成员函数，在派生类中可以访问。在派生类中不可以访问基类中的private数据成员，例如：

```cpp
class CEmployee{
public:
    void Output(){
    cout<<m_ID<<endl;
    cout<<m_Name<<endl;
    cout<<m_Depart<<endl;
    }
    int m_ID;
protected:
    char m_Name[128];
private: 
    char m_Depart[128];
 };
 
 class COperator :private CEployee{
    void Output(){
    cout<<m_ID;
    cout<<m_Name<<endl;
    cout<<m_Depart<<endl;   //错误
    cout<<m_Password<<endl;
    }
private:
    char m_Password[128];
    bool LOgin();
    };



```
(三)、保护型派生
   保护型派生表示对于基类中的public、protect数据成员和成员函数，在派生类中均为protected。protected类型在派生类的定义时可以被访问，用派生类声明的对象不能被访问。protected成员可以被基类的所有派生类使用，这一性质可以沿着继承树无限向下传播。
   因为保护型派生的派生类得内部数据不能被随意修改，该类得维护部分只有在内部运行，这就起到了很好的封装作用。把一个类分为两部分，一部分是公共的，另一部分是保护的，保护成员对于使用者来说是不可见的，也是不需要了解的，这就减少了类与其他代码的关联程度。类的功能是独立的，他不依赖于应用程序的运行环境，既可以放到这个程序中使用，也可以放到另一个程序中使用。这就能够非常容易地用一个类替换另一个类。类访问限制的保护机制使人们编制的应用程序更加可靠和已维护。
   ***构造函数访问顺序***
   父类和子类中都有构造函数和析构函数，那么子类对象在创建时是父类先进行构造，还是子类先进行构造？同样在子类对象释放时，是父类先进行释放，还是子类先进行释放？这都是有先后顺序的。答案是当从父类派生一个子类并声明一个子类的对象是时，它将先调用父类的构造函数，然后调用当前类的构造函数来创建对象；在释放子类对象时，先调用的是当前类的析构函数，然后是父类的析构函数。
   **构造函数访问顺序**
   

```cpp
#include"stdafx.h"
#include<iostream>
using namespace std;
class CEmployee{
public: 
  int m_ID;
  char m_Name[128];
  char m_Depart[128];
  CEmployee(){
  cout<<"CEmployee类的构造函数被调用"<<endl;
  }
  ~CEmployee(){
  cout<<"CEmployee类析构函数被调用"<<endl;
  }
  };
  class COperator:public CEmployee{
  public:
    char m_Password[128];
    COperator(){
    strcpy(m_Name,"MR");
    cout<<" COperator类的构造函数被调用了"<<endl;
    }
    ~ COperator(){
    cout<<" COperator类析构函数被调用了"<<endl;
    }
 };
 int main(int argc ,char* argv[]){
   COperator optr;
   return 0;
   }
    
```
在分析完对象的构建、释放过程后，会考虑这样一种情况：定义一个基类类型的指针，调用子类的构造函数为其构建对象，当对象释放时，需要调用父类的析构函数还是先调用子类的析构函数，在调用父类的析构函数呢？
  答案是如果析构函数是虚函数，就先调用子类的析构函数，然后再调用父类的析构函数；如果析构函数不是虚函数，就只调用父类的析构函数。
  可以想象，如果子类中某个数据成员在堆中分配了空间，父类中的析构函数就不是虚成员函数，将使子类的析构函数不能被调用，其结果是对象不能被正确释放，导致内存泄漏。因此，在编写类的析构函数时，析构函数通常是虚函数。构造函数调用顺序不受基类在成员初始化表中是否存在以及被列出的顺序影响。
  
  
