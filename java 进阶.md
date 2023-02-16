# *java 进阶*

## <font class="text-color-13" color="#ffeb3b">Collections</font> 工具类
* 常用方法
1. List\<T\> <font class="text-color-11" color="#8bc34a">synchronizedList</font>(List\<T\> list) 返回由指定列表支持的同步（线程安全）列表。
2. void <font class="text-color-11" color="#8bc34a">sort</font>(List\<T> list) 根据其元素的自然顺序，将指定的列表按升序 排序。
3.  void <font class="text-color-11" color="#8bc34a">sort</font>(List\<T\> list, Comparator\<? super T> c) 根据指定比较器产生的顺序对指定列表进行排序。
4.  void <font class="text-color-11" color="#8bc34a">copy</font>(List\<? super T> dest, List\<? extends T> src) 将一个列表中的所有元素复制到另一个列表中。
5.  boolean <font class="text-color-11" color="#8bc34a">disjoint</font>(Collection\<?> c1, Collection\<?> c2) 如果两个指定的集合没有共同的元素，则返回true。
6.  void <font class="text-color-11" color="#8bc34a">fill</font>(List\<? super T> list, T obj) 用指定元素替换指定列表的所有元素。
7.  int <font class="text-color-11" color="#8bc34a">frequency</font>(Collection\<?> c, Object o) 返回指定集合中等于指定对象的元素数。
8.  List\<T> <font class="text-color-11" color="#8bc34a">unmodifiableList</font>(List\<? extends T> list) 返回指定列表的不可修改视图。进行 add 和 remove 等操作编译会报错。
9.  public static void <font class="text-color-11" color="#8bc34a">shuffle</font>(List\<?> list) ：用于随机打乱集合内的元素。这个方法可以用于打乱数组、列表等任何实现了 List 接口的集合。

## <font class="text-color-13" color="#ffeb3b">深拷贝</font>
* 两种方式：
    1. 拷贝构造器
    2. 提供一个getCopy方法
```java
public class AptBuilding {

    private String name;
    private List<AptUnit> aptUnitList = new ArrayList<>();


     //return a deep copy list of aptUnitList
    public List<AptUnit> getAptUnitListCopy(){
        List<AptUnit> res = new ArrayList<>();
        for(AptUnit unit : aptUnitList){
            res.add(new AptUnit(unit));
        }
        return res;
    }
}
```
```java
public class AptUnit {

    enum Size{STUDIO,ONEBEDROOM,TWOBEDROOMS,THREEBEDROOMS}

    private final int unitNumber;
    private int price;
    private boolean occupied;
    private final Size size;

// 构造器
    public AptUnit(int unitNumber, int price, boolean occupied, Size size) {
        this.unitNumber = unitNumber;
        this.price = price;
        this.occupied = occupied;
        this.size = size;
    }

//的一种方式： 拷贝构造器
    public AptUnit(AptUnit aptUnit){
        this.unitNumber = aptUnit.getUnitNumber();
        this.price = aptUnit.getPrice();
        this.occupied = aptUnit.isOccupied();
        this.size = aptUnit.getSize();
    }
    
//第二种方式： 提供一个拷贝方法
    public AptUnit getCopy(AptUnit aptUnit){
        return new AptUnit(aptUnit.getUnitNumber(), aptUnit.getPrice(), aptUnit.isOccupied(),aptUnit.getSize());
    }


    public int getUnitNumber() {
        return unitNumber;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }

    public boolean isOccupied() {
        return occupied;
    }

    public void setOccupied(boolean occupied) {
        this.occupied = occupied;
    }

    public Size getSize() {
        return size;
    }
}

```



