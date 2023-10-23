# day05

**1.方法**

跟函数有点像（题外话）

**i.求和**

```java
public static int sum(int a,int b){
    int c =a+b;
    return c;
}
```

**ii.无返回值**

```java
 public static void printHelloWorld(int n){
        for (int i = 0; i < n; i++) {
            System.out.println("Hello World!");
        }
 }
```

**iii.方法被调用时，是进入到**栈内存**中运行**

参数传递也跟C语言函数差不多

**iv.方法重载**

   **一个类**中，出现**多个方法的名称相同**，但是他们的**形参列表是不同的**，那么这些方法就称为**方法重载**

```java
    public static void main(String[] args) {
        test();
        test(100);
    }

    public static void test() {
        System.out.println("test1");
    }
    public static  void test(int a){
        System.out.println("tes2"+a);
    }
    void test(double a){
        
    }
    
}
```

v.``return;``:可以用在无返回值的方法中，跳出bing'j结束当前方法的执行

**2.案例**

i.评委打分

```java
import java.util.Scanner;

public class Test3 {
    public static void main(String[] args) {
        System.out.println("the contestant's score is:"+getAverageScore(6));
    }
    public static  double getAverageScore(int n){//接受评委的人数
        int[] scores =new int[n];
        Scanner sc =new Scanner(System.in);
        for (int i = 0; i < scores.length; i++) {
            System.out.println("请录入第"+(i+1)+"个评委的分数:");
            int score = sc.nextInt();
            scores[i]=score;
        }
        //找最高分和最低分
        int sum =0;
        int max=scores[0];
        int min =scores[0];
        for (int i = 0; i < scores.length; i++) {
            int score =scores[i];
            sum+=score;
            if(score>max){
                max =score;
            }
            if(score<min){
                min =score;
            }
        }
        return 1.0 * (sum - max - min) / (n - 2);
    }
}
```

ii.生成验证码

```java
import java.util.Random;
import java.util.Scanner;

public class Test2 {
    public static void main(String[] args) {
        Scanner sc =new Scanner(System.in);
        int n = sc.nextInt();//接受验证码长度
        System.out.println(createCode(n));
    }
    public static String createCode(int n){
        Random r =new Random();
        //定义一个String变量用于记录产生的每位随机字符
        String code ="";
        for (int i = 0; i < n; i++) {
        //每个位置随机生成一个字符，可能是数字，可能是大小写字母
        int type =  r.nextInt(3);//0,1,2之间的随机数
            switch(type){
                case 0:
                    code += r.nextInt(10);
                    //随机一个数字字符
                    break;
                case 1:
                    char ch1 = (char) (r.nextInt(26)+65);
                    code += ch1;
                    //随机一个大写字符  A->65   Z->65+25
                    break;
                case 2:
                    //随机一个小写字符
                    char ch2 =(char)(r.nextInt(26)+97);
                    code+=ch2;
                    break;
                default:
                    throw new IllegalStateException("Unexpected value: " + type);
            }
        }
        return  code;
    }
}
```

iii.加密（局限）

```java
public class Test4 {
    public static void main(String[] args) {
        System.out.println(encrypt(1983));

    }
    public static String encrypt(int number){
        int[] numbers =split(number);//split方法可以拆分
        for (int i = 0; i < numbers.length; i++) {
            numbers[i]=(numbers[i]+5)%10;
        }
        reverse(numbers);
        String data="";
        for (int i = 0; i < numbers.length; i++) {
            data+=numbers[i];
        }
        return data;
    }

    public static void reverse(int[] numbers) {
        for (int i = 0, j=numbers.length-1; i <j ; i++,j--) {
            int temp =numbers[j];
            numbers[j]=numbers[i];
            numbers[i]=temp;
        }
    }

    public static int[] split(int number) {
        int[] numbers =new int[4];
        numbers[0]=(number/1000)%10;
        numbers[1]=(number/100)%10;
        numbers[2]=(number/10)%10;
        numbers[3]=(number/1)%10;

        return numbers;
    }
}
```

主要是数组的反转，数字的分解

iv.拷贝数组（几乎没有实用性）

```java
public class Test5 {
    public static void main(String[] args) {
        int[] arr = {11, 22, 33, 44};
        int[] arr2 = copy(arr);
        printArray(arr2);
    }
    public static void printArray(int[] array){
        System.out.print("[");
        for (int i = 0; i < array.length; i++) {
            System.out.print(i== array.length-1?array[i]:array[i]+",");
        }
        System.out.println("]");
    }
    public static int[] copy(int[] arr){
        int[] arr2 =new int[arr.length];
        for (int i = 0; i < arr.length; i++) {
            arr2[i]=arr[i];
        }
        return  arr2;
    }
}
```

v.