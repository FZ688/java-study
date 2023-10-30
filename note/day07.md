# day07

## 1.this关键字

### this**是一个变量，可以用在方法中，**来拿到当前对象

```java
public class Student{  
	public void pirntThis(){
        System.out.println(this);
    }
}
```

```java
public class Test1 {
    public static void main(String[] args) {
        Student s1 =new Student();
        System.out.println(s1);
        s1.pirntThis();

        Student s2 =new Student();
        System.out.println(s2);
        s2.pirntThis();
    }
}
```

输出结果tudg.object.Student@1b6d3586
				tudg.object.Student@1b6d3586
				tudg.object.Student@4554617c
				tudg.object.Student@4554617c

### this执行原理

* this通过s1（存着new出来的Student对象的地址）找到Student对象，然后通过学生对象（存有类Student的地址）调用类Student中的printThis方法。

* Student对象调用方法的时候会把自己对象的地址传给方法里的this接受

也就是说**this可以拿到调他的那个对象**

（会给方法加一个参数）

```java
public void pirntThis(Student this){
        System.out.println(this);
}
```



### this应用

* 解决变量名称冲突问题

```java
public class Student{
   double score;[^1]
	public void printPass(double score[^2]){
    	if(this.score[^1]>score[^2]){
        System.out.println("pass");

    	}else{
        System.out.println("fail");
        }
	}
}
```

```java
Student s3 = new Student();
s3.score =325;
s3.printPass(250);
```

输出结果：pass

## 2.构造器

### i.构造器是一种特殊的方法：名字必须与所在类名一样，不能写返回类型

 构造器也可以**重载**

### ii.构造器的**特点**：

创建对象时，对象会去根据括号里的参数情况来选择对应构造器执行

``Student s =new Student()``

### iii.构造器的**应用**

创建对象时，同时完成对对象成员变量的初始化赋值。（把对象要处理的值给构造器）

```java
public Student1(String name, double score){
    System.out.println("有参数构造器被触发执行了");
    this.name =name;//重要
    this.score=score;//重要
}
```

```java
public class Test {
    public static void main(String[] args) {
        Student1 s1=new Student1();
        s1.name="fz";
        s1.score=100;

        Student1 s2 =new Student1("bozi",99);
    }
}
```

### iv.其他注意事项

* 类在设计的时候，如果不写构造器，java会自动生成一个无参数构造器

* 一旦定义了有参数构造器，java就不会自动生成一个无参数构造器了，**此时建议自己手写一个无参数构造器**

  