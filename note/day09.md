# day09

**1.案例**

   i.设计一个类(成员变量要private)保存数据，然后设置get set方法，再设置一个有参构造器（方便赋值），顺便写一个无参构造器

   ii.设计一个操作类，定义一个(类的)数组来处理多个对象，写一个有参构造器用于接受别人送过来的（类的)数组

   iii.准备全部数据

```java
public class Movie {
    private int id;
    private String name;
    private double price;
    private double score;
    private String director;
    private String actor;
    private String info;
    //有参构造器和无参构造器


    public Movie() {
    }

    public Movie(int id, String name, double price, double score, String director, String actor, String info) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.score = score;
        this.director = director;
        this.actor = actor;
        this.info = info;
    }


    //提供get set方法

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public double getScore() {
        return score;
    }

    public String getDirector() {
        return director;
    }

    public String getActor() {
        return actor;
    }

    public String getInfo() {
        return info;
    }

    public void setId(int id) {
        this.id = id;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public void setScore(double score) {
        this.score = score;
    }

    public void setDirector(String director) {
        this.director = director;
    }

    public void setActor(String actor) {
        this.actor = actor;
    }

    public void setInfo(String info) {
        this.info = info;
    }
}
```

```java
public class MovieOperator {
    private Movie[] movies;
    //写一个有参构造器
    public MovieOperator(Movie[] movies){
        this.movies=movies;
    }
    //展示系统全部电影信息 movies ={m1,m2,m3,....}
    public void  printAllMovies(){
        System.out.println("-----系统全部电影信息如下-----");
        for (int i = 0; i < movies.length; i++) {
            Movie m =movies[i];
            System.out.println("编号"+m.getId());
            System.out.println("名称"+m.getName());
            System.out.println("价格"+m.getPrice());
            System.out.println("---------------------------------");

        }
    }
    //2.根据电影的编号查询出该电影的详细信息并展示
    public void searchMovieByid(int id){
        for (int i = 0; i < movies.length; i++) {
            Movie m = movies[i];
            if(m.getId()==id){
                System.out.println("该电影详情如下");
                System.out.println("编号"+m.getId());
                System.out.println("名称"+m.getName());
                System.out.println("价格"+m.getPrice());
                System.out.println("得分"+m.getScore());
                System.out.println("导演"+m.getDirector());
                System.out.println("主演"+m.getActor());
                System.out.println("其他信息"+m.getInfo());
                return;
            }
        }
        System.out.println("没有该电影信息");
    }
}
```

```java
import java.util.Scanner;

public class Test {
    public static void main(String[] args) {
        //1、设计一个电影类
        //2.设计电影操作类
        //3.准备全部电影数据
       Movie[] movies =new Movie[4];
       Movie m1 =new Movie(1,"水门桥",38.9,9.8,"徐克","吴京","12万人想看");
       Movie m2 =new Movie(2,"出拳吧",39,7.8,"唐晓白","田雨","3.5万人想看");
       Movie m3 =new Movie(3,"月球陨落",42,7.9,"罗兰","贝瑞","17.9万人想看");
       Movie m4 =new Movie(4,"一点就到家",35,8.7,"许宏宇","刘昊然","10.8万人想看");
       movies[0]=m1;
       movies[1]=m2;
       movies[2]=m3;
       movies[3]=m4;
       //4.创建一个电影操作类的对象，接收电影数据，并对其进行业务处理

        MovieOperator operator =new MovieOperator(movies);
        operator.printAllMovies();
        operator.searchMovieByid(3);


        Scanner sc =new Scanner(System.in);
        while (true) {//死循环使程序进行
            System.out.println("==电影信息系统==");
            System.out.println("1、查询全部电影信息");
            System.out.println("2、根据id查询某个电影的详细信息展示");
            System.out.println("请输入操作命令：");
            int command =sc.nextInt();
            switch (command){
                case 1:
                    operator.printAllMovies();
                    break;
                case 2:
                    int id = sc.nextInt();
                    operator.searchMovieByid(id);
                    break;
                default:
                    System.out.println("您输入有误");
            }
        }

    }
}
```

**2.成员变量和局部变量的区别**

​	i.类中位置不同：成员变量(类中，方法外)、局部变量（常见于方法中）

​	ii.初始化值不同：成员变量(有默认值，不需要初始化赋值)，局部变量(没有默认值，**使用之前必须完成赋值**)
​	iii.内存位置不同：成员变量（new出来的对象，存在于堆内存），局部变量（栈内存）
​	iv.作用域不同：成员变量（整个对象），局部变量（在所归属的大括号中）

​    v.生命周期不同：成员变量（与对象同生共死），局部变量(方法调用而生，方法结束而亡)

**3.回顾**

创建对象:``类名 对象名 =new 构造器()``

**4.常用API**

包:分门别类管理程序,类似于文件夹，有利于程序管理和维护

**建包的语法格式**//先建包(idea自动的)再建类

```java
package tudg.javabean;
public class Student{
    
}
```

​	i.同一个包下的程序，可以直接访问

​	ii.访问其他包下的程序，必须**导包**才能访问

​	iii.自己的程序中调用java提供的程序，也需要导包才可以使用（例如Scanner)

​		**java.lang**包下的程序不需要导包，可以直接使用

​	iv.访问多个其他包下的程序，这些程序名又一样的情况下，默认只能导入一个程序，另一个程序必须带包名和类名来访问

**5.String**

| 构造器                           | 说明                                   |
| -------------------------------- | -------------------------------------- |
| public   String()                | 创建一个空白字符串对象，不含有任何内容 |
| public   String(String original) | 根据传入的字符串内容，来创建字符串对象 |
| public  String(char[] chars)     | 根据字符数组的内容来创建字符串对象     |
| public  String(byte[] byte)      | 根据字节数的内容，来创建字符串对象     |

