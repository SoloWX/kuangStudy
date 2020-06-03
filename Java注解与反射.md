### 1. 注解

#### 1.1 什么是注解

- Annotation是jdk1.5开始引入的新技术

- Annotation的作用：

    - 不是程序本身，可以对程序作出解释

    - **可以被其他程序（例如编译器）读取**

- Annotation的格式

    - “@注解名”，也可以带参数，例如：@SuppressWarnings(value="unchcked")

- Annotation在哪里使用？
    - 可以附加在package、class、method、field上，相当于给它们添加了额外的辅助信息，可以通过反射机制编程实现对这些元数据的访问。

#### 1.2 内置注解

- @Override - 检查该方法是否是重写方法。如果发现其父类，或者是引用的接口中并没有该方法时，会报编译错误。
- @Deprecated - 标记过时方法。如果使用该方法，会报编译警告。
- @SuppressWarnings - 指示编译器去忽略注解中声明的警告。

#### 1.3 元注解(meta-annotation)

- 元注解的作用就是负责注解其他注解，Java定义了4个标准的元注解

- ==@**Retention**== - 标识这个注解怎么保存，是只在代码中，还是编入class文件中，或者是在运行时可以通过反射访问。(RUNTIME > CLASS > SOURCE)
- @Documented - 标记这些注解是否包含在用户文档中。
- ==@**Target**== - 标记这个注解应该是哪种 Java 成员。可以用在那些地方
- @Inherited - 标记这个注解是继承于哪个注解类(默认 注解并没有继承于任何子类)
- 从 Java 7 开始，额外添加了 3 个注解:
    - @SafeVarargs - Java 7 开始支持，忽略任何使用参数为泛型变量的方法或构造函数调用产生的警告。
    - @FunctionalInterface - Java 8 开始支持，标识一个匿名函数或函数式接口。
    - @Repeatable - Java 8 开始支持，标识某注解可以在同一个声明上使用多次。

#### 1.4 自定义注解

- 使用@interface自定义注解
- 格式： public @interface 注解名{定义内容}

![image-20200510220357689](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200510220357689.png)

```java
package annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@SuppressWarnings("all")
public class AnnotationDemo1 {
    @Override
    public String toString() {
        return super.toString();
    }

    @MyAnnotation("zhouhui")
    public void test(){

    }
}
/**
 * @author 10483
 * 自定义注解：Target和Retention很重要，一般都要写
 */
@Target(value = {ElementType.METHOD,ElementType.FIELD})
@Retention(value = RetentionPolicy.RUNTIME)
@interface MyAnnotation{
    //注解的参数格式：参数类型 + 参数名 + ();
    String value();
    //可以用default设置默认值，这样使用注解时就可以不用写参数
    int id() default 0;
    String[] name() default {"swpu","uest"};
}
```

### 2. 反射机制(Reflection)

#### 2.1 概述

- 反射是Java被视为动态语言的关键，反射机制允许程序在执行期借助于Reflection API取得任何类的内部信息，并且能直接操作任意对象的内部属性及方法。

- 加载完类之后，在堆内存的方法区中就产生了一个Class类型的对象(一个类只有一个Class对象)，这个对象就包含了完整的类的结构信息。我们可以通过这个对象看到类的结构。这个对象就像一面镜子，透过这个镜子看到类的结构，所以称之为反射。

    ```java
    Class c = Class.forName("java.lang.String")
    ```

> 正常方式：引入需要的“包类”名称——>通过new实例化——>取得实例化对象
>
> **反射方式：**实例化对象——>getClass()方法——>得到完整的“包类”名称

**Java反射优点和缺点**

- 优点
    - 可以实现动态创建对象和编译，体现出很大的灵活性
- 缺点
    - 对性能有影响，使用反射基本上是一种解释操作，我们可以告诉JVM，我们希望做什么并且它满足我们的要求，这类操作总是慢于直接执行相同的操作

#### 2.2 获取反射对象

```java
package reflection;

import javafx.scene.effect.Reflection;

import java.lang.annotation.ElementType;
import java.lang.annotation.Target;

public class ReflectionDemo1 {
    public static void main(String[] args) throws ClassNotFoundException {
        //通过反射获取类的对象
        Class c1 = Class.forName("reflection.User");
        System.out.println(c1);	

        //一个类在内存中只有一个Class对象
        //一个类被加载后，类的整个结构都会被封装在Class对象中
        System.out.println(c1.getName());
        System.out.println(c1.getAnnotation(c1));
    }
}
//创建一个实体类
class User{
    private String name;
    private int age;
    private int id;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", id=" + id +
                '}';
    }
}

```

