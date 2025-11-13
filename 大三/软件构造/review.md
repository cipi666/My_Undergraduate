# <center>软件构造复习大纲

## <center>重要语法

### Java数据类型
1. 基本数据类型（数值型，字符型，布尔型） $\rightarrow$ 变量中直接存储的是数据本身的值。（栈内存）
2. 引用数据类型（类，接口，数组） $\rightarrow$ 变量中存储的是对象在内存中的地址。（堆内存）

### Java输入与输出
#### 标准输入System\.in
**System.in是一个InputStream（字节输入流）类的对象**，通常采用以下两种封装方式：

1. 使用字符流
```
BufferedReader stdin = new BufferedReader(new InputStreamReader(System.in));
System.out.print("enter a line:");
System.out.println(stdin.readLine());
```
2. 使用```java.util.Scanner```
```
Scanner stdin = new Scanner(System.in);
System.out.print("enter a line:");
System.out.println(stdin.nextLine());
```
#### 标准输出System.out
print和println的参数完全一样，不同之处在于println输出后换行而print不换行。write方法用来输出字节数组，在输出时不换行。

### Java异常机制
异常指不期而至的各种状况，如：文件找不到、网络连接失败、非法参数等。异常是一个事件，它发生在程序运行期间，干扰了正常的指令流程。Java通过API中Throwable类的众多子类描述各种不同的异常。

#### 问答题考点：throw和throws的用法
```
public static int getElement(int[] arr, int index) throws Exception,IOException { 
    if(arr==null) { 
        throw new NullPointerException("指针为空");
    }else if(index>=arr.length-1) {
        throw new ArrayIndexOutOfBoundsException("数组越界");
    } 
    int ele = arr[index]; 
    return ele;
}
```
- **共同点**：两者都是**消极处理异常的方式，只负责抛出异常**，但是不会由函数去处理异常，真正的处理异常由函数的上层调用处理
- **区别**：
  - throws用于方法头，表示的只是异常的申明；而throw用于方法内部，抛出的是异常对象；
  - throws可以一次性抛出多个异常，而throw只能抛出一个。

#### Java虚拟机
JVM是通过软件来模拟Java字节码的指令集，是Java程序的运行环境。其特点有：
1. 一次编译，到处运行；
2. 自动内存管理；
3. 自动垃圾回收功能。

#### Java垃圾回收
C语言和C++采用**显式分配器**将堆空间完全暴露给用户，优点在于功力深厚的程序员可以很好地利用堆空间内存。其缺点也很明显，每一次分配内存后都要手动释放，否则很容易引起内存泄漏。

Java的核心思想是面向对象，屏蔽了很多底层细节，让程序员更多地关注“对象”。Java使用**隐式分配器**，程序员只管创建对象使用**堆内存**，回收交给垃圾回收器。

Java的垃圾回收器在执行引擎中，垃圾回收的主要对象是**JVM堆空间**。

## <center>面向对象
**面向对象的三大特性：封装，继承和多态。**
### 简答题考点：面向对象与面向过程的优缺点
- 面向过程：
  - 优点：简单逻辑下快速开发，计算效率高
  - 缺点：灵活性差、无法适用复杂情况
- 面向对象：
  - 优点：低耦合、易复用、易扩展
  - 缺点：性能相对低
### 简答题考点：类与对象的关系
- 类是对象的抽象，是创建对象的模板（代表了同一批对象的共性与特征） 
- 对象是类的具体实例（不同对象之间还存在着差异）
- 同一个类可以定义多个对象（一对多关系）
- 类是**静态**的，类的存在、语义和关系在程序设计时（执行前）就已经定义好了。
- 对象是**动态**的，对象在程序执行时可以被创建，修改，删除。
### 简答题考点：封装的优点
- **安全性**：数据和数据相关的操作被包装成对象，可以控制数据的访
问权限。
- **高内聚**：一种对象只做好一件（或者一类相关的）事情，对象内部
的细节外部不关心也看不到。便于修改内部代码，提高可维护性。
- **低耦合**：不同种类的对象间相互的依赖尽可能地降低。简化外部调
用，便于调用者使用，便于扩展和协作。
- **可复用性**：面向对象编程的主要目的是方便程序员组织和管理代码，
快速梳理编程思路，带来编程思想上的革新。
### 类的构造方法
构造方法是用于创建类对象的特殊方法。它的主要作用是初始化对象的属性，确保对象在创建时处于合法的初始状态。构造方法的特点包括：
- 方法名必须与类名相同。
- 没有返回类型（包括void）。
- 只能通过new关键字调用，不能像普通方法那样直接调用。
- 支持重载，可以根据参数列表的不同定义多个构造方法。
- 构造方法不能被static修饰，也不能被子类继承，但子类可以通过super()调用父类的构造方法。
```
public class Person {
   private String name;
   private int age;
   // 构造方法
   public Person(String name, int age) {
       this.name = name;
       this.age = age;
   }
}
```
#### this关键字
代表当前对象的引用。只能在类的实例方法或构造方法内使用，指向调用该方法的那个对象实例。
```this.name = name```，前面的```name```是类中```private String name```语句定义的私有变量。后面的是构造方法中的参数。
通过构造方法中```this.name = name```语句对私有变量```name```进行了赋值。

