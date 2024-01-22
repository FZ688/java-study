

# 常用API

* API 应用程序接口

## 0.String 类

| 构造器                           | 说明                                   |
| -------------------------------- | -------------------------------------- |
| public   String()                | 创建一个空白字符串对象，不含有任何内容 |
| public   String(String original) | 根据传入的字符串内容，来创建字符串对象 |
| public  String(char[] chars)     | 根据字符数组的内容来创建字符串对象     |
| public  String(byte[] byte)      | 根据字节数的内容，来创建字符串对象     |

```java
public class StringDemo1 {
    public static void main(String[] args) {
        String name ="fz";
        System.out.println(name);//第一种方式:直接使用双引号

        //第2种方式:new String创建字符串对象，并调用构造器初始化字符串
        String rs1 =new String();
        System.out.println(rs1);

        String rs2 =new String("fz");
        System.out.println(rs2);

        char[] chars ={'f','z','好', '好','好'};
        String rs3 =new String(chars);
        System.out.println(rs3);

        byte[] bytes={97,98,99};
        String rs4 =new String(bytes);
        System.out.println(rs4);
    }
}
```

输出结果:

```java
fz

fz
fz好好好
abc
```

### String的常用方法

| 方法名                                                       | 说明                                                     |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| public int **length()**                                      | 获取字符串的长度返回（就是字符个数）                     |
| public char **charAt(int index)**                            | 获取某个索引位置处的字符返回                             |
| public char[]  **toCharArray()**                             | 将当前字符串转换成字符数组返回                           |
| public boolean **equals(object anobject)**                   | 判断当前字符串与另一个字符串的内容一样，一样返回true     |
| public boolean **equalsIgnoreCase(String anotherstring)**    | 判断当前字符串与另一个字符串的内容是否一样（忽略大小写） |
| public String **substring(int beginIndex,int endIndex)**     | 根据开始和结束索引进行截取，得到新的字符串（包前不包后） |
| public String **substring(int beginIndex)**                  | 从传入的索引处截取，截取到末尾，得到新的字符串返回       |
| public String **replace(CharSequence target,CharSequence replacement)** | 使用新值，将字符串中的旧值替换，得到新的字符串           |
| public boolean **contains(CharSequence s)**                  | 判断字符串中是否包含了某个字符串                         |
| public boolean **startsWith(String prefix)**                 | 判断字符串是否以某个字符串内容开头，开头返回true,反之    |
| public string[] **split(String regex)**                      | 把字符串按照某个字符串内容分割，并返回字符串数组回来     |

```java
public class StringDemo2 {
    public static void main(String[] args) {
        String s ="fz好好好";
        //1.获取字符串的长度
        System.out.println(s.length());

        //2.提取字符串中某个索引位置处的字符
        char c =s.charAt(1);
        System.out.println(c);//z

        //2.字符串遍历
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            System.out.println(ch);
        }
        //3.把字符串转换成字符数组
        char[] chars = s.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            System.out.println(chars[i]);
        }

        //4.判断字符串内容，内容一样返回ture
        String s1 =new String("fz");
        String s2 =new String("fz");
        System.out.println(s1==s2);//结果是false，因为比较的是地址
        System.out.println(s1.equals(s2));//返回ture

        //5.忽略大小写比较字符串内容
        String c1 ="fz688";
        String c2 ="FZ688";
        System.out.println(c1.equals(c2));//false
        System.out.println(c1.equalsIgnoreCase(c2));//ture

        //6.截取字符串内容(包前不包后)
        String s3 ="落魄JAVA在线炒粉";
        String rs = s3.substring(0,6);//(包前不包后),输出落魄JAVA
        System.out.println(rs);

        //7.从当前索引位置一直截取到字符串末尾
        String rs2 = s3.substring(6);
        System.out.println(rs2);//输出在线炒粉

        //8.把字符串的某个内容替换成新内容，并返回新的字符串对象给我们
        String info ="学java狠狠赚一笔";
        String rs3 = info.replace("赚","*");
        System.out.println(rs3);//学java狠狠*一笔

        //9.判断字符串中是否包含某个关键字
        String info2 = "java是最好的编程语言";
        System.out.println(info2.contains("java"));//ture
        System.out.println(info2.contains("Java"));//false

        //10.判断字符串是否以某个字符串开头
        String rs4 = "双非计算机大于985文科";
        System.out.println(rs4.startsWith("双非"));//ture

        //11.把字符串按照某个指定内容分割成多个字符串，放到一个字符串数组返回给我们
        String rs5 ="计科,软工,信安,人工智能";
        String[] name = rs5.split(",");
        for (int i = 0; i < name.length; i++) {
            System.out.println(name[i]);
        }

    }
}
```

### String的注意事项

i.**String对象的内容不可改变，被称为不可变字符串对象**

   只要是以"....."方式写出的字符串对象，会在**堆内存**中的**字符串常量池**中存储

   每次试图改变字符串对象实际上是**新产生了新的字符串对象了**，变量**每次都是指向了新的字符串对象**，之前的字符串对象的内容

   确实没有改变

ii.**只要是以"......"方式写出的字符串对象，会存储到 ==字符串常量池==，==且相同内容的字符串只存储一份==!(节约内存)**

但通过new方式创建字符串对象，**每new一次都会产生一个新的对象放在堆内存中**。

```java
public class StringDemo3 {
    public static void main(String[] args) {
        String s1 ="abc";
        String s2 ="abc";
        System.out.println(s1==s2);//ture

        char[] chars ={'a','b','c'};
        String a1 = new String(chars);
        String a2 = new String(chars);
        System.out.println(a1==a2);//false

    }
}
```

java存在编译优化机制：" a"+ "b"+"c "会直接转成"abc"

```java
String b1="abc";
String b2 ="a"+"b"+"c";
System.out.println(b1==b2);//ture
```

### 案例 ①:完成用户登录

系统正确的登录名和密码是：fz/123456，请在控制台开发一个登陆界面，接收用户输入的登录名和密码，判断用户是否登录成功，登陆成功后提示:"欢迎进入系统“。（最多给用户三次登陆机会)

i.开发登录界面，提示用户通过键盘输入登录名和密码

ii.设计一个登录方法，对用户的登录名和密码进行正确性认证

iii.根据登陆方法返回的认证结果，判断用户是否登陆成功

iv.使用循环控制登录界面最多显示3次

```java
public class StringTest4 {
    public static void main(String[] args) {
        Scanner sc =new Scanner(System.in);
        for (int i =0;i<3;i++) {
            System.out.println("请您输入登录名称:");
            String LoginName  = sc.next();
            System.out.println("请您输入登录密码:");
            String PassWord =sc.next();
            boolean rs =login(LoginName,PassWord);
            if(rs){
                System.out.println("欢迎进入系统");
                break;
            }else{
                System.out.println("登录名或者密码错误");
            }
        }
    }

    //登录方法:接受用户登录名和密码，返回认证的结果
    public static boolean login(String LoginName,String PassWord){
        String okLoginName ="fz";
        String okPassWord ="123456";
        //判断系统是否登陆成功
//        if(okLoginName.equals(LoginName)&&okPassWord.equals(PassWord)){
//            return true;
//        }else{
//            return false;
//        }
        return okLoginName.equals(LoginName)&&okPassWord.equals(PassWord);
    }
}
```