#### 2.3 获取Class类的几种方法

![image-20200517091228219](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200517091228219.png)

![image-20200517091256134](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200517091256134.png)

 ```java
package reflection;

/**
 * @author 10483
 * 获取Class类的几种方法
 */
public class ReflectionDemo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Person person = new Student();
        System.out.println("这是："+person.name);

        //方式一：通过对象获得getClass
        Class c1 = person.getClass();
        System.out.println(c1.hashCode());

        //方式二：通过forName方法获得
        Class c2 = Class.forName("reflection.Student");
        System.out.println(c2.hashCode());

        //方式三：通过类名.Class获得
        Class c3 = Student.class;
        System.out.println(c3.hashCode());

        //方式四：基本内置类的包装类中的TYPE属性
        Class c4  = Integer.TYPE;
        System.out.println(c4.hashCode());

        //获取父类类型
        System.out.println(c1.getSuperclass());
    }
}

class Person{
    public String name;

    public Person() {
    }

    public Person(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                '}';
    }
}

class Student extends Person{
    public Student() {
        this.name = "学生";
    }
}

class Teacher extends Person{
    public Teacher() {
        this.name = "老师";
    }
}
 ```

> 几乎所有类型都有Class类

#### 2.4 类加载内存分析

**类的加载与ClassLoader的理解**

- **加载**：将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时数据结构，然后生成一个代表这个类的java.lang.Class对象
- **链接**：将Java类的二进制代码合并到JVM的运行状态之中的过程
    - 验证：确保加载的类信息符合JVM规范，没有安全方面的问题
    - 准备：正式为类变量(static)分配内存并设置类变量默认初始值的阶段，这些内存都将在方法区中进行分配
    - 解析：虚拟机常量池内的符号引用(常量名)替换为直接引用(地址)的过程
- **初始化**
    - 执行类构造器<clinit>()方法的过程。类构造器<clinit>()方法是由编译器自动收集类中所有类变量的赋值动作和静态代码块中的语句合并产生的。(类构造器是构造类信息的，不是构造该类对象的构造器)。
    - 当初始化一个类的时候，如果发现其父类还没有进行初始化，则需要先触发其父类的初始化。
    - 虚拟机会保证一个类的<clinit>()方法在多线程环境中被正确加锁和同步。

```java 
package reflection;

public class ReflectionDemo4 {
    public static void main(String[] args) {
        A a = new A();
        System.out.println(A.m);
        /*
        1.加载到内存，会产生一个类对于的class对象
        2.链接，链接结束后 m=0
        3.初始化
            <clinit>(){
                System.out.println("静态代码块初始化！");
                m = 300;
                m = 100;
            }

         最终m=100
         */
    }
}

class A{

    static {
        System.out.println("静态代码块初始化！");
        m = 300;
    }
    static int m = 100;

    public A(){
        System.out.println("无参构造初始化！");
    }
}
```

![image-20200517100716387](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200517100716387.png)

#### 2.5 分析类的初始化

**什么时候会发生类初始化？**

- **类的主动引用**（一定会发生类的初始化）
    - 当虚拟机启动，先初始化main方法所在的类
    - new一个类的对象
    - 调用类的静态成员(**除了final常量**)和静态方法
    - 使用java.lang.reflect包的方法对类进行反射调用
    - 当初始化一个类，如果其父类没有被初始化，则会先初始化它的父类
- **类的被动引用**（不会发生类的初始化）
    - 当访问一个静态域时，只有真正声明这个域的类才会被初始化。例如：当通过子类引用父类的静态变量，不会导致子类初始化
    - 通过数组定义类引用，不会触发此类的初始化
    - 引用常量不会触发此类的初始化（常量在链接阶段就存入调用类的常量池中了）

```java
package reflection;

public class ReflectionDemo5 {
    static {
        System.out.println("Main被加载");
    }
    public static void main(String[] args) throws ClassNotFoundException {
        //1.主动引用
        //Son son = new Son();
        //2.反射也会引起主动引用
        //Class.forName("reflection.Son");

        //不会产生类的引用的方法

        //System.out.println(Son.b);

        //Son[] array = new Son[5];

        System.out.println(Son.M);
    }
}

class Father{
    static int b = 2;
    static {
        System.out.println("父类被加载");
    }
}

class Son extends Father{
    static {
        System.out.println("子类被加载");
        m = 300;
    }
    static int m = 100;
    static final int M = 1;
}
```

