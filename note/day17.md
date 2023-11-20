# day17

## 继承

java中提供了一个关键字**extends**，用这个关键字，可以让一个类和另一个类建立起父子关系





### 继承的特点

* 子类能继承父类的非私有成员（成员变量、成员方法）

### 继承后对象的创建

* 子类的对象是由子类、父类共同完成的。

  ```java
  package tudg.d7_extends;
  /*父类*/
  public class A {
      //公开成员
      public int i;
      public void print1(){
          System.out.println("print1");
      }
      //私有成员
      private int j;
      private void print2(){
          System.out.println("print2");
      }
  }
  ```

```java
public class B extends A {
    public int k;
    //子类可以继承父类的非私有成员
    public void print3(){

        System.out.println(i);
        print1();

    }
}
```

```java
public class Test {
    public static void main(String[] args) {
    B b =new B();
        System.out.println(b.i);
        System.out.println(b.k);
        b.print1();
        b.print3();

    }
}
```

```java
0
0
print1
0
print1
```

### 继承的好处和应用场景

**1.好处：**

* 减少重复代码的编写

  ![](C:\Users\fz\Pictures\Screenshots\屏幕截图 2023-11-10 225747.png)

**2.应用场景：**

```java
public class People {
    private String name;
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
}
```

```java
public class Users extends People{
    private String major;

    public String getMajor() {
        return major;
    }

    public void setMajor(String major) {
        this.major = major;
    }

    public void printInfo(){
        System.out.println(getName()+"的专业："+major);
    }
}
```

```java
public class Test {
    public static void main(String[] args) {
        Users u = new Users();
        u.setName("张三");
        u.setMajor("java");
        System.out.println(u.getName());
        System.out.println(u.getMajor());
        u.printInfo();
    }
}
```

```java
输出结果：//
张三
java
张三的专业：java
```

### 继承的相关注意事项

#### 1.权限修饰符

用来限制类中的成员（成员变量、成员方法、构造器、代码块...）能够访问的范围。

|  修饰符   | 在本类中 | 同一个包下的其他类里 | 任意包下的子类里（在子类中访问，在外面创建子类对象不算） | 任意包下的任意类里 |
| :-------: | :------: | :------------------: | :------------------------------------------------------: | :----------------: |
|  private  |    √     |                      |                                                          |                    |
|   缺省    |    √     |          √           |                                                          |                    |
| protected |    √     |          √           |                            √                             |                    |
|  public   |    √     |          √           |                            √                             |         √          |

**private  <  缺省  <   protected   <  public**

```java
package tudg.d9_modifer;

public class Fu {
    //1。私有：只能在本类中访问
    private void privateMethod(){

        System.out.println("私有方法");
    }
    //2.缺省：本类，同一个包下的类
    void defaultMethod(){
        System.out.println("缺省");
    }
    //3.proteced:本类、同一个包下的类、任意包下的子类
    protected void protectedMethod(){
        System.out.println("protected");
    }

    //4.public:本类、同一个包下的类、任意包下的子类、任意包下的任意类
    public void publicMethod(){
        System.out.println("public");
    }

    public void test(){

        privateMethod();
        defaultMethod();
        protectedMethod();
        publicMethod();

    }

}
```

```java
package tudg.d9_modifer;

import javafx.scene.input.DataFormat;

import java.text.DateFormat;

public class Demo {
    public static void main(String[] args) {

        Fu f = new Fu();
        f.defaultMethod();
        f.protectedMethod();
        f.publicMethod();
    }
}
```

```java
package tudg.d10_modifer;

import tudg.d9_modifer.Fu;

public class Zi extends Fu {
    public void test(){
        protectedMethod();
        publicMethod();
    }

}
```

```java
package tudg.d10_modifer;

import tudg.d9_modifer.Fu;

public class Demo2 {
    public static void main(String[] args) {
        Fu f =new Fu();
        f.publicMethod();
    }
}
```

#### 2.单继承

Java是**单继承的**，Java中的类**不支持多继承**，但是**支持多层继承**。

```java
public class Test {
    public static void main(String[] args) {


    }
}

class A {}
class B {}

class C extends A {}
/*报错
class C extends A ,B{}*/

class D extends B{}
```

#### 3.Object 类

* object 类是 java 所有类的祖宗类。我们写的任何一个类，其实都是objet类的子类或子孙类。

  ```java
  public class Test {
      public static void main(String[] args) {
          A a = new A();
          a.hashCode();
  
      }
  }
  
  class A extends Object{}
  class B {}
  
  class C extends A {}
  /*报错
  class C extends A ,B{}*/
  
  class D extends B{}
  ```

#### 4.方法重写

* 当子类觉得父类中的某个方法不好用，或者无法满足自己的需求时，**子类可以重写一个方法名称、参数列表一样的方法**，去覆盖父类的这个方法，这就是方法重写给

* 注意：重写后，方法的访问，Java会遵循**就近原则**。

```java
public class A {
    public void print1(){
        System.out.println("111");
    }

    public void print2(int a,int b){
        System.out.println("22222");
    }
}
```

```JAVA
public class B extends A{
    /*方法重写*/
    public void print1(){
        System.out.println("66666");
    }

    public void print2(int a,int b){
        System.out.println("666");
    }
}
```