### 案例②使用String开发验证码

随机产生验证码，验证码的每位可能是数字、大写字母、小写字母

i.设计一个方法，该方法接收一个整型参数，最终返回对应位数的随机验证码

ii.方法内定义2个字符串变量：1个用来记住生成的验证码，1个用来记住要用到的全部字符。

iii.定义for循环控制生成多少位随机字符，每次得到一个字符范围内的随机索引，根据索引提取该字符，把该字符交给code变量连接起来，循环借宿后，在循环外返回code即可

```java
public class StringTest5 {
    public static void main(String[] args) {
        System.out.println(createCode(4));
        System.out.println(createCode(5));
    }
    public static String createCode(int n){
        String code="";
        String data="abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        Random r =new Random();
        for (int i = 0; i < n; i++) {
            int index = r.nextInt(data.length());
            code +=data.charAt(index);
        }
        return  code;
    }
}
```



## 1.Object类

#### i.常见方法：

| 方法名                               | 说明                         |
| ------------------------------------ | ---------------------------- |
| public    String    toString()       | 返回对象的字符串表示形式     |
| public    boolean   equals(Object o) | 判断两个对象( 地址) 是否相等 |
| protected    Object    clone()       | 对象克隆                     |

```java
public class Student {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
    //重写equals方法，比较两个对象的内容一样
    //比较者 s2  == this
    //被比较者 s1  == o

    @Override
    public boolean equals(Object o) {
        //1。判断两对象的地址是否一样，即同一对象，如果相等，返回true
        if (this == o) return true;
        //判断 o 是 null 直接返回 false ，或者比较者的类型与被比较者的类型不一样，返回false
        if (o == null || this.getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name);
    }



    @Override
    public String toString() {
        return "Student{"+"name'"+name+'\''+",age"+age+'}';
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

```java
    public static void main(String[] args) {
        Student s1 =new Student("aa",21);
        System.out.println(s1.toString());

        Student s2 =new Student("aa",21);
        System.out.println(s2.toString());
        System.out.println(s2.equals(s1));
        System.out.println(s2==s1);
    }
}
```

> Student{name'aa',age21}
> Student{name'aa',age21}
> true
> false

### ii.Object 类提供的的对象克隆方法

| 方法名                                                | 说明     |
| ----------------------------------------------------- | -------- |
| protected   Object   <font color='red'>clone()</font> | 对象克隆 |

#### 浅克隆

拷贝出的新对象，与原对象中的数据一模一样

（**引用类型拷贝的只是地址**）

```java
public class User implements Cloneable{
    private int id;  //编号
    private String userName; //用户名
    private String passWord; //密码
    private double[] scores; //分数

    public User(){

    }

    public User(int id, String userName, String passWord, double[] scores) {
        this.id = id;
        this.userName = userName;
        this.passWord = passWord;
        this.scores = scores;
    }

    public int getId() {
        return id;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        //super 去调用父类object中的clone方法
        return super.clone();
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public String getPassWord() {
        return passWord;
    }

    public void setPassWord(String passWord) {
        this.passWord = passWord;
    }

    public double[] getScores() {
        return scores;
    }

    public void setScores(double[] scores) {
        this.scores = scores;
    }
}
```

```java
public class Test2 {
    public static void main(String[] args) throws CloneNotSupportedException {
        User u1 =new User(1,"fz","wo666",new double[]{99.0,99.5});
        User u2 = (User) u1.clone();   //protected 修饰, clone出来的是Object类型对象，要转成User类型
        System.out.println(u1.getId());
        System.out.println(u1.getPassWord());
        System.out.println(u1.getUserName());
        System.out.println(u1.getScores());
        System.out.println("---------------------");
        System.out.println(u2.getId());
        System.out.println(u2.getPassWord());
        System.out.println(u2.getUserName());
        System.out.println(u2.getScores());
    }
}
```

> 1
> wo666
> fz
>
> [D@1b6d3586
>
> ----------------------------------
>
> 1
> wo666
> fz
> [D@1b6d3586

#### 深克隆

对象中基本类型的数据直接拷贝。

对象中的字符串数据拷贝的还是地址。（字符串常量池还是共享）

对象中**还包含的其他对象，不会拷贝地址，会创建新对象。**

```java
@Override
protected Object clone() throws CloneNotSupportedException {
    //super 去调用父类object中的clone方法
    User u2 = (User) super.clone();
    u2.scores = u2.scores.clone();
    return u2;
}
```

> 1
> wo666
> fz
>
> [D@1b6d3586
>
> ----------------------------
>
> 1
> wo666
> fz
> [D@4554617c

## 2.Objects 类

一个工具类 (**final**) ，提供了很多操作对象的静态方法给我们使用

提供静态方法可直接用类名去调

#### i.常见方法

| 方法名                                                       | 说明                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| public  static  boolean   <font color='red'>equals (Object  a, Object b)</font> | 先做非空判断，再比较两个对象                         |
| public  static  boolean   <font color='red'> isNull (Object obj)</font> | 判断对象是否为 null ，为 null 返回 true，反之        |
| public  static  boolean   <font color='red'>nonNull (Object  obj)</font> | 判断对象是否不为 null ，不为 null 则返回 true ，反之 |

##### equals 方法

```java
String s1 = "abc";
String s2 = "abc";
System.out.println(s1.equals(s2));				//输出 true
System.out.println(Objects.equals(s1, s2));		//输出 true
```

Objects 类 **equals**方法的好处：更安全，更好

```java
String s1 = null;
String s2 = "abc";
System.out.println(s1.equals(s2));      	//空指针异常
System.out.println(Objects.equals(s1, s2)); //输出 false
```

##### isNull 方法

```java
String s1 = null;
String s2 = "abc";
System.out.println(Objects.isNull(s1));     //true
System.out.println(s1 == null);             //跟上同理
System.out.println(Objects.isNull(s2));     //false
System.out.println(s2 == null);             //跟上同理
```

##### nonNull方法

```java
String s1 = null;
String s2 = "abc";
System.out.println(Objects.nonNull(s2));	//true
System.out.println(Objects.nonNull(s1));	//false
```

## 3.包装类

* 包装类就是把基本类型的数据包装成对象（引用数据类型）。

| 基本数据类型                  | 对应的包装类（引用数据类型）       |
| :---------------------------- | :--------------------------------- |
| byte                          | Byte                               |
| short                         | Short                              |
| <font color='red'>int </font> | <font color='red'>Integer</font>   |
| long                          | Long                               |
| <font color='red'>char</font> | <font color='red'>Character</font> |
| float                         | Float                              |
| double                        | Double                             |
| boolean                       | Boolean                            |

###    Integer类

* java会**自动装箱**，把基本数据类型转换成对象，无需再使用  `Integer.valueOf()` 赋值

* java也有**自动拆箱**

  可以自动把包装类的对象转换成对于的基本数据类型
### 为什么要使用包装类？
* 泛型和集合不支持基本数据类型，只能支持引用数据类型

* ```java
  Integer a1=12;
  int a2 =a1;
  System.out.println(a1);    //12
  System.out.println(a2);    //12
  