### 子类的构造方法
子类不能直接extends继承父类的构造方法，子类使用super语句来继承父类的构造方法。

#### 问答题考点：关键字super和this的区别
- 相同：
  - 指向对象实例​：都指向一个对象实例，​不能在 static 上下文（静态方法、静态块）中使用。
  - ​调用构造器​：都可用于构造方法中，调用其他构造器 (this(...) 调用本类，super(...) 调用父类)。

- 不同：
  - 指代对象: 当前类实例​ (自己)  V.S.  父类部分实例​ (父类)
  - ​存在前提: ​任何对象都存在  V.S.  必须存在继承关系
  - 主要用途：解决成员与局部变量同名冲突  V.S. 调用父类构造器

## <center>设计模式

### <center>设计模式的分类
1. 按照目的来分
    - 创建型模式（工厂方法，抽象工厂，单例）
    - 结构型模式
    - 行为型模式（模板方法，迭代器，观察者，策略）
2. 根据范围来分
    - 类（工厂方法，模板方法）
    - 对象（抽象工厂，单例，迭代器，观察者，策略）

### <center>单例模式
**保证一个类仅有一个实例，并提供一个访问它的全局访问点**

#### （1）饿汉式
```
public class Singleton{
    private static Singleton singleton01 = new Singleton(); // 天然线程安全

    private Singleton{}

    public static Singleton getInstance(){
        return singleton01;
    }
}
```
缺点：会造成内存浪费。
#### （2）懒汉式
```
public class Singleton{
    private static Singleton singleton02;

    private Singleton(){}

    public statc Singleton getInstance(){
        if (singleton02 == NULL){
            singleton02 = new Singleton();
        }
        return singleton02;
    }
}
```
缺点：可能会创建多个实例。
**解决方法一：加入同步锁**
```
public class Singleton{
    private static Singleton singleton02;

    private Singleton(){}

    public static synchronized Singleton getInstance(){ // 线程安全，但是效率低
        if (singleton02 == NULL){
            singleton02 = new Singleton();
        }
        return singleton02;
    }
}
```
**解决方法二：双重检验锁**
```
public class Singleton{
    private static Singleton singleton02;

    private Singleton(){}

    public static Singleton getInstance(){
        if (singleton02 == NULL){
            synchornized (Singleton.class){
                if (singleton02 == NULL){
                    singleton02 = new Singleton();
                }
            }
        }
        return sigleton02;
    }
}
```
#### 利用反射破坏单例
通过反射中的```setAccessible(true)```覆盖Java中的访问控制，进而调用私有的构造函数。

**抵御反射破坏**

```
public class Singleton{
    private static Singleton singleton = new Singleton();

    private Singleton{
        if (singleton != NULL){
            throw new RuntimeException("单例构造器禁止通过反射调用");
        }
    }
    public static Singleton getInstance(){
        ...
        return singleton;
    }
}
```
### <center>简单工厂模式

#### UML类图
![简单工厂](./figure/1.png)

#### 代码实现
```
public interface Car{
    void showTheBrand();
}
```
```
public class Audi implements Car{
    @override
    void showTheBrand(){
        system.out.println("Audi");
    }
} 
```
```
public class BMW implements Car{
    @override
    void showTheBrand(){
        system.out.println("BMW");
    }
} 
```
```
public class Benz implements Car{
    @override
    void showTheBrand(){
        system.out.println("Benz");
    }
} 
```
```
public class SimpleFactory{
    public static Car giveMeACar(String brandName){
        if ("BMW".equals(brandName)){
            return new BMW();
        }
        if ("Benz".equals(brandName)){
            return new Benz();
        }
        if ("Audi".equals(brandName)){
            return new Audi();
        }
        return null;
    }
}
```


### <center>工厂模式

#### UML类图
在简单工厂的基础上加上新的工厂：

![工厂](./figure/2.png)

