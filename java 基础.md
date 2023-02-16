# *java 基础*
参考：
1. [](https://)https://www.bilibili.com/video/BV1Rx411876f?p=191&vd_source=9e3463963a6ca5cfc43abb7cfd8527dd
2. [](https://)http://www.voidme.com/java


## <font class="text-color-13" color="#ffeb3b">IDEA快捷键</font>
* alt + enter : 纠错
* ctrl + p：查看参数列表
* alt+鼠标拖动：多行编辑
[](https://)https://blog.csdn.net/weixin_45395059/article/details/125591122
[](https://)https://blog.csdn.net/he_xin2009/article/details/124289128
## <font class="text-color-13" color="#ffeb3b">变量</font>
* <font class="text-color-11" color="#8bc34a">实例变量</font>：在堆中
* <font class="text-color-11" color="#8bc34a">静态变量</font>：在方法区中
* <font class="text-color-11" color="#8bc34a">局部变量</font>：在栈中
* 一行可以声明多个变量，但不能同时赋值
``` java
int a,b,c; // 同时声明三个变量
    a = 100;
    b = 200;
    c = 300;
```
* 声明其它进制整型。
``` java
        int a = 100; // 十进制
        int b = 010; // 八进制
        int c = 0b10; // 二进制
        int d = 0x10; // 十六进制
```
* 小容量可以自动转换成大容量，这种操作称为：<font class="text-color-12" color="#cddc39">自动类型转换</font>。
* 声明long类型变量，(不加L就是向下转型：错误)
```java
    long e = 2147483648L;
```
* 大容量转换成小容量，要想编译通过，必须加强制类型转换符，进行<font class="text-color-12" color="#cddc39">强制类型转换</font>（可能损失精度）。
```java
        long x = 100L;
        int y = (int)x;

        byte b = (byte)300 // 丢失精度
```
* 当整数型字面量没有超出 byte/short/char 类型范围，那么这个整数型字面量可以直接赋值给变量。
* 多种数据类型做混合运算，最终结果是“最大容量”对应的类型。
* 小数默认为double类型，声明float须转换。
```java
        double a = 3.14;
        float b = 3.14f;
        float c = (float)3.14;
```

## <font class="text-color-13" color="#ffeb3b">运算符</font>
* <font class="text-color-15" color="#ff9800">三目运算符</font>：布尔表达式 ? 表达式1 : 表达式2
* 当 + 两边任意一边是字符串，则进行字符串拼接。

## <font class="text-color-13" color="#ffeb3b">接收键盘输入</font>
```java
// 创建一个键盘扫描器对象
        Scanner scanner = new Scanner(System.in);

        int a = scanner.nextInt(); // 接收一个int类型的数据
        String s = scanner.next(); // 接收一个字符串
        String l = scanner.nextLine();  // 接收一行输入
```

## <font class="text-color-13" color="#ffeb3b">控制语句</font>
* switch语句（支持int和string类型的值，使用 == 比较），不使用break会出现case穿透现象。
```java
         int x = 2;

        switch (x){
            case 1:
                System.out.println("case 1");
                break;
            case 2:
                System.out.println("case 2");
                break;
            case 3:
                System.out.println("case 3");
                break;
            default:
                System.out.println("default");
```
* do while语句
```java
        int i = 1;
        do{
            System.out.println(i++);
        }while (i <= 10);
```
* break可以终止最近的for循环
* break使用标识符可以终止指定的for循环
```java
        a:for (int i = 1; i <= 10; i++) {
            b:for (int j = 0; j <= 10; j++) {
                System.out.println("j = " + j);
                if(j == 5){
                    break a; // 终止最外层循环
                }
            }
            System.out.println("i = " + i);
        }
```
* continue语句： 终止当前“本次”循环，直接进入下一次循环继续执行

## <font class="text-color-13" color="#ffeb3b">类</font>
* 一个java文件中可以有多个class。
* public 的类可以没有，如果有的话，public修饰的类必须和源文件名保持一致。
* 构造方法：创建对象，并且同时给对象的属性赋值。（实例变量没有手动赋值的时候，系统会赋默认值）
### <font class="text-color-15" color="#ff9800">静态代码块</font>
* 类加载时执行，只执行一次，并且在main方法执行之前执行。（类加载时机）
```java
   static{
        System.out.println("类加载");
    }
```
### <font class="text-color-15" color="#ff9800">实例代码块</font>
* 只要构造方法执行，必然在构造方法执行之前，自动执行“实例语句块”中的代码。（对象构建时机）
```java
{
    System.out.println("构造方法执行");
}
```
### <font class="text-color-15" color="#ff9800">finalize()</font> 
* JVM垃圾回收器负责调用这个方法，finalize只需要重写。当一个java对象即将被垃圾回收器回收的时候，垃圾回收器负责调用finalize()方法。（System.gc()可以建议垃圾回收器启动）
### <font class="text-color-15" color="#ff9800">this</font> 
* this 是一个变量，一个引用，保存当前对象的内存地址，指向自身。
* this 存储在堆中，对象的内部。
* this 只能使用在实例方法中。谁调用这个实例方法，this就是谁。所以this代表当前对象。
* this. 可以省略，但在实例方法或构造方法中，为了区分实例与局部变量，不能省略。
* this(实际参数列表)：可以通过当前构造方法调用另一个本类的构造方法。（this( )只能出现在构造方法第一行）
```java
    public Computer() {
        this(23,"turing",false);
    }

    public Computer(int ID, String name, boolean laptop) {
        this.ID = ID;
        this.name = name;
        this.laptop = laptop;
    }
```
### <font class="text-color-15" color="#ff9800">类加载器</font> 
* 专门负责加载类的命令/工具
* JDK 自带 3个类加载器
    1. 启动类加载器
    2. 扩展类加载器
    3. 应用类加载器
* 代码开始执行之前，会将所有类加载到JVM中。
    首先会通过“启动类加载器”加载核心类库，如果加载不到则通过“扩展类加载器”加载扩展库。“应用类加载器”负责加载 classpath 中的类。
* [](https://)https://blog.csdn.net/xyy1028/article/details/122575090
* java 为了保证类加载的安全，使用了<font class="text-color-15" color="#ff9800">双亲委派机制</font>，优先从“启动类加载器”加载（父），再从“扩展类加载器”加载（母），最后才会考虑从“应用类加载器”中加载，直到加载到为止。


## <font class="text-color-13" color="#ffeb3b">内部类</font>
* [](https://)http://www.voidme.com/java-object-oriented/java-inner-classes
### <font class="text-color-15" color="#ff9800">实例内部类</font>
```java
        Outer out = new Outer();
        Outer.Inner in = out.new Inner();

        in.display();

class Outer{
    private int num = 100;

    class Inner{   // 实例内部类
        public Inner() {
        }

        public void display(){
            System.out.println(num);
        }
    }

}
```
### <font class="text-color-15" color="#ff9800">静态内部类</font>
```java
        Outer.Inner.doSome();

        // 创建静态内部类对象
        Outer.Inner in = new Outer.Inner();
        in.doOther();

class Outer{

    public static class Inner{   // 静态内部类

        public static void doSome(){
            System.out.println("静态内部类的静态方法执行");
        }

        public void doOther(){
            System.out.println("静态内部类的实例方法执行");
        }

    }

}
```
### <font class="text-color-15" color="#ff9800">局部内部类</font>
```java
        Outer out = new Outer();
        out.display();

class Outer{
    private int num = 100;

    public void display(){
        class Inner{      // 局部内部类
            public void print(){
                System.out.println(num);
            }
        }
        Inner in = new Inner();
        in.print();
    }

}
```

### <font class="text-color-15" color="#ff9800">匿名内部类</font>
* 匿名内部类属于局部内部类，可以在参数列表中对接口进行实现。无法复用。
```java
        myMath mm = new myMath();

        mm.mySum(new compute() {  // 匿名内部类
            @Override
            public int sum(int a, int b) {
                return a + b;
            }
        }, 200, 600);

interface compute{
    int sum(int a, int b);
}

class myMath{
    public int mySum(compute compute,int a, int b){
        return compute.sum(a,b);
    }
}
```




## <font class="text-color-13" color="#ffeb3b">方法</font>
* <font class="text-color-15" color="#ff9800">静态方法</font>：带 static 的方法，在当前类调用可省略 class. ，跨类调用不可以省略。
* <font class="text-color-15" color="#ff9800">实例方法</font>：不带 static 的方法，调用必须先new对象。
* 工具类的方法一般为静态方法。
* <font class="text-color-15" color="#ff9800">方法重载</font> (overload)：
    1.同一个类中
    2.方法名相同
    3.参数列表不同
```java
    public static int sum(int x, int y) {
        return x + y;
    }
    
    public static long sum(long x, long y) {
        return x + y;
    }
```
* 参数传递的时候，不管是基本数据类型还是引用数据类型，统一都是将盒子中盒子中保存的那个“值”复制一份传递下去。（值可能是数字也可能是地址）
* 变量分为基本数据类型和引用数据类型。
* <font class="text-color-15" color="#ff9800">局部变量</font>：方法体中声明的变量。
* <font class="text-color-15" color="#ff9800">成员变量</font>：方法外，类体内声明的变量。
    成员变量又分为：<font class="text-color-12" color="#cddc39">实例变量</font>，<font class="text-color-12" color="#cddc39">静态变量</font>。
    - 静态变量在类加载时初始化，不需要new对象，静态变量的空间就开辟出来了。
    - static 静态变量储存在方法区。
```java
class test{
    int a; // 成员变量中的实例变量
    static int b; // 成员变量中的静态变量
    
    public static void m1(){  // 静态方法
        int c; // 局部变量
    } 
    
    public void m2(){} // 实例方法
}
```
## <font class="text-color-13" color="#ffeb3b">JVM</font>
* <font class="text-color-15" color="#ff9800">栈</font>：方法执行，会压栈。（局部变量）
* <font class="text-color-15" color="#ff9800">堆</font>：new出来的队形在堆中。垃圾回收器主要针对。（实例变量）
* <font class="text-color-15" color="#ff9800">方法区</font>：类的信息，字节码信息，代码片段。（静态变量）


## <font class="text-color-13" color="#ffeb3b">继承</font>
* 所有类默认继承 Object 类。
* 子类继承父类，除构造方法外，剩下的都可以继承。但是私有的属性 (private) 无法在子类中直接访问，可以通过继承的方法间接访问。
* 本质上，子类继承父类之后，是将父类继承过来的方法归为自己所有。所以实际上调用的不是父类的方法，而是子类自己的方法。（因为已经继承过来了就属于自己的）
* <font class="text-color-15" color="#ff9800">方法重写</font> (overwrite)：子类将继承过来的方法给覆盖掉了。
    1. 两个类必须要有继承关系。
    2. 重写之后的方法和之前的方法具有相同的返回值类型，方法名，形参列表。
    注：子类重写方法返回值类型允许更小，不能更大
    4. 访问权限不能更低，可以更高。
    5. 重写之后的方法不能比之前的方法抛出更多的异常，可以更少。
    6. 方法覆盖只针对于方法，和属性无关。
    7. 私有方法无法覆盖。
    8. 构造方法不能被继承，所以构造方法也不能被覆盖。
    9. 方法覆盖只针对于实例方法，静态方法覆盖没有意义。因为静态方法和对象无关，虽然可以使用引用.调用，但实际运行时还是class.调用。（无法运用多态机制）
* <font class="text-color-15" color="#ff9800">super</font>：
    1. super能出现在实例方法和构造方法中。不能使用在静态方法中。
    2. super 是 this 指向的那个对象中的一块空间，表示当前对象的父类型特征。
    3. super. 大部分情况下可以省略。当父类与子类有同名属性或方法，想在子类中访问父类属性或方法时，不能省略 super. 。
    4. super( ) 只能出现在构造方法第一行，通过当前构造方法调用“父类”中的构造方法。目的是：创建子类对象的时候先初始化父类型特征。
    5. 当一个构造方法第一行，既没有this( )，有没有super( )，默认会有一个super( )，表示通过当前子类的构造方法调用父类的无参数构造方法。所以必须保证父类的无参数构造方法是存在的。（this()和super()不能共存）
* <font class="text-color-15" color="#ff9800">final</font>：
    final 可以修饰变量，方法，和类。
    1. final 修饰的类无法被继承。
    2. final 修饰的方法无法被重写。
    3. final 修饰的变量（基本和引用类型），只能赋一次值。
        final 修饰的引用只能指向一个对象，并且只能永远指向该对象。（对象里面数据可以修改）
    4. final 修饰的实例变量，系统不管赋默认值，要求必须手动赋值。
    5. final 修饰的实例变量一般和static联合使用，称为常量。
    

## <font class="text-color-13" color="#ffeb3b">多态</font>
* 父类型的引用指向子类型的对象。
    ### <font class="text-color-11" color="#8bc34a">转型</font>
    * 向上转型：子 ---> 父（自动类型转换）
```java
        Animal a = new Cat();
        a.move();
```
```
    > cat move!
```
* 向下转型：父 ---> 子（强制类型转换，需要加强制类型转换符）
```java
class Animal {
  public void makeSound() {
    System.out.println("Animal makes a sound");
  }
}

class Dog extends Animal {
  @Override
  public void makeSound() {
    System.out.println("Dog barks");
  }
}

Animal animal = new Dog();
Dog dog = (Dog) animal;
dog.makeSound();
```

* 无论向上还是向下转型，两种类型之间必须有继承关系。（不适用接口）

* 多态表示编译的时候一种形态，运行的时候另一种形态。
* <font class="text-color-15" color="#ff9800">编译阶段</font>：编译器只知道a的类型是Animal，所以编译器在检查语法的时候，会去Animal.class字节码文件中找move()方法，找到后，绑定上move()方法，编译通过，静态绑定成功。（编译阶段属于静态绑定）
* <font class="text-color-15" color="#ff9800">运行阶段</font>：运行阶段的时候，实际在堆内存中创建的对象是Cat对象，所以move的时候，真正参与move的对象是一只猫，所以运行阶段会动态执行Cat对象的move()方法。这个过程属于运行阶段绑定。（运行阶段属于动态绑定）
* 当需要访问的是“子类”对象中特有的方法。此时必须进行向下转型。
```java
Cat c = (Cat)a;
c.catchMouse();
```
```
> cat catch mouse!
```
* 强制类型转换有风险，可能出现ClassCastException（类型转换异常），如何避免？
    <font class="text-color-15" color="#ff9800">instanceof</font> 运算符：可以在运行阶段动态判断引用指向的对象的类型。
    （语法：引用 instanceof 类型）
```java
if(a instanceof Cat){
    Cat c = (Cat)a;
    c.catchMouse
}
```
* instanceof 判断后如果为真，可直接创建一个强转后的对象。
```java
    public static void doSome(Object o){
        if(o instanceof Student student){
            System.out.println(student.getName());
        }
    }
```

* instanceof 和 getclass() 区别：
    1. getClass：返回的运行时类型，因此它不考虑继承，仅判断引用指向的具体类型。
    2. instanceof：比较的是继承关系或者实现关系类的类型,子类对象或者实现类对象放在前面。
* 开发中的作用：OCP（对扩展开放，对修改关闭）
    编译的时候，编译器发现p是Pet类，会去Pet类中找eat()方法，结果找到了，编译通过。
    运行的时候，底层实际的对象是什么，就自动调用到该实际对象的eat()方法上。
    这就是多态的使用。
```java
public void feed(Pet p){
    p.eat();
}
```

## <font class="text-color-13" color="#ffeb3b">抽象类</font>
* 类和类之间具有共同特征，将这些共同特征提取出来，形成的就是抽象类。类到对象是实例化，对象到类是抽象。
```java
abstract class C{
    // 类体
}
```
* 抽象类无法创建对象。抽象类有构造方法，这个构造方法是供子类使用的。
* 抽象方法：没有实现的方法，没有方法体的方法。
```java
    public abstract void dosome();
```
* 抽象类中不一定有抽象方法，但抽象方法必须出现在抽象类中。抽象类中也可以有非抽象方法。
* 一个非抽象类继承抽象类，必须将抽象类中的抽象方法重写。（对抽象的实现）


## <font class="text-color-13" color="#ffeb3b">接口</font>
* 接口是特殊的抽象类。（完全抽象）
```java
interface inter{
    // 常量
    // 抽象方法
}
```
* 接口包含两部分：1. 常量    2. 抽象方法 （没有构造器）
* 常量的 public static final 可以省略。 
* 接口中都是抽象方法，所以接口中方法不能有方法体。public abstract 可以省略。
* 接口中所有元素都是 public修饰的。
* 类和接口之间叫做实现：implements。
* 当一个非抽象类实现接口，必须将抽象类中所有方法实现（重写）。
* 接口和接口支持多继承，类和接口支持多实现。
* 接口和接口之间进行强制类型转换的时候，没有继承关系，也可以强转。
    注：运行时可能出现 ClassCastExeption，需加 instanceof进行判断。
```java
        M m = new L();

        m.m1();
        // m.m2();  错误：找不到符号m2 

        if(m instanceof K){
            K k = (K)m;
            k.m2();
        }

        if(m instanceof L){
            L l = (L)m;
            l.m2();
        }

interface M{
    void m1();
}

interface K{
    void m2();
}

class L implements M, K{
    public void m1() {
        System.out.println("m1执行");
    }

    public void m2() {
        System.out.println("m2执行");
    }
}
```
* extends 和 implements 可以同时出现
```java
class cat extends Animal implements flyable{
    
}
```

## <font class="text-color-13" color="#ffeb3b">Lamda表达式</font>
* [](https://)https://blog.csdn.net/qq_45263520/article/details/123772771
* 函数式接口：一个接口中，要求实现类必须实现的抽象方法，有且只有一个。
```java
        Math myMath = (x,y) -> x + y;

        System.out.println(myMath.sum(2, 3));

@FunctionalInterface
interface Math {
    int sum(int a, int b);
}
```
* 静态方法引用
```java
        Math myMath = Calulation::diff;

        System.out.println(myMath.diff(10, 55));

class Calulation{

    public static int diff(int a, int b){
        return a >= b ? a - b : b - a;
    }

}

@FunctionalInterface
interface Math {
    int diff(int a, int b);
}
```
* 实例方法引用
```java
        Math myMath = new Calulation()::diff;

        System.out.println(myMath.diff(10, 55));

class Calulation{

    public int diff(int a, int b){
        return a >= b ? a - b : b - a;
    }

}

@FunctionalInterface
interface Math {
    int diff(int a, int b);
}
```



## <font class="text-color-13" color="#ffeb3b">包</font>
* package 是一个关键字，后面加包的名字。package 语句只允许出现在java源代码的第一行。
* import（导包）：什么时候使用？
    A 类中使用 B 类
    1. A 和 B 类在同一个包下，不需要使用 import
    2. A 和 B 类不在同一个包下，需要使用 import
* import 语句只能出现在 package 语句之下，class 声明语句之上。
* java.lang.* 这个包下的类不需要使用 import 导入。


## <font class="text-color-13" color="#ffeb3b">访问控制权限</font>
1. private 只能在本类中访问。
2. public 在任何位置都可以访问。
3. “默认” 只能在本类，以及同包下访问。
4. protected 只能在本类、同包、以及子类中访问。


| 访问控制修饰符                                               | 本类 | 同包 | 子类 | 任意位置 |
| ------------------------------------------------------------ | ---- | ---- | ---- | -------- |
| <font class="text-color-15" color="#ff9800">public</font>    | yes  | yes  | yes  | yes      |
| <font class="text-color-15" color="#ff9800">protected</font> | yes  | yes  | yes  | no       |
| <font class="text-color-15" color="#ff9800">默认</font>      | yes  | yes  | no   | no       |
| <font class="text-color-15" color="#ff9800">private</font>   | yes  | no   | no   | no       |


## <font class="text-color-13" color="#ffeb3b">数组相关方法</font>
* 数组拷贝：System.arraycopy(源数组, 起始位置, 目标数组, 目标起始位置, 拷贝长度)
* Arrays 工具类
    1. Arrays.sort(源数组) : 对数组排序。
    2. Arrays.binarySearch(源数组, 查找的元素)：二分查找已经排序的数组，返回下标。（如果重复则返回其中一个的下标）

## <font class="text-color-13" color="#ffeb3b">String</font>
* 双引号括起来的字符串是不可变的，直接存储在方法区的“字符串常量池”中。
* 常用方法：
    1. charAt(下标)：返回字符串指定下标的字符。
    2. compareTo(字符串)：字典顺序比较两个字符串。（0：前后一致；大于0：前大后小；小于0：前小后大）
    3. contains(字符串)：判断前面的字符串中是否包含指定子字符串。
    4. endsWith(字符串)：判断前面的字符串是否以指定字符串结尾。
    5. startsWith(字符串)：判断前面的字符串是否以指定字符串开始。
    6. equals(字符串)：比较两字符串是否一样。返回布尔值。
    7. equalsIgnoreCase(字符串)：比较两字符串是否一样，忽略大小写。
    8. getBytes()：将字符串转换成字节数组，ASCII码。（Byte[]）
    9. indexOf(字符串)：判断指定子字符串在当前字符串中第一次出现的索引。
    10. isEmpty()：判断字符串是否为空字符串。
    11. lastIndexOf：判断指定子字符串在当前字符串中最后一次了出现的索引。
    12. split(REGEX)：按照指定正则表达式字符串分割，返回 String[]。
    13. length()：返回字符串的长度。
    14. matches()：告知字符串是否匹配给定的正则表达式字符串。
    15. replace(需替换的字符串, 字符串)：替换子字符串。
    16. substring(开始下标, 结束下标)：截取字符串，左闭右开。（可以没有结束下标）
    17. toCharArray()：将字符串转换成 char[]。
    18. toLowerCase() / toUpperCase()：字符串转换成小写/大写。
    19. trim()：去除字符串的前后空白。
    20. valueOf()：静态方法，将“非字符串”转换成字符串。（对象调用toString()）
### <font class="text-color-15" color="#ff9800">StringBuffer：</font>
* StringBuffer 底层是一个 byte 数组，初始化容量是16，尽可能给定一个大一些的初始化容量。
* 使用 append() 方法拼接字符串，追加时，若底层数组满了，则会自动扩容。
* 有 synchronized 修饰，在多线程环境下运行是安全的。
```java
        StringBuffer stringBuffer = new StringBuffer();
        stringBuffer.append("a");
        stringBuffer.append(true);
        stringBuffer.append(123);

        System.out.println(stringBuffer);    // atrue123
```
### <font class="text-color-15" color="#ff9800">StringBuilder</font> 
* 功能相同，没有 synchronized 修饰，在多线程环境下运行是不安全的。
* 常用方法
    StringBuilder append(String str)：向当前 StringBuilder 对象追加字符串。
    StringBuilder insert(int offset, String str)：向当前 StringBuilder 对象的指定位置插入字符串。
    StringBuilder delete(int start, int end)：从当前 StringBuilder 对象的指定位置开始，删除给定长度的字符。
    StringBuilder reverse()：将当前 StringBuilder 对象的内容翻转。
    int length()：返回当前 StringBuilder 对象的字符数。
    void setLength(int newLength)：设置当前 StringBuilder 对象的字符数。
    char charAt(int index)：返回当前 StringBuilder 对象中指定位置的字符。
    StringBuilder replace(int start, int end, String str)：将当前 StringBuilder 对象从指定位置开始到结束位置替换为指定字符串。
    StringBuilder substring(int start)：返回从指定位置开始到当前 StringBuilder 对象末尾的字符串。
    StringBuilder substring(int start, int end)：返回从指定位置开始到结束位置的字符串。
    String toString()：返回当前 StringBuilder 对象的字符串表示。
## <font class="text-color-13" color="#ffeb3b">包装类</font>
* java 中为8种基本数据类型对应准备了8种包装类型。8种包装类属于引用数据类型。

| 基本数据类型 | 包装类型 |
| -------- | -------- |
| byte     | Byte     |
| short     | Short    |
| int     | Integer    |
| long     | Long     |
| float     | Float     |
| double     | Double     |
| boolean     | Boolean   |
| char  | Character     |

```java
       Integer i = new Integer(100);  // 装箱
       Integer m = 100;  // 自动装箱 

        int a = i.intValue();   // 拆箱
        int b = i;     // 自动拆箱
```
* == 不会触发自动拆箱，比较内存地址。
* java 为了提高程序的执行效率，将 -128 ~ 127 之间所有的包装对象提前创建好，放到了一个方法区的“整数型常量池”中，目的是只要用这个区间的数据不需要 new。直接整数型常量池中取出。
```java
        Integer a = 127;
        Integer b = 127;
        Integer c = 128;
        Integer d = 128;

        System.out.println(a == b);   // true
        System.out.println(c == d);   // false
```
* 静态方法 parseInt()，parseDouble()，parseFloat。
```java
        int i = Integer.parseInt("123");  // String --> int
        double d = Double.parseDouble("3.14");
        float f = Float.parseFloat("12.5");
```
* 进制转换静态方法
```java
       String binary = Integer.toBinaryString(10);
        String hex = Integer.toHexString(10);
        String oct = Integer.toOctalString(10);

        System.out.println(binary);  // 1010
        System.out.println(hex);  // a
        System.out.println(oct);  // 12
```

## <font class="text-color-13" color="#ffeb3b">日期时间处理</font>
* 获取当前日期
```java
        Date date = new Date();
        System.out.println(date);   // 当前时间
```
* SimpleDateFormat 是 java.text 包下的，负责日期格式化。
    yyyy 年
    MM 月
    dd 日
    HH 时
    mm 分
    ss 秒
    SSS 毫秒
```java
        Date nowTime = new Date();

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        String nowTimeStr = sdf.format(nowTime);
        System.out.println(nowTimeStr);  // 自定义格式当前时间
```
* 字符串转日期类型。（需要 throws ParseException）
```java
        String time = "2023-01-11 22:45:17 652";

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        Date dateTime = sdf.parse(time);
        System.out.println(dateTime);  // Wed Jan 11 22:45:17 EST 2023
```
* System.currentTimeMillis() 计算程序执行时间。
```java
    long start= System.currentTimeMillis();   /*开始时间*/
    System.out.println("-----------程序执行时间为：" + (System.currentTimeMillis() - start) +"毫秒---------------");
```
## <font class="text-color-13" color="#ffeb3b">数字格式化</font>
    \# 任意数字
    ， 千分位
    . 小数点
    0 不够时补零
```java
        DecimalFormat df = new DecimalFormat("###,###.##");
        String str = df.format(1234.567);
        System.out.println(str);   // 1,234.57
```
* 随机数
```java
        Random rand = new Random();
        int num = rand.nextInt(101);  // 产生一个 0-100 之间的随机数
```

## <font class="text-color-13" color="#ffeb3b">枚举类型</font>
* [](https://)http://www.voidme.com/java-object-oriented/java-enum-types
* 枚举也是一种引用数据类型，编译后生成 class 文件，默认继承 Enum 类。Enum类中的 compareTo方法修饰符为 final 所以枚举类型不能重写这个方法。
* 枚举中的每一个值可以看做常量。
* 枚举类型不能继承，因为隐式继承 Enum，可以实现接口。
* <font class="text-color-11" color="#8bc34a">values</font>() 静态方法可以获取这个枚举类型的数组。
* int <font class="text-color-11" color="#8bc34a">ordinal</font>() ：返回此枚举常量的序数（它在其枚举声明中的位置，其中初始常量分配的序数为零）。
```java
    public static Result doSomething(int i){
        if(i == 10){
            return Result.SUCCESS;
        }
        else if(i == 0){
            return Result.FAIL;
        }
        else return Result.UNKNOWN;
    }


enum Result {
    SUCCESS, FAIL, UNKNOWN
}
```
* 枚举类中可以有构造器（默认 private）与方法。
```java
public enum DistributionRuleEnum {
    NORMAL(1,"快速配送"),
    PICKUP_YOURSELF(2,"自提"),
    APPOINTMENT_DELIVERY(3,"预约配送"),
    DOOR_TO_DELIVERY(4,"上门配送")
    ;

    private int type;
    private String desc;

    DistributionRuleEnum(int type, String desc) {
        this.type = type;
        this.desc = desc;
    }

    public int getType() {
        return type;
    }

    public String getDesc() {
        return desc;
    }
}
```
* 枚举类中的枚举类
```java
public enum DeliveryCompany {
    MEITUAN("美团",Color.YELLOW),
    ELEME("饿了么",Color.BLUE),
    XIAOHONGCHE("小红车",Color.RED),
    FANTUAN("饭团",Color.GREEN)
    ;
    private final String desc;
    private final Color color;
    public enum Color{RED,BLUE,YELLOW,GREEN}

    DeliveryCompany(String name, Color color) {
        this.desc = name;
        this.color = color;
    }

    public Color getColor() {
        return this.color;
    }
}
```



## <font class="text-color-13" color="#ffeb3b">异常</font>
* 异常在java中以类和对象的形式存在。
* 异常的继承结构。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_342250c2b3ab41cf4125fc6c514ae541.jpg)
* 编译时异常和运行时异常都发生在运行阶段。编译阶段异常不会发生。
* <font class="text-color-15" color="#ff9800">运行时异常</font>（受检/控异常）：在编写程序阶段，可以选择处理，也可以不处理。
* <font class="text-color-15" color="#ff9800">编译时异常</font>（非受检/控异常）：必须在编写程序的时候预先对这种异常进行处理，如果不处理，编译器报错。
* 编译时异常发生概率比运行时异常高。
* 对异常的两种处理（编译时异常）方式。
1. 在方法声明位置上，使用 <font class="text-color-15" color="#ff9800">throws</font> 关键字。（可以抛父类）（可以同时抛多个异常）
```java
   public static void main(String[] args) throws IOException {

        doSome();

    }


    public static void doSome() throws IOException {
        System.out.println("haha");
    }
```

2. 使用 <font class="text-color-15" color="#ff9800">try catch</font> 语句进行异常的捕捉。
```java
    public static void main(String[] args) {

        try {
            // try 尝试
            doSome();
        } catch (IOException e) {
            // 捕捉异常之后走的分支。
        }
        // try...catch 把异常抓住之后，这里的代码会继续执行。

    }


    public static void doSome() throws IOException {
        System.out.println("haha");
    }
```
* try 语句中某一行出现异常后，后续代码不会执行。
* 只要异常没有捕捉，采用上报的方式，出异常的方法之后代码不会执行。
* try...catch 把异常抓住之后，后续的代码会继续执行。
* catch 后面的小括号中的类型可以是具体的异常类型，也可以是该异常类型的父类型。
* catch 可以写多个，建议catch的时候，精确地一个个处理，利于程序调试。catch 写多个的时候，从上到下，必须遵守从小到大。
* 可以catch多个异常。
```java
        try{
            System.out.println(100/0);
        }
        catch (ArithmeticException | NullPointerException e){
            System.out.println("出现异常！");
        }
```
* 异常对象的常用方法。getMessage()  /  printStackTrace()
```java
       NullPointerException e = new NullPointerException("空指针异常");

        System.out.println(e.getMessage());

        e.printStackTrace();

        System.out.println("haha"); // 正常执行
```
* java 后台打印异常堆栈追踪信息的时候，采用了异步线程的方式打印。
* <font class="text-color-15" color="#ff9800">finally</font>：finally中的代码一定会执行，即使try中出现了异常。可以把流的关闭放在其中。
```java
        FileInputStream fs = null;
        try{
            fs = new FileInputStream("E:\\Code File");

            String s = null;
            s.toString();
        }
        catch (IOException e){
            System.out.println("文件路径不存在！");
        }
        catch (NullPointerException e){
            System.out.println("空指针异常！");
        }
        finally {
            if(fs != null){
                try {
                    fs.close();
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }
        }
```
* try 可以和 finally 单独一起使用，try 不能单独使用。
* <font class="text-color-15" color="#ff9800">自定义异常</font>
    1. 编写一个类继承 Exception（编译时） 或 RuntimeException（运行时）。
    2. 提供两个构造方法，一个无参数的，一个带有String参数的。
```java
public class MyException extends Exception {
    public MyException() {
    }

    public MyException(String message) {
        super(message);
    }
}
```

## <font class="text-color-13" color="#ffeb3b">集合</font>
* 集合在java.util.* 下
* java中集合分为两大类：
* 单个方式存储元素，这一类集合超级父接口：java.util.Collection
![](https://huatu.98youxi.com/markdown/work/uploads/upload_01d4300cae7a24d77e063074e809d939.jpg)
* 以键值对的方式存储元素，这一类集合超级父接口：java.util.Map
![](https://huatu.98youxi.com/markdown/work/uploads/upload_25a66feafe890265a2bacf9ceda533b5.jpg)
---
### <font class="text-color-15" color="#ff9800">Collection</font> 接口常用方法：
1. boolean <font class="text-color-11" color="#8bc34a">add</font>(Object o)
2. int <font class="text-color-11" color="#8bc34a">size</font>()
3. void <font class="text-color-11" color="#8bc34a">clear</font>()
4. boolean <font class="text-color-11" color="#8bc34a">contains</font>(Object o)
5. boolean <font class="text-color-11" color="#8bc34a">remove</font>(Object o) 
6. boolean <font class="text-color-11" color="#8bc34a">isEmpty</font>()
7. Object[] <font class="text-color-11" color="#8bc34a">toArray</font>()
---
###  <font class="text-color-15" color="#ff9800"> Iterator 和 Iterable 接口</font>
```java
        Collection c = new HashSet();

        c.add("a");
        c.add("b");
        c.add(123);
        
        Iterator it = c.iterator();   // 所有Collection子类通用
        while (it.hasNext()) {
            System.out.println(it.next());
        }
```
* 获取的迭代器对象，迭代器用来遍历集合，此时相当于对当前集合的状态拍了一个快照，迭代器迭代的时候会参照这个快照进行迭代。删除元素之后，集合的结构发生了变化，应该重新获取迭代器。否则出现异常：ConcurrentModificationException。要使用迭代器的remove方法删除元素。
* 任意类可以实现 Iterable 接口，只需要重写 iterator() 方法。
```java
public class CardList implements Iterable<Card> {

    ArrayList<Card> cardArrayList;


    @Override
    public Iterator<Card> iterator() {
        return cardArrayList.iterator();
    }
}
```
* <font class="text-color-7" color="#03a9f4">获取集合容器中不同的迭代器</font>：
```java
        Course english = new Course();
        english.addStudent(new Student(123,"wjh"));
        english.addStudent(new Student(777,"fds"));

        english.addGrade(new Grade("final",78));
        english.addGrade(new Grade("midterm",89));

        Iterator<Student> it1 = english.getStudentIterator();
        while (it1.hasNext()) {
            System.out.println(it1.next());
        }

        Iterator<Grade> it2 = english.getGradeIterator();
        while (it2.hasNext()) {
            System.out.println(it2.next());
        }
```
```java
public class Course {

    private ArrayList<Student> students = new ArrayList<>();
    private ArrayList<Grade> grades = new ArrayList<>();

    public Iterator<Student> getStudentIterator(){
        return students.iterator();
    }

    public Iterator<Grade> getGradeIterator(){
        return grades.iterator();
    }


    public void addStudent(Student student) {
        students.add(student);
    }

    public void addGrade(Grade grade){
        grades.add(grade);
    }
}
```
* <font class="text-color-7" color="#03a9f4">lamda 表达式实现 Iterable 接口</font>
```java
        Course english = new Course();
        english.addStudent(new Student(123,"wjh"));
        english.addStudent(new Student(777,"fds"));

        english.addGrade(new Grade("final",78));
        english.addGrade(new Grade("midterm",89));

        Iterator<Student> it1 = english.studentsIterate.iterator();
        while (it1.hasNext()) {
            System.out.println(it1.next());
        }

        Iterator<Grade> it2 = english.gradesIterate.iterator();
        while (it2.hasNext()) {
            System.out.println(it2.next());
        }
```
```java
public class Course {

    private ArrayList<Student> students = new ArrayList<>();
    private ArrayList<Grade> grades = new ArrayList<>();

    Iterable<Student> studentsIterate = students::iterator;
    Iterable<Grade> gradesIterate = grades::iterator;


    public void addStudent(Student student) {
        students.add(student);
    }

    public void addGrade(Grade grade){
        grades.add(grade);
    }
}
```

* <font class="text-color-11" color="#8bc34a">迭代器模式</font>：[](https://)https://blog.csdn.net/a745233700/article/details/83690748


---
### <font class="text-color-15" color="#ff9800">List</font> 接口常用方法：
1. void <font class="text-color-11" color="#8bc34a">add</font>(int index, E element)
2. E <font class="text-color-11" color="#8bc34a">get</font>(int index)
3. int <font class="text-color-11" color="#8bc34a">indexOf</font>(Object o)
4. int <font class="text-color-11" color="#8bc34a">lastIndexOf</font>(Object o)
5. E <font class="text-color-11" color="#8bc34a">remove</font>(int index)
6. E <font class="text-color-11" color="#8bc34a">set</font>(int index, E element)
#### <font class="text-color-7" color="#03a9f4">ArrayList</font>
* 初始化容量是10，创建时可以传入一个容量，底层是一个 Object[] 数组，内存地址连续。
* size获取的是集合中元素的个数。（和容量无关）
* 可以使用 ArrayList(Collection c) 创建。将c中元素存进ArrayList，存入顺序为c的迭代器获取的顺序。
* 查找效率高，末尾添加效率高。
* Collections.synchronizedList() 转换为线程安全。
```java
        List myList = new ArrayList(); // 非线程安全的
        // 变成线程安全的
        Collections.synchronizedList(myList);
        myList.add(123);
```
#### <font class="text-color-7" color="#03a9f4">LinkedList</font>
* 底层为双向链表数据结构，内存地址不连续。
* LinkedList没有初始化容量。
* 随机增删效率高。

---

### <font class="text-color-15" color="#ff9800">Set</font> 接口：

#### <font class="text-color-7" color="#03a9f4">TreeSet</font>
* 放在 TreeSet 中的元素需要实现 Comparable 接口，equals() 可以不用写。或者声明时传入 Comparator 进行比较。
* 迭代器采用的是中序遍历的方式：左根右。
* 常用方法：
1. E <font class="text-color-11" color="#8bc34a">higher</font>(E e) 返回此集合中严格大于给定元素的最小元素，或者null如果不存在这样的元素。
2. E <font class="text-color-11" color="#8bc34a">lower</font>(E e) 返回此集合中严格小于给定元素的最大元素，或者null如果不存在这样的元素。
3.  E <font class="text-color-11" color="#8bc34a">first</font>() 返回此集合中当前的第一个（最低）元素。
4.  E <font class="text-color-11" color="#8bc34a">last</font>() 返回此集合中当前的最后一个（最高）元素。
5.  E <font class="text-color-11" color="#8bc34a">floor</font>(E e) 返回此集合中小于或等于给定元素的最大元素，或者null如果不存在这样的元素。
6.  E <font class="text-color-11" color="#8bc34a">ceiling</font>(E e) 返回此集合中大于或等于给定元素的最小元素，或者null如果不存在这样的元素。
7.  E <font class="text-color-11" color="#8bc34a">pollFirst</font>() 检索并删除第一个（最低）元素，或者null如果此集合为空则返回。
8.  E <font class="text-color-11" color="#8bc34a">pollLast</font>() 检索并删除最后一个（最高）元素，null如果此集合为空则返回。
---
### <font class="text-color-15" color="#ff9800">泛型</font> 
* 使用泛型之后，List集合只允许存储指定的数据类型。
```java
        Animal a = new Cat();
        Cat c = new Cat();
        Dog d = new Dog();

        List<Animal> myList = new ArrayList<Animal>();

        myList.add(a);
        myList.add(c);
        myList.add(d);
        Iterator<Animal> it = myList.iterator(); // 表示迭代器只能迭代Animal类型
        while (it.hasNext()) {
            System.out.println(it.next());
        }

class Animal{
    public void move(){
        System.out.println("动物移动!");
    }
}

class Dog extends Animal{
    public void move() {
        System.out.println("狗在跑！");
    }
}

class Cat extends Animal{
    public void move() {
        System.out.println("猫在跑！");
    }
}
```
* 泛型这种语法机制，只在程序编译阶段起作用，只是给编译器参考的。（运行阶段泛型没用）
* 集合中元素的数据类型更加统一。从集合中取出的元素时泛型指定的类型，不需要进行大量的向下转型。
* 自动类型推断机制。（钻石表达式）
```java
List<Animal> myList = new ArrayList<>();
```
#### <font class="text-color-7" color="#03a9f4">自定义泛型</font>
```java
        Testing<String> t1 = new Testing<>();
        Testing<Integer> t2 = new Testing<>();

        t1.doSome("good");
        t2.doSome(1200);
        
        String s = t1.get();
        Integer i = t2.get();

class Testing<haha>{

    public void doSome(haha h){
        System.out.println(h);
    }

    public haha get(){
        return null;
    }

}
```
* 自定义泛型的时候，<>尖括号中的是一个标识符，随便写。
* 不用泛型就是Object类型。
*  泛型约束：
[](https://)http://www.voidme.com/java-object-oriented/java-generic-constraints
[](https://)https://blog.csdn.net/jdsjlzx/article/details/70479227
*  泛型方法：[](https://)http://www.voidme.com/java-object-oriented/java-generic-methods-constructors
```java
public class doTest {

    public static void main(String[] args) {

        List1<Integer> l1 = new List1<>(128);

        List2<String> l2 = new List2<>("hi");
        List2<Integer> l3 = new List2<>(86);

        doSome(l1,l2);
        doOther(l1,l3);

    }

    // 方法使用泛型：约束参数类型只能写死
    public static void doSome(List1<Integer> l1, List2<String> l2){
        System.out.println(l1.element);
        System.out.println(l2.element);
    }

    // 泛型方法：可以灵活地约束参数类型
    public static <T> void doOther(List1<T> l1, List2<T> l2){
        System.out.println(l1.element);
        System.out.println(l2.element);
    }
}
```
```java
class List1<T> {
    T element;

    public List1(T element) {
        this.element = element;
    }
}


class List2<T> {
    T element;

    public List2(T element) {
        this.element = element;
    }
}
```
---

### <font class="text-color-15" color="#ff9800">foreach</font> （增强for循环）
* 语法：
```java
for(元素类型 变量名 : array或Collection){
    System.out.println(变量名);
}
```
* 缺点：没有下标。
---
### <font class="text-color-15" color="#ff9800">Map</font> 接口常用方法：
* Map 和 Collection 没有继承关系。
* key 和 value 都是引用数据类型，key起主导作用。
1. V <font class="text-color-11" color="#8bc34a">put</font>(K key, V value) ：向Map集合添加键值对，key重复value会覆盖。
2. void <font class="text-color-11" color="#8bc34a">clear</font>() ：清空Map集合
3. boolean <font class="text-color-11" color="#8bc34a">containsKey</font>(Object key) ：判断Map集合是否包含某个key
4. boolean <font class="text-color-11" color="#8bc34a">containsValue</font>(Object value) ：判断Map集合是否包含某个value
5. V <font class="text-color-11" color="#8bc34a">get</font>(Object key) ：通过key获取value
6. boolean <font class="text-color-11" color="#8bc34a">isEmpty</font>() ：判断Map集合中元素个数是否为0
7. set\<K\> <font class="text-color-11" color="#8bc34a">keySet</font>() ：获取Map集合再所有的Key，返回一个 Set。
8. Collection\<V\> <font class="text-color-11" color="#8bc34a">values</font>() ：获取Map集合中所有的value，返回一个Collection。
9. int <font class="text-color-11" color="#8bc34a">size</font>() ：获取Map集合键值对的个数
10. V <font class="text-color-11" color="#8bc34a">remove</font>(Object key) ：通过key删除键值对
11. Set\<Map.Entry\<K,V\>\> <font class="text-color-11" color="#8bc34a">entrySet</font>() ：将Map集合转换成Set集合。
----
* Map集合通过entrySet()方法转换成的这个Set集合，Set集合中元素的类型是 Map.Entry<K,V>
    Map.Entry 是Map中的静态内部类。
* contains 底层调用的都是 equals() 方法进行比对。
* Map集合的遍历：
```java
       Map<Integer,String> map = new HashMap<>();

       map.put(21,"David");
       map.put(72,"Alex");
       map.put(55,"Bob");
       map.put(36,"Jerry");

       // 第一种方式：获取所有的key，通过遍历key来遍历value。
       Set<Integer> set_1 = map.keySet();

               // 迭代器
       Iterator<Integer> it_1 = set_1.iterator();
        while (it_1.hasNext()) {
            Integer key = it_1.next();
            String value = map.get(key);
            System.out.println(key + " = " + value);
        }

                // 增强for循环
        for(Integer key : set_1){
            System.out.println(key + " = " + map.get(key));
        }

        // 第二种方式：把Map集合直接全部转换成Set集合
        Set<Map.Entry<Integer,String>> set_2 = map.entrySet();

                // 迭代器
        Iterator<Map.Entry<Integer,String>> it_2 = set_2.iterator();
        while(it_2.hasNext()){
            Map.Entry<Integer,String> entry = it_2.next();
            Integer key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key + " = " + value);
        }

                // 增强for循环
        for(Map.Entry<Integer,String> entry : set_2){
            Integer key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key + " = " + value);
        }
```
* 第二种方式效率更高。
#### <font class="text-color-7" color="#03a9f4">HashMap</font>
* HashMap集合的 get() 和 put() 方法，会先后调用key的 hashCode() 和 equals() 方法。所以 key 部分的元素这两个方法都需要重写。（HashSet中的元素也需要）
* HashMap 的默认初始化容量是16，加载因子是0.75。
    默认加载因子是指当HashMap底层数组元素（包括链表上的）达到数组的容量的75%的时候，数组扩容为2倍。
* HashMap 集合初始化容量必须是2的次幂。这是为了达到散列均匀，提高HashMap存取效率所必须的。
* 如果节点的单向链表中元素达到8，同时数组长度达到64，单向链表会变成红黑树。当红黑树上节点小于6时，会重新把红黑树变成单向链表。
#### <font class="text-color-7" color="#03a9f4">Properties</font>
* setProperty()和getProperty()方法
```java
        Properties pro = new Properties();

        pro.setProperty("wjh","haha");
        pro.setProperty("wg","good");
        pro.setProperty("hl","hi");

        System.out.println(pro.getProperty("wjh"));
        System.out.println(pro.getProperty("hl"));
        System.out.println(pro.getProperty("wg"));
```
---
### <font class="text-color-15" color="#ff9800">Queue</font> 接口：
#### <font class="text-color-7" color="#03a9f4">PriorityQueue</font>
* 该队列的头部是相对于指定顺序的最小元素，元素需重写 compareTo方法。或者声明时传入 Comparator 进行比较。
* 常用方法：
1. E <font class="text-color-11" color="#8bc34a">peek</font>() 检索但不删除此队列的头部，或者null如果此队列为空则返回。
2. E <font class="text-color-11" color="#8bc34a">poll</font>() 检索并移除此队列的头部，或者null如果此队列为空则返回。


## <font class="text-color-13" color="#ffeb3b">Comparable</font> 接口
* 比较规则只有一个的时候，建议实现 Comparable 接口。
* 实现 Comparable 接口，在类中重写 compareTo 方法。
```java
    class Customer implements Comparable<Customer>{
        int age;
        
        @Override
        public int compareTo(Customer o) {
            return this.age - o.age;
        }
    }
```
* CompareTo() 的返回值：
    \> 0 ：调用对象 \> 参数对象
    = 0 ：调用对象 \= 参数对象
    \< 0 ：调用对象 \< 参数对象

## <font class="text-color-13" color="#ffeb3b">Comparator</font> 接口
* 如果比较规则有多个，需要在多个比较规则之间频繁切换，建议使用 Comparator 接口。（符合OCP）
* 创建具体 Comparator 类，实现 Comparator 接口。
```java
        // 创建 TreeSet 集合的时候，需要使用这个比较器。
        // 给构造方法传递一个比较器
        TreeSet<Customer> customers = new TreeSet<>(new CustomerComparator());
        customers.add(new Customer(1000));
        customers.add(new Customer(123));
        customers.add(new Customer(777));
        customers.add(new Customer(569));

        for(Customer customer : customers){
            System.out.println(customer);
        }

class Customer {
    int age;

    public Customer(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Customer{" +
                "age=" + age +
                '}';
    }
}


class CustomerComparator implements Comparator<Customer> {
    @Override
    public int compare(Customer o1, Customer o2) {
        return o1.age - o2.age;
    }
}
```
* 使用匿名内部类实现
```java
        // 创建 TreeSet 集合的时候，需要使用这个比较器。
        // 给构造方法传递一个比较器
        TreeSet<Customer> customers = new TreeSet<>(new Comparator<Customer>() {
            @Override
            public int compare(Customer o1, Customer o2) {
                return o1.age - o2.age;
            }
        });
        customers.add(new Customer(1000));
        customers.add(new Customer(123));
        customers.add(new Customer(777));
        customers.add(new Customer(569));

        for(Customer customer : customers){
            System.out.println(customer);
        }

class Customer {
    int age;

    public Customer(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Customer{" +
                "age=" + age +
                '}';
    }
}
```
* 使用 lamda 表达式实现
```java
        List<Student> students = new ArrayList<Student>();
        students.add(new Student(67,"Jerry"));
        students.add(new Student(11,"Bob"));
        students.add(new Student(45,"Alex"));
        students.add(new Student(23,"David"));
        
        // Comparator<Student> studentComparator = (o1, o2) -> o1.getId() - o2.getId();
        
        //Lamda 表达式实现 Comparator 接口
        students.sort((o1, o2) -> o1.getId() - o2.getId());

        for (Student student : students){
            System.out.println(student);
        }

class Student {

    private int id;
    private String name;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}
```
## <font class="text-color-13" color="#ffeb3b">IO流</font>
* IO 流四大家族的首领：（都是抽象类）
    1. java.io.InputStream 字节输入流
    2. java.io.OutputStream 字节输出流
    3. java.io.Read 字符输入流
    4. java.io.Write 字符输出流
* 所有流都实现了 java.io.Closable 接口，都是可关闭的，都有 <font class="text-color-15" color="#ff9800">close()</font> 方法，用完之后一定要关闭。
* 所有的输出流都实现了 java.io.Flushable 接口，都是可刷新的，都有 <font class="text-color-15" color="#ff9800">flush</font>() 方法，输出流在最终输出之后，一定要记得刷新一下。表示将管道中剩余为输出的数据强行输出完，清空管道，否则可能丢失数据。
* 工程 Project 的根目录就是IDEA的默认当前路径。
* 需要掌握的流：
    * <font class="text-color-11" color="#8bc34a">文件流</font>：
    1. java.io.FileInputStream
    2. java.io.FileOutputStream
    3. java.io.FileReader
    4. java.io.FileWriter
    * <font class="text-color-11" color="#8bc34a">转换流（将字节流转换成字符流）</font>：
    5. java.io.InputStreamReader
    6. java.io.InputStreamWriter
    * <font class="text-color-11" color="#8bc34a">缓冲流</font>：
    7. java.io.BufferedReader
    8. java.io.BufferedWriter
    9. java.io.BufferedInputStream
    10. java.io.BufferedOutputStream
    * <font class="text-color-11" color="#8bc34a">数据流</font>
    11. java.io.DataInputStream
    12. java.io.DataOutputStream
    * <font class="text-color-11" color="#8bc34a">对象流</font>
    13. java.io.ObjectInputStream
    14. java.io.ObjectOutputStream
    * <font class="text-color-11" color="#8bc34a">标准输出流</font>
    15. java.io.PrintWriter
    16. java.io.PrintStream
---
### <font class="text-color-15" color="#ff9800">文件专属流</font>
#### <font class="text-color-7" color="#03a9f4">FileInputStream</font>
* 创建文件字节输入流
```java
        FileInputStream fis = null;
        try {
            fis = new FileInputStream("src/Test_1/test_file.txt");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
* int <font class="text-color-11" color="#8bc34a">read</font>() 从此输入流中读取一个字节的数据并返回，或者 -1由于已到达文件末尾而没有更多数据。
* 一次读一个 byte，内存和硬盘交互太频繁，耗费大量时间和资源
```java
        FileInputStream fis = null;
        try {
            fis = new FileInputStream("src/Test_1/test_file.txt");
            int readData = 0;   // 循环读
            while ((readData = fis.read()) != -1) {
                System.out.println(readData);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
* int <font class="text-color-11" color="#8bc34a">read</font>(byte[] b) 一次最多读取 b.length 个字节，返回的是读取到的字节数量，-1表示没有读到。
* 使用 String 的构造方法 ：<font class="text-color-11" color="#8bc34a">String</font>(byte[] bytes, int offset, int length)
```java
        FileInputStream fis = null;
        try {
            
            fis = new FileInputStream("test.txt");
            byte[] bytes = new byte[4];   // 创建byte数组循环读入
            int readCount = 0;
            while((readCount = fis.read(bytes)) != -1){
                System.out.print(new String(bytes,0,readCount));
            }

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

```
* int <font class="text-color-11" color="#8bc34a">available</font>() 返回可以从此输入流中读取（或跳过）的剩余字节数的估计值，而不会被下一次为此输入流的方法调用阻塞。
* 这种方法不太适合大文件。
```java
        FileInputStream fis = null;
        try {

            fis = new FileInputStream("test.txt");
            byte[] bytes = new byte[fis.available()];   // 只创建一个大 byte 数组读取
            fis.read(bytes);
            System.out.println(new String(bytes));

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis != null){
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```

* long <font class="text-color-11" color="#8bc34a">skip</font>(long n) 跳过并丢弃n个输入流中的数据字节。
---
#### <font class="text-color-7" color="#03a9f4">FileOutputStream</font>
* <font class="text-color-11" color="#8bc34a">FileOutputStream</font>(String name, boolean append) 创建文件输出流以写入具有指定名称的文件。append 为 true 则以追加的方式写入，不会清空原文件内容。
* void <font class="text-color-11" color="#8bc34a">write</font>(byte[] b) 将b.length指定字节数组中的字节写入此文件输出流。
* void <font class="text-color-11" color="#8bc34a">write</font>(byte[] b, int off, int len) 将len指定字节数组中的字节从偏移量开始写入off此文件输出流。
* 文件如果不存在会自动新建。
```java
        FileOutputStream fos = null;
        try {

            fos = new FileOutputStream("write.txt",true);
            byte[] bytes = {97,98,99,100};
            fos.write(bytes);

            String s = "波斯特对应问题";
            byte[] bs = s.getBytes();
            fos.write(bs);
            
            fos.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fos != null) {
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
---
#### <font class="text-color-7" color="#03a9f4">文件复制</font>
```java
        FileInputStream fis = null;
        FileOutputStream fos = null;
        try {

            fis = new FileInputStream(filePath);
            fos = new FileOutputStream(directory);
            byte[] bytes = new byte[1024 * 1024];
            int readCount = 0;
            while ((readCount = fis.read(bytes)) != -1){
                fos.write(bytes, 0, readCount);
            }

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (fos != null) {
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
#### <font class="text-color-7" color="#03a9f4">FileReader</font>
* 文件字符输入流，只能读取普通文本（能用记事本编辑的都是普通文本文件）。
```java
        FileReader reader = null;
        try {
            reader = new FileReader("read.txt");
            char[] chars = new char[4];
            int readCount = 0;
            while((readCount = reader.read(chars)) != -1) {
                System.out.print(new String(chars,0,readCount));
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
#### <font class="text-color-7" color="#03a9f4">FileWriter</font>
```java
        FileWriter writer = null;
        try {
            writer = new FileWriter("write.txt");
            char[] chars = {'我','是','学','生'};
            writer.write(chars,0,4);
            writer.write("乔姆斯基范式");  // 可直接写入String

            writer.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (writer != null) {
                try {
                    writer.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```    
#### <font class="text-color-7" color="#03a9f4">普通文本文件复制</font>
```java
        FileReader in = null;
        FileWriter out = null;
        try {
            in = new FileReader("read.txt");
            out = new FileWriter("write.txt");

            char[] chars = new char[1024 * 512];
            int readCount = 0;
            while((readCount = in.read(chars)) != -1){
                out.write(chars,0,readCount);
            }

            out.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (in != null) {
                try {
                    in.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (out != null) {
                try {
                    out.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
---
### <font class="text-color-15" color="#ff9800">缓冲流</font>

#### <font class="text-color-7" color="#03a9f4">BufferedReader</font>
* 带有缓冲区的字符输入流
* 使用这个流的时候不需要自己创建char和byte数组，自带缓冲。
* <font class="text-color-11" color="#8bc34a">BufferedReader</font>(Reader in) ：构造器
* 当一个流的构造方法中需要一个流的时候，这个被传进来的流叫做：<font class="text-color-15" color="#ff9800">节点流</font>。
* 外部负责包装的这个流叫做：<font class="text-color-15" color="#ff9800">包装流 / 处理流</font>。
* 对于包装流来说，只需要关闭最外层的流，里面的流会一起被关闭。
* String <font class="text-color-11" color="#8bc34a">readLine</font>() ：读取一行文本，但不带换行符。
```java
        FileReader reader = null;
        try {
            reader = new FileReader("read.txt");
            BufferedReader in = new BufferedReader(reader);
            String s = null;
            while((s = in.readLine()) != null){
                System.out.println(s);
            }

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
* 通过转换流转换： InputStreamReader 可以将字节流转换成字符流。
```java
        FileInputStream fis = null;
        try {
            // 字节流
            fis = new FileInputStream("read.txt");
            // 通过转换流转换
            InputStreamReader reader = new InputStreamReader(fis);
            // 传入 BufferedReader 构造方法
            BufferedReader br = new BufferedReader(reader);
            
                        // 可以合并
//            BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream("read.txt")));

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
---
#### <font class="text-color-7" color="#03a9f4">BufferedWriter</font>
* 带有缓冲的字符输出流
```java
        BufferedWriter bw = null;
        try {

            bw = new BufferedWriter(new FileWriter("write.txt",true));
            bw.write("正则语言");
            bw.flush();

        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (bw != null){
                try {
                    bw.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
---
### <font class="text-color-15" color="#ff9800">数据流</font>

#### <font class="text-color-7" color="#03a9f4">DataOutputStream</font>
* 这个流可以将数据连同数据的类型一并写入文件。这个文件不是普通文本文档（记事本打不开）。
* <font class="text-color-11" color="#8bc34a">DataOutputStream</font>(OutputStream out) ：构造方法，创建一个新的数据输出流以将数据写入指定的底层输出流。
```java
        DataOutputStream dos = null;
        try {
            dos = new DataOutputStream(new FileOutputStream("data"));
            byte b = 12;
            short s = 100;
            int i = 1234;
            long l = 765L;
            float f = 3.5f;
            double d = 123.4;
            boolean sex = true;
            char c = 'b';

            dos.writeByte(b); // 把数据以及数据的类型一并写入文件
            dos.writeShort(s);
            dos.writeInt(i);
            dos.writeLong(l);
            dos.writeFloat(f);
            dos.writeDouble(d);
            dos.writeBoolean(sex);
            dos.writeChar(c);

            dos.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (dos != null){
                try {
                    dos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
---
#### <font class="text-color-7" color="#03a9f4">DataInputStream</font>
* 数据字节输入流
* DataOutputStream 写的文件，只能使用 DataInputStream 去读，并且读的时候需要提前知道写入的顺序。度的顺序和写的顺序需要一致。
```java
        DataInputStream dis = null;
        try {

            dis = new DataInputStream(new FileInputStream("data"));

            byte b = dis.readByte();
            short s = dis.readShort();
            int i = dis.readInt();
            long l = dis.readLong();
            float f = dis.readFloat();
            double d = dis.readDouble();
            boolean sex = dis.readBoolean();
            char c = dis.readChar();

            System.out.println(b);
            System.out.println(s);
            System.out.println(i);
            System.out.println(l);
            System.out.println(f);
            System.out.println(d);
            System.out.println(sex);
            System.out.println(c);

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (dis != null){
                try {
                    dis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
---
### <font class="text-color-15" color="#ff9800">标准输出流</font>

#### <font class="text-color-7" color="#03a9f4">PrintStream</font>
* 标准输出流不需要手动 close() 关闭。
* <font class="text-color-11" color="#8bc34a">PrintStream</font>(OutputStream out) ：构造方法
* 将标准输出流指向某一文件。
```java
    public static void main(String[] args) throws FileNotFoundException {

        PrintStream out = new PrintStream(new FileOutputStream("log"));
        System.setOut(out);

        System.out.println("上下文无关语言");

    } 
```
* 可以用来实现日志工具
```java
    public static void log(String msg){
        // 保存最原始的输出流
        PrintStream out = System.out;
        try {
            // 标准输出流指向日志文件
            PrintStream printStream = new PrintStream(new FileOutputStream("log",true));
            // 改变输出方向
            System.setOut(printStream);
            // 日期格式化
            Date nowTime = new Date();
            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
            String timeStr = sdf.format(nowTime);
            System.out.println(timeStr + ": " + msg);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        // 将标准输出流重定向至控制台
        System.setOut(out);
    }
```
### <font class="text-color-15" color="#ff9800">IO与properties集合联合使用</font>
* properties 的 load 方法
void <font class="text-color-11" color="#8bc34a">load</font>(InputStream inStream) ：从输入字节流中读取属性列表（键和元素对）。
void <font class="text-color-11" color="#8bc34a">load</font>(Reader reader) 以简单的面向行的格式从输入字符流中读取属性列表（键和元素对）。
String <font class="text-color-11" color="#8bc34a">getProperty</font>(String key) ：在此属性列表中搜索具有指定键的属性。
* 文件格式：等号左边做key，右边做value，称作<font class="text-color-15" color="#ff9800">属性配置文件</font>，建议以 .properties 结尾，key 重复 value 会自动覆盖，#可以注释。
```
username=admin
password=32467
```
* properties 是专门存放属性配置文件内容的一个类。
```java
        FileReader reader = null;
        try {

            reader = new FileReader("userinfo.properties");
            Properties properties = new Properties();
            // load方法读取流中的属性配置文件信息
            properties.load(reader);
            System.out.println(properties.getProperty("username"));

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
---
## <font class="text-color-13" color="#ffeb3b">File类</font>
* File和流没有关系，不能完成文件的读和写。
* File 对象：文件和路径名的抽象表示形式。（可能对应的是目录，也可能是文件）

### <font class="text-color-15" color="#ff9800">File类常用方法</font>
* <font class="text-color-11" color="#8bc34a">File</font>(String pathname) ：File通过将给定的路径名字符串转换为抽象路径名来创建一个新实例。
* <font class="text-color-11" color="#8bc34a">boolean</font> exists() ：测试此抽象路径名表示的文件或目录是否存在。
* boolean <font class="text-color-11" color="#8bc34a">createNewFile</font>() ：当且仅当具有此名称的文件尚不存在时，以原子方式创建一个以此抽象路径名命名的新空文件。
```java
        File f1 = new File("E:\\game\\log");

        if(!f1.exists()){
            f1.createNewFile();
        }
```

* boolean <font class="text-color-11" color="#8bc34a">mkdir</font>() ：创建以此抽象路径名命名的目录。
* boolean <font class="text-color-11" color="#8bc34a">mkdirs</font>() ：创建以此抽象路径名命名的目录，包括任何必需但不存在的父目录。（多重目录）
* String <font class="text-color-11" color="#8bc34a">getParent</font>() ：返回此抽象路径名的父目录的路径名字符串，或者 null如果此路径名未命名父目录。
* File <font class="text-color-11" color="#8bc34a">getParentFile</font>() 返回此抽象路径名的父目录的抽象路径名，或者null如果此路径名未命名父目录。
* String <font class="text-color-11" color="#8bc34a">getAbsolutePath</font>() 返回此抽象路径名的绝对路径名字符串。
* File <font class="text-color-11" color="#8bc34a">getAbsoluteFile</font>() ：返回此抽象路径名的绝对形式。
* boolean <font class="text-color-11" color="#8bc34a">delete</font>() ：删除此抽象路径名表示的文件或目录。
* String <font class="text-color-11" color="#8bc34a">getName</font>() ：返回此抽象路径名表示的文件或目录的名称。
* boolean <font class="text-color-11" color="#8bc34a">isFile</font>() ：测试此抽象路径名表示的文件是否为普通文件。
* boolean <font class="text-color-11" color="#8bc34a">isDirectory</font>() ：测试此抽象路径名表示的文件是否为目录。
* long <font class="text-color-11" color="#8bc34a">lastModified</font>() ：返回上次修改此抽象路径名表示的文件的时间。（从1970年到现在的总毫秒数）
```java
        File f1 = new File("E:\\game\\log");
    // 获取最后修改时间
        long modifyTime = f1.lastModified();
        Date time = new Date(modifyTime);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        System.out.println(sdf.format(time));
```
* long <font class="text-color-11" color="#8bc34a">length</font>() 返回此抽象路径名表示的文件的长度。（字节数）
* File[] <font class="text-color-11" color="#8bc34a">listFiles</font>() 返回一个抽象路径名数组，表示此抽象路径名表示的目录中的文件。
```java
        File f1 = new File("E:\\Code File");

        File[] files = f1.listFiles();

        for(File file : files){
            System.out.println(file.getAbsolutePath());
        }
```
* 拷贝目录（递归）
```java
    public static boolean copyDirectory(File srcFile, File destFile){
        if(srcFile.isFile()){
            copyFile(srcFile,destFile);
            return true;
        }
        else {
            String src = srcFile.getAbsolutePath();
            String dest = destFile.getAbsolutePath();
            File newDir = new File(dest += "/" + src.substring(Math.max(src.lastIndexOf("\\"),src.lastIndexOf("/")) + 1));
            if(! newDir.exists()){
                newDir.mkdir();
            }
            else return false;

            File[] files = srcFile.listFiles();
            for (File file : files) {
                copyDirectory(file, newDir);
            }
            return true;
        }
    }
```
## <font class="text-color-13" color="#ffeb3b">序列化和反序列化</font>
### <font class="text-color-15" color="#ff9800">序列化</font>（serialize）
* 把java对象存储到文件中，将java对象的状态保存下来的过程。
* final void <font class="text-color-11" color="#8bc34a">writeObject</font>(Object obj) 将指定对象写入 ObjectOutputStream。
```java
        Account account = new Account(1123,"Jerry");

        ObjectOutputStream oos = null;
        try {
            oos = new ObjectOutputStream(new FileOutputStream("Account"));
            // 序列化account对象
            oos.writeObject(account);
            oos.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (oos != null) {
                try {
                    oos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }       
```
* 参与序列化和反序列化的对象，必须实现 Serializable 接口。
* Serializable 接口只是一个标志接口。
```java
public interface Serializable {
}
```
* Serializable 接口是给JVM参考的，JVM看到这个接口后会为改类自动生成一个序列化版本号。
---
### <font class="text-color-15" color="#ff9800">反序列化</font>（deserialize）
* 将文件中的数据重新恢复到内存中，恢复成java对象。
```java
       ObjectInputStream ois = null;
        try {

            ois = new ObjectInputStream(new FileInputStream("Account"));
            // 反序列化对象
            Object obj = ois.readObject();
            System.out.println(obj);

        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (ois != null) {
                try {
                    ois.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
```
---
### <font class="text-color-15" color="#ff9800">序列化多个对象</font>
* 将对象放到集合中，序列化集合。
```java
        List<Account> accountList = new ArrayList<>();
        accountList.add(new Account(234,"Jerry"));
        accountList.add(new Account(657,"Bob"));
        accountList.add(new Account(985,"Sam"));

        ObjectOutputStream oos = null;
        try {
            oos = new ObjectOutputStream(new FileOutputStream("Account"));
            oos.writeObject(accountList);
            oos.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (oos != null) {
                try {
                    oos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```
* 取出时可以强制类型转换
```java
        ObjectInputStream ois = null;
        try {

            ois = new ObjectInputStream(new FileInputStream("Account"));
            Object obj = ois.readObject();
            List<Account> accountList = (List<Account>)obj;
            for (Account account : accountList) {
                System.out.println(account);
            }

        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (ois != null) {
                try {
                    ois.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
```
---
### <font class="text-color-15" color="#ff9800">transient</font>
* 有 transient 关键字的属性，不参与序列化
```java
    private transient String holder;
```
* 反序列化后读出来对象这个属性的值为 null
---
### <font class="text-color-15" color="#ff9800">序列化版本号</font>
* java语言区分类的机制：首先通过类名进行比对，如果类名一样，靠序列化版本号进行区分。
* 类改动以后，编译后自动生成的序列化版本号会改变。缺陷：一旦代码确定之后，不能进行后续的修改，因为只要修改，必然会进行重新编译，此时会生成全新的序列化版本号，JVM会认定其为一个全新的类。反序列化之前序列化的对象会因为序列化版本号不匹配而报错。
* 凡是一个类实现了 Serializable 接口，建议给该类提供一个固定不变的序列化版本号。这样，以后即使代码修改了，但是版本号不变，JVM会认为是同一个类。
```java
private static final long serialVersionUID = 5375435475L;
```
---
## <font class="text-color-13" color="#ffeb3b">多线程</font>
* 进程是一个应用程序。（1个进程是一个软件）
* 线程是一个进程中的执行场景 / 执行单元，一个进程可以启动多个线程。
* 运行java程序会先启动JVM，而JVM就是一个进程，JVM再启动一个主线程调用main方法，同时启动一个GC线程负责看护，回收垃圾。所有java程序至少有两个线程并发。（GC线程和main方法的主线程）
* 进程和线程区别：
进程A和进程B的内存独立不共享。
java中，线程A和线程B堆内存和方法区内存共享，栈内存独立，一个线程一个栈。每个栈和栈之间互不干扰，各自执行，称为多线程并发，提高程序处理效率。
---
### <font class="text-color-15" color="#ff9800">实现线程的方式</font>
#### <font class="text-color-7" color="#03a9f4">第一种：继承 Thread 类</font>
* 编写一个类，直接继承 java.lang.Thread，重写 run 方法。
* void <font class="text-color-11" color="#8bc34a">run</font>() ：该方法在执行时由线程运行。
* void <font class="text-color-11" color="#8bc34a">start</font>() 安排此线程开始执行。
```java
    public static void main(String[] args) {
        // 这里是 main 方法，这里的代码属于主线程，在主栈中压栈
        // 新建一个分支线程对象
        MyThread myThread = new MyThread();

        // 启动线程
        myThread.start();
        // 这里的代码还是运行在主线程中
        for (int i = 0; i < 1000; i++) {
            System.out.println("主线程 ---> " + i);
        }

    }

class MyThread extends Thread {
    @Override
    public void run() {
        // 编写程序，这段程序运行在分支线程中（分支栈）。
        for (int i = 0; i < 1000; i++) {
            System.out.println("分支线程 ---> " + i);
        }
    }
}
```
* start() 方法的作用是：启动一个分支线程，在JVM中开辟一个新的栈空间。只要新的栈空间开辟出来，start() 方法就结束了，线程启动成功。
* 启动成功的线程会自动调用 run() 方法，并且run()方法在分支栈的底部（压栈）。main() 方法在主栈底部，run和main是平级的。(只调用 run() 方法不会开辟新的栈空间，还是在主栈中执行)
* run() 当中异常不能 throws，只能 try catch，因为 run() 方法在父类中没有抛出任何异常，子类不能比父类抛出更多异常。
---

#### <font class="text-color-7" color="#03a9f4">第二种：实现 Runnable 接口</font>
* 定义一个可运行的类，实现 java.lang.Runnable 接口，实现 run() 方法。
* <font class="text-color-11" color="#8bc34a">Thread</font>(Runnable task) ：Thread构造器，初始化一个新Thread。
```java
    public static void main(String[] args) {
        // 这里是 main 方法，这里的代码属于主线程，在主栈中压栈

        // 创建一个可运行的对象，将可运行的对象封装成一个线程对象
        Thread myThread = new Thread(new MyRunnable());

        // 启动线程
        myThread.start();
        // 这里的代码还是运行在主线程中
        for (int i = 0; i < 100; i++) {
            System.out.println("主线程 ---> " + i);
        }

    }

class MyRunnable implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("分支线程 ---> " + i);
        }
    }
}
```
* 第二种方式实现接口比较常用，因为一个类实现了接口，它还可以继承其它的类，更灵活。
* <font class="text-color-15" color="#ff9800">匿名内部类</font>实现 Runnable 接口
```java
    public static void main(String[] args) {
        // 这里是 main 方法，这里的代码属于主线程，在主栈中压栈

        // 匿名内部类实现 Runnable 接口，封装成线程对象
        Thread myThread = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 100; i++) {
                    System.out.println("分支线程 ---> " + i);
                }
            }
        });

        // 启动线程
        myThread.start();
        // 这里的代码还是运行在主线程中
        for (int i = 0; i < 100; i++) {
            System.out.println("主线程 ---> " + i);
        }

    }
}
```
* <font class="text-color-15" color="#ff9800">Lamda表达式</font>实现 Runnable 接口
```java
    public static void main(String[] args) {
        // 这里是 main 方法，这里的代码属于主线程，在主栈中压栈
        
        // Lamda表达式实现 Runnable 接口，封装成线程对象
        Thread myThread = new Thread(() -> {
            for (int i = 0; i < 100; i++) {
                System.out.println("分支线程 ---> " + i);
            }
        });

        // 启动线程
        myThread.start();
        // 这里的代码还是运行在主线程中
        for (int i = 0; i < 100; i++) {
            System.out.println("主线程 ---> " + i);
        }

    }
}
```
#### <font class="text-color-7" color="#03a9f4">第三种：实现 Callable 接口</font>
* 创建 FutureTask 对象。
    [](https://)https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/concurrent/FutureTask.html
* 这种方式实现的线程可以获取线程的返回值
* V <font class="text-color-11" color="#8bc34a">get</font>() ：如有必要，等待计算完成，然后检索其结果。
* 效率较低，在获取执行结果时，当前线程受阻塞。
```java
    public static void main(String[] args) throws ExecutionException, InterruptedException {

        // 创建 FutureTask 对象，传入对 Callable 接口的实现
        FutureTask<Integer> task = new FutureTask(new MyCall());

        // 创建线程对象，传入 FutureTask 对象
        Thread myThread = new Thread(task);
        myThread.start();

        // 可能导致当前线程阻塞
        int result = task.get();
        
    }
```
```java
class MyCall implements Callable<Integer>{

    @Override
    public Integer call() throws Exception {
        int res = 100;
        return 100;
    }
}
```


---
### <font class="text-color-15" color="#ff9800">线程的生命周期</font>
![](https://huatu.98youxi.com/markdown/work/uploads/upload_a4cf4b14a80c48c121e6081f9aa181f4.jpg)

---
### <font class="text-color-15" color="#ff9800">Thread 常用方法</font>
* final void <font class="text-color-11" color="#8bc34a">setName</font>(String name) ：将此线程的名称更改为等于 argument name。
* final String <font class="text-color-11" color="#8bc34a">getName</font>() ：返回此线程的名称，默认名字：Thread-0，Thread-1 ...
* static Thread <font class="text-color-11" color="#8bc34a">currentThread</font>() ：静态方法，返回当前线程的 Thread 对象。
```java
    public static void main(String[] args) {
        // 这里是 main 方法，这里的代码属于主线程，在主栈中压栈

        // Lamda表达式实现 Runnable 接口，封装成线程对象
        Thread myThread = new Thread(() -> {
            for (int i = 0; i < 50; i++) {
                System.out.println("分支线程 ---> " + i);
            }
            System.out.println(Thread.currentThread().getName()); // Thread-0
        });

        // 启动线程
        myThread.start();
        // 这里的代码还是运行在主线程中
        for (int i = 0; i < 50; i++) {
            System.out.println("主线程 ---> " + i);
        }
        System.out.println(Thread.currentThread().getName());  // main

    }
```
* static void <font class="text-color-11" color="#8bc34a">sleep</font>(long millis) ：使当前正在执行的线程休眠（进入阻塞状态）指定的毫秒数，放弃占有CPU时间片，让给其他线程使用。
```java
        // 每隔一秒执行一次循环中的代码
        for (int i = 0; i < 50; i++) {
            System.out.println(Thread.currentThread().getName() + " --> " + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
```
* void <font class="text-color-11" color="#8bc34a">interrupt</font>() 中断此线程，可以利用 catch 语句块终止睡眠。
* final void <font class="text-color-11" color="#8bc34a">stop</font>() ：已弃用，这种方法本质上是不安全的，直接杀死线程，可能导致数据丢失。
#### <font class="text-color-7" color="#03a9f4">终止线程</font>
* 使用布尔标记位
```java
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread myThread = new Thread(myRunnable);
        
        // 启动 myThread 线程
        myThread.start();

        // 主线程睡 3s
        for (int i = 0; i < 3; i++) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        // 终止线程时，把标记为改为 false
        myRunnable.run = false;

    }


class MyRunnable implements Runnable {

    // 布尔标记
    boolean run = true;

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            if(run){
                System.out.println(Thread.currentThread().getName() + " --> " + i);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            else{
                // 结束之前保存数据
                return; // 终止当前线程
            }
        }
    }
}
```
---
### <font class="text-color-15" color="#ff9800">线程调度</font>
* 常见的线程调度模型：
    1. 抢占式调度模型：线程的优先级高，抢到的CPU时间片概率高一些/多一些，java采用的就是抢占式调度模型。
    2. 平均式调度模型：平均分配CPU时间片。每个线程占有的CPU时间片长度一样。
#### <font class="text-color-7" color="#03a9f4">线程调度相关方法</font>
* final void <font class="text-color-11" color="#8bc34a">setPriority</font>(int newPriority) 更改此线程的优先级。
* final int <font class="text-color-11" color="#8bc34a">getPriority</font>() 返回此线程的优先级。
* 最低优先级：1 
* 默认优先级：5
* 最高优先级：10
```java
    public static void main(String[] args) {

        Thread currentThread = Thread.currentThread();

        Thread myThread = new Thread(() -> {
            System.out.println(Thread.currentThread().getName() + "线程的默认优先级：" + Thread.currentThread().getPriority());
            Thread.currentThread().setPriority(1);
            // 分支线程循环
            for (int i = 0; i < 100; i++) {
                System.out.println(Thread.currentThread().getName());
            }
        });

        myThread.start(); // 启动分支线程

        System.out.println(currentThread.getName() + "线程的默认优先级：" + currentThread.getPriority());
        currentThread.setPriority(10);
        // 主线程循环
        for (int i = 0; i < 100; i++) {
            System.out.println(Thread.currentThread().getName());
        }

    }
```
* static void <font class="text-color-11" color="#8bc34a">yield</font>() 向调度程序提示当前线程愿意放弃其当前对处理器的使用。会让当前线程从“运行状态”回到“就绪状态”。（回到就绪后有可能还会再次抢到）
```java
    public static void main(String[] args) {

        Thread currentThread = Thread.currentThread();

        Thread myThread = new Thread(() -> {
            // 分支线程循环
            for (int i = 0; i < 100; i++) {
                if(i % 5 == 0){
                    Thread.yield();
                }
                System.out.println(Thread.currentThread().getName() + "--->" + i);
            }
        });

        myThread.start(); // 启动分支线程

        // 主线程循环
        for (int i = 0; i < 100; i++) {
            System.out.println(Thread.currentThread().getName() + "--->" + i);
        }

    }
```

* final void <font class="text-color-11" color="#8bc34a">join</font>() 等待此线程终止。
```java
   public static void main(String[] args) {

        Thread currentThread = Thread.currentThread();

        Thread myThread = new Thread(() -> {
            // 分支线程循环
            for (int i = 0; i < 100; i++) {
                System.out.println(Thread.currentThread().getName() + "--->" + i);
            }
        });

        myThread.start(); // 启动分支线程

        // 主线程循环
        for (int i = 0; i < 100; i++) {
            if(i == 50){
                try {
                    myThread.join(); // myThread线程合并到当前线程中，myThread执行直到结束
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println(Thread.currentThread().getName() + "--->" + i);
        }

    }
```
---
### <font class="text-color-15" color="#ff9800">线程安全</font>
* 什么时候数据在多线程并发的环境下会存在安全问题？（三个条件）
    1. 多线程并发
    2. 有共享数据
    3. 共享数据有修改行为
* 局部变量在栈中，不存在线程安全问题。
* <font class="text-color-11" color="#8bc34a">线程同步机制</font>：线程不能并发，需排队执行。会牺牲一部分效率。
* <font class="text-color-7" color="#03a9f4">异步编程模型</font>：线程t1和t2各自执行，互相不管，谁也不需要等谁，多线程并发，效率较高。
* <font class="text-color-7" color="#03a9f4">同步编程模型</font>：线程t1和t2，其中一个线程执行的时候必须等待另一个线程执行结束，两个线程之间有等待关系，效率较低。
#### <font class="text-color-7" color="#03a9f4">synchronized()</font>

* 线程同步的语法机制：<font class="text-color-15" color="#ff9800">synchronized()</font> ，后面小括号中传的这个数据必须是多线程共享的数据，才能达到多线程排队。
```java
        synchronized (排队线程的共享的对象){ 
            // 线程同步代码块
        }
```
* () 中写什么？具体看想要让哪些线程同步：
    假设 t1, t2, t3, t4, t5 有5个线程，只希望 t1, t2, t3 排队， t4, t5不需要排队。则在 () 中写一个 t1, t2, t3 共享的对象。而这个对象对于 t4, t5 来说不是共享的。
* <font class="text-color-15" color="#ff9800">对象锁</font>：java中，任何对象都有“一把锁”（标记）。
    1. 假设 t1 先执行了，遇到了synchronized ()，这个时候 t1 自动找 () 中的对象的对象锁，找到之后 t1 会占有这把锁，然后执行同步代码块中的程序，直到同步代码块结束，这把锁才会被 t1 释放。
    2. 假设 t1 已经占有这把锁，此时 t2 也遇到synchronized ()，也会去找 () 中的对象的对象锁，结果这把锁被 t1 占有， t2 只能在同步代码块外等待  t1 结束执行完同步代码块后释放这把锁，然后 t2 占有这把锁，进入同步代码块执行程序。
    3. 注：这里的共享对象一定是你需要排队执行的这些线程所共享的。
    4. [](https://)https://blog.csdn.net/guoguo527/article/details/118004077?app_version=5.14.0&csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22118004077%22%2C%22source%22%3A%22unlogin%22%7D&utm_source=app
* <font class="text-color-15" color="#ff9800">锁池</font>
![](https://huatu.98youxi.com/markdown/work/uploads/upload_159189774d566edd3caeacb1d93524ff.jpg)
---
#### <font class="text-color-7" color="#03a9f4">账户类例子</font>
```java
    public static void main(String[] args) {
        // 创建账户对象
        Account act = new Account("act01",10000);
        // 创建两个线程
        Thread t1 = new AccountThread(act);
        Thread t2 = new AccountThread(act);

        t1.setName("t1");
        t2.setName("t2");
        // 启动取款线程
        t1.start();
        t2.start();

    }
```
```java
public class Account {
    // 账号
    private String actno;
    // 余额
    private double balance;

    public Account() {}

    public Account(String actno, int balance) {
        this.actno = actno;
        this.balance = balance;
    }

    public String getActno() {
        return actno;
    }

    public void setActno(String actno) {
        this.actno = actno;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }

    // 取款方法
    public void withdraw(double money) {
        // 以下的代码必须是线程排队的，不能并发。一个线程把这里的代码全部执行结束之后，另一个线程才能进来
        synchronized (this){ // 线程同步代码块
            // 取款之前余额
            double before = this.getBalance();
            // 取款之后余额
            double after = before - money;
            // 模拟网络延迟1秒
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            // 更新余额
            this.setBalance(after);
        }
    }
}
```
```java
public class AccountThread extends Thread {
    // 线程共享同一个账户对象
    private Account act;

    // 通过构造方法传入账户对象
    public AccountThread(Account act) {
        this.act = act;
    }

    @Override
    public void run() {
        // 取款
        act.withdraw(5000);
        System.out.println(Thread.currentThread().getName() + "对账户" + act.getActno() + "取款成功，余额：" + act.getBalance());
    }
}
```
* synchronized 也可以出现在实例方法上，一定锁的是 this ，不能是其他对象，所以不灵活。
* 另一个缺点：synchronized 出现在实例方法上，表示整个方法体都需要同步，可能会无故扩大同步范围，导致程序执行效率降低，所以这种方式不常用。
* 优点：代码更少，更简洁。如果共享的对象就是 this ，并且同步的代码块就是整个方法体，建议使用这种方式。
```java
    public synchronized void withdraw(double money) {
            // 取款之前余额
            double before = this.getBalance();
            // 取款之后余额
            double after = before - money;
            // 模拟网络延迟
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            // 更新余额
            this.setBalance(after);
    }
```
* synchronized 还可以使用在静态方法上，表示找类锁，类锁永远只有一把。即使创建100个对象，类锁也只有一把。
* synchronized 会让程序的执行效率降低，用户体验不好，系统的用户吞吐量降低。解决办法：
    1. 尽量使用局部变量代替实例变量和静态变量。
    2. 如果必须是实例变量，可以考虑创建多个对象，这样实例变量的内存就不共享了。（每个线程对应一个对象，没有数据安全问题）
---
#### <font class="text-color-7" color="#03a9f4">死锁</font>
* synchronized 的嵌套使用，可能会导致死锁发生。
```java
        Object o1 = new Object();
        Object o2 = new Object();

        MyThread1 myThread1 = new MyThread1(o1,o2);
        MyThread2 myThread2 = new MyThread2(o1,o2);

        myThread1.start();
        myThread2.start();
```
```java
class MyThread1 extends Thread{
    Object o1;
    Object o2;

    public MyThread1(Object o1, Object o2) {
        this.o1 = o1;
        this.o2 = o2;
    }

    @Override
    public void run() {
        synchronized (o1){
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o2){
            }
        }
    }
}
```
```java
class MyThread2 extends Thread{
    Object o1;
    Object o2;

    public MyThread2(Object o1, Object o2) {
        this.o1 = o1;
        this.o2 = o2;
    }

    @Override
    public void run() {
        synchronized (o2){
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o1){
            }
        }
    }
}
```
---
### <font class="text-color-15" color="#ff9800">守护线程</font>
* java 中线程分为用户线程和守护线程。一般守护线程（后台线程）是一个死循环，所有的用户线程只要结束，守护线程自动结束。其中具有代表性的是垃圾回收线程。
```java
    public static void main(String[] args) {
        MyDaemon myDaemon = new MyDaemon();
        // 将线程设置为守护线程
        myDaemon.setDaemon(true);
        myDaemon.start();

        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + "--->" + i );
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

}
```
```java
class MyDaemon extends Thread{
    @Override
    public void run() {
        int i = 0;
        while (true) {  // 死循环，用户线程结束，守护线程自动终止
            System.out.println(Thread.currentThread().getName() + "--->" + (++i));
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```
---
#### <font class="text-color-7" color="#03a9f4">定时器</font>
* java.util.Timer 类
* [](https://)https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/Timer.html
* <font class="text-color-11" color="#8bc34a">Timer</font>(String name, boolean isDaemon) ：创建一个新的计时器，其关联的线程具有指定的名称，并且可以指定为 作为守护进程运行。
* void <font class="text-color-11" color="#8bc34a">schedule</font>(TimerTask task, Date time) ：安排指定的任务在指定的时间执行。
* void <font class="text-color-11" color="#8bc34a">schedule</font>(TimerTask task, long delay, long period) 安排指定任务重复固定延迟执行，在指定延迟后开始。
* void <font class="text-color-11" color="#8bc34a">schedule</font>(TimerTask task, long delay) 安排指定的任务在指定的延迟后执行。
* 需要实现 TimerTask 类。
```java
        // 创建定时器对象
        Timer timer = new Timer();
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH-mm");
        Date firstTime = sdf.parse("2023-2-2 03-59");
        // 指定定时任务（任务，第一次执行时间，间隔）
        timer.schedule(new LoggerTimeTask(),firstTime,1000 * 10);
```
```java
class LoggerTimeTask extends TimerTask{

    @Override
    public void run() {
        System.out.println("正在执行");
    }
}
```
--- 
### <font class="text-color-15" color="#ff9800">Wait 和 Notify</font>
* Object 类中的方法
* final void <font class="text-color-11" color="#8bc34a">wait</font>() ：让正在此对象的监视器上的线程进入等待状态，并且释放占有的该对象的锁。
* final void <font class="text-color-11" color="#8bc34a">notify</font>() ：唤醒在此对象的监视器上等待的单个线程。
* final void <font class="text-color-11" color="#8bc34a">notifyAll</font>() ：唤醒在此对象的监视器上等待的所有线程。
#### <font class="text-color-7" color="#03a9f4">生产者和消费者模式</font>
* 生产线程负责生产，消费线程负责消费，要达到均衡。
* Wait 和 Notify 方法建立在线程同步的基础之上。因为多线程需要同时操作一个仓库。有线程安全问题。
```java
    public static void main(String[] args) {

        // 创建一个共享仓库对象
        List list = new ArrayList();
        // 创建生产和消费线程
        Thread t1 = new Thread(new Producer(list));
        Thread t2 = new Thread(new Consumer(list));

        t1.setName("生产者线程");
        t2.setName("消费者线程");

        t1.start();
        t2.start();

    }
```
```java
// 生产线程
class Producer implements Runnable{
    private List list;

    public Producer(List list) {
        this.list = list;
    }

    @Override
    public void run() {
        while(true){
            synchronized (list){ // 给 list 加锁
                if(list.size() > 0){ // 大于0,说明仓库中已经有一个元素了。
                    // 当前线程进入等待状态，并且释放 list 的锁。
                    try {
                        list.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                // 程序能执行到这里，说明仓库是空的，可以生产
                Object obj = new Object();
                list.add(obj);
                System.out.println(Thread.currentThread().getName() + " ---> " + obj);
                // 唤醒消费者进行消费
                list.notify();
            }
        }
    }
}
```
```java
// 消费线程
class Consumer implements Runnable{
    private List list;

    public Consumer(List list) {
        this.list = list;
    }

    @Override
    public void run() {
        while (true){
            synchronized (list){  // 给 list 加锁
                if(list.size() == 0){  // 等于0,说明仓库中没有元素了。
                    try {
                        list.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                // 程序能执行到这里，说明仓库是空的，可以生产
                Object obj = list.remove(0);
                System.out.println(Thread.currentThread().getName() + " ---> " + obj);
                // 唤醒生产者生产
                list.notify();
            }
        }
    }
}
```
---
## <font class="text-color-13" color="#ffeb3b">反射</font>
* 作用：通过 java 的反射机制可以操作字节码文件。
* 相关类：java.lang.<font class="text-color-11" color="#8bc34a">Class</font> ：整个字节码文件
    java.lang.reflect.<font class="text-color-11" color="#8bc34a">Method</font> ：字节码中的方法字节码
    java.lang.reflect.<font class="text-color-11" color="#8bc34a">Constructor</font> ：字节码中的构造方法字节码
    java.lang.reflect.<font class="text-color-11" color="#8bc34a">Field</font> ：字节码中的属性字节码
* 反射机制让代码更具通用性，可变化的内容都写进配置文件中，将来修改配置文件之后，创建的对象不一样了，调用的方法也不同了，但是java代码不需要做任何改动。
---
###  <font class="text-color-15" color="#ff9800">获取Class 三种方式</font>
* static Class\<?> <font class="text-color-11" color="#8bc34a">forName</font>(String className) 返回Class与具有给定字符串名称的类或接口关联的对象。会导致类加载，静态代码块会执行。
* 如果只希望一个类的静态代码块执行，其他代码一律不执行，可以使用：Class.forName("完整类名")
```java
        // 第一种方式
        Class c1 = null;
        try {
            c1 = Class.forName("java.lang.String"); // c1代表String.class文件，或者代表String类型
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }

        // 第二种方式
        String s = "abc";
        Class c2 = s.getClass(); // c2代表String.class文件，或者代表String类型

        // 第二种方式
            // java 中任何一种类型，包括基本数据类型，都有.class属性
        Class c3 = String.class;
```
---
###  <font class="text-color-15" color="#ff9800">实例化对象</font>
* T <font class="text-color-11" color="#8bc34a">newInstance</font>() ：已弃用。 调用这个类的无参构造方法，完成对象的创建。必须保证无参构造存在。
* 通过反射机制，读取 properties 属性配置文件实例化不同的对象。（符合OCP原则）
```java
        // 通过IO流读取 classinfo.properties 文件
        FileReader reader = new FileReader("classinfo.properties");
        // 创建 Properties 对象
        Properties pro = new Properties();
        pro.load(reader);
        reader.close();

        String className = pro.getProperty("className");
        Class c = Class.forName(className);
        Object obj = c.newInstance();
        System.out.println(obj);
```
---
###  <font class="text-color-15" color="#ff9800">获取类路径下文件的绝对路径</font>
* 这个方式可以获取到在src下文件的绝对路径
* Thread.currentThread() ：当前线程对象
* getContextClassLoader() ：可以获取到当前线程的类加载器对象
* getResource() ：获取资源，当前线程的类加载器默认从类的根路径下加载资源。括号里面路径从src开始写。(类文件要加 .class)
```java
String path = Thread.currentThread().getContextClassLoader().getResource("bean/User.class").getPath();
```
* 可以以流的形式返回
```java
        InputStream reader = Thread.currentThread().getContextClassLoader().getResourceAsStream("bean/classinfo.properties");

        Properties properties = new Properties();

        properties.load(reader);
        String className = properties.getProperty("className");
        System.out.println(className);
```
#### <font class="text-color-7" color="#03a9f4">资源绑定器</font>
* java.util包下提供了一个资源绑定器，只能绑定xxx.properties文件，便于获取属性配置文件中的内容。
* static final ResourceBundle <font class="text-color-11" color="#8bc34a">getBundle</font>(String baseName)  ：使用指定的基本名称、默认语言环境和调用方模块获取资源包。
* 使用以下方式时，属性配置文件必须放到类路径下，路径后面的扩展名不能写。
```java
        ResourceBundle bundle = ResourceBundle.getBundle("bean/classinfo");
        String className = bundle.getString("className");
        System.out.println(className);
```
---
###  <font class="text-color-15" color="#ff9800">获取 field</font>
<font class="text-color-7" color="#03a9f4">Class</font> 对象相关方法：
* Field[] <font class="text-color-11" color="#8bc34a">getFields</font>()  ：返回一个Field数组，其中包含反映此Class对象所表示的类或接口的所有可访问公共字段。
* Field[] <font class="text-color-11" color="#8bc34a">getDeclaredFields</font>()  :返回一个Field数组反映此Class对象表示的类或接口声明的所有字段。
* String <font class="text-color-11" color="#8bc34a">getName</font>()  ：返回此Class对象表示的实体（类、接口、数组类、原始类型或 void）的名称。
* String <font class="text-color-11" color="#8bc34a">getSimpleName</font>() ：返回源代码中给定的基础类的简单名称。
* int <font class="text-color-11" color="#8bc34a">getModifiers</font>()  ：返回此类或接口的 Java 语言修饰符，以整数编码。

<font class="text-color-7" color="#03a9f4">Field</font> 对象相关方法：
* String <font class="text-color-11" color="#8bc34a">getName</font>()  ：返回此Field对象表示的字段的名称。
* int <font class="text-color-11" color="#8bc34a">getModifiers</font>()  ：Field以整数形式返回此对象表示的字段的 Java 语言修饰符。

<font class="text-color-7" color="#03a9f4">Modifier</font> 类：
* static String <font class="text-color-11" color="#8bc34a">toString</font>(int mod)  ：静态方法，返回描述指定修饰符中的访问修饰符标志的字符串。
```java
    public static void main(String[] args) throws IOException, ClassNotFoundException {

        // 获取类
        Class studentClass = Class.forName("Test_1.Student");

        // 获取类中的公共 field
        Field[] fields = studentClass.getFields();
        System.out.println(fields.length); // 2
        Field f = fields[0];
        System.out.println(f.getName());  // num

        // 获取类中所有的 field
        Field[] fs = studentClass.getDeclaredFields();
        System.out.println(fs.length);  // 5

        for(Field field : fs){
            // 修饰符
            int modifier = field.getModifiers();
            String modifierName = Modifier.toString(modifier);
            // 类型
            String fieldType = field.getType().getSimpleName();
            // 名字
            String fieldName = field.getName();

            System.out.println(modifierName + " " + fieldType + " " + fieldName);
        }

//        public int num
//        private String name
//        protected int age
//        boolean sex
//        public static final double PI

    }
```
```java
public class Student {
    // 4个field，采用不同访问权限控制符
    public int num;
    private String name;
    protected int age;
    boolean sex;
    public static final double PI = 3.1415926;
}
```
#### <font class="text-color-7" color="#03a9f4">反编译 field</font>
```java
    public static String decompile_field(String referencePath) throws ClassNotFoundException {
        StringBuilder builder = new StringBuilder();

        Class theClass = Class.forName(referencePath);

        builder.append(Modifier.toString(theClass.getModifiers()) + " "
                + theClass.getSimpleName() + " {\n");

        Field[] fields = theClass.getDeclaredFields();

        for (Field field : fields) {
            builder.append("\t");
            builder.append(Modifier.toString(field.getModifiers()));
            builder.append(" ");
            builder.append(field.getType().getSimpleName());
            builder.append(" ");
            builder.append(field.getName());
            builder.append(";\n");
        }

        builder.append("}");
        return builder.toString();
    }
```
---
### <font class="text-color-15" color="#ff9800">访问对象属性</font>
Field 方法：
* void <font class="text-color-11" color="#8bc34a">set</font>(Object obj, Object value) ： Field将指定对象参数上此对象表示的字段设置为指定的新值。
* Object <font class="text-color-11" color="#8bc34a">get</font>(Object obj)  ：Field返回指定对象上this 表示的字段的值。
* void <font class="text-color-11" color="#8bc34a">setAccessible</font>(boolean flag)  ：将此反射对象的标志设置accessible为指示的布尔值。
```java
        Class myClass = Class.forName("Test_1.Student");
        Object o = myClass.newInstance();

        Field numField = myClass.getDeclaredField("num");

        numField.set(o,123);
        System.out.println(numField.get(o));
```
---
### <font class="text-color-15" color="#ff9800">可变长度参数</font>
* 要求参数个数：0 - N 个
* 可变长度参数在参数列表中必须在最后一个位置上
* 可变长度参数可以当做一个数组来看待
```java
        method(1,2,3,4);

        int[] array = {6,4,7,8,43,3};
        method(array);
```
```java
    public static void method(int... args){
        for (int i = 0; i < args.length; i++){
            System.out.println(args[i]);
        }
    }
```
---
### <font class="text-color-15" color="#ff9800">反编译方法</font>
Method 方法：
* String <font class="text-color-11" color="#8bc34a">getName</font>()  ：返回此Method 对象表示的方法的名称，作为String.
* Class\<?>[] <font class="text-color-11" color="#8bc34a">getParameterTypes</font>()  ：返回一个对象数组，Class这些对象按声明顺序表示此对象表示的可执行文件的形式参数类型。
* int <font class="text-color-11" color="#8bc34a">getModifiers</font>()  ：返回此对象表示的可执行文件的 Java 语言修饰符。
```java
    public static String decompile_method(String referencePath) throws ClassNotFoundException {
        StringBuilder builder = new StringBuilder();

        Class theClass = Class.forName(referencePath);

        builder.append(Modifier.toString(theClass.getModifiers()) + " "
                + theClass.getSimpleName() + " {\n");

        Method[] methods = theClass.getMethods();

        for (Method method : methods) {
            builder.append("\t");
            builder.append(Modifier.toString(method.getModifiers()));
            builder.append(" ");
            builder.append(method.getReturnType().getSimpleName());
            builder.append(" ");
            builder.append(method.getName());
            builder.append(" (");
            Class[] parameterTypes = method.getParameterTypes();
            for(Class parameterType : parameterTypes) {
                builder.append(parameterType.getSimpleName());
                builder.append(",");
            }
            if(parameterTypes.length != 0) builder.deleteCharAt(builder.length() - 1);
            builder.append(") \n");
        }

        builder.append("}");
        return builder.toString();
    }
```
#### <font class="text-color-7" color="#03a9f4">反射机制调用方法</font>
Class 方法
* Method <font class="text-color-11" color="#8bc34a">getMethod</font>(String name, Class\<?>... parameterTypes)  ：返回一个Method对象，该对象反映了该Class对象所表示的类或接口的指定公共成员方法。
* Method <font class="text-color-11" color="#8bc34a">getDeclaredMethod</font>(String name, Class\<?>... parameterTypes) 返回一个Method对象，该对象反映了该 Class对象表示的类或接口的指定声明方法。

Method 方法
* Object <font class="text-color-11" color="#8bc34a">invoke</font>(Object obj, Object... args)  ：Method 在具有指定参数的指定对象上调用此对象表示的基础方法。
```java
    public static void main(String[] args) throws Exception {

        Class theClass = Class.forName("Test_1.Student");

        Object student = theClass.newInstance();

        Method m1 = theClass.getDeclaredMethod("doHomeworks",String.class);
        Method m2 = theClass.getDeclaredMethod("doHomeworks",int.class, String.class);
        Method m3 = theClass.getDeclaredMethod("snap");


        Object returned1 = m1.invoke(student,"Bob");
        Object returned2 = m2.invoke(student,100,"Jerry");
        m3.setAccessible(true);
        m3.invoke(student);

        System.out.println(returned1);
        System.out.println(returned2);
    }
```
```java
public class Student {

    public boolean doHomeworks(String name){
        System.out.println(name + "写作业");
        return true;
    }

    public int doHomeworks(int score, String name){
        System.out.println(name + "作业分数：" + score);
        return 1;
    }

    private void snap(){
        System.out.println("睡觉");
    }
}
```
---
### <font class="text-color-15" color="#ff9800">setAccessible()方法</font>
* 屏蔽 java 运行时访问检查。
* https://blog.csdn.net/gao_zhennan/article/details/123828322
---

### <font class="text-color-15" color="#ff9800">反编译构造器</font>
```java
    public static String decompile_Constructor(String referencePath) throws ClassNotFoundException {
        StringBuilder builder = new StringBuilder();

        Class theClass = Class.forName(referencePath);

        builder.append(Modifier.toString(theClass.getModifiers()) + " "
                + theClass.getSimpleName() + " {\n");

        Constructor[] constructors = theClass.getConstructors();

        for (Constructor constructor : constructors) {
            builder.append("\t");
            builder.append(Modifier.toString(constructor.getModifiers()));
            builder.append(" ");
            builder.append(theClass.getSimpleName());
            builder.append(" (");
            Class[] parameterTypes = constructor.getParameterTypes();
            for(Class parameterType : parameterTypes) {
                builder.append(parameterType.getSimpleName());
                builder.append(",");
            }
            if(parameterTypes.length != 0) builder.deleteCharAt(builder.length() - 1);
            builder.append(") \n");
        }

        builder.append("}");
        return builder.toString();
    }
```
#### <font class="text-color-7" color="#03a9f4">反射机制调用构造器</font>
Class 方法
* Constructor\<T> <font class="text-color-11" color="#8bc34a">getConstructor</font>(Class\<?>... parameterTypes)  ：返回一个Constructor对象，该对象反映此Class 对象表示的类的指定公共构造函数。
* Constructor\<T> <font class="text-color-11" color="#8bc34a">getDeclaredConstructor</font>(Class\<?>... parameterTypes) 返回一个Constructor对象，该对象反映此 Class对象表示的类的指定构造函数。
```java
        Class theClass = Class.forName("Test_1.Student");

        Object student = theClass.newInstance();

        Constructor c1 = theClass.getDeclaredConstructor(String.class);
        Constructor c2 = theClass.getDeclaredConstructor(int.class,boolean.class);

        Object o1 =  c1.newInstance("Bob");
        Object o2 =  c2.newInstance(15,true);

        System.out.println(o1);  // Student{num=0, name='Bob', age=0, sex=false}
        System.out.println(o2);  // Student{num=0, name='null', age=15, sex=true}
```
```java
public class Student {
    // 4个field，采用不同访问权限控制符
    public int num;
    private String name;
    protected int age;
    boolean sex;
    private static final double PI = 3.1415926;

    public Student(){}
    public Student(String name) {
        this.name = name;
    }

    public Student(int age, boolean sex) {
        this.age = age;
        this.sex = sex;
    }

    @Override
    public String toString() {
        return "Student{" +
                "num=" + num +
                ", name='" + name + '\'' +
                ", age=" + age +
                ", sex=" + sex +
                '}';
    }
}
```
### <font class="text-color-15" color="#ff9800">反射获取父类和接口</font>
* Class\<? super T> <font class="text-color-11" color="#8bc34a">getSuperclass</font>()  ：返回Class表示由 this 表示的实体（类、接口、原始类型或 void）的直接超类Class。
* Class\<?>[] <font class="text-color-11" color="#8bc34a">getInterfaces</font>()   ：Class返回由该对象表示的类或接口直接实现的接口。
```java
    public static String decompile_super_interfaces(String referencePath) throws ClassNotFoundException {
        StringBuilder builder = new StringBuilder();
        Class theClass = Class.forName(referencePath);

        builder.append("Super class ---> ");
        Class superClass = theClass.getSuperclass();
        builder.append(superClass.getSimpleName());
        builder.append("\nInterfaces ---> ");
        Class[] interfaces = theClass.getInterfaces();
        for(Class inter : interfaces) {
            builder.append(inter.getSimpleName());
            builder.append(" ");
        }

        return builder.toString();
    }
```




