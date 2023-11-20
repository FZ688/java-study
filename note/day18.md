# day18

## 多态

* 多态实在**继承/实现**情况下的一种现象，表现为：对象多态、行为多态。

### 1.多态的前提

* 有**继承/实现**关系 ；存在父类引用子类对象 ；**存在方法重写**

### 2.多态的注意事项

* 多态是对象、行为的多态，java中的属性（成员变量）不谈多态。

```java
package com.tudg.d1_polymophism;
//父类
public class People {
    public void run(){
        System.out.println("people run");
    }
}
```

```java
public class Student extends People{
    @Override
    public void run() {
        System.out.println("学生跑步");
    }
}
```

```java
public class Teacher extends People {
    @Override
    public void run() {
        System.out.println("Teacher run");
    }

}
```

```java
public class Test {
    public static void main(String[] args) {
        People p1 = new Teacher();
        p1.run();//编译看左边，运行看右边
        People p2 = new Student();
        p2.run();
    }
}
```

> Teacher run
> 学生跑步

* 编译看左边，运行看右边

* **对于变量**，编译看左边，运行看左边

```java
public class People {
    public String name = "父类people的名称";
```

```java
public class Student extends People{
    public String name = "子类学生的名称";
```

```java
People p1 = new Teacher();
System.out.println(p1.name);
```

输出结果:

> **父类people的名称**

### 3.使用多态的好处

* 在多态形势下，右边对象是解耦合的，更便于扩展和维护。

* 定义方法时，使用父类类型的形参，可以接收一切子类对象，扩展性更强、更便利。


### 4.多态下会产生的一个问题：

* 多态下不能使用子类的独有功能。

### 5.类型转换

* **自动类型转换：**父类 变量名 = new 子类();                  例如：People p = new Teacher();
* **强制类型转换：**==子类 变量名 =（子类)父类变量==       例如：Teacher  t =(Teacher) p;

#### 强制类型转换的一个注意事项

* 存在继承/实现关系就可以在编译阶段进行强制类型转换，编译阶段不会报错
* 运行时，如果发现对象的真实类型与**强制转换后的类型不同，就会报类型转换一次(ClassCastException)的错误出来**

#### 强转前，Java建议：

* 使用instanceof关键字，判断当前对象的真实类型，再进行强转。

```java
p instanceof  Student
```

代码如下

```java
public class Test {
    public static void main(String[] args) {
        //1多态可以实现解耦合，右边对象可以随时切换，后续业务随之改变
        People p1 =new Student();
        p1.run();
//        p1.test();调布不了子类独有的功能

        //强制类型转换
        Student s1 =(Student)p1;
        s1.test();

        //强制类型转换可能存在的问题:编译阶段有继承或者实现关系就可以强制转换，但是运行时可能出现类型转换异常
        //Teacher t1 =(Teacher)p1; //运行时出现异常:ClassCastException

        if (p1 instanceof Student){
            Student s2 =(Student)p1;
            s2.test();
        }else {
            Teacher t2 =(Teacher)p1;
            t2.teach();
        }
        System.out.println("----------------");
        Student s =new Student();
        //对象回调
        go(s);
        Teacher t  =new Teacher();
        go(t);
    }
        //2.可以使用父类类型的变量作为形参，可以接受一切子类对象
        public static void go(People p1){
            if (p1 instanceof Student){
                Student s =(Student)p1;
                s.test();
            }else if(p1 instanceof  Teacher){
                Teacher t =(Teacher)p1;
                t.teach();
            }
        }
}
```

```java
public class People {
    public String name = "父类people的名称";
    public void run(){
        System.out.println("people run");
    }
}
```

```java
public class Student extends People{
    public String name ="子类Student的名称";

    @Override
    public void run(){
        System.out.println("学生run");
    }
    public void test(){
        System.out.println("学生需要考试");
    }
}
```

```java
public class Teacher extends People{
    public String name ="子类Teacher的名称";
    @Override
    public void run() {
        System.out.println("Teacher run");
    }
    public void teach(){
        System.out.println("Teacher teach");
    }
}
```
