# day15

## 1.static

* 叫静态，可以修饰成员变量，成员方法。

###  i.成员变量按照有无static修饰，分为两种

* 类变量：**会被类的全部对象共享**

* 实例变量（对象的变量）：**无static**修饰，属于每个对象的

  ```java
  public class Student{
      //类变量
      static String name;  /*有static修饰，属于类，在计算机只有一份，会被类的全部对象共享
      //实例变量（对象的变量）
      int age;
  }
  ```

  

1.对于**类变量**，可以使用**类名.类变量（推荐）**访问

​				对象.类变量（不推荐）

2.对于**实例变量**，只能**对象.实例变量**，属于对象，每个对象中都有一份

3.**类变量**：属于类，与类一起加载一次，在内存中只有一份，可以被类和类的所有对象共享。

```java
public class Test {
    public static void main(String[] args) {
        /*static方法的用法和特点*/

        //类名.类变量（推荐）
        Student.name="张三";

        //对象.类变量（不推荐）
        Student s1=new Student();
        s1.name ="李四";

        Student s2=new Student();
        s2.name ="王五";
        System.out.println(s1.name);//  王五
        System.out.println(Student.name);// 王五

        /*2.实例变量的用法*/
        s1.age=20;
        s2.age=28;
        System.out.println(s1.age);//20
        System.out.println(s2.age);//28
    }
}
```

### ii.类变量的应用场景

案例：系统启动后，要求用户类可以记住自己创建了多少个用户对象了

（创建对象实际上就是new一个对象，new一个对象会调用无参构造器）

```java
public class User{
    //类变量
    public static int number;
    
    //构造器
    public User(){
        User.number++;
    }
}
```

代码如下

```java
public class User {
    //类变量一般会用public修饰
    public static int number;
    public User(){
    //在同一个类中，访问自己类的类变量，才可以省略类名不写
        number++;
    }
}
```

```java
public class Test2 {
    public static void main(String[] args) {
        User u1 =new User();
        User u2 =new User();
        User u3 =new User();
        User u4 =new User();

        System.out.println(User.number);//4
    }
}
```

## 2.成员方法的分类

* **类方法**：有static修饰的成员方法，属于类。（**类名.类方法**）

* **实例方法**：无static修饰的成员方法，属于对象。（**对象.实例方法**）

  ```java
  public class Student {
      //类方法
      public static void printHelloWorld(){
          System.out.println("Hello World");
          System.out.println("Hello World");
      }
  
      double score;
      //实例方法
      public void printPass(){
  
          System.out.println(score>=60?"pass":"fail");
      }
  }
  ```

  ```java
  public class Test {
      public static void main(String[] args) {
          //类方法的用法
          Student.printHelloWorld();
  
          Student s =new Student();
          s.printHelloWorld();//不推荐
  
          s.printPass();
      }
  }
  ```

## 3.搞懂main方法

* main方法是**类方法**（static修饰）
* main方法如何跑的呢？  >>     java Test ---->**Test.main(...)**

