---
title: Java 学习笔记
date: 2017-06-23 11:29:39
tags:  ['java']
---

``` bach
"hexo-generator-json-content": "^3.0.1",  //今天报错待解决
```

####  Mac配置java环境

- 第一步： vi .zshrc
- 第二步： 将这段文字输入 export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_121.jdk/Contents/Home
  export PATH=$JAVA_HOME/bin:$PATH  
- 第三步： 输入source .zshrc 这样就可以使得环境变量起作用了
- 第四步： echo $JAVA_HOME看看有没有输出刚才配置的路径


##### Class JavaLaunchHelper is implemented in both...  报错处理
``` java 
//  Go to ➤ (Help | Edit Custom Properties...) 
idea_rt
idea.no.launcher=true
```

#### 创建一个简单的demo

一. 打开textEdit软件 设置:preferences > Format > Plain text 创建hello.java文件

    ``` java
    public class hello{
        public static void main(String[] args){
            System.out.println("hello world");
        }
    }
    ```
    
二. 找到当前文件目录 注意文件夹名字和类名一致(源程序)

``` bash
javac hello.java
```

三. 生成一个hello.class的文件,然后执行（字节码程序）

``` bash
java hello
```

##### 乘法口诀

``` java
// i 代表行数
for(int i=1;i<=9;i++){
     for(int j=1;j<=i;j++){
         System.out.print(j + " * " + i + " = " + (i*j) + "\t");
     }
     System.out.println()
}
            


```

###### Java数组的可变参数
``` java
public class app {
    public static void main(String[] args) {
//        第一种传递数组
        double[] arr1 = {10.0, 23.0, 12.0, 13};
        double sum = getSum(arr1);
//        第二种传递方式(可变参数)
        double sum = getSum(0.8, 123.0, 2341, 3, 3.0);  //单个放在前面，避免歧义
        System.out.println(sum);
    }
    static double getSum(double cutoff, double... arr) {
        double sum = 0;
        for (double price : arr) {
            sum += price * cutoff;
        }
        return sum;
    }
}
```

##### java.util.Arrays 工具
```
public class array {
    public static void main(String[] args) {
        int[] arr = {1, 34, 5, 5, 65, 7, 76, 33};
        // 打印
        String arrString = java.util.Arrays.toString(arr);
        System.out.println(arrString);
        // 排序
        java.util.Arrays.sort(arr, 2, 6);
        System.out.println(java.util.Arrays.toString(arr));
        // 二分法
        int index = java.util.Arrays.binarySearch(arr,5);
        System.out.println(index);
    }
}
```

######  java中的变量(成员变量和局部变量)：
|  |存在位置|生命周期开始  |生命周期结束|在内存中的位置|
|:---:|:---:|:---:|:---:|:---:|
|类变量|字段，使用static修饰|当所在字节码被加载进JVM|当JVM停止|方法区|
|实例变量|字段，没有使用static修饰|当创建类的对象的时候|当该对象被GC回收|堆|
|局部变量|方法形参，代码块中，方法内|当代码执行到初始化变量的时候|所在的方法／代码块结束|当前方法的栈帧中|

##### this存在与两个位置。
      -构造器中：表示当前创建的对象
      -方法中：那个调用this调用的方法，this表示那一个对象
``` java
class User {
    private String name;     // 私有变量默认是null
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;    // this的使用
    }
    public void showThis (){
        System.out.println(this.name);
    }
}

public class thisDemo {
    public static void main(String[] args) {
//        创建user1对象
        User user1 = new User();
        user1.setName("lily");
        String name = user1.getName();
        System.out.println(name);
//        创建user2对象
        User user2 = new User();
        user2.setName("lucy");
        // this的调用
        user1.showThis();
        user2.showThis();
    }
}
```

#####  面向对象-子类初始化过程

``` java
class Animal {
    private String name;
    private int age;

    public void Fly() {
        System.out.println("会飞翔");
    }

    Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

}
// 继承Animal这个类
class Fish extends Animal {
    private String color;

    Fish(String name, int age, String color) {
        super(name, age);   // 父类私有变量赋值
        this.color = color;
    }

    // override 覆盖父类的方法
    public void Fly() {
        System.out.println("我会游泳");
        System.out.println(color + ", " + getName() + super.getAge());
    }
}


public class Superdemo {
    public static void main(String[] args) {
        Fish fish = new Fish("金枪鱼", 5, "yello");
        fish.Fly();
        String name = fish.getName();
        System.out.println(name);
        
        Object obj = "ABC";
    //  instanceof 判断对象是否是某一个类的实例
        System.out.println(obj instanceof Object);  //true
        System.out.println(obj instanceof String);  //true
    //  getClass()获取对象的实例类型
        System.out.println(obj.getClass() == String.class);  //true
    }
}
```