  ArrayList<Integer> list = new ArrayList<>();
  list.add(12);
  list.add(13);
  System.out.println(list.get(1));  //13
  int rs = list.get(1);  //自动拆箱
  ```

### 包装类的其他常见操作

* 可以把基本类型的数据转换成字符串类型

| public static String toString(double d) |
| :-------------------------------------- |
| public String toString();               |

```java
/*1.把基本数据类型转换成字符串*/
Integer a =23 ;
String rs1 = Integer.toString(a);  //23
System.out.println(rs1+1);    //231

Double b = 2.3;
String rs2 = Double.toString(b);
System.out.println(rs2+1);  //2.31

String rs3 =a.toString();  //Integer类中已经对toString方法进行的重写
System.out.println(rs3+1); //231

String rs4 =a+"";//与上面等价
System.out.println(rs4+1); //231
```

* 可以把字符串类型的数值转换成数值本身对应的数据类型

```java
/*2，把字符串类型的数值转换成相应的基本类型*/
String ageStr = "29";
int age = Integer.valueOf(ageStr); //29,也可以用paserInt
System.out.println(age+1);  //30;


String scoreStr = "99.5";
double score = Double.valueOf(scoreStr); //99.5，也可以用parseDouble
System.out.println(score+1);  //100.5;
```

## 4.StringBuilder类（操作字符串）

* StringBuilder代表可变字符串对象，**相当于是一个容器**，它里面装的字符串是可以改变的，**就是用来操作字符串的**

* 好处：**StringBuilder比String更适合做字符串的修改操作，效率会更高，代码也会更简洁。**

| 构造器                                                     | 说明                                       |
| ---------------------------------------------------------- | ------------------------------------------ |
| public  <font color='red'>StringBuilder()</font>           | 创建一个空白的可变字符串对象，不含任何内容 |
| public  <font color='red'>StringBuilder(String str)</font> | 创建一个指定字符串内容的可变字符串对象     |

| 方法名称                                                     | 说明                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| public  StringBuilder  <font color='red'>append(任意类型)</font> | 添加数据并返回StringBuilder对象本身                     |
| public  StringBuilder  <font color='red'>reverse()</font>    | 将对象的内容反转                                        |
| public  int  <font color='red'>length()</font>               | 返回对象内容长度                                        |
| public  String <font color='red'>toString()</font>           | 通过toString()方法就可以实现把StringBuilder转换为String |

```java
StringBuilder s = new StringBuilder("gdut");
/*拼接*/
s.append(12);
s.append("好好好");
System.out.println(s);

/*支持链式编程*/
s.append("好好好").append(12).append("promissing");

//反转字符串
s.reverse();
System.out.println(s);

//返回字符串长度
System.out.println(s.length());
System.out.println(s.capacity()); //容量
System.out.println(s.charAt(0)); //获取指定位置的字符
System.out.println(s.toString()); //转换为字符串
System.out.println(s.substring(0,3)); //截取字符串
System.out.println(s.delete(0,3)); //删除字符串
System.out.println(s.insert(0,"gdut")); //插入字符串
System.out.println(s.replace(0,3,"gdut")); //替换字符串
```

```java
public class Test3 {
    public static void main(String[] args) {
        //设计一个方法，用于返回整型数组的内容，要求返回的数组内容格式如：[11,22,33]
        int[] arr = new int[]{11,22,33};
        String rs = getArrayData(arr);
        System.out.println(rs);
    }