#### 代码实现
```
public interface Car{
    void showTheBrand();
}
```
```
public class Audi implements Car{
    @override
    void showTheBrand(){
        system.out.println("Audi");
    }
} 
```
```
public class BMW implements Car{
    @override
    void showTheBrand(){
        system.out.println("BMW");
    }
} 
```
```
public class Benz implements Car{
    @override
    void showTheBrand(){
        system.out.println("Benz");
    }
} 
```
```
public interface CarFactory{
    Car buildACar();
}
```
```
public class BMWFactory implements CarFactory{
    @override
    Car buildACar(){
        return new BMW();
    }
}
```
```
public class BenzFactory implements CarFactory{
    @override
    Car buildACar(){
        return new Benz();
    }
}
```
```
public class AudiFactory implements CarFactory{
    @override
    Car buildACar(){
        return new Audi();
    }
}
```
```
public class FactoryTest{
    public static void main(String[] args){
        BMWFactory carfactory = new BMWFactory();
        Car mayCar = carFactory.buildACar();
        mayCar.showTheBrand();
    }
}
```
优点：
利于扩展和维护，比如新增加一种车，只需要对应创建具体产品类和负责生产新品种车的具体工厂即可。符合“开闭原则”，便于扩展。
缺点：
不支持等级。
### <center>抽象工厂模式
**主要用于解决“一类产品”的创建问题**，与工厂方法模式的区别：
1. 工厂方法模式只有一个抽象产品类，而抽象工厂模式有多个。
2. 工厂方法模式的具体工厂类只能创建一个具体产品类的实例，而抽象工厂模式可以创建多个。
#### UML类图
![抽象工厂](./figure/3.png)
#### 代码实现
```
public interface AbstractCarFactory{
    BClassCar build_B_ClassCar();
    CClassCar build_C_ClassCar();
}
```
```
public interface BClassCar{
    void showClassB();
}
```
```
public interface CClassCar{
    void showClassC();
}
```
具体实现省略
```
public class AbtractFactoryTest{
    public static void main(String[] args){
        BMWFactory bmwFactory = new BMWFactory();
        BenzFactory benzFactory = new benzFactory();

        bmwFactory.build_B_ClassCar().showClassB();
    }
}
```
优点：
1. 隔离了具体类的生成，将创建和使用解耦。
2. 添加新的产品族很方便，无需修改已有系统，符合“开闭原则”。
缺点：
1. 增加新的产品等级很麻烦，违背了“开闭原则”。

### <center>策略模式
**定义一系列的算法,把每一个算法封装起来, 并且使它们可相互替换，从而使得算法可独立于使用它的客户而变化。并将逻辑判断移到Client中去（即由客户端决定在什么情况下使用什么具体策略）。**

策略模式的三个基本角色：
1. 抽象策略角色：通常由一个接口或抽象类实现，此角色给出所有的具体策略类所需要的接口。
2. 具体策略角色：包装了相关算法或行为。
3. 环境角色：持有一个策略的引用。

#### UML类图
![策略模式](./figure/4.png)

#### 代码实现
例子：假设现在要设计一个卖书的电子商务网站，本网站可能对所有的高级会员提供每本20％的促销折扣；对中级会员提供每本10％的促销折扣；对初级会员没有折扣。根据描述，折扣是根据以下的几个算法中的一个进行的：
- 算法一：对初级会员没有折扣。
- 算法二：对中级会员提供10％的促销折扣。
- 算法三：对高级会员提供20％的促销折扣。
```
//抽象策略类
public interface MemberStrategy{
    public double calcPrice(double booksPrice);
}
```
```
//具体策略1
public class PrimaryMemberStrategy implements MemberStrategy{
    @override
    public double clacPrice(double booksPrice){
        return booksPrice;
    }
}
```
```
//具体策略2
public class IntermediateMemberStrategy implements MemberStrategy{
    @override
    public double clacPrice(double booksPrice){
        return 0.9 * booksPrice;
    }
}
```
```
//具体策略3
public class AdvancedMemberStrategy implements MemberStrategy{
    @override
    public double clacPrice(double booksPrice){
        return 0.8 * booksPrice;
    }
}
```
```
public class Network { //持有一个具体的策略对象 
    private MemberStrategy strategy; 
    public Network(MemberStrategy strategy){ 
        this.strategy = strategy; 
    } 

    public double quote(double booksPrice){   
        return this.strategy.calcPrice(booksPrice); 
    } 
} 
```
```
public class Client{
    public static void main(Srting[] args){
        MemberStrategy strategy = new AdvancedMemberStrategy();
        Network network = new Network(strategy);
        double quote = network.quote(300);
        System.out.println(quote);
    }
}
```
优点：
- 提供了一种替代继承的方法，而且既保持了继承的优点（代码重用）还比继承更灵活（算法独立，可以任意扩展）。
- 它把采取哪一种算法或采取哪一种行为的逻辑与算法本身分离，避免程序中使用多重条件转移语句，使系统更灵活，并易于扩展。
- 遵守大部分设计原则，高内聚、低偶合。
  
