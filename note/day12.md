# day12

**1.ArrayList使用**

Array是泛型类

| 构造器           | 说明                 |
| ---------------- | -------------------- |
| public ArrayList | 创建一个空的集合对象 |

| 常用方法名                            | 说明                                   |
| ------------------------------------- | -------------------------------------- |
| public boolean add(E e)               | 将指定的元素添加到此集合的未尾         |
| public void add(int index, E element) | 在此集合中的指定位置插入指定的元素     |
| public E get(int index)               | 返回指定索引处的元素                   |
| public int size()                     | 返回集合中的元素的个数                 |
| public E remove(int index)            | 删除指定素引处的元素，返回被删除的元素 |
| public boolean remove(Object o)       | 删除指定的元素，返回删除是否成功       |
| public E set(int index,E element)     | 修改指定索引处的元素，返回被修改的元素 |

可以用    **<>**    约束数据类型

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

**2.掌握从容器中找出某些数据并成功删除的技巧**

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

**3.ArrayList综合案例**

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

为了阅读方便，关于ATM系统的项目就放在明天的#day13#了