    public static String getArrayData(int[] arr){
        //1.判断arr是否为null
        if (arr == null){
            return null;
        }

        //2.定义一个StringBuilder对象
     /*   StringBuilder sb = new StringBuilder("[");
        for (int i = 0; i < arr.length; i++) {
            sb.append(arr[i]).append(",");
        }
        sb.delete(sb.length()-1,sb.length());
        sb.append("]");*/

        StringJoiner sb =new StringJoiner(",","[","]");
        for (int i = 0; i < arr.length; i++) {
            sb.add(arr[i]+"");
        }
        return sb.toString();
    }
}
```

## 5.StringBuffer类（线程安全）

用法与StringBuilder一样

## 6.StringJoiner类

* 跟StringBuilder一样，也是用来操作字符串的，也可以看成是一个容器，创建之后里面的内容是可变的

* 可以提高字符串的操作效率，**在有些场景下使用它操作字符串，代码会更简洁**

| 构造器                                           | 说明                                                         |
| ------------------------------------------------ | ------------------------------------------------------------ |
| public  StringJoiner (间隔符号)                  | 创建一个StringJoiner对象，指定拼接时的间隔符号               |
| public  StringJoiner(间隔符号,开始符号,结束符号) | 创建一个StringJoiner对象，指定拼接时的建个符号，开始符号，结束符号 |

| 方法名称                                 | 方法                                         |
| ---------------------------------------- | -------------------------------------------- |
| public StringJoiner  **add(添加的内容)** | 添加数据，并返回对象本身                     |
| public  int  length()                    | 返回长度（字符出现的个数）                   |
| public  String  toString()               | 返回一个字符串（该字符串就是拼接之后的结果） |

```java
StringJoiner s =new StringJoiner(",");
s.add("a");
s.add("b");
s.add("c");
System.out.println(s); //a,b,c

StringJoiner s2 =new StringJoiner(",","[","]");
s2.add("a");
s2.add("b");
s2.add("c");
System.out.println(s2);//[a,b,c]
```

## 7.Math类

* 代表数学，是一个工具类，里面提供的都是对数据进行操作的一些静态方法

| 方法名                                                       | 说明                                  |
| ------------------------------------------------------------ | ------------------------------------- |
| public  static  int  <font color='red'>abs(int  a)</font>    | 获取参数绝对值                        |
| public  static  double <font color='red'>ceil(double  a)</font> | 向上取整                              |
| public  static  double <font color='red'>floor(double  a)</font> | 向下取整                              |
| public  static  int  <font color='red'>round(float  a)</font> | 四舍五入                              |
| public  static  int  <font color='red'>max(int  a,  int  b)</font> | 获取两个int值中的较大值               |
| public  static  double  <font color='red'>pow(double  a,  double  b)</font> | 返回a的b次幂的值                      |
| public  static  double  <font color='red'>random()</font>    | 返回值为double的随机值，范围[0.0,1.0) |

```java
System.out.println(Math.abs(0)); //0
System.out.println(Math.abs(1)); //1
System.out.println(Math.abs(-1)); //1
System.out.println(Math.ceil(4.000001));    //5.0
System.out.println(Math.ceil(4.000000));   //4.0
System.out.println(Math.floor(4.99999));     //4.0
System.out.println(Math.round(4.000001));   //4.0
System.out.println(Math.round(4.50000));    //5.0
System.out.println(Math.round(4.49999));    //4.0
System.out.println(Math.sqrt(4));   //2.0
System.out.println(Math.max(1,2));  //2
System.out.println(Math.min(1,2));  //1
System.out.println(Math.pow(2,3));  //8.0
System.out.println(Math.PI);  //3.141592653589793
System.out.println(Math.E);   //2.718281828459045
System.out.println(Math.random()); //0.0~1.0
System.out.println(Math.random()*10); //0.0~10.0
System.out.println((int)(Math.random()*10)); //0~10
System.out.println((int)(Math.random()*10+1)); //1~10
```

## 8.System类

* System代表程序所在的系统，也是一个工具类

| 方法名                                        | 说明                                                         |
| --------------------------------------------- | ------------------------------------------------------------ |
| public  static  void  **exit(int  status)**   | 终止当前运行的Java虚拟机（非零状态代码表示异常终止）         |
| public  static  long  **currentTimeMillis()** | 返回当前系统的时间毫秒值形状（从1970-1-1 0:0:0开始走到此刻的毫秒值) |

```java
long time = System.currentTimeMillis();
System.out.println(time);

for (int i = 0; i < 1000000; i++) {
    System.out.println(i);
}
long time2 = System.currentTimeMillis();
System.out.println(time2);
System.out.println((time2 - time)/1000+"s");
```

## 9.Runtime类

* 代表程序所在的运行环境

* Runtime 是一个单例类

| 方法名                                    | 说明                                   |
| ----------------------------------------- | -------------------------------------- |
| public  static  Runtime  **getRuntime()** | 返回与当前Java应用程序关联的运行时对象 |
| public  void  **exit(int  status)**       | 终止当前运行的虚拟机                   |
| public  int  **availableProcessors()**    | 返回Java虚拟机可用的处理器数。         |
| public  long  **totalMemory()**           | 返回Java虚拟机中的内存总量             |
| public  long  **freeMemory()**            | 返回Java虚拟机中的可用内存             |
| public  Process **exec(String command)**  | 启动某个程序，并返回代表该程序的对象   |

```java
Runtime r = Runtime.getRuntime();

//r,exit(0);
System.out.println("处理器数量：" + r.availableProcessors());
System.out.println("空闲内存：" + r.freeMemory() / 1024 / 1024 + "MB");
System.out.println("最大内存：" + r.maxMemory() / 1024 / 1024 + "MB");
System.out.println("总内存：" + r.totalMemory() / 1024 / 1024 + "MB");
System.out.println("系统时间：" + r.totalMemory());

Process p = r.exec("notepad");  //打开记事本
Thread.sleep(5000);   //暂停5秒
p.destroy();  //关闭记事本
```

## 10.BigDecimal类

* 用于解决浮点型运算时，出现结果失真的问题。

| 构造器                                                       | 说明                        |
| :----------------------------------------------------------- | :-------------------------- |
| public  BigDecimal(double  val)      **注意：不推荐使用这个** | 将 double 转换为 BigDecimal |
| public  **BigDecimal(String  val)**                          | 将 String 转成 BigDecimal   |

| 方法名                                                       | 说明                          |
| :----------------------------------------------------------- | :---------------------------- |
| public  static  BigDecimal  **valueOf(double  val)**         | 转换一个 double 成 BigDecimal |
| public  BigDecimal  **add(BigDecimal  b)**                   | 加法                          |
| public  BigDecimal  **subtract(BigDecimal  b)**              | 减法                          |
| public  BigDecimal  **multiply(BigDecimal  b)**              | 乘法                          |
| public  BigDecimal  **divide(BigDecimal  b)**                | 除法                          |
| public  BigDecimal **divide(另一个BigDecimal对象，精确几位，舍入模式)** | 除法、可以控制精确到小数几位  |
| public  double  **doubleValue()**                            | 将 BigDecimal 转换为 double   |

```java
 double a =0.001;
  double b = 0.009;
  double c = a + b;
  System.out.println(c);
/*  BigDecimal a1 = new BigDecimal(Double.toString(a));
  BigDecimal b1 = new BigDecimal(Double.toString(b));*/

  //把小数转换成字符串，再封装成BigDeciaml对象来运送
  BigDecimal a1 =BigDecimal.valueOf(a);
  BigDecimal b1 =BigDecimal.valueOf(b);

  BigDecimal c1 = a1.add(b1);
  System.out.println(c1);

  BigDecimal d1 = b1.subtract(a1);
  System.out.println(d1);

  BigDecimal e1 = a1.multiply(b1);
  System.out.println(e1);

  BigDecimal f1 = a1.divide(b1,2, RoundingMode.HALF_UP);
  System.out.println(f1);

