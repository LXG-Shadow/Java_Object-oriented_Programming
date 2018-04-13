<notice>教程读者请不要直接阅读本文件，因为诸多功能在此无法正常使用，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)学习完整教程。如果您喜欢我们的教程，请在右上角给我们一个“Star”，谢谢您的支持！</notice>

类进阶
======

你已经成功入门面向对象编程啦👍 那么让我们继续往下看看吧~

构造方法
-----
接下来介绍的是“构造方法”这一个概念。

每个类都有构造方法。如果没有专门为类定义构造方法，Java编译器将会为该类提供一个默认构造方法。在创建一个对象的时候，至少要调用一个构造方法。构造方法的名称必须与类同名，一个类可以有多个构造方法。

下面，让我们再来看一段Java代码，来看看在Java中，类、对象、方法三者的体现：
<lab lang="java" parameters="filename=Dog.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Dog {
  String name;
  String sex;
  int age;

  public void bark(){
    System.out.println("I'm barking!!!");
  }

  public void eat(){
    System.out.println("I'm eating!!!");
  }

  public void showInfo(){
    System.out.println("My name is " + name + ", and my sex is " + sex + ". I'm " + age + " years old.");
  }

  public static void main(String[] args) {
    Dog myPuppy = new Dog();
    myPuppy.name = "CoolmyPuppy";
    myPuppy.age = 2;
    myPuppy.sex = "male";

    myPuppy.bark();
    myPuppy.eat();
    myPuppy.showInfo();

  }
}
</lab>
让我们从上面这段Java代码中，分析其中类、对象，以及行为。

首先，我们新建了一个Dog类。这就好比自然界中，“狗”这个物种的统称。我们为这一个Dog类，赋予了name、sex、age，这三种属性。而这，就是Dog类中所有的对象（具体的狗）所共同具有的属性。我们还为这个类定义了四种行为：bark()、eat()，showInfo()，main()，前三种行为是这个类中，每一个具体的对象（具体的狗）所能够具有的行为。而main()行为则是Java程序执行的入口方法，也就是说，Java程序首先从main()方法开始执行。

在main()方法中，我们通过
```java
Dog myPuppy = new Dog();
```
语句新建了一个对象，名叫myPuppy。也就是说，在“狗”这个大类中，诞生了一只名为“myPuppy”的狗。 这只myPuppy，由于它是一条狗，它自然而然继承了其所在的“狗”这一物种，所具有的所有属性与行为。也就是说，myPuppy具有name、sex、age三种属性，myPuppy能够bark、eat、showInfo。我们随即通过
```Java
myPuppy.name = "CoolmyPuppy";
myPuppy.age = 2;
myPuppy.sex = "male";
```
三行语句来设置myPuppy的三个属性。并通过
```Java
myPuppy.bark();
myPuppy.eat();
myPuppy.showInfo();
```
三行语句来调用myPuppy的三种行为。

可这样写的话，每一次都需要定义myPuppy的行为。让我们来改写上面那段代码，看看“构造方法(constructor)”究竟是什么。
```Java
public class Dog {
    public Dog(String name, String sex, int age){
        System.out.println("My name is " + name + ", and my sex is " + sex + ". I'm " + age + " years old.");
    }

    public void bark() {
        System.out.println("I'm barking!");
    }

    public void eat() {
        System.out.println("I'm eating!");
    }

    public static void main(String[] args) {
        Dog myPuppy = new Dog("CoolmyPuppy","male", 2);
        myPuppy.bark();
        myPuppy.eat();
    }
}
```
对比上下两段代码，你发现了什么？  火眼金睛的你一定发现了：这里少掉了三行对`name`、`sex`和`age`的定义，转而新建了一个形如`public Dog(){}`的方法：
```java
public Dog(String name, String sex, int age){
    System.out.println("My name is " + name + ", and my sex is " + sex + ". I'm " + age + " years old.");
}
```
这个方法，就是一个构造方法。这里的“构造”是“方法”的定语。通过这个方法，我们定义了`Dog`这一个类所具有的三个属性：`name`、`sex`和`age`。这三个属性作为这个“构造方法” 的传入参数。在这个方法体中，我们使用`System.out.println()`方法，向屏幕输出一行信息。然后，在`main()`方法中，我们和前面一样，新建了一个`Dog`类的对象：`myPuppy`。区别之处在于，这一次，我们用于新建对象的语句
```Java
Dog myPuppy = new Dog("CoolmyPuppy","male", 2);
```
在括号中传入了三个参数，这三个参数就依次对应着构造方法中的三个传入参数。原先的showInfo()方法实现的功能，在这里也并入了构造方法中如下这一行语句。
```Java
System.out.println("My name is " + name + ", and my sex is " + sex + ". I'm " + age + " years old.");
```
在我们原先的程序中，我们没有显式地定义一个构造方法，但Java编译器实际上已经为我们定义了一个。

在我们刚才定义的这个构造方法中，我们写的是：
```Java
public Dog(String name, String sex, int age){
    System.out.println("My name is " + name + ", and my sex is " + sex + ". I'm " + age + " years old.");
}
```
这个方法中，并没有返回值类型、返回值。也就是说，构造方法是没有返回值的，并且构造方法的名称必须与类名相同。

