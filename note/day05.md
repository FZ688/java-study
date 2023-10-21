# day05

**1.方法**

跟函数有点像（题外话）

i.求和

```java
public static int sum(int a,int b){
    int c =a+b;
    return c;
}
```

ii.无返回值

```java
 public static void printHelloWorld(int n){
        for (int i = 0; i < n; i++) {
            System.out.println("Hello World!");
        }
 }
```

iii.方法被调用时，是进入到**栈内存**中运行

参数传递也跟C语言函数差不多

iv.方法重载

   **一个类**中，出现**多个方法的名称相同**，但是他们的**形参列表是不同的**，那么这些方法就称为**方法重载**