  //把BigDecimal转换为double类型
  double rs = f1.doubleValue();
  System.out.println(rs);
```



## 11.Date类

* 代表的是日期和时间

| 构造器                   | 说明                                           |
| ------------------------ | ---------------------------------------------- |
| public  Date()           | 创建一个Date对象，代表的是系统当前此时日期时间 |
| public  Date(long  time) | 把时间毫秒值转换成Date日期对象                 |

| 常见方法                          | 说明                                           |
| --------------------------------- | ---------------------------------------------- |
| public  long  getTime()           | 返回从1970年1月1日 00:00:00 走到此时的总毫秒数 |
| public  void  setTime(long  time) | 设置日期对象的时间为当前时间毫秒值对应的时间   |

```java
Date d =new Date();
System.out.println(d); //Wed Jan 17 18:40:26 CST 2024

//2.拿到时间毫秒值
long time = d.getTime();
System.out.println(time);

//3.把时间毫秒值转化为日期对象，2s后的时间是多少
time+=2*1000;
Date  d2 = new Date(time);
System.out.println(d2); //Wed Jan 17 18:40:28 CST 2024

//4.直接把日期对象的时间通过setTime方法进行修改
Date d3 = new Date();
d3.setTime(time);
System.out.println(d3); //Wed Jan 17 18:40:28 CST 2024
```

## 12.SimpleDateFormat 类

* 代表简单日期格式化，可以用来把日期对象、时间毫秒格式化成我们想要的形式

| 常见构造器                                    | 说明                                     |
| --------------------------------------------- | ---------------------------------------- |
| public  **SimpleDateFormat(String  pattern)** | 创建简单日期格式化对象，并封装时间的格式 |

| 格式化时间的方法                                | 说明                                |
| ----------------------------------------------- | ----------------------------------- |
| public  final  String  **format(Date  date)**   | 将日期格式化成日期/时间字符串       |
| public  final  String  **format(Object  time)** | 将时间毫秒值格式化成日期/时间字符串 |

时间格式符号

|   2020-11-11   13:27:06   |   yyyy-MM-dd   HH-mm:ss   |
| :-----------------------: | :-----------------------: |
| 2020年11月11日   13:27:06 | yyyy年MM月dd日   HH:mm:ss |

此外，还有`EEE`代表星期几  ，`a`代表  上午/下午

### SimpleDateFormat解析字符串时间成为日期对象

| 解析方法                                | 说明                       |
| --------------------------------------- | -------------------------- |
| public  Date  **parse(String  source)** | 把字符串时间解析成日期对象 |

```java
Date d = new Date();
System.out.println(d);

long time = d.getTime();
System.out.println(time);


//格式化日期对象,和时间毫秒值--->字符串
SimpleDateFormat  sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss EEE a");
String rs = sdf.format(d);
String rs1 = sdf.format(time);
System.out.println(rs);
System.out.println(rs1);
System.out.println("====================");


//字符串--->时间对象
String dateStr = "2020-12-12 12:12:12";
//指定的时间格式必须与被解析的时间格式一样，否则会出问题
SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
Date d2 = sdf1.parse(dateStr);
System.out.println(d2); //Sat Dec 12 12:12:12 CST 2020
```

### 案例：秒杀活动

```java
String start = "2023年11月11日 0:0:0"; //开始时间
String end = "2023年11月11日 0:10:0"; //结束时间
String xm = "2023年11月11日 0:01:10"; //小明下单时间
String xh = "2023年11月11日 0:10:57"; //小红下单时间

//把字符串解析成时间对象
SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
Date d1 =sdf.parse(start);
Date d2 = sdf.parse(end);
Date d3 = sdf.parse(xm);
Date d4 = sdf.parse(xh);

//把日期对象转换成时间毫秒值然后进行比较
long time1 = d1.getTime();
long time2 = d2.getTime();
long time3 = d3.getTime();
long time4 = d4.getTime();
if(time3>=time1 && time3<=time2){
    System.out.println("小明秒杀成功");
}else{
    System.out.println("小明秒杀失败");
    System.out.println("小明下单时间："+d3);
    System.out.println("开始时间："+d1);
    System.out.println("结束时间："+d2);
    System.out.println("当前时间："+new Date());
}
System.out.println("================================");
if(time4>=time1 && time4<=time2){
    System.out.println("小红秒杀成功");
}else {
    System.out.println("小红秒杀失败");
    System.out.println("小红下单时间："+d4);
    System.out.println("开始时间："+d1);
    System.out.println("结束时间："+d2);
    System.out.println("当前时间："+new Date());
}
```

## 13.Calendar 类

* 代表系统此刻时间对应的日历
* 通过它可以单独获取、修改时间中的年、月、日、时、分、秒等。

| 方法名                                              | 说明                        |
| --------------------------------------------------- | --------------------------- |
| public    static    Calendar  **getInstance()**     | 获取当前日历对象            |
| public    int    **get(int  field)**                | 获取日历中的某个信息        |
| public    final    Date  **getTime()**              | 获取日期对象。              |
| public    long    **getTimeInMillis()**             | 获取时间毫秒值              |
| public    void    **set(int  field,  int  value )** | 修改日历的某个信息          |
| public    void    **add(int  field,  int  amount)** | 为某个信息增加/减少指定的值 |

```java
Calendar now = Calendar.getInstance();
System.out.println(now);

System.out.println(now.get(Calendar.YEAR));
System.out.println(now.get(Calendar.MONTH)+1);

//拿到日历中记录的日期对象
Date d =now.getTime();
System.out.println(d);

//拿到时间毫秒值
long time = now.getTimeInMillis();
System.out.println(time);

//修改日历中的某个信息
now.set(Calendar.MONTH,1); //修改月份为2月份
System.out.println(now);

//为某个信息增加/减少多少
now.add(Calendar.DAY_OF_YEAR,100);  //增加100天
System.out.println(now);
now.add(Calendar.DAY_OF_YEAR,-100); //减少100天
System.out.println(now);
```

## 14.代替Calendar

### i .`LocalDate` : 年、月、日、星期（本地日期）

```java
LocalDate ld = LocalDate.now();
int year = ld.getYear();        //年
int month = ld.getMonthValue();  //月
int day = ld.getDayOfMonth();  //日
int dayOfYear = ld.getDayOfYear(); //年中的第几天
int dayOfWeek = ld.getDayOfWeek().getValue(); //星期几
System.out.println(year + "-" + month + "-" + day);  //2024-1-18
System.out.println(ld);                         //2024-01-18
System.out.println(year);           //2024
System.out.println(dayOfYear);       //18
System.out.println(dayOfWeek);      //4

//2.直接修改某个信息：withYear、withMonth、withDayOfMonth、withDayOfYear,每次修改都会返回一个新的日期对象
LocalDate ld2 = ld.withYear(2077);
LocalDate ld3 = ld.withMonth(12);
System.out.println(ld2);        //2077-01-18
System.out.println(ld3);        //2024-12-18

//3.把某个信息加多少，plusYears,plusMonths,plusDays,plusWeeks
LocalDate ld4 = ld.plusYears(1);
System.out.println(ld4);        //2025-01-18
LocalDate ld5 = ld.plusDays(100);
System.out.println(ld5);        //2024-04-27

//4.把某个信息减多少,minusYears,minusMonths,minusDays,minusWeeks
LocalDate ld6 =ld.minusDays(100);
System.out.println(ld6);        //2023-10-10
LocalDate ld7 = ld.minusWeeks(1);
System.out.println(ld7);        //2024-01-11

//5.获取指定日期的LocalDate对象，public static LocalDate of(int year, int month, int dayOfMonth)
LocalDate ld8 = LocalDate.of(2077,9,27);
System.out.println(ld8);        //2077-09-27
LocalDate ld9 = LocalDate.of(2077,9,27);

//6.判断两个日期对象是否相等，在前还是在后 : equals  isBefore isAfter
System.out.println(ld8.equals(ld9)); //true
System.out.println(ld8.isBefore(ld)); //false
System.out.println(ld8.isAfter(ld)); //true
```

### ii.`LocalTime`:时、分、秒、纳秒（本地时间）

```java
//获取本地时间对象
LocalTime lt =LocalTime.now();
System.out.println(lt);  //16:02:59.602

//1.获取本地时间中的信息
int hour = lt.getHour();
int minute = lt.getMinute();
int second = lt.getSecond();
int nano = lt.getNano();

//2.修改时间: withHour,withMinute,withSecond,withNano
LocalTime lt2 = lt.withHour(22);
LocalTime lt3 = lt.withMinute(10);
LocalTime lt4 = lt.withSecond(20);
LocalTime lt5 = lt.withNano(200);
System.out.println(lt2);
System.out.println(lt3);
System.out.println(lt4);
System.out.println(lt5);

//3.减多少：minusHours,minusMinutes,minusSeconds,minusNanos
LocalTime lt6 = lt.minusHours(1);
System.out.println(lt6);

//加多少：plusHours,plusMinutes,plusSeconds,plusNanos
LocalTime lt7 = lt.plusHours(1);
System.out.println(lt7);


//获取指定时间的LocalTime对象
LocalTime lt8 = LocalTime.of(12,22,26);
LocalTime lt9 = LocalTime.of(12,22,26);

//判断两个时间对象是否相等,在前还是在后
System.out.println(lt8.equals(lt9)); //true
System.out.println(lt8.isBefore(lt)); //ture
System.out.println(lt8.isAfter(lt)); //false
```

### iii.`LocalDateTime`:代表本地日期、时间（年、月、日、星期、时、分、秒、纳秒）

```java
//可以把LocalDateTime转换成LocalDate和LocalTime
LocalDateTime ldt = LocalDateTime.now();
LocalDate ld = ldt.toLocalDate();
LocalTime lt = ldt.toLocalTime();
System.out.println(ld);
System.out.println(lt);

//也可以把LocalDate和LocalTime合并
LocalDateTime ldt2 = LocalDateTime.of(ld, lt);
System.out.println(ldt2);
```

一、它们**获取对象**的方案都是调用 `now()`方法 得到**系统当前时间**对应的该对象

例如：

```java
LocalDate ld = LocalDate.now();
LocalTime lt = LocalTime.now();
LocalDateTime ldt = LocalDateTime.now();
```

二、**获取指定时间的对象**都是调用`of(...)`方法

例如:

```java
LocalDate ld = LocalDate.of(2009,11,11);
LocalTime lt = LocalTime.of(22,56,59);
LOcalDateTime ldt = LocalDateTime.of(2009,11,11,22,56,59) //也可以是 LocalDateTime.of(ld,lt);
```

三、获取年、月、日….

```java
getYear();   //年
getMonthValue(); //月
getDayOfMonth(); //日
getDayOfYear();  //一年中的第几天
getDayOfWeek();   //获取星期几
getHour();    //时
getMinute();   //分
getSecond();   //秒
getNano();    //纳秒
```

四、年月日的操作

```java
修改某个信息，返回新日期对象：withYear、withMonth、withDayOfMonth、withDayOfYear、withHour、withMinute...
某个信息加多少，返回新日期对象：plusYears、plusMonths、plusDays、plusWeeks、plusHours、plusMinutes....
某个信息减多少，返回新日期对象：minusYears、minusMonths、minusDays、minusWeeks、.....    
判断两个日期对象是否相等，在前还是在后 : equals、isBefore、isAfter    
```

### iv.`ZoneId` :时区

例如：Asia/Shanghai

UTC :世界标准时间

中国标准时间：**UTC+8小时**

洲名/城市名：Asia/Shanghai    、国家名/城市名： America/New_York

| 方法名                                            | 说明                     |
| ------------------------------------------------- | ------------------------ |
| public  static  Set<String>  getAvailableZoneId() | 获取Java中支持的所有时区 |
| public  static  ZoneId  **systemDefault()**       | 获取系统默认时区         |
| public  static  ZoneId  **of(String  zoneId)**    | 获取一个指定时区         |

### v.`ZonedDateTime`：带时区的时间

例如：2024-01-19T00:41:00.242+08:00[Asia/Shanghai]

使用方法与 `LocalDateTime` 相像

| 方法名                                                       | 说明                               |
| ------------------------------------------------------------ | ---------------------------------- |
| public  static  ZonedDateTime   **now()**                    | 获取当前时区的ZonedDateTime对象    |
| public  static  ZonedDateTime   **now(ZoneId  zone)**        | 获取指定时区的ZonedDateTime 对象   |
| getYear、getMonthValue、getDayOfMonth、getDayOfYear、getDayOfWeek、getHour、getHour、getMinute、getSecond、getNano | 获取年、月、日、时、分、秒、纳秒等 |
| public  ZonedDateTime  **withXxx(时间)**                     | 修改时间系列的方法                 |
| public  ZonedDateTime  **minusXxx(时间)**                    | 减少时间系列的方法                 |
| public  ZonedDateTime  **plusXxx(时间)**                     | 增加时间系列的方法                 |

```java
ZoneId zoneId = ZoneId.systemDefault();  //获取系统默认时区
System.out.println(zoneId.getId());
System.out.println(ZoneId.getAvailableZoneIds());  //得到Java支持的全部时区Id

ZoneId  zoneId2 = ZoneId.of("America/New_York");


//public static ZoneDateTime now(ZoneId zone)   获取某个时区的ZoneDateTime对象
ZonedDateTime zonedDateTime = ZonedDateTime.now(zoneId);
ZonedDateTime newYork = ZonedDateTime.now(zoneId2);
System.out.println(newYork);


//获取世界标准时间UTC，可以使用Clock.systemUTC()方法获取UTC时区的Clock对象。
ZonedDateTime utc = ZonedDateTime.now(Clock.systemUTC());
System.out.println(utc);


//获取系统默认时区的ZonedDateTime对象，使用ZonedDateTime.now()方法。
ZonedDateTime now = ZonedDateTime.now();
System.out.println(now);
System.out.println(now.getYear());
System.out.println(now.getZone());

Calendar instance = Calendar.getInstance(TimeZone.getTimeZone(zoneId));
System.out.println(instance);
```

获取世界标准时区的代码是：

```java
//获取世界标准时间UTC，可以使用Clock.systemUTC()方法获取UTC时区的Clock对象。
ZonedDateTime utc = ZonedDateTime.now(Clock.systemUTC());
System.out.println(utc);
```

## 15.代替 Date

### i. `Instant` :时间线上的某个时刻/时间戳

​    例如：2024-01-18T17:24:11.772Z

* 通过获取instant的对象可以拿到此刻的时间，该时间由两部分组成：从1970-01-01  00:00:00 开始走到此刻的**总秒数+不够1秒的纳秒数**

| 方法名                                | 说明                                     |
| ------------------------------------- | ---------------------------------------- |
| public  static  Instant  **now()**    | 获取当前时间的 Instant 对象（标准时间）  |
| public  long  **getEpochSecond()**    | 获取从1970-01-01T00:00:00 开始记录的秒数 |
| public  int  **getNano()**            | 从时间线开始，获取从第二个开始的纳秒数   |
| plusMillis  plusSeconds   plusNanos   | 增加时间系列的方法                       |
| minusMillis  minusSeconds  minusNanos | 减少时间系列的方法                       |
| equals   、 isBefore   、isAfter      | 判断时间系列的方法                       |

```java
//1.创建Instant对象，获取此刻时间信息
Instant now = Instant.now();
System.out.println(now);

//2.获取总秒数
long second = now.getEpochSecond();
System.out.println(second);

//3.不够一秒的纳秒数
long nano = now.getNano();
System.out.println(nano);

System.out.println("-----------------");
Instant instant = now.plusSeconds(999);
System.out.println(instant);
Instant instant1 = now.minusSeconds(999);
System.out.println(instant1);

//Instant对象的作用:做代码性能分析，或者记录用户的操作时间点
Instant now1 = Instant.now();
//代码执行
Instant now2 = Instant.now();
System.out.println(now2.getNano() - now1.getNano());
```

## 17.代替SimpleDateFormat

### i.`DateTimeFormatter`:格式化器，用于时间的格式化、解析

| 方法名                                                     | 说明               |
| ---------------------------------------------------------- | ------------------ |
| public  static  DateTimeFormatter  **ofPattern(时间格式)** | 获取格式化时间对象 |
| public  String  **format(时间对象)**                       | 格式化时间         |

其实还有另一种方法，就是LocalDateTime提供的

| 方法名                                                       | 说明       |
| ------------------------------------------------------------ | ---------- |
| public  String  **format(DateTimeFormatter  formatter)**     | 格式化时间 |
| public  static  LocalDateTime  **parse(CharSequence  text, DateTimeFormatter  formatter)**** | 解析时间   |

```java
//1.创建一个时间格式化器对象
DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH:mm:ss");

//2.对时间进行格式化
LocalDateTime now = LocalDateTime.now();
System.out.println(now);

String str = dtf.format(now);    //正向格式化
System.out.println(str);

//3.格式化时间，其实还有一种方法
String rs = now.format(dtf);    //反向格式化
System.out.println(rs);


//4.解析时间一般使用LocalDateTime提供的解析方法解析
String dateStr = "2020年11月11日 11:11:11";
LocalDateTime parse =LocalDateTime.parse(dateStr,dtf);
System.out.println(parse);
```

## 18.Period :计算日期间隔（年、月、日）

* 用于计算两个LocalDate对象相差的年数、月数、天数。

| 方法名                                                       | 说明                            |
| ------------------------------------------------------------ | ------------------------------- |
| public  static  Period  **between(LocalDate  start,  LocalDate  end)** | 传入2个日期对象，得到Period对象 |
| public  int  **getYear()**                                   | 计算隔几年，并返回              |
| public  int  **getMonths()**                                 | 计算隔几个月，并返回            |
| public  int  **getDays()**                                   | 计算隔多少天，并返回            |

```java
LocalDate start = LocalDate.of(2020, 1, 1);
LocalDate end = LocalDate.of(2020, 12, 31);
System.out.println(start.until(end));   //P11M30D

Period period =Period.between(start,end);
System.out.println(period);         //P11M30D
System.out.println(period.getYears());  //0
System.out.println(period.getMonths());  //11
System.out.println(period.getDays());   //30
```

## 19.Duration（持续时间）

* 可以用于计算两个时间对象相差的天数、小时数、分数、秒数、纳秒数;
* 支持LocalTime、LocaDateTime、Instant等时间。

| 方法名                                                       | 说明                               |
| ------------------------------------------------------------ | ---------------------------------- |
| public  static  Duration  **between(开始时间对象1，截止时间对象2)** | 传入两个时间对象，得到Duration对象 |
| public  long  **toDays()**                                   | 计算隔多少天，并返回               |
| public  long  **toHours()**                                  | 计算隔多少小时，并返回             |
| public  long  **toMinutes()**                                | 计算隔多少分钟，并返回             |
| public  long  **getSeconds()**                               | 计算隔多少秒，并返回               |
| public  long  **toMillis()**                                 | 计算隔多少毫秒，并返回             |
| public  long  **toNanos()**                                  | 计算隔多少纳秒，并返回             |

```java
    LocalDateTime start = LocalDateTime.of(2075,11,11,5,11,11);
    LocalDateTime end =  LocalDateTime.of(2077,12,11,11,20,11);
    Duration duration =Duration.between(start,end);   //PT18270H9M
    System.out.println(duration);
    System.out.println(duration.toDays());
    System.out.println(duration.toHours());
    System.out.println(duration.toMillis());
    System.out.println(duration.toMinutes());
    System.out.println(duration.toNanos());
    System.out.println(duration.getSeconds());
```

## 20.Arrays

* 用来操作数组的工具类

  | 方法名                                                       | 说明                                           |
  | ------------------------------------------------------------ | ---------------------------------------------- |
  | public  static  String  **toString(类型[]  arr)**            | 返回数组的内容                                 |
  | public  static  int[]  **copyOfRange(类型[]  arr,  起始索引,  结束索引)** | 拷贝数组（指定范围、包前不包后）               |
  | public  static  **copyOf(类型[] arr,  int  newLength)**      | 拷贝数组，可以指定新数组的长度（一般用来扩容） |
  | public  static  **setAll(double[]  array,  IntToDoubleFunction  generator)** | 把数组中的原数据改为新数据                     |
  | public  static  void  **sort(类型[]  arr)**                  | 对数组进行排序（默认升序）                     |

  ```java
  ///1.public  static String toString(int[] a)
  //返回指定数组的内容的字符串表示形式
  int[] arr = {1,2,3,4,5,70,60};
  String str1 = Arrays.toString(arr);
  System.out.println(str1);
  
