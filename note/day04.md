# day04

## 1.生成随机数(Random)

​	i.导包(自动的）:``imoport java.util.Random;``

​	ii.得到随机数对象: ``Random r = new Random();``

​	iii.调用随机数功能获取0-9之间的随机数:``int number = r.nextInt(10)+1;``

指定区间(10~30)：``int number = r.nextInt(21)+10;``

而在c++/和c里呢，`#include <cstdlib>` 、``#include <ctime>``

​						         ``srand(time(0));``

​					             ``int number = rand()%10+1``

## 2.猜数字程序

```java
import java.util.Random;
import java.util.Scanner;

public class RandomTest2 {
    public static void main(String[] args) {
        Random r =new Random();
        int ans = r.nextInt(100)+1;
        while(true){
            System.out.println("please input your guess:");
            Scanner sc =new Scanner(System.in);
            int guess= sc.nextInt();
            if(guess>ans){
                System.out.println("Too Large");
            }else if(guess<ans){
                System.out.println("Too small");
            }else{
                System.out.println("You are right");
                break;
            }
        }
    }
}
```

## 3.<font color='red'>数组</font>

i.java定义数组有些格式跟C语言不同（但是定义的时候也可以跟C语言的一样）是如下格式:

``String[] arr={0};``

ii.**静态初始化数组**的格式：

```java
int[] ages = new int[]{12,24,36}  ;
//或者简化版本如下
int[] ages ={12,24,36};`
//可以和C语言一样
int ages[]={12,24,36};
```

iii.用``arr.length``可以访问数组的元素个数

iv.**动态初始化数组**:

`int[] arr = new int[3];`

`arr[0] = 10;`

boolean类型的默认值为**false**，String类型的默认值为**null**

vi.遍历数组

```java
import java.util.Scanner;

public class ArrayTest6 {
    public static void main(String[] args) {
        double sum =0;
        Scanner sc =new Scanner(System.in);
        double[] scores = new double[6];
        for (int i = 0; i < scores.length; i++) {
            System.out.println("请输入当前第"+(i+1)+"个人的分数");

            scores[i]=sc.nextDouble();
        }
        for (int i = 0; i < scores.length; i++) {
            sum+=scores[i];
        }
        System.out.println("The Final Score is:"+sum/scores.length);
    }
}
```

## 4.Java内存分配

* 方法区（字节码文件[^xxx.class      main]先加载到这里）
* 栈(方法运行时所进入的内存，变量也是在这里[^main......])
* 堆(new出来的东西会在这块内存中开辟空间并产生地址)
* 本地方法栈
* 程序计数器

例如 ``int a =20; int[] arr =new int [3]``

  a是变量，放在栈中，a变量存储的数据就是20这个值

new int[3]是创建一个数组对象，会在堆内存中开辟区域存储3个整数

arr是变量，在栈中，arr存储的是数组对象在堆内存中的地址值

## 5.多个变量指向同一个数组

```java 
int[] arr1={11,22,33};
int[] arr2= arr1;
```

指向null时就不能访问了

## 6.数组反转

```java
public class ArrayReverse {
    public static void main(String[] args) {
        int[] arr ={10,20,30,40,50};
        for (int i = 0,j=arr.length-1; i <j ; i++,j--) {
            int temp =arr[j];
            arr[j]=arr[i];
            arr[i]=temp;

        }
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]+" ");
        }
    }
}
```

重点是那个i<j

## 7.随机排序

```java
import java.util.Scanner;

public class RandomRank {
    public static void main(String[] args) {
        int[] codes = new int[5];
        Scanner sc =new Scanner(System.in);
        for (int i = 0; i < codes.length; i++) {
            System.out.println("please input"+" No."+(i+1)+":");
            int code =sc.nextInt();
            codes[i] = code;
        }
        Random r =new Random();
        for (int i = 0; i < codes.length; i++) {
            int index;
            index = r.nextInt(5);
            int temp = codes[index];
            codes[index]=codes[i];
            codes[i]=temp;


        }
        for (int i = 0; i < codes.length; i++) {
            System.out.println(codes[i]+" ");
        }
    }
}
```