## <font class="text-color-13" color="#ffeb3b">Optional 类</font>
* Optional类(java.util.Optional)是一个容器类，代表一个值存在或不存在，原来用null表示一个值不存在，现在Optional可以更好的表达这个概念。并且可以避免空指针异常。
* 常用方法：
1. Optional.<font class="text-color-11" color="#8bc34a">of</font>(T t)：创建一个Optional实例
2. Optional.<font class="text-color-11" color="#8bc34a">empty</font>()：创建一个空的Optional实例
3. Optional.<font class="text-color-11" color="#8bc34a">ofNullable</font>(T t)：若t不为null,创建Optional实列，否则创建空实例
4. <font class="text-color-11" color="#8bc34a">isPresent</font>()：如果值存在，返回 true，否则返回 false
5. <font class="text-color-11" color="#8bc34a">orElse</font>(T t)：如果值存在，返回值，否则返回 t
6. <font class="text-color-11" color="#8bc34a">orElseGet</font>(Supplier s)：如果调用对象包含值，返回该值，否则返回s获取的值
7. <font class="text-color-11" color="#8bc34a">ifPresent</font>(Consumer action) ：如果存在值，则使用该值执行给定的操作，否则不执行任何操作。
8. T <font class="text-color-11" color="#8bc34a">get</font>() ：如果Optional有值，则返回值，否则抛出NoSuchElementException。
* 示例
```java
        Person p1 = new Person(1125,University.MCGILL);
        Person p2 = new Person(3389,Job.DRIVER);

        p1.setHouse(new House());

// 使用者获取前需先判断是否 empty
        // 第一种获取方法
        if(p1.getHouse().isPresent()){
            House h1 = p1.getHouse().get();
            System.out.println(h1);
        }

        // 第二种获取方法
        House h2 = p1.getHouse().orElse(null);
        if (h2 != null) {
            System.out.println(h2);
        }

        // 第三种获取方法 （lamda 表达式）
        p1.getHouse().ifPresent(System.out::println);
```
```java
public class Person {

     private int id;
     private Optional<Job> job;
     private Optional<University> university;
     private boolean isStudent;
     private Optional<House> house;

    public Person(int id, University university) {  // 学生对象构造器
        this.id = id;
        this.isStudent = true;
        this.university = Optional.of(university);
        this.job = Optional.empty();
        this.house = Optional.empty();
    }

    public Person(int id, Job job){    // 工作者对象构造器
        this.id = id;
        this.isStudent = false;
        this.university = Optional.empty();
        this.job = Optional.of(job);
        this.house = Optional.empty();
    }

    public void setHouse(House house){
        this.house = Optional.of(house);
    }

    public Optional<House> getHouse() {
        return house;
    }
}



enum Job{COOK, DRIVER, HUNTER, POLICE}
enum University{MCGILL, UBC, UOFT}

class House{

}
```
## <font class="text-color-13" color="#ffeb3b">注解</font>
* 注解是一种引用数据类型，编译之后也生成class文件
* 注解给编译器参考，和运行阶段没有关系。
* 注解使用时的语法格式：@注解类型名
* 注解可以出现在类上，属性上，方法上，变量上等任意位置。（可以在注解类型上）
* <font class="text-color-15" color="#ff9800">内置注解</font>：
    1. <font class="text-color-11" color="#8bc34a">@Override</font>  ：表示一个方法声明打算重写父类中的另一个方法。标志性注解，方法若带有这个注解，编译器会进行编译检查，如果没有重写父类方法，编译器报错。
    2. <font class="text-color-11" color="#8bc34a">@Deprecated</font> ：用次注释注释的元素，不鼓励程序员使用。
    3. <font class="text-color-11" color="#8bc34a">@Documented</font> ：指定该注解是否会在javadoc体现
    4. <font class="text-color-11" color="#8bc34a">@Inherited</font> ：子类会继承父类注解
* <font class="text-color-15" color="#ff9800">元注解</font>：用来标注“注解类型”的注解，常见的元注解：
    1. <font class="text-color-11" color="#8bc34a">@Target</font> ：用来标注“被标注的注解”最终修饰在哪里，
    @Target(ElementType.METHOD)表示该注解只能出现在方法上。
    2. <font class="text-color-11" color="#8bc34a">@Retention</font> ：保持性策略，用来标注“被标注的注解”最终保存在哪里，
    @Retention(RetentionPolicy.SOURCE) ：编译器使用后，直接丢弃这种策略的注释
    @Retention(RetentionPolicy.CLASS) ：编译器将把注解记录在 class 文件中。当运行 java 程序时，JVM不会保留注释。这是默认值。
    @Retention(RetentionPolicy.RUNTIME) ：编译器将把注解记录在 class 文件中。当运行 java 程序时，JVM会保留注释。可以通过反射机制获取该注释。
* 注解可以有属性，可以设定默认值。如果一个注解的属性名字是value，并且只有这一个属性，在使用的时候该属性名可以省略。
    属性类型：byte short int long float double boolean char String Class Enum 以及它们的数组形式（数组只有一个元素大括号可以省略）