  //2.public static int[] copyOfRange(int[] original, int from, int to)
  //复制数组的一部分到新数组中,(包前不包后）
  int[] arr2 = Arrays.copyOfRange(arr,2,5);
  System.out.println(Arrays.toString(arr2));  //[3, 4, 5]
  
  //3.public static copyOf(int[] original, int newLength)
  //复制数组的一部分到新数组中,指定长度一般用来扩容数组
  int[] arr3 = Arrays.copyOf(arr,10);
  System.out.println(Arrays.toString(arr3));  //[1, 2, 3, 4, 5, 70, 60, 0, 0, 0]
  
  //4。public static setAll(double[] array, IntToDoubleFunction generator)
  //将数组中的元素设置为指定的值
  double[] price = new double[]{99.8,128,100};
  //把所有价格打八折，然后存进去
  Arrays.setAll(price, new IntToDoubleFunction() {
      @Override
      public double applyAsDouble(int value) {
          //value = 0 1 2
          return price[value]*0.8;
      }
  });
  System.out.println(Arrays.toString(price));  //[79.84, 102.4, 80]
  
  //5.public static sort(int[] a)
  //对数组进行升序排序
  Arrays.sort(price);
  System.out.println(Arrays.toString(price));
  ```

如果数组中存储的是对象，如何排序？

### 方式一：让该对象的类实现`Comparable`（比较规则）接口,然后重写`compareTo`方法，自己来制定比较规则

```java
@Override
public int compareTo(Student o) {
    //约定1：如果左边对象大于右边对象，请您返回正整数
    //约定2：如果左边对象小于右边对象，请您返回负整数
    //约定3：如果左边对象等于右边对象，请您返回0
   /* if (this.age > o.age) {
        return 1;
    } else if (this.age < o.age) {
        return -1;
    }
    return 0;*/
    return this.age - o.age; //简化代码
}
```

```java
public class Student implements Comparable<Student>{
    private String name;
    private double height;
    private int age;

