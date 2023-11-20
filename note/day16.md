---

---

# day16

## 类方法的应用场景

类方法最常见的应用场景是做**工具类**

工具类中的方法都是一些类方法，每个方法都是用来完成一个功能的，工具类是给开发人共同使用的

```java
import java.util.Random;

public class MyUtil {
    public static String createCode(int n){
        String code ="";
        String data = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
        Random random = new Random();
        for (int i = 0; i < n; i++) {
            int  index = random.nextInt(data.length());
            code += data.charAt(index);
        }
        return code;
    }
}
```

* 实例方法需要创建对象来调用，此时对象只是为了调用方法，对象占内存，这样会浪费内存。

* 类方法，直接用类名调用即可，调用方便，节省内存

## 工具类没有创建对象的需求，建议将工具类的构造器进行私有

```java
private MyUtil(){
    
}
```

对工具类进行私有，因为工具类没有必要创建对象

## static的注意事项

1.类方法中可以直接访问类的成员，但不可以直接访问实例成员。

```java
static String schoolName ;//类变量
double score;//实例变量

//同一个类中访问类成员可以省略类名不写

/*1.类方法中可以直接访问类的成员，不可以直接访问实例成员*/
public static void printHelloWorld(){

    schoolName = "TUDG";
    printHelloWorld2();

    
}
//类方法
public static void printHelloWorld2(){

}
```

2.实例方法中既可以直接访问类成员，也可以直接访问实例成员。

```java
/*2.实例方法中既可以直接访问类成员，也可以直接访问实例成员*/
public void printPass(){
    schoolName="tudg2"; //可以直接访问类变量
    printHelloWorld2(); //可以直接访问类方法
    System.out.println(score);//可以直接访问实例变量
    printPass2(); //可以直接访问实例方法
}
//实例方法
public void printPass2(){

}
```

3.实例方法中可以出现this关键字，类方法中不可以出现this关键字

```java
public void printPass(){
    schoolName="tudg2"; //可以直接访问类变量
    printHelloWorld2(); //可以直接访问类方法
    System.out.println(score);//可以直接访问实例变量
    printPass2(); //可以直接访问实例方法
    System.out.println(this); //this关键字
}
//实例方法
public void printPass2(){

}
```

```java
0.0
tudg.d4_static_attetion.Student@1b6d3586
```



## static应用——代码块

* **代码块**是类的五大成分之一（成员变量、构造器、方法、**代码块**、内部类）

### 代码块分为两种：

* **静态代码块**：	>格式：static{}

  ​                   	 >特点：**类加载时自动执行，由于类只会加载一次，所以静态代码块也只会执行一次**

​								>作用：完成类的初始化，例如：对类变量的初始化赋值。

```Java
public class Student {
    static int number = 80;
    static String schoolname;

    /*静态代码块*/
    static {
        System.out.println("静态代码块执行了~");
        schoolname = "清华大学";                                //初始化赋值
    }
}
```

```java
public class Test {
    public static void main(String[] args) {
        System.out.println(Student.number);
        System.out.println(Student.number);
        System.out.println(Student.number);
        System.out.println(Student.schoolname);
    }
}
```

```java
静态代码块执行了~
80
80
80
清华大学
```

* **实例代码块**： >格式: {}

​							  >特点: **每次创建对象，执行实例代码块，并在构造器前执行**

​							 

```java
/*实例代码块*/

{
    
    System.out.println("实例代码块执行了~");
    System.out.printlin("有人创建对象了"+this);
    
}

//实例代码块在构造器前执行
public Student() {
    System.out.println("无参构造器执行了~");
}

public Student(String name) {
    System.out.println("有参数构造器执行了");
}
```

```java
静态代码块执行了~
80
80
80
清华大学
实例代码块执行了~
有人创建了对象，tudg.d5_block.Student@1b6d3586
无参构造器执行了~
实例代码块执行了~
有人创建了对象，tudg.d5_block.Student@4554617c
有参数构造器执行了
```

## static应用——单例设计模式

* 确保一个类只有一个对象

  ### 饿汉式单例（拿对象时，对象早就创建好了）

* 把类的构造器私有
* 定义一个类变量记住类的一个对象
* 定义一个类方法，返回对象

```java
public class A {
    //2.定义一个类变量记住类的一个对象
    private static A a = new A();
    //1.必须私有的构造器
    private A() {

    }
    //3.提供一个公共的静态方法，返回类变量
    public static A getObject() {
        return a;
    }
}
```

```java
public class Test1 {
    public static void main(String[] args) {
        A a1 = A.getObject();
        A a2 = A.getObject();
        System.out.println(a1);
        System.out.println(a2);//两次都那同一个对象，说明A类是一个单例类

    }
}
```

```java
tudg.d6_singleInstance.A@1b6d3586
tudg.d6_singleInstance.A@1b6d3586
```

### 懒汉式单例（拿对象时，才开始创建对象）

**写法：**

* 把类的构造器私有；
* 定义一个类变量用于存储对象；
* 提供一个类方法，保证返回的是同一个对象

```java
public class B {
    //2.定义一个类变量，用于存储这个类的一个对象
    private static B b;
    //1.把类的构造器私有
    private B() {

    }
    //3.定义一个类方法，这个方法要保证第一次调用时才创建一个对象，后面调用时都会用这同一个对象返回
    public static B getInstance() {
       if(b==null){
           System.out.println("第一次创建对象~");
           b=new B();
       }
       return b;
    }
}
```

```java
public class Test2 {
    public static void main(String[] args) {
        B b1 =B.getInstance();//第一次创建对象
        B b2 =B.getInstance();//第二次创建对象
        System.out.println(b1==b2);
    }

}
```

```java
第一次创建对象~
true
```