```java
@MyAnnotation(n = "Some")
    public static void doSome(){
        System.out.println("do");
    }
```
```java
public @interface MyAnnotation {
    String name() default "";
}
```
### <font class="text-color-15" color="#ff9800">反射注解</font>
Class 方法
* \<A extends Annotation> A <font class="text-color-11" color="#8bc34a">getAnnotation</font>(Class\<A> annotationClass)  ：如果存在这样的注释，则返回此元素对指定类型的注释，否则返回 null。
* boolean \<font class="text-color-11" color="#8bc34a">isAnnotationPresent\</font>(Class\<? extends Annotation> annotationClass)  ：如果此元素上存在指定类型的注释，则返回 true ，否则返回 false。
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
@MyAnnotation(n = "一个学生类")
public class Student {
}
```
```java
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
    String name() default "";
}
```
* 注解在程序当中可作为一种标记，可以使用反射机制获取注解后进行不同的操作。

## <font class="text-color-13" color="#ffeb3b">单例模式</font>
* 单例模式是一种常用的设计模式，它保证一个类只有一个实例，并且提供全局访问点。在Java应用程序中，单例模式用于保证系统中只有一个实例的类。
* 步骤：
    1. 构造器私有化 -> 防止直接new对象
    2. 类的内部创建对象
    3. 向外暴露一个静态的公共方法。getinstance
### <font class="text-color-15" color="#ff9800">饿汉式</font>
```java
public class Singleton01 {
    // 构造器私有化
    private Singleton01(){};
    // 先创建好这个 Singleton 的对象实例
    private static Singleton01 INSTANCE = new Singleton01();
    // 提供一个 public 的静态方法，可以返回instance
    public static Singleton01 getInstance(){
        return INSTANCE;
    }
}
```
### <font class="text-color-15" color="#ff9800">懒汉式</font>
```java
public class Singleton02 {
    // 构造器私有化
    private Singleton02(){};
    // 静态 Singleton02 属性
    private static Singleton02 INSTANCE;
    // 提供一个 public 的静态方法，可以返回instance
    public static Singleton02 getInstance(){
        if(INSTANCE == null){
            INSTANCE = new Singleton02();
        }
        return INSTANCE;
    }
}
```

## <font class="text-color-13" color="#ffeb3b">享元模式</font>
* 享元模式是一种编程模式，它通过共享对象来有效地支持大量细粒度对象。它将对象分成内部状态和外部状态两个部分。内部状态是可以共享的，而外部状态是不可以共享的。
### <font class="text-color-15" color="#ff9800">实际Factory类</font>
```java
interface Shape {
   void draw();
}
```
```java
class Circle implements Shape {
   private String color;
   private int x;
   private int y;
   private int radius;

   public Circle(String color){
      this.color = color;		
   }

   public void setX(int x) {
      this.x = x;
   }

   public void setY(int y) {
      this.y = y;
   }

   public void setRadius(int radius) {
      this.radius = radius;
   }

   @Override
   public void draw() {
      System.out.println("Circle: Draw() [Color : " + color + ", x : " + x + ", y :" + y + ", radius :" + radius);
   }
}
```
```java
class ShapeFactory {
   private static final HashMap<String, Shape> circleMap = new HashMap<>();

   public static Shape getCircle(String color) {
      Circle circle = (Circle)circleMap.get(color);

      if(circle == null) {
         circle = new Circle(color);
         circleMap.put(color, circle);
         System.out.println("Creating circle of color : " + color);
      }
      return circle;
   }
}
```
* 这个代码中，我们通过定义一个ShapeFactory类来管理所有的圆形（Circle类）对象，并使用一个HashMap维护对象的池。如果请求一个颜色的圆形，而这个颜色的圆形对象不存在，那么我们会创建一个新的圆形对象，并将它加入
### <font class="text-color-15" color="#ff9800">静态代码块</font>
```java
        ATM a = new ATM();

        Banknote b1 = a.getBankNotes(5);
        Banknote b2 = a.getBankNotes(5);
        Banknote b3 = a.getBankNotes(23);
        Banknote b4 = a.getBankNotes(23);

        System.out.println(b1 == b2);  // true
        System.out.println(b3 == b4);  // false