#### 2.6 类加载器

**类加载器的作用**：将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时数据结构，然后在堆中生成一个代表这个类的java.lang.Class对象，作为方法区中类数据的访问入口。

**类缓存**：标准JavaSE类加载器可以按要求查找类，但一旦某个类被加载到类加载器中，它将维持加载（缓存）一段时间。不过JVM垃圾回收机制可以回收这些Class对象。

![image-20200518224311218](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200518224311218.png)

**类加载器分类**

![image-20200518224448645](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200518224448645.png)

```java
package reflection;

public class ReflectionDemo6 {
    public static void main(String[] args) throws ClassNotFoundException {
        //获取系统类的加载器
        ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();
        System.out.println(systemClassLoader);

        //获取系统类加载器的父类加载器：扩展类加载器
        ClassLoader parent = systemClassLoader.getParent();
        System.out.println(parent);

        //获取扩展类加载器的父类加载器：根加载器(C/C++)
        ClassLoader parent1 = parent.getParent();
        System.out.println(parent1);

        //测试当前类是哪个加载器加载的
        ClassLoader classLoader = Class.forName("reflection.ReflectionDemo6").getClassLoader();
        System.out.println(classLoader);

        //测试jdk内置类的加载器
        ClassLoader classLoader1 = Class.forName("java.lang.Object").getClassLoader();
        System.out.println(classLoader1);

        //获取系统类加载器都可以加载的路径
        System.out.println(System.getProperty("java.class.path"));
    }
}
```

#### 2.7 获取类的运行时结构

```java
package reflection;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

/**
 * @author 10483
 * 获取类的信息
 */
public class ReflectionDemo7 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException, NoSuchMethodException {
        Class c1 = Class.forName("reflection.User");

        //获取类的名字
        //类名加包名
        System.out.println(c1.getName());
        //仅获得类名
        System.out.println(c1.getSimpleName());

        //获得类的属性
            //getFields()只能找到public属性
            //getField() 获得指定属性
        Field[] fileds = c1.getFields();
            //getDeclaredFields()可以找到所有属性
            //getDeclaredField()获得指定属性
        fileds = c1.getDeclaredFields();
        for(Field filed : fileds){
            System.out.println(filed);
        }

        System.out.println(c1.getDeclaredField("id"));
        System.out.println("==================");
        //获得类的方法
            //getMethods()获取本类及其父类的全部public方法
            //getMethod() 获得指定的方法 (public)
        Method[] methods = c1.getMethods();
        for(Method method :methods){
            System.out.println("正常的："+method);
        }
        System.out.println("==================");
            //getDeclaredMethods()获取本类的所有方法
            //getDeclaredMethod() 获取指定的方法
        methods = c1.getDeclaredMethods();
        for(Method method :methods){
            System.out.println("getDeclaredMethods："+method);
        }

        System.out.println("==================");
        //获得类的构造器
            //getConstructors: 获取public类型
        Constructor[] constructors = c1.getConstructors();
        for(Constructor constructor:constructors){
            System.out.println(constructor);
        }
            //getDeclaredConstructors:获取所有
        constructors = c1.getDeclaredConstructors();
        for(Constructor constructor:constructors){
            System.out.println("private: " + constructor);
        }

        //获得指定的构造器
        Constructor aim = c1.getConstructor(String.class, int.class, int.class);
        System.out.println("指定构造器：" + aim);
    }
}
```



#### 2.8 动态创建对象执行方法

- 创建类的对象：调用Class对象的newInstance方法
    - 类必须有一个无参构造器
    - 类的构造器的访问权限需要有
- 若类没有无参构造器，如何创建对象？？
    - 1.通过Class类的getDeclaredConstructor(Class....parameterTypes)取得本类的指定构造器
    - 2.向构造器的形参中传递一个对象数组进去，里面包含了构造器中所需的各个参数
    - 3.通过Constructor实例化对象
- 通过反射获得类的方法后，如何执行方法？？
    - 通过invoke  进行方法调用
    - 通过setAccessible(true)开启权限
    - ![image-20200519152254945](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200519152254945.png)

