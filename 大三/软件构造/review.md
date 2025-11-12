# 软件构造复习

## 设计模式

### 设计模式的分类
1. 按照目的来分
    - 创建型模式（工厂方法，抽象工厂，单例）
    - 结构型模式
    - 行为型模式（模板方法，迭代器，观察者，策略）
2. 根据范围来分
    - 类（工厂方法，模板方法）
    - 对象（抽象工厂，单例，迭代器，观察者，策略）

### 单例模式
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
### 简单工厂模式

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
### 工厂模式

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