```
```java
public class ATM {

    private static final HashMap<Integer, Banknote> bankNotes;

    static {  // 静态代码块初始化常用面额的钞票
        final int[] values = {5,10,20,50,100};
        bankNotes = new HashMap<Integer, Banknote>(5);
        for(int value : values){
            bankNotes.put(value,new Banknote(value));
        }
    }

    public Banknote getBankNotes(int value){
        if(!bankNotes.containsKey(value)) return new Banknote(value);
        return bankNotes.get(value);
    }

}
```
```java
public class Banknote {
    private final int value; // 面额

    public Banknote(int value) {
        this.value = value;
    }
}
```
## <font class="text-color-13" color="#ffeb3b">空对象模式</font>
* 空对象模式是一种设计模式，主要目的是为了在不需要处理NULL的情况下，提供一个空对象，代替NULL。该模式通过把NULL对象看作一种特殊的对象，这样就可以替代NULL并保证程序继续运行。在Java中，可以通过在类中定义一个空对象来实现该模式，从而避免在访问NULL对象时出现空指针异常。
* <font class="text-color-15" color="#ff9800">静态内部类</font>实现如下：
```java
    public static void main(String[] args) {
        AbstractShape shape = AbstractShape.NULL;
        System.out.println(shape.area());  // 0.0

        shape = new Circle(5.0);
        System.out.println(shape.area());  // 78.53981633974483
    }
```
```java
public abstract class AbstractShape {
    public abstract double area();

    public static final AbstractShape NULL = new NullShape();

    private static class NullShape extends AbstractShape {  // 静态内部类来代表空对象
        @Override
        public double area() {
            return 0.0;
        }
    }
}
```
```java
public class Circle extends AbstractShape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}
```


## <font class="text-color-13" color="#ffeb3b">JUnit 单元测试</font>
* 一个开源的java语言的单元测试框架
* TestCase：一个TestCase表示一个测试
* TestSuite：一个TestSuite包含一组TestCase，表示一组测试
* TestFixture：一个TestFixture表示一个测试环境
* TestResult：用于收集测试结果
* TestRunner：用于运行测试
* TestListener：用于监听测试过程，收集测试数据
* Assert：用于断言测试结果是否正确
```java
public class Operation {
    public int add(int a, int b){
        return a + b;
    }

    public int sub(int a, int b){
        return a - b;
    }

    public int mult(int a, int b){
        return a * b;
    }

    public int div(int a, int b){
        return a / b;
    }
}
```
```java
class OperationTest extends Operation {

    @BeforeEach
    void setUp() {
    }

    @AfterEach
    void tearDown() {
    }

    @Test
    void testAdd() {
        assertEquals(3,new Operation().add(1,2));
    }

    @Test
    void testSub() {
        assertEquals(21,new Operation().sub(24,3));
    }

    @Test
    void testMult() {
        assertEquals(18,new Operation().mult(3,6));
    }

    @Test
    void testDiv() {
        assertEquals(3,new Operation().div(9,3));
    }
}
```
* <font class="text-color-15" color="#ff9800">测试用方法</font>：(x为方法执行实际的结果)
    1. fail("msg")：直接失败
    2. assertEquals(期望值, x)：断言相等，判断实际执行结果是否等于期望值
    3. assertArrayEquals({1,2,3}, x) ：断言数组相等
    4. assertEquals(3.1416,x,0.0001) ：浮点数断言相等，要加误差值
    5. assertNull(x) ：断言为null
    6. assertTrue(x) ：断言为true
    7. assertFalse(x) ：断言为false
    8. assertNotEquals()
    9. assertNotNull()
* 在 @Before 方法中初始化测试资源
* 在 @After 方法中释放测试资源
* 单个 @Test 方法执行前会创建新的...Test实例，实例变量的状态不会传递给下一个 @Test 方法
* 单个 @Test 方法执行前后会执行 @Before和@After方法

## <font class="text-color-13" color="#ffeb3b">绘图</font>
* Graphics类：https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/java/awt/Graphics.html
### <font class="text-color-15" color="#ff9800">画圆案例</font>
* MyPanel 对象就是一个画板
* Graphics g 把 g 理解成一支画笔
* Graphics 提供了很多绘图方法
* JFrame对应窗口，可以理解成是一个画框
```java
public class DrawCircle extends JFrame {  // JFrame对应窗口，可以理解成是一个画框

