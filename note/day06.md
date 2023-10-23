# day06

**1.面向对象基础**

​	跟C语言的结构体很像

​	i.**开发一个个对象，把数据交给对象，再调用对象的方法来完成对数据的处理**

​	ii.对象本质上是一种特殊的**数据结构**

​	iii.class也就是**类**，是对象的设计图（模板）

​		跟链表很像吧，s1指向new出来的对象的地址，new出来的对象里面有类的的地址，类的地址指向Student.class

  ```java
  public class 类名(){
      1.变量，用来说明对象可以处理什么数据
      2.方法，描述对象有什么功能，也就是可以对数据进行什么样的处理
         ...
  }
  ```

有了类就可以创建出对象

```java
类名 对象名 = new 类名();
```

------------------------------------------------------------------------------------------------------

```java
public class Test {
    public static void main(String[] args) {
        //1.创建学生对象
        Student s1 = new Student();
        s1.name ="FZ";
        s1.chinese=150;
        s1.math = 150;
        s1.printScore();
        s1.AvergeScore();
        //2.再创建一个学生对象
        Student s2 =new Student();
        s2.name ="FZ01";
        s2.math=150;
        s2.chinese=150;
        s2.printScore();
        s2.AvergeScore();

    }
}
```

s1里存着对象的地址

**2.识别引用类型的变量**

* ``Student s1 = new Student();``

因为s1变量中存储的是对象的地址，因此变量s1也称为引用类型的变量（跟指针很像)

**3.注意事项**

​	i.类中定义的变量是**成员变量**（对象的属性)，类中定义的方法也成为**成员方法**（对象的行为)

​	ii.成员变量有默认值（0   ,  0.0  , null)，并不需要初始化

​	iii.**一个代码文件中，可以写多个class类，但只能一个用public修饰**

​		**public修饰的类名必须是代码的文件名**

   iv.对象与对象之间的数据不会相互影响，**多个对象指向同一个变量时就会相互影响了**

```java
Student s1 = new Student();
s1.name ="FZ";
Student s2=s1;//把s1变量中存储的学生对象地址赋值给了s2变量，即同时指向同一个new出来的Student对象
s2.name ="ZF"//这个时候s1.name的值就是"ZF“
```

v.如果某个对象没有一个变量引用他，则该对象无法操作

``s1=null;``

``s2=null;``

则``s1.name``无法访问name







