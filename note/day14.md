# day14

### 登录功能实现

 a.如果系统没有任何账户对象，则不允许登录

 b.让用户输入登录的卡号，先判断卡号是否正确，如果不正确要给出提示

 c.如果卡号正确，让用户输入账户密码，如果密码不正确要给出提示，如果密码也正确，要给出的登陆成功的提示

```java
private void login(){
    System.out.println("==系统登录==");
    //1.判断系统是否存在账户对象，存在才能登录，不存在直接结束登陆操作
    if(accounts.size()==0){
        System.out.println("当前系统中无任何账户");
        return;
    }
    while (true) {
        System.out.println("请输入您的登录卡号：");
        String cardid= sc.next();
        //判断卡号是否存在
        Account acc =getAccountByCardId(cardid);
        if(acc==null){
            //卡号不存在
            System.out.println("您输入的卡号不存在，请确认~~");
        }else {
            System.out.println("请您输入登录密码:");
            String passWord = sc.next();
            //判断密码是否正确
            while (true) {
                if(acc.getPassWord().equals(passWord)){
                    System.out.println("恭喜您，"+acc.getUserName()+"成功登陆了系统，您的卡号是:"+acc.getCardid());
                    return;
                }else{
                    System.out.println("您输入的密码不正确，请确认~");
                }
            }
        }
    }


}
```

### 用户登录成功后，需要**用户操作页展示、查询账户、退出账户**等功能

```java
private void showUserCommand(){
    while (true) {
        System.out.println(loginAcc.getUserName()+"您可以选择如下功能进行账户的处理===");
        System.out.println("1.查询账户");
        System.out.println("2.存款");
        System.out.println("3.取款");
        System.out.println("4.转账");
        System.out.println("5.密码修改");
        System.out.println("6.退出登录");
        System.out.println("7.注销当前账户");
        System.out.println("请选择：");
        int command =sc.nextInt();
        switch (command){
            case 1:
                //查询当前账户
                showLoginAccount();
                break;
            case 2:
                //存款
                break;
            case 3:
                //取款
                break;
            case 4:
                //转账
                break;
            case 5:
                //密码修改
                break;
            case 6:
                //退出
                System.out.println(loginAcc.getUserName()+",您退出系统成功");
                return;
            case 7:
                //注销当前账户
                break;
            default:
                System.out.println("您当前选择的操作不存在，请确认");
        }
    }
}
```

```java
private void showLoginAccount (){
    System.out.println("==当前您的账户信息如下==");
    System.out.println("卡号:"+loginAcc.getCardid());
    System.out.println("户主:"+loginAcc.getUserName());
    System.out.println("性别"+loginAcc.getSex());
    System.out.println("余额:"+loginAcc.getMoney());
    System.out.println("每次取现额度:"+loginAcc.getLimit());

}
```

### 存款、取款功能的实现

1.取钱时要判断账户的余额是否大于100，如果够，让用户输入取款金额

2.判断取款金额是否超过了当次限额，以及余额是否足够

```java
private void depositMoney() {
    System.out.println("==存钱操作==");
    System.out.println("请您输入存款金额");
    double money = sc.nextDouble();
    loginAcc.setMoney(loginAcc.getMoney()+money);
    System.out.println("恭喜您存钱"+money+"成功，余额是："+loginAcc.getMoney());
}
```

```java
private void drawMoney() {
    System.out.println("==取钱操作==");
    //判断账户余额是否大于100元
    if(loginAcc.getMoney()<100){
        System.out.println("您的账户余额不足100元");
        return;
    }
    while (true) {
        System.out.println("请您输入取款金额");
        double money =sc.nextDouble();
        if(loginAcc.getMoney()>=money){
            //账户中的余额足够
            //判断当前取款金额是否超过单次限额
            if(money> loginAcc.getLimit()){
                System.out.println("您当前取款金额超过了每次限额，您每次最多可取："+loginAcc.getLimit());

            }else{
                //更新当前账户的余额
                loginAcc.setMoney(loginAcc.getMoney()-money);
                System.out.println("您取款："+money+"成功，取款后您剩余"+loginAcc.getMoney());
                break;
            }
        }else{
            System.out.println("余额不足，您的账户中的余额是:"+loginAcc.getMoney());
            ;
        }
    }
}
```

### 用户转账功能

  i.转帐前要判断自己账户是否有钱，系统中是否有其他账户

  ii.接下来让用户输入对方卡号，判断对方账户是否存在，账户如果存在，还需要认证对方账户的户主姓氏

  

```java
private void transferMoney() {
    System.out.println("==用户转账==");
    if(accounts.size()<2){
        System.out.println("当前系统中只有你一个账户，无法为其它账户转账");
        return;
    }
    if(loginAcc.getMoney()==0){
        System.out.println("您的账户中余额为0，无法进行转账");
        return;
    }
    while (true) {
        System.out.println("请您输入对方的卡号：");
        String cardid =sc.next();
        Account acc =getAccountByCardId(cardid);
        if(acc==null){
            System.out.println("您输入的对方的卡号不存在~");
        }else {
            //对方账户存在,让用户认证对方姓氏
            String name ="*"+ acc.getUserName().substring(1);

            System.out.println("请您输入【"+name+"】姓氏");
            String preName= sc.next();
            if(acc.getUserName().startsWith(preName)){
                System.out.println("认证通过");
                while (true) {
                    System.out.println("请您输入转账给对方的金额：");
                    double money =sc.nextDouble();
                    //判断金额是否超过自己的余额
                    if(loginAcc.getMoney()>=money){
                        //更新自己的账户余额和对方的账户余额
                        loginAcc.setMoney(loginAcc.getMoney()-money);
                        acc.setMoney(acc.getMoney()+money);
                        System.out.println("您转账成功了~~~");
                        return;
                    }else {
                        System.out.println("您余额不足，无法给对方转账"+money+"元，您最多转账"+loginAcc.getMoney()+"元~");
                    }
                }
            }else {
                System.out.println("您认证的姓氏有问题");
            }


        }
    }

}
```

### 销户

```java
private boolean deleteAccount() {
    System.out.println("==进行销户操作==");
    //问用户是否确定销户
    System.out.println("请问您确认销户吗？y/n");
    String command = sc.next();
    switch (command){
        case "y":
            //判断用户的账户中是否有钱
            if(loginAcc.getMoney()==0){
                accounts.remove(loginAcc);
                System.out.println("您的账户已经成功注销~~");
                return true;

            }else {
                System.out.println("您的账户中存在金额，不允许销户~~");
                return false;
            }

        default:
            System.out.println("好的，您的账户保留");
            return false;
    }

}
```

### 密码修改

 i.要认证用户当前的密码

 ii.认证通过后，需要用户输入2次新密码

ii.两次密码一样，则更新账户密码，并回到欢迎页

```java
private void updatePassWord() {
    //提醒用户认证当前密码
    while(true) {
        System.out.println("请您输入当前账户的密码:");
        String passWord = sc.next();
        //认证密码是否正确
        if (loginAcc.getPassWord().equals(passWord)) {
            //修改密码
            while (true) {
                System.out.println("请您输入新密码：");
                String newPassWord =sc.next();
                System.out.println("请您再次输入密码:");
                String okPassWord =sc.next();
                if(okPassWord.equals(newPassWord)){
                    loginAcc.setPassWord(okPassWord);
                    System.out.println("密码修改成功！");
                    return;
                }else{
                    System.out.println("您输入的两次密码不一致~~");
                }
            }

        } else {
            System.out.println("您当前输入的密码不正确");
        }
    }
}
```

---------------------------

明天开始构思ddl系统

