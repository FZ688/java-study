# day08

## 1.封装(面向对象的三大特征之一)

用类设计对象处理某一个事物的数据时，应该要把处理的数据，以及处理数据的方法，设计到一个对象中去

i.封装的设计规范：合理隐藏(private)，合理暴露(public)

```java
public class Student2 {
    private double score;//防止瞎赋值
    public void setScore(double score){
        if(score>=0&&score<=100) {
            this.score = score;

        }else{
            System.out.println("数据非法");
        }
    }
    public double getScore(){
        return score;
    }

    public void printPass(){
        System.out.println(score>=60?"Pass":"Fail");
    }
}
```

```java
public class Test {
    public static void main(String[] args) {
        Student2 s1 =new Student2();
        s1.setScore(-99);
        System.out.println(s1.getScore());
    }
}
```

## 实体JavaBean

实体类：一种特殊形式的类，保存某个事物的数据

​	i.类中的成员变量都要私有，并且要对外提供相应的getXxx方法，setXxx方法（用来保存数据的java类）

​	ii.类中必须要有一个公共的无参的构造器

```java
public class Student3 {
    //1.成员变量全部私有并提供get set方法
    private String name;
    private double score;
   // 2.必须为类提供一个无参数构造器

    public Student3() {
    }//无参构造器

    public Student3(String name, double score) {
        this.name = name;
        this.score = score;
    }
	//get set方法
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }
}
```

```java
public class Test {
    public static void main(String[] args) {
        Student3 s1 =new Student3();
        s1.setName("fz");
        s1.setScore(99);
        System.out.println(s1.getName());
        System.out.println(s1.getScore());
    }
}
```

### 应用：实体类只负责数据存取，可以把数据的处理交给其他类来完成，实现数据和数据业务处理相分离

```java
public class Student3Operator {
    private Student3 student;
    //一个有参构造器
    public Student3Operator(Student3 student){
     this.student=student;//重要，把传进来的s1送给上面的的 private Student3 student
    }
    public void printPass(){
        if(student.getScore()>=60){
            System.out.println(student.getName()+"pass");
        }else {
            System.out.println(student.getName()+"fail");
        }
    }
}
```

```java
public class Test {
    public static void main(String[] args) {
        Student3 s1 =new Student3();
        s1.setName("fz");
        s1.setScore(99);
        System.out.println(s1.getName());
        System.out.println(s1.getScore());

        Student3Operator operator =new Student3Operator(s1);//把s1对象送给操作类
        operator.printPass();
    }
}
```

-----------------------------------------------------------------------------------



明天写系统