    public Student() {
    }

    public Student(String name, double height, int age) {
        this.name = name;
        this.height = height;
        this.age = age;
    }

   

    //制定比较规则
    //this   o
    @Override
    public int compareTo(Student o) {
        //约定1：如果左边对象大于右边对象，请您返回正整数
        //约定2：如果左边对象小于右边对象，请您返回负整数
        //约定3：如果左边对象等于右边对象，请您返回0
       /* if (this.age > o.age) {
            return 1;
        } else if (this.age < o.age) {
            return -1;
        }
        return 0;*/
        return this.age - o.age; //简化代码
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", height=" + height +
                ", age=" + age +
                '}';
    }
}
```

```java
Student[] students = new Student[4];
students[0] = new Student("张三",188.2,26);
students[1] = new Student("李四",168.2,24);
students[2] = new Student("王五",168.2,22);
students[3] = new Student("赵六",178.2,23);

Arrays.sort(students);
System.out.println(Arrays.toString(students));
```

### 方式二：使用下面这个`sort`方法，创建`Comparator`比较器接口的匿名内部类对象，然后自己制定比较规则

```java
public static <T> void sort(T[] arr, Comparator<? super T> c)  对数组进行排序，支持自定义规则
```

实例代码如下(传入小数)：

```java
Arrays.sort(students, new Comparator<Student>() {
    @Override
    public int compare(Student o1, Student o2) {
        /*//制定比较规则，左边对象o1，右边对象o2
        if (o1.getAge() > o2.getAge()){
            return 1;
        }else if (o1.getAge() < o2.getAge()){
            return -1;
        }
        return 0; //如果上面两个条件都不满足，返回0，表示两个对象相等。*/

        return Double.compare(o1.getHeight(), o2.getHeight()); //升序
        //return Double.compare(o2.getHeight(), o1.getHeight()); //降序
    }
});
```

## ArrayList（一种集合)

1.**集合**是一种容器，用来**装数据**，类似于数组

   集合**大小可变**，开发中用的更多

2.ArrayList会提供**创建容器对象的方式**和提供**相应的方法对容器进行操作**<u>(增删改查)</u>

### 1.ArrayList使用

Array是泛型类

| 构造器           | 说明                 |
| ---------------- | -------------------- |
| public ArrayList | 创建一个空的集合对象 |

| 常用方法名                                  | 说明                                   |
| ------------------------------------------- | -------------------------------------- |
| public boolean **add(E e)**                 | 将指定的元素添加到此集合的未尾         |
| public void **add(int index, E element)**** | 在此集合中的指定位置插入指定的元素     |
| public E **get(int index)**                 | 返回指定索引处的元素                   |
| public int **size()**                       | 返回集合中的元素的个数                 |
| public E **remove(int index)**              | 删除指定素引处的元素，返回被删除的元素 |
| public boolean **remove(Object o)**         | 删除指定的元素，返回删除是否成功       |
| public E **set(int index,E element)****     | 修改指定索引处的元素，返回被修改的元素 |

可以用    **<>**    约束数据类型（泛型)

```java
ArrayList<String> list = new ArrayList<>();
```

```java
mport java.util.ArrayList;

public class ArrayListDemo1 {
    public static void main(String[] args) {
        //1.创建一个ArrayList的集合对象
        ArrayList<String> list = new ArrayList<>();
        list.add("fz666");
        list.add("fz666");
        list.add("www");
        System.out.println(list);

        //2.往集合中的某个索引位置处添加一个数据
        list.add(1,"MySQL");//从第二个位置插入“MySQL”，第二个位置是索引1
        System.out.println(list);//[fz666, MySQL, fz666]

        //3.根据索引获取集合中某个索引位置处的值
        String rs= list.get(1);
        System.out.println(rs);//MySQL

        //4.获取集合的大小
        System.out.println(list.size());//4

        //5.根据索引删除集合中的某个元素值
        System.out.println(list.remove(1));//MySQL
        System.out.println(list);//[fz666, fz666, www]

        //6。直接删除某个元素值，删除成功返回true
        System.out.println(list.remove("www"));//ture
        System.out.println(list);//[fz666, fz666]

        //********默认删除的是第一次出现的这个“fz666"数据*******
        list.add(1,"nihao");
        System.out.println(list.remove("fz666"));//true
        System.out.println(list);//[nihao, fz666]

        //7.修改某个索引位置处的数据，修改后返回原来的值给我们
        System.out.println(list.set(1,"fzaaa"));//fz666
        System.out.println(list);//[nihao, fzaaa]
        
    }
}
```

#### 掌握从容器中找出某些数据并成功删除的技巧

```java
import java.util.ArrayList;

public class ArrayListTest2 {
    public static void main(String[] args) {
//    需求：现在假如购物车中存储了如下这些商品：Jva入门，宁夏枸杞，黑枸杞，人字拖，特级枸杞，枸杞子。现在用户不想买枸杞了，选择了批量删除，请完成该需求。
//    分析：
//     ①后台使用ArrayList集合表示购物车，存储这些商品名。
//     ②遍历集合中的每个数据，只要这个数据包含了“枸杞”则删除它。
//     ③输出集合看是否已经成功删除了全部枸杞数据了。
        ArrayList<String> list =new ArrayList<>();
        list.add("Java入门");
        list.add("宁夏枸杞");
        list.add("黑枸杞");
        list.add("人字拖");
        list.add("特级枸杞");
        list.add("枸杞子");
        System.out.println(list);

        //找出包含枸杞的数据并删除

//        //方式一：每次删除一个数据后，让i往左边退一步
//        for (int i = 0; i < list.size(); i++) {
//            String ele = list.get(i);
//            if(ele.contains("枸杞")){
//                list.remove(ele);
//                i--;//挺重要的一步
//            }
//        }
//        System.out.println(list);

     //方式二：从集合的后面倒着遍历并删除
        for (int i = list.size()-1; i >=0 ; i--) {
            String ele =list.get(i);
            if(ele.contains("枸杞")){
                list.remove(ele);

            }
        }
        System.out.println(list);
    }
}
```

### 2.ArrayList综合案例

```java
public class Food {
    private String name;
    private  double price;
    private String desc;

