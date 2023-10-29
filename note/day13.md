# day13

**ATM系统**

**i.分析：**

1.面向对象编程：每个**账户**都是一个账户对象，所以需要**设计账户类Accout**；

​							 **ATM** 同样是一个对象，需要设计类，代表ATM管理系统，负责**对账户的处理**；

2.使用集合容器：ATM管理类中需要提供一个容器用于存储系统全部账户对象的信息，我们选用**ArrayList集合**

3.程序流程控制

4.API进行比较分析：例如String

**系统架构搭建**

  a.定义一个**账户类Account**，至少需要包含（卡号、姓名、性别、密码、余额、每次取现额度）

  b.定义一个**ATM类**，用来代表ATM系统，负责提供所有的业务需要，比如：展示ATM的系统欢迎页、开通账户、转账......

  c.定义一个**测试类Test**，对系统进行测试

  **系统欢迎页设计**

  在ATM类设计一个方法**start()**,方法里负责展示欢迎界面

```java
public class Account {
    private String cardid;
    private String userName;
    private char  sex;
    private String passWord;
    private double money;
    private double limit;//限额
	
    
    //默认有无参构造器
    public String getCardid(){
        return getCardid();
    }
    public String getUserName(){
        return userName;
    }
    public char getSex(){
        return sex;
    }

    public String userName(){
        return userName;
    }

    public double getMoney() {
        return money;
    }

    public double getLimit(){
        return limit;
    }

    public String getPassWord() {
        return passWord;
    }

    public void setCardid(String cardid) {
        this.cardid = cardid;
    }
    public void setUserName(String userName){
        this.userName=userName;
    }

    public void setSex(char sex){
        this.sex=sex;
    }

    public void setLimit(double limit) {
        this.limit = limit;
    }

    public void setMoney(double money) {
        this.money = money;
    }

    public void setPassWord(String passWord) {
        this.passWord = passWord;
    }


}
```

```java
import java.util.ArrayList;
import java.util.Scanner;

public class ATM {
    public ArrayList<Account> accounts =new ArrayList<>();//[]
    private Scanner sc =new Scanner(System.in);//给ATM自己用要封装
    //启动ATM系统
    public void  start(){
        while (true) {
            System.out.println("===欢迎您进入到了ATM系统===");
            System.out.println("1.用户登录");
            System.out.println("2.用户开户");
            System.out.println("请选择:");
            int command =sc.nextInt();
            switch (command){
                case 1:
                    break;
                case 2:
                    break;
                default:
                    System.out.println("没有该操作~~");
            }
        }
    }

}
```

```java
public class Test {
    public static void main(String[] args) {
        ATM atm =new ATM();
        atm.start();
    }
}
```

**开户功能实现**

 a.新增一个账户，即往系统的**账户集合中添加一个账户对象**

 b.用户信息包含：姓名、性别、密码、每次取现额度、卡号（8位数字，由系统自动生成，卡号之间不能重复)

   ①为新开的账户生成一个新卡号

```java
 private void createAccount(){//ATM类自己调用，建议封装
        System.out.println("==系统开户操作==");
        //1.创建一个账户对象，用于封装用户的开户信息
        Account acc =new Account();
        //2.需要用户输入自己的用户信息，赋值给账户对象
        System.out.println("请您输入您的账户名称:");
        String name =sc.next();
        acc.setUserName(name);
        while (true) {
            System.out.println("请输入您的性别:");
            char sex = sc.next().charAt(0);
            if(sex=='男'||sex=='女'){
                acc.setSex(sex);
                break;
            }else{
                System.out.println("您输入的性别有误~只能是男或女~");
            }
        }
        while (true) {
            System.out.println("请您输入您的账户密码：");
            String passWord =sc.next();
            System.out.println("请确认您的账户密码：");
            String okpassWord =sc.next();
            //判断两次密码是否一样
            if(okpassWord.equals(passWord)){
                acc.setPassWord(okpassWord);
                break;
            }else{
                System.out.println("您输入的两次密码不一致，请您确认~~~");
            }
        }
        System.out.println("请您输入取现额度:");
        double limit= sc.nextDouble();
        acc.setLimit(limit);
        //由系统为这个账户自动生成卡号，不能重复
        String newCardid= createCardId();
        acc.setCardid(newCardid);


        //3.把这个账户对象，存入到账户集合中去
        accounts.add(acc);
        System.out.println("恭喜您，"+acc.getUserName()+"开户成功，您的卡号是:"+acc.getCardid());
    }
    //返回8位数字的卡号，不能与其他账号重复
    private String createCardId(){
        while (true) {
            String cardid="";
            //使用循环，循环8次，每次产生随机数给cardid连接起来
            Random r= new Random();
            for (int i = 0; i < 8; i++) {
               int data=  r.nextInt(10);
               cardid += data;
            }
            //判断cardid的卡号是否与其他账户中的卡号重复
            Account acc = getAccountByCardId(cardid);
            if (acc==null){
                //说明cardid没有找到账号对象，不重复可以返回
                return cardid;
            }
        }
    }
    //根据卡号查询账户对象返回 accounts =[c1,c2,c3....]
    private  Account getAccountByCardId(String cardId){
        //遍历全部账户对象
        for (int i = 0; i < accounts.size(); i++) {
            Account acc= accounts.get(i);
            if(acc.getCardid().equals(cardId)){
                return acc;
            }
        }
        return null;//查无此账户
    }
}
```

```java
public String getUserName(){
    return userName+(sex=='男'?"先生":"女士");
}
```