缺点：
- 客户端必须知道所有的策略类，并自行决定使用哪一个策略类。这就意味着客户端必须理解这些算法的区别，以便适时选择恰当的算法类。换言之，策略模式只适用于客户端知道算法或行为的情况。
- 由于策略模式把每个具体的策略实现都单独封装成为类，如果备选的策略很多的话，那么对象的数目就会很可观。

### <center>迭代器模式
**在客户访问类与聚合类之间插入一个迭代器，这分离了聚合对象与其遍历行为，对客户也隐藏了其内部细节，且满足“单一职责原则”和“开闭原则”。**
提供一种方法顺序访问一个聚合对象中各个元素, 而又无须暴露该对象的内部表示。
#### UML类图
![迭代器](./figure/5.png)

### <center>数据访问对象模式
数据访问对象模式的参与者：
- 数据访问对象接口：定义了在一个模型对象上要执行的标准操作。
- 数据访问对象实体类：实现接口，负责从数据源获取数据。
- 模型对象/数值对象：简单的普通对象，包含了get/set方法来存储通过使用DAO类检索到的数据。

优点：隔离数据层
缺点：代码量增加

#### UML类图
![DAO](./figure/6.png)

#### 代码实现
**Step 1:创建数值对象**
```
public class Student{
    private String name;
    private int rollNo;

    Student(String name, int rollNo){
        this.name = name;
        this.rollNo = rollNo;
    }
    public String getName(){
        return name;
    }
    public int getRollNo(){
        return rollNo;
    }
    public String setName(String name){
        this.name = name;
    }
    public int setRollNo(int rollNo){
        this.rollNo = rollNo;
    }
}
```
**Step 2:创建数据访问对象接口**
```
public interface StudentDao{
    List<Student> getAllStudents();
    Student getStudent(int rollNo);
    void updateStudent(Student student);
    void deleteStudent(Student student);
}
```
**Step 3:创建数据访问对象实体类**
略

### <center>MVC模式（模型视图控制器模式）
每个组件的三个特征：内容/外观/行为

### <center>模板方法模式
主要包含：
- AbstractClass抽象类：给出顶层逻辑的骨架。
- ConcreteClass具体类：实现父类定义的一个或多个抽象方法。

一个抽象类可以有任意多个具体子类，每一个抽象类都可以给出抽象方法的不同实现。

### <center>观察者模式
观察者模式(Observer Pattern)：定义对象间的一种一对多依赖关系，使得每当一个对象状态发生改变时，其相关依赖对象皆得到通知并被自动更新。观察者模式是一种对象行为型模式。
- 抽象目标：把所有对观察者对象的引用保存在一个集合中，每个抽象目标都可以有任意数量的观查者。
- 抽象观察者：为所有具体的观察者定义一个接口，在得到目标的通知时更新自己。
- 具体目标：在具体主题内部状态改变时，给所有登记过的观察者发出通知。具体主题角色通常用一个子类实现。
- 该角色实现抽象观察者角色所要求的更新接口，以便使本身的状态与主题的状态相协调。通常用一个子类实现。如果需要，具体观察者角色可以保存一个指向具体主题角色的引用。

#### UML类图
![DAO](./figure/7.png)

#### 代码实现
```
// 抽象目标
public abstract class MySubject{
    protected ArrayList observers = new ArrayList();
    public void attach(MyObserver observer){
        observers.add(observer);
    }
    public void detach(MyObserver observer){
        observers.remove(observer);
    }
    public abstract void cry();
}
```
```
public class Cat extends MySubject{
    public void cry(){
        System.out.println("mao jiao!");
        for (Object obs:observers){
            ((MyObservers)obs).response();
        }
    }
}
```
```
\\ 观察者接口
public interface MyObservers{
    void response();
}
```
```
public class Dog implements MyObserver{
   public void response(){
      System.out.println("狗跟着叫！");
   }  
}
```
```
public class Mouse implements MyObserver{
   public void response(){
      System.out.println("run！");
   }  
}
```
观察者模式优点：
- 可以实现表示层和数据逻辑层的分离
- 在观察目标和观察者之间建立一个抽象的耦合
- 支持广播通信，简化了一对多系统设计的难度
- 符合开闭原则，增加新的具体观察者无须修改原有系统代码，在具体观察者与观察目标之间不存在关联关系的情况下，增加新的观察目标也很方便。

观察者模式缺点：
- 将所有的观察者都通知到会花费很多时间
- 如果存在循环依赖时可能导致系统崩溃
- 没有相应的机制让观察者知道所观察的目标对象是怎么发生变化的，而只是知道观察目标发生了变化

