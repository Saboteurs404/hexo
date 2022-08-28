***除法运算符的用法***
Java中的除法运算符相比较其他运算符来说有对点特殊，在这里将分为两种情况依次说明其用法，当两个操作数是int类型时的相除
例如：

```java
int i=11/2;
```

//结果是5，因为i是整数，所以除法运算的结果会省略后面的小数点
当两个操作数时float或者double类型时，就是正常的除法运算了，
例如：

```java
double i=9.8;
double j=3.2;
double result=i/j;
System.out.println(result);//此时result的值为3.0625；
**
```

*取模运算符的用法***
取模运算也叫取余，求余的字面意思就是求被除数除以除数，整数后还余下多少？
用法如下：

```java
int i=11%2;
//这里i=1;表示11被2整除5次还余1.    
//求余的正负号说明：主要是取决于前面一个数是正数还是负数，不管后面数。如下：    
int i=-11%2;//这里i=-1    
int i=10%2;//这里i=0;就是10被2刚好整除5次，没有余数。
```

```java
package step1;import java.util.Scanner;
public class Cal {   
 public static void main(String[] args) {        
 /*********start*********/     
        Scanner scan = new Scanner(System.in);       
        System.out.println("请输入第一个整数");        
        int a=scan.nextInt();        
        System.out.println("请输入第二个整数");     
        int b=scan.nextInt();   
        System.out.println("两数相加的结果为："+ (a+b));   
        System.out.println("两数相减的结果为："+ (a-b));
        System.out.println("两数相乘的结果为："+ (a*b));
        System.out.println("两数相除的结果为："+ (a/b));
        System.out.println("两数取余数的结果为："+ (a%b));       
   }
}

```
***运算符的说明***

 1. ==      :   检查如果两个操作数的值是否相等，去过相等则条件为真。
 2. ！=    ：  检查如果两个操作数的值是否相等，如果之不相等则条件为真
 3. >   ：  检查如果两个操作数的值是否大于右侧操作数的值，如果是，那么条件为真
 4. <    ：   检查左侧操作数的值是否小于右操作数的值，如果是那么操作数为真
 5. >=   ：   检查左操作数的值是否大于或等于右侧操作数的值，如果是那么条件为真
 6. <=    ：   检查左操作数的值是否小于或等于右侧操作数的值，如果是那么条件为真
 