```JAVA
public class Test {
    public static void main(String[] args) {
        B b =new B();
        b.print1();
        b.print2(2,3);
    }
}
```

就近原则

```mathematica
66666
666
```

##### 方法重写其他注意事项：

* 重写小技巧：使用**Override注解**，他可以指定java编译器，检查我们方法重写的格式是否正确，代码可读性也会更好
* 子类重写父类方法时，访问权限必须大于或者等于父类该方法的权限（**public > protect > 缺省**）
* 重写的方法返回值类型，必须与被重写方法的返回值类型一样，或者范围更小
* 私有方法（private）、静态方法（static）不能被重写，如果重写会报错的。

**声明不变，重新实现**

##### 方法重现的常见应用场景

* 子类重写Object类的toString()方法，以便返回对象的内容

  ```java
  public class Student extends Object{
          private String name;
          private int age;
  
      public Student() {
      }
  
      public Student(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
      @Override
      public String toString(){
          return "Student{name:"+name+",age:"+age+"}";
      }
  }
  ```

```java
Student s = new Student("fz",18);
System.out.println(s.toString());
System.out.println(s);//默认调toString，返回地址，可以重写返回内容
```

```java
Student{name:fz,age:18}
Student{name:fz,age:18}
```

#### 5.子类中访问其他成员的特点

##### i.子类中访问其他成员（成员变量、成员方法），是依照**就近原则**的。

```java
public class F {
    String name ="父类名称";
    public void print1(){

        System.out.println("==父类的print1方法执行==");

    }
}
```

```java
public class Z extends F{
    String name ="子类名称";
    public void showName(){
        String name ="局部名称";
        System.out.println(name);//局部名称
        System.out.println(this.name);//子类名称
        System.out.println(super.name);//父类名称
    }
}
```

```java
public class Test {
    public static void main(String[] args) {
        Z z = new Z();
        z.showName();
    }
}
```

```java
局部名称
子类名称
父类名称
```

重写也是就近选择

```java
  @Override

    public void print1() {
        System.out.println("===子类的print1方法执行了====");
    }

    public void showMethod(){
        print1();           //调子类重写的
        super.print1();     //调父类
    }
}
```

在**子类方法访问其他成员**也是依照**就近原则**

*  先子类局部范围找
* 然后子类成员范围找
* 然后父类成员范围找，如果父类范围还没找到则报错

##### ii.super关键字

可以指定访问父类的成员

#### 6.子类构造器的特点

* 子类的全部构造器，都会先调用父类的构造器，再执行自己。

```java
public class F {
    public F(){
        System.out.println("==父类F的无参数构造器执行了==");
    }
}
```

```java
public class Z extends F{
    public Z(){
        super();//默认存在的
        System.out.println("====子类Z的无参数构造器执行了");
    }

    public Z(String name){
        super();//默认存在的)
        System.out.println("====子类Z的有参数构造器执行了");
    }
}
```

```java
public class Test {
    public static void main(String[] args) {
        Z z = new Z();
        Z z2 =new Z("z2");
    }
}
```

> ==父类F的无参数构造器执行了==
> ====子类Z的无参数构造器执行了
> ==父类F的无参数构造器执行了==
> ====子类Z的有参数构造器执行了

* 如果**父类没有无参数构造器**，则我们**必须在子类构造器**的第一行手写**super(.....)**，指定去**调用父类的有参数构造器**。

##### i.子类构造器调用父类构造器的应用场景

```java
package tudg.d14_extends_constructor;

public class Test2 {
    public static void main(String[] args) {
        Teacher t =new Teacher("张三",20,"java");
        System.out.println(t.getName()+","+t.getAge()+","+t.getSkill());

    }
}

class Teacher extends People{
    private String skill;
    public Teacher(String name,int age,String skill){
        super(name,age);
        this.skill = skill;
    }

    public String getSkill() {
        return skill;
    }

    public void setSkill(String skill) {
        this.skill = skill;
    }
}
class People{
    private String name;
    private int age;

    public People(){

    }
    public People(String name, int age){
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

#### 7.this(...)调用兄弟构造器

* 任意类的构造器中，是可以通过this(...)去调用该类的其他构造器的。

```java
public class Test3 {
    public static void main(String[] args) {
        Student s1 =new Student("ee",26,"gdut");
        //如果学生没有填写学校，那么学校默认就是genshin
        Student s2 =new Student("ee",26);
        System.out.println(s1.getSchoolName());
        System.out.println(s2.getSchoolName());

    }
}

class Student{
    private String name;
    private int age;
    private String schoolName;

    public Student() {

    }
    public Student(String name, int age) {
        this(name,age,"genshin");
    }

    public Student(String name, int age, String schoolName) {
        this.name = name;
        this.age = age;
        this.schoolName = schoolName;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getSchoolName() {
        return schoolName;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
            this.age = age;
    }

    public void setSchoolName(String schoolName) {
        this.schoolName = schoolName;
    }

}
```

>输出结果如下：
>
>
>
>gdut
>genshin

##### 注意事项

super(...)和this(...)都只能放在构造器的第一行，因此有了this(...)就不能写super(...)了