    public Food() {
    }

    public Food(String name, double price, String desc) {
        this.name = name;
        this.price = price;
        this.desc = desc;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public String getDesc() {
        return desc;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public void setDesc(String desc) {
        this.desc = desc;
    }


}
```

```java
import java.util.ArrayList;
import java.util.Scanner;

public class FoodOperator {
    //1.定义一个ArrayList集合对象，负责存储菜品对象信息
    private ArrayList<Food> foodList = new ArrayList<>();
    //foodlist[]

    //2.开发上架菜品功能
    public void addFood(){
        //3.创建一个菜品对象，封装上架的菜品信息
        Food f =new Food();
        //4.录入菜品信息
        Scanner sc =new Scanner(System.in);
        System.out.println("请您输入该菜品名称:");
        String name =sc.next();
        f.setName(name);

        System.out.println("请您输入菜品价格:");
        double price =sc.nextDouble();
        f.setPrice(price);

        System.out.println("请您输入菜品描述:");
        String desc =sc.next();
        f.setDesc(desc);

        //5.把菜品对象存入集合中去
        foodList.add(f);
        System.out.println("上架成功");
    }
    //6.展示菜品
    //foodlist=[f1,f2,f3,...]
    public void showAllFoods(){
        if(foodList.size()==0){
            System.out.println("什么菜品都没有");
            return;
        }
        for (int i = 0; i < foodList.size(); i++) {
            foodList.get(i);
            Food f= foodList.get(i);
            System.out.println(f.getName());
            System.out.println(f.getPrice());
            System.out.println(f.getDesc());
            System.out.println("--------------------------------------");

        }

    }
    //负责展示操作界面
    public void start(){
        while (true) {
            System.out.println("请选择功能:");
            System.out.println("1.上架菜品");
            System.out.println("2.展示菜品");
            System.out.println("3.退出");
            Scanner sc =new Scanner(System.in);
            System.out.println("请选择您的操作：");
            String  command =sc.next();
            switch (command){
                case "1":
                    addFood();
                    break;
                case "2":
                    showAllFoods();
                    break;
                case "3":
                    System.out.println("下次再来哦~");
                    return;
                default:
                    System.out.println("您输入的命令不存在");
            }
        }
    }

}
```

```java
import java.util.ArrayList;

public class ArrayListTest3 {
    public static void main(String[] args) {
        FoodOperator operator =new FoodOperator();
        operator.start();
    }
    //需求：完成菜品的上架，以及菜品的信息浏览功能
    //1.设计菜品类Food，负责创建菜品对象，封装菜品数据
    //2.设计一个菜品操作类,FoodOperator
    

}
```

