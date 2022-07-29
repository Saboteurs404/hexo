## 二维数组的使用

二维数组是指以一维数组作为元素的数组。
语法：数据类型[行][列]数组名。
二维数组的初始化
静态:例如：

```java
int[][]stuScores={
{80,90,70},
{23,45,56},
{2334,4564,56767}//结尾处不要用逗号；
};
```

动态：

```java
//方法一：
int[][] stuScores=new int[6][3];
//方法二：
int[][]stuScores;
     stuScores=new int[6][3];
//方法三：
int[][] stuScores=new int[3][];
         stuScores[0]=new int[3];
         stuScore[1]=new int[2];
         stuScore[2]=new int[5];
         //不规则数组声明

```

访问数组中的元素：

```java
int[][] arr=new int[4][3];
//确定你访问的数据在那一行
arr[1];
//确定你访问的数据在那一列
arr[1][2];
```

下面举个列子来循环输入二维数组，循环输出二维数组，，循环改变二维数组的数据：

```java

public class HelloWorld {
public static void main(String[] args) {
 /********** Begin **********/
   int i=0,j=0;
    int[][] scores={
     {92,85},
      {91,65},
       {90,33}
        };
    for(i=0;i<scores.length;i++){
        for(j=0;j<scores[i].length;j++){
          System.out.println(scores[i][j]);
          scores[i][j]=j+1;
      }
    }
    for(i=0;i<scores.length;i++){
        for(j=0;j<scores[i].length;j++){
            System.out.println(scores[i][j]);
            }
      }

          /********** End **********/
    }
}

```