那这个构造器到底有什么用呢？请看下面这段代码：
<lab lang="java" parameters="filename=Dog.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Dog {
    public Dog(String name, String sex, int age){
        System.out.println("My name is " + name + ", and my sex is " + sex + ". I'm " + age + " years old.");
    }
    public static void main(String[] args){
        Dog myDog1 = new Dog("Tom", "Male", 2);
        Dog myDog2 = new Dog("Sam", "Male",3);
        Dog myDog3 = new Dog("Lily","Female",4);
        Dog myDog4 = new Dog("Sally","Female",5)
    }
}
</lab>
在这个例子中，我们需要一次性new出许许多多个属于`Dog`这个类的对象（具体的一条条狗）。所有的狗都具有名称、性别、年龄这三个属性。因此，我们在`public Dog()`这个构造方法中，提前定义了这三个属性，这三个属性，就作为整个类所有的是对象都共有的属性。这样一来，我们在`main`方法中`new`对象时，就无需在一个一个地定义这三个属性了。这为我们提高了非常多的效率。因此，“构造方法”就相当于，提前“构造”出了一个框架，这个框架每个对象都可以用，只需要在这个框架上赋予不同的内容即可。

访问器和更改器
-----
接下来，我们看看如何更加方便地读取和设置Java属性值。习惯上，我们使用getter与setter方法来存取Java属性值。这两种方法分别叫“访问器（Accessor）”与“更改器(Mutator)”——（人们总喜欢给简单的事物赋予复杂高级的名称）。使用这两种方法，能够为我们提供一个访问、修改、读取属性值的中间层，可以提高程序的安全性，避免数据被恶意篡改，也是面向对象编程的核心思想之一。习惯上，getter方法与setter方法的命名为：getXXX,setXXX.

在下面这段代码中，setName()就是更改器(Mutator)，而getName()就是访问器(Accessor)。
```java
public class Dog{
    String name;
    public void setName(String inName){
        name = inName;
    }
    public String getName( ){
        System.out.println("Dog name is: " + name );
        return name;
    }
    public static void main(String []args){
        /* 创建对象 */
        Dog myDog = new Dog();
        /* 通过方法来设定name */
        myDog.setName("myPuppy");
        /* 调用另一个方法获取name */
        myDog.getName( );
        /*你也可以像下面这样访问成员变量 */
        System.out.println("name值 : " + myDog.getName() );
    }
}
```
来试试看编译运行结果吧！
<lab lang="java" parameters="filename=car.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Dog{
    String name;
    public void setName(String inName){
        name = inName;
    }
    public String getName( ){
        System.out.println("Dog name is: " + name );
        return name;
    }
    public static void main(String []args){
        /* 创建对象 */
        Dog myDog = new Dog();
        /* 通过方法来设定name */
        myDog.setName("myPuppy");
        /* 调用另一个方法获取name */
        myDog.getName( );
        /*你也可以像下面这样访问成员变量 */
        System.out.println("name值 : " + myDog.getName() );
    }
}
</lab>

方法重载
-----
方法重载指的是，多个方法有同样的名字，却有不同的传入参数列表。看下面这段代码：
```java
public class cat {
    String name;
    String type;
    double weight;
    int age;
    public cat(){
        name = " ";
        weight = 0;
        type = " ";
        System.out.println("I am an undefined cat.");
    }
    public cat(String name, double weight, String type){
        this.name = name;
        this.weight = weight;
        this.type = type;
        System.out.println("My name is " + name + " and my weight is " + weight + " and I am a " + type + " cat.");
    }
    public cat(String name, double weight, String type, int age){
        this.name = name;
        this.weight = weight;
        this.type = type;
        this.age = age;
        System.out.println("My name is " + name + " and my weight is " + weight + " and I am a " + type + " cat who is " + age + " years old.");
    }
    public static void main(String[] args){
        cat cat1 = new cat();
        cat cat2 = new cat("Kitty", 2, "Garfield");
        cat cat3 = new cat("Mew", 3, "Garfield", 3);
    }
}
```
其中，我们有三个同名的`cat`方法。 它们的区别在于，前者的传入参数列表为空，后者则定义了三个传入参数，再后者则定义了四个。程序在执行的时候，会根据用户给其的传入参数不同，自动给出它所要调用的方法。对象`cat1`的传入参数列表为空，故`cat1`自动对应的是第一个`cat()`方法；对象`cat2`有三个传入参数，故`cat2`自动对应的是第二个`cat`方法；对象`cat3`有四个传入参数，故`cat3`自动对应的是第三个`cat`方法。

来试试看编译运行结果吧！
<lab lang="java" parameters="filename=car.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class cat {
    String name;
    String type;
    double weight;
    int age;
    public cat(){
        name = " ";
        weight = 0;
        type = " ";
        System.out.println("I am an undefined cat.");
    }
    public cat(String name, double weight, String type){
        this.name = name;
        this.weight = weight;
        this.type = type;
        System.out.println("My name is " + name + " and my weight is " + weight + " and I am a " + type + " cat.");
    }
    public cat(String name, double weight, String type, int age){
        this.name = name;
        this.weight = weight;
        this.type = type;
        this.age = age;
        System.out.println("My name is " + name + " and my weight is " + weight + " and I am a " + type + " cat who is " + age + " years old.");
    }
    public static void main(String[] args){
        cat cat1 = new cat();
        cat cat2 = new cat("Kitty", 2, "Garfield");
        cat cat3 = new cat("Mew", 3, "Garfield", 3);
    }
}
</lab>

小练习
-----

在这里练习吧：
<lab lang="java" parameters="filename=Hello.java">
<notice>练习环境在此无法显示，请移步至[程谱 coderecipe.cn](https://coderecipe.cn/learn/1)查看。</notice>
public class Hello {
   public static void main(String[] args) {
     // 在这里添加你的代码
   }
}
</lab>