```java
package reflection;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

//动态的创建对象，通过反射
public class ReflectionDemo8 {
    public static void main(String[] args) throws Exception {
        Class c1 = Class.forName("reflection.User");

        //构造一个对象
            //本质是调用了类的无参构造器
        User user = (User)c1.newInstance();
        System.out.println(user);

        //通过构造器创建对象
        Constructor constructor = c1.getConstructor(String.class, int.class, int.class);
        User user2 =(User) constructor.newInstance("zh", 12, 40);
        System.out.println(user2);

        //通过反射调用普通方法
        User user3 =(User) c1.newInstance();
        //通过反射获取一个方法
        Method setName = c1.getDeclaredMethod("setName", String.class);

        //invoke:激活
        //(对象，“方法的值”)
        setName.invoke(user3,"zh");
        System.out.println(user3.getName());

        //通过反射操作属性
        User user4 = (User)c1.newInstance();
        Field name = c1.getDeclaredField("name");

        //不能直接操作私有属性
        //通过setAccessible(true)开启权限
        name.setAccessible(true);
        name.set(user4,"wss");
        System.out.println(user4.getName());
    }
}
```

#### 2.9 反射获取泛型信息

![image-20200519160552414](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200519160552414.png)

```java
package reflection;
/*
*1.获取类的方法     用getMethod
*2.获取方法中所有泛型参数    method.getGenericParameterTypes();
*3.遍历 并判断参数是否为结构化参数ParameterizedType
*4.若是，强制转化为真实参数     getActualTypeArguments()
*/
import java.lang.reflect.Method;
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;
import java.util.List;
import java.util.Map;

/**
 * @author 10483
 * 通过反射获取泛型
 */
public class ReflectionDemo10 {
    public void Test01(Map<String,User> map, List<User> list){
        System.out.println("Test01");
    }

    public Map<String,User> Test02(){
        System.out.println("Test02");
        return null;
    }

    public static void main(String[] args) throws NoSuchMethodException {
        //获取方法
        Method method = ReflectionDemo10.class.getMethod("Test01", Map.class, List.class);

        //获取方法的所有泛型参数
        Type[] genericParameterTypes = method.getGenericParameterTypes();

        //遍历 
        for(Type genericParameterType:genericParameterTypes){
            System.out.println("====" + genericParameterType);
            //判断泛型参数是否为参数化类型
            if(genericParameterType instanceof ParameterizedType){
                //若是，则强制转化类型为真实类型，然后打印
                Type[] actualTypeArguments = ((ParameterizedType) genericParameterType).getActualTypeArguments();
                for(Type actualType :actualTypeArguments){
                    System.out.println(actualType);
                }
            }
        }

        System.out.println("================================");
        method = ReflectionDemo10.class.getMethod("Test02",null);

        Type returnType = method.getGenericReturnType();
        if(returnType instanceof ParameterizedType){
            //若是，则强制转化类型为真实类型，然后打印
            Type[] actualTypeArguments = ((ParameterizedType) returnType).getActualTypeArguments();
            for(Type actualType :actualTypeArguments){
                System.out.println(actualType);
            }
        }


    }
}
```

#### 2.10 获取注解信息

![image-20200519161618071](C:\Users\10483\AppData\Roaming\Typora\typora-user-images\image-20200519161618071.png)

```java
package reflection;

import java.lang.annotation.*;
import java.lang.reflect.Field;

/**
 * @author 10483
 * 练习反射操作注解
 */
public class ReflectionDemo11 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException {
        Class c1 = Class.forName("reflection.Student2");

        //通过反射获得注解
        Annotation[] annotations = c1.getAnnotations();
        for(Annotation annotation:annotations){
            System.out.println(annotation);
        }

        //获取注解的value值
        Tablezhou tablezhou = (Tablezhou)c1.getAnnotation(Tablezhou.class);
        //System.out.println(tablezhou);
        String value = tablezhou.value();
        System.out.println(value);

        System.out.println("=======================");
        //获取类指定的注解
        Field name = c1.getDeclaredField("name");
        Filedzhou annotation = name.getAnnotation(Filedzhou.class);
        System.out.println(annotation.columnName());
        System.out.println(annotation.length());
        System.out.println(annotation.type());
    }
}

@Tablezhou("db_Student")
class Student2{

    @Filedzhou(columnName = "db_id",type = "int",length = 10)
    private int id;
    @Filedzhou(columnName = "db_age",type = "int",length = 10)
    private int age;
    @Filedzhou(columnName = "db_name",type = "varchar",length = 3)
    private String name;

    public Student2() {
    }

    public Student2(int id, int age, String name) {
        this.id = id;
        this.age = age;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Student2{" +
                "id=" + id +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}

/**
 * @author 10483
 * 类名的注解
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@interface Tablezhou{
    String value();
}

/**
 * @author 10483
 * 属性的注解
 */
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
@interface Filedzhou{
    String columnName();
    String type();
    int length();
}
```

