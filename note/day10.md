# day10

**5.String**

**i.String类创建对象封装字符串数据的方式（两种方式）**

| 构造器                           | 说明                                   |
| -------------------------------- | -------------------------------------- |
| public   String()                | 创建一个空白字符串对象，不含有任何内容 |
| public   String(String original) | 根据传入的字符串内容，来创建字符串对象 |
| public  String(char[] chars)     | 根据字符数组的内容来创建字符串对象     |
| public  String(byte[] byte)      | 根据字节数的内容，来创建字符串对象     |

续昨天的

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

**ii.String的常用方法**

| 方法名                                                       | 说明                                                     |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| public int length（）                                        | 获取字符串的长度返回（就是字符个数）                     |
| public char charAt(int index)                                | 获取某个索引位置处的字符返回                             |
| public char[]  toCharArray（）:                              | 将当前字符串转换成字符数组返回                           |
| public boolean equals(object anobject)                       | 判断当前字符串与另一个字符串的内容一样，一样返回true     |
| public boolean equalsIgnoreCase(String anotherstring)        | 判断当前字符串与另一个字符串的内容是否一样（忽略大小写） |
| public String substring(int beginIndex,int endIndex)         | 根据开始和结束索引进行截取，得到新的字符串（包前不包后） |
| public String substring(int beginIndex)                      | 从传入的索引处截取，截取到末尾，得到新的字符串返回       |
| public String replace(CharSequence target,CharSequence replacement) | 使用新值，将字符串中的旧值替换，得到新的字符串           |
| public boolean contains(CharSequence s)                      | 判断字符串中是否包含了某个字符串                         |
| public boolean startswith(String prefix)                     | 判断字符串是否以某个字符串内容开头，开头返回true,反之    |
| public string[] split(String regex)                          | 把字符串按照某个字符串内容分割，并返回字符串数组回来     |

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