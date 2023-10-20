**1.开发步骤:**编写代码，编译代码（使用javac编译成‘    .class’字节码文件），运行代码（使用java运行)

**2.我的第一个程序**

> **HelloWorld.java**

```java
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("Hello World");
    }
}
```

[^注意]:**<u>HelloWorld是类名，文件名称必须与代码中的类名称一致。</u>**

+ **编译命令:** javac HelloWorld.java
+ **运行命令:**java HelloWorld

**3.JDK的组成(Java开发工具包)**

**i.JRE**（java的运行环境）

     JVM:Java虚拟机，真正运行Java程序的地方
    
     核心类库：Java自己写好的程序，可以调用（API）

**ii.开发工具：java javac**

**4.java程序经javac编译后生成class文件在虚拟机上运行（我们的程序只需要开发一次，就可以在各种安装了JVM的系统平台上运行**

**5.管理Java程序:project—>model—>package—>class(编译后放在out目录)**



**------今天安装了JDk1.8和IDEA,花了挺长时间的，希望接下来好好努力吧**

