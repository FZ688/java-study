# day03

**1.逻辑运算符**

在java里，逻辑运算符跟C语言有所不同(短路机制倒是跟C语言一样，其他跟位运算挺像)

**&**  --->逻辑与  

**|** --->逻辑非

**！**  --->逻辑非

**^**   --->逻辑异或

**&&** --->短路与 

**||**  ---> 短路或

**2.键盘录入**

+ **导包一般不需要我们自己做，idea会自动帮助我们导包的**

例如 ``import java.util.Scanner;``

+ **创建一个扫描器对象 ``Scanner sc = new Scanner(System.in);``**

+ **等待接收用户输入的数据：**``int 变量名 =sc.nextInt();``

​													``String 变量名= sc.next();``

**3.分支结构**

i.if语句和switch语句基本跟C语言里差不多

ii.*switch(表达式)中的表达式类型只能是* **byte ，short ,int ,char ,enum, String**

  不支持**double , float, long**

**4.循环结构**

死循环可以做服务器程序

```java
for(;;){
    
}
//------------
while(ture){
    System.out.println("nihao");
}
//************
do{
    System.out.println("nihao");
}while(ture);
```