    // 定义一个面板
    private MyPanel mp = null;

    public static void main(String[] args) {
        new DrawCircle();
    }

    public DrawCircle() { // 构造器
        // 初始化面板
        mp = new MyPanel();
        // 把面板放入到窗口（画框）
        this.add(mp);
        // 设置窗口大小
        this.setSize(600,400);
        // 当点击窗口小×，程序退出
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        // 可以显示
        this.setVisible(true);
    }

}
```
```java
public class MyPanel extends JPanel {

    @Override
    public void paint(Graphics g) { // 绘图方法
        super.paint(g);  // 调用父类的方法完成初始化
        // 画出一个圆形
        g.drawOval(50,50,100,100);
    }

}
```
* Graphics常用方法：
* abstract void <font class="text-color-11" color="#8bc34a">drawLine</font>(int x1, int y1, int x2, int y2) ：(x1, y1)在点之间和(x2, y2) 此图形上下文的坐标系中使用当前颜色绘制一条线 。
* void <font class="text-color-11" color="#8bc34a">drawRect</font>(int x, int y, int width, int height) ：绘制指定矩形的轮廓。
* abstract void <font class="text-color-11" color="#8bc34a">drawOval</font>(int x, int y, int width, int height) ：绘制椭圆的轮廓。
* abstract void <font class="text-color-11" color="#8bc34a">fillRect</font>(int x, int y, int width, int height) ：填充指定的矩形。
* abstract void <font class="text-color-11" color="#8bc34a">fillOval</font>(int x, int y, int width, int height) ：用当前颜色填充由指定矩形包围的椭圆。
* abstract boolean <font class="text-color-11" color="#8bc34a">drawImage</font>(Image img, int x, int y, ..) ：画图片
* abstract void <font class="text-color-11" color="#8bc34a">drawString</font>(String str, int x, int y) 使用此图形上下文的当前字体和颜色绘制指定字符串给定的文本。
* abstract void <font class="text-color-11" color="#8bc34a">setFont</font>(Font font) ：将此图形上下文的字体设置为指定的字体。
* abstract void <font class="text-color-11" color="#8bc34a">setColor</font>(Color c) ：将此图形上下文的当前颜色设置为指定颜色。
* 画图片
```java
        // 获取图片资源 路径为相对于根目录的位置
        Image image = Toolkit.getDefaultToolkit().getImage(MyPanel.class.getResource("/Image/cat.jpg"));
        g.drawImage(image,300,300,129,115,this);
```
* 画字符串
```java
        // 画字符串
        g.setColor(Color.BLUE);
        g.setFont(new Font("隶书",Font.CENTER_BASELINE,50));
        g.drawString("玖玖",300,500); // 坐标为字符串的左下角
```
### <font class="text-color-15" color="#ff9800">事件处理</font>
* 小球移动案例
```java
public class BallMove extends JFrame {

    MyPanel mp;

    public static void main(String[] args) {
        BallMove ballMove = new BallMove();
    }

    public BallMove() {
        mp = new MyPanel();
        this.add(mp);
        // 窗口JFrame，可以监听键盘事件
        this.addKeyListener(mp);
        this.setLocation(500,250);
        this.setSize(1000,750);
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setVisible(true);
    }
}
```
```java
// KeyListener 是监听器，可以监听键盘事件
class MyPanel extends JPanel implements KeyListener {

    int x = 120;
    int y = 150;

    @Override
    public void paint(Graphics g) {
        super.paint(g);
        g.fillOval(x,y,20,20);
    }

    @Override
    public void keyTyped(KeyEvent e) { // 有字符输出时，该方法会触发

    }

    @Override
    public void keyPressed(KeyEvent e) {  // 当某个键按下时，该方法会触发
        switch (e.getKeyCode()){
            case KeyEvent.VK_S :
                y += 5;
                break;
            case KeyEvent.VK_W:
                y -= 5;
                break;
            case KeyEvent.VK_A:
                x -= 5;
                break;
            case KeyEvent.VK_D:
                x += 5;
                break;
        }
        this.repaint();
    }

    @Override
    public void keyReleased(KeyEvent e) {  // 当某个键松开时，该方法触发

    }
}
```







