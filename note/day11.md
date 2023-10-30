# day11

### 1.String的注意事项

   #### i.String对象的内容不可改变，被称为不可变字符串对象**

   只要是以"....."方式写出的字符串对象，会在**堆内存**中的**字符串常量池**中存储

   每次试图改变字符串对象实际上是**新产生了新的字符串对象了**，变量**每次都是指向了新的字符串对象**，之前的字符串对象的内容

   确实没有改变

ii.只要是以"......"方式写出的字符串对象，会存储到**字符串常量池**，且相同内容的字符串**只存储一份**！；(节约内存)

​	但通过new方式创建字符串对象，**每new一次都会产生一个新的对象放在堆内存中**。

​	

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

### 2.案例 ①:完成用户登录

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

#### 案例②使用String开发验证码

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

### ArrayList（一种集合)

1.**集合**是一种容器，用来**装数据**，类似于数组

   集合**大小可变**，开发中用的更多

2.ArrayList会提供**创建容器对象的方式**和提供**相应的方法对容器进行操作**<u>(增删改查)</u>



