# 第 16 章 反射（Reflection）
2016-09-29 转自：https://github.com/JustinSDK/JavaSE6Tutorial/blob/master/docs/CH16.md 

Java 提供的反射机制允许您于执行时期动态加载类别、检视类别信息、生成对象或操作生成的对象，要举反射机制的一个应用实例，就是在集成开发环境中所提供的方法提示或是类别检视工具，另外像 JSP 中的 JavaBean 自动收集请求信息也使用到反射，而一些软件开发框架（Framework）也常见到反射机制的使用，以达到动态加载用户自定义类别的目的。

即使您暂时用不到反射机制，也建议您花时间看看这个章节，藉由对反射机制的认识，您可以了解 Java 中是如何加载类别的，而且了解到每个被载入的类别在 JVM 中，都以 Class 类别的一个实例存在的事实。

--------------

## 16.1 类别载入与检视

即使您拿到一个类别并对它一无所知，但其实它本身就包括了许多信息，Java 在需要使用到某个类别时才会将类别加载，并在 JVM 中以一个 java.lang.Class 的实例存在，从 Class 实例开始，您可以获得类别的许多讯息。

### 16.1.1 简介 Class 与类别载入

Java 在真正需要使用一个类别时才会加以加载，而不是在程序启动时就加载所有的类别，因为大多数的使用者都只使用到应用程序的部份资源，在需要某些功能时才加载某些资源，可以让系统的资源运用更有效率（Java 本来就是为了资源有限的小型设备而设计的，这样的考虑是必然的）。

一个 java.lang.Class 对象代表了 Java 应用程序在运行时所加载的类别或接口实例，也用来表达 enum（属于类别的一种）、 annotation（属于接口的一种）、数组、原生型态（Primitive type）、void；Class 类别没有公开的（public）建构方法，Class 对象是由 JVM 自动产生，每当一个类别被加载时，JVM 就自动为其生成一个 Class 对象。

您可以透过 Object 的 getClass() 方法来取得每一个对象对应的 Class 对象，或者是透过 "class" 常量（Class literal），在取得 Class 对象之后，您就可以操作 Class 对象上的一些公开方法来取得类别的基本信息，范例 16.1 简单的使用 getClass() 方法来取得 String 类别的 Class 实例，并从中得到 String 的一些基本信息。

#### **范例 16.1  ClassDemo.java**
```java
package onlyfun.caterpillar;
 
public class ClassDemo {
    public static void main(String[] args) {
        String name = "caterpillar";
        Class stringClass = name.getClass();
        System.out.println("类别名称：" + 
                    stringClass.getName()); 
        System.out.println("是否为接口：" + 
                    stringClass.isInterface()); 
        System.out.println("是否为基本型态：" + 
                    stringClass.isPrimitive()); 
        System.out.println("是否为数组对象：" + 
                    stringClass.isArray()); 
        System.out.println("父类别名称：" + 
                    stringClass.getSuperclass().getName());
    }
} 
```

执行结果：

    类别名称：java.lang.String
    是否为接口：false
    是否为基本型态：false
    是否为数组对象：false
    父类别名称：java.lang.Object

您也可以直接使用以下的方式来取得 String 类别的 Class 对象：

    Class stringClass = String.class;
    
Java 在真正需要类别时才会加载类别，所谓「真正需要」通常指的是要使用指定的类别生成对象时（或是用户指定要加载类别时，例如使用 Class.forName() 加载类别，或是使用 ClassLoader 的 loadClass() 加载类别，稍后都会说明）。使用类别名称来宣告参考名称并不会导致类别的加载，可以设计一个测试类别的印证这个说法。

#### **范例 16.2  TestClass.java**
```java
package onlyfun.caterpillar;

public class TestClass {
    static {
        System.out.println("类别被载入");
    }
}
```

在范例中定义了一个静态区块，「默认」在类别第一次被加载时会执行静态区块（说默认的原因，是因为可以设定加载类别时不执行静态区块，使用 Class 生成对象时才执行静态区块，稍后会介绍），藉由在文本模式下显示讯息，您可以了解类别何时被加载，可以使用范例 16.3 来测试类别加载时机。

#### **范例 16.3  LoadClassTest.java**
```java
package onlyfun.caterpillar;

public class LoadClassTest {
    public static void main(String[] args) {
        TestClass test = null;
        System.out.println("宣告TestClass参考名称");
        test = new TestClass();
        System.out.println("生成TestClass实例");
    }
}
```

执行结果：

    宣告TestClass参考名称
    类别被载入
    生成TestClass实例

从执行结果中可以看出，宣告参考名称并不导致 TestClass 类别被加载，而是在使用 "new" 生成对象时才会加载类别。

Class 的讯息是在编译时期就被加入至 .class 档案中，这是 Java 支持执行时期型别辨识（RTTI，Run-Time Type Information或Run-Time Type Identification）的一种方式，在编译时期编译程序会先检查对应的 .class 档案，而执行时期JVM在使用某类别时，会先检查对应的 Class 对象是否已经加载，如果没有加载，则会寻找对应的 .class 档案并载入，一个类别在 JVM 中只会有一个 Class 实例，每个类别的实例都会记得自己是由哪个 Class 实例所生成，您可以使用 getClass() 或 .class 来取得 Class 实例。

![每个对象会记得生成它的 Class 实例](../images/img16-01.png)

图 16.1 每个对象会记得生成它的 Class 实例

在 Java 中，数组也是一个对象，也有其对应的 Class 实例，这个对象是由具相同元素与维度的数组所共享，而基本型态像是 boolean, byte, char, short, int, long, float, double 以及关键词 void，也都有对应的 Class 对象，您可以用类别常量（Class literal）来取得这些对象。

#### **范例 16.4  ClassDemo2.java**
```java
package onlyfun.caterpillar;

public class ClassDemo2 { 
    public static void main(String[] args) { 
        System.out.println(boolean.class); 
        System.out.println(void.class); 

        int[] iarr = new int[10];
        System.out.println(iarr.getClass().toString());

        double[] darr = new double[10];
        System.out.println(darr.getClass().toString());
    } 
}
```

执行结果：

    boolean
    void
    class [I
    class [D

在 Java 中数组确实是以对象的形式存在，其对应的类别是由 JVM 自动生成，当您使用 toString() 来显示数组对象的描述时，[表示为数组型态，并加上一个型态代表字，范例中I表示是一个 int 数组，而 D 表示是一个 double 数组，16.2.4 还会对数组对象加以讨论。

### 16.1.2 使用 Class.forName() 载入类别

在一些应用中，您无法事先知道使用者将加载什么类别，而必须让使用者指定类别名称以加载类别，您可以使用 Class 的静态 forName() 方法实现动态加载类别，范例 16.5 是个简单示范，可以让您可以指定类别名称来获得类别的相关信息。

#### **范例 16.5  ForNameDemo.java**
```java
package onlyfun.caterpillar;
 
public class ForNameDemo {
    public static void main(String[] args) { 
        try {
            Class c = Class.forName(args[0]);
            System.out.println("类别名称：" + 
                          c.getName()); 
            System.out.println("是否为接口：" + 
                             c.isInterface()); 
            System.out.println("是否为基本型态：" + 
                             c.isPrimitive()); 
            System.out.println("是否为数组：" + c.isArray()); 
            System.out.println("父类别：" + 
                             c.getSuperclass().getName());
        }
        catch(ArrayIndexOutOfBoundsException e) {
            System.out.println("没有指定类别名称");
        }
        catch(ClassNotFoundException e) {
            System.out.println("找不到指定的类别");
        }
    }
} 
```

在指定类别给 forName() 方法后，如果找不到指定的类别，会丢出 ClassNotFoundException 例外，一个的执行结果如下：

    java onlyfun.caterpillar.ForNameDemo java.util.Scanner
    类别名称：java.util.Scanner
    是否为接口：false
    是否为基本型态：false
    是否为数组：false
    父类别：java.lang.Object

Class 的静态 forName() 方法有两个版本，范例16.5所示范的是只指定类别名称的版本，而另一个版本可以让您指定类别名称、加载类别时是否执行静态区块、指定类别加载器（Class loader）：

    static Class forName(String name, boolean initialize, ClassLoader loader)
    
之前曾经说过，预设上在加载类别的时候，如果类别中有定义静态区块则会执行它，您可以使用 forName() 的第二个版本，将 initialize 设定为 false，如此在加载类别时并不会马上执行静态区块，而会在使用类别建立对象时才执行静态区块，为了印证，您可以先设计一个测试类别。

#### **范例 16.6  TestClass2.java**
```java
package onlyfun.caterpillar;

public class TestClass2 {
    static {
        System.out.println("[执行静态区块]");
    }
}
```

范例 16.6 中只定义了静态区块显示一段讯息，以观察静态区块何时被执行，您可以设计范例 16.7 使用第一个版本的 forName() 方法。

#### **范例 16.7  ForNameDemoV1.java**
```java
package onlyfun.caterpillar;
 
public class ForNameDemoV1 {
    public static void main(String[] args) { 
        try {
            System.out.println("载入TestClass2");
            Class c = Class.forName("onlyfun.caterpillar.TestClass2");

            System.out.println("使用TestClass2宣告参考名称");
            TestClass2 test = null;

            System.out.println("使用TestClass2建立对象");                        
            test = new TestClass2();
        }
        catch(ClassNotFoundException e) {
            System.out.println("找不到指定的类别");
        }
    }
}
```

执行结果如下：

    载入TestClass2
    [执行静态区块]
    使用TestClass2宣告参考名称
    使用TestClass2建立对象

从执行结果中可以看到，第一个版本的 forName() 方法在加载类别之后，默认会马上执行静态区块，来看看范例 16.8 中使用第二个版本的 forName() 方法会是如何。

#### **范例 16.8  ForNameDemoV2.java**
```java
package onlyfun.caterpillar;
 
public class ForNameDemoV2 {
    public static void main(String[] args) { 
        try {
            System.out.println("载入TestClass2");
            Class c = Class.forName(
                         "onlyfun.caterpillar.TestClass2", 
                         false, // 加载类别时不执行静态方法
                         Thread.currentThread().getContextClassLoader());

            System.out.println("使用TestClass2宣告参考名称");
            TestClass2 test = null;

            System.out.println("使用TestClass2建立对象");                        
            test = new TestClass2();
        }
        catch(ClassNotFoundException e) {
            System.out.println("找不到指定的类别");
        }
    }
}
```

执行结果如下：

    载入TestClass2
    使用TestClass2宣告参考名称
    使用TestClass2建立对象
    [执行静态区块]

由于使用第二个版本的 forName() 方法时，设定 initialize 为 false，所以加载类别时并不会马上执行静态区块，而会在使用类别建立对象时才去执行静态区块，第二个版本的 forName() 方法会需要一个类别加载器（Class loader），范例中所使用的是主线程的类别加载器，16.1.4 还会详细介绍 Java 中的类别加载器机制。

### 16.1.3 从 Class 中获取信息

Class 对象表示所加载的类别，取得 Class 对象之后，您就可以取得与类别相关联的信息，像是套件（package）（别忘了 package 也是类别名称的一部份）、建构方法、方法成员、数据成员等的讯息，而每一个讯息，也会有相应的类别型态，例如套件的对应型态是 java.lang.Package，建构方法的对应型态是 java.lang.reflect.Constructor，方法成员的对应型态是 java.lang.reflect.Method，数据成员的对应型态是 java.lang.reflect.Field 等。

来看个简单的示范，范例 16.9 可以让您取得所指定类别上的套件名称。

#### **范例 16.9  ClassInfoDemo.java**
```java
package onlyfun.caterpillar;
 
public class ClassInfoDemo {
    public static void main(String[] args) { 
        try {
            Class c = Class.forName(args[0]);
            Package p = c.getPackage();
            System.out.println(p.getName());
        }
        catch(ArrayIndexOutOfBoundsException e) {
            System.out.println("没有指定类别");
        }
        catch(ClassNotFoundException e) {
            System.out.println("找不到指定类别");
        }
    }
}
```

执行结果：

    java onlyfun.caterpillar.ClassInfoDemo java.util.ArrayList
    java.util

您可以分别取回 Field、Constructor、Method等对象，分别代表数据成员、建构方法与方法成员，范例16.10 简单的实作了取得类别基本信息的程序。

#### **范例 16.10  SimpleClassViewer.java**
```java
package onlyfun.caterpillar;

import java.lang.reflect.*;

public class SimpleClassViewer {
     public static void main(String[] args) { 
        try {
            Class c = Class.forName(args[0]);
            // 取得套件代表对象
            Package p = c.getPackage();
            
            System.out.printf("package %s;%n", p.getName());
            
            // 取得型态修饰，像是class、interface
            int m = c.getModifiers();
            
            System.out.print(Modifier.toString(m) + " ");
            // 如果是接口
            if(Modifier.isInterface(m)) {
                System.out.print("interface ");
            }
            else {
                System.out.print("class ");
            }
            
            System.out.println(c.getName() + " {");

            // 取得宣告的数据成员代表对象
            Field[] fields = c.getDeclaredFields();
            for(Field field : fields) {
                // 显示权限修饰，像是public、protected、private
                System.out.print("\t" + 
                    Modifier.toString(field.getModifiers()));
                // 显示型态名称
                System.out.print(" " + 
                    field.getType().getName() + " ");
                // 显示数据成员名称
                System.out.println(field.getName() + ";");
            }

            // 取得宣告的建构方法代表对象            
            Constructor[] constructors = 
                            c.getDeclaredConstructors();
            for(Constructor constructor : constructors) {
                // 显示权限修饰，像是public、protected、private
                System.out.print("\t" + 
                     Modifier.toString(
                       constructor.getModifiers()));
                // 显示建构方法名称
                System.out.println(" " + 
                      constructor.getName() + "();");
            }
            // 取得宣告的方法成员代表对象             
            Method[] methods = c.getDeclaredMethods();
            for(Method method : methods) {
                // 显示权限修饰，像是public、protected、private
                System.out.print("\t" + 
                     Modifier.toString(
                              method.getModifiers()));
                // 显示返回值型态名称
                System.out.print(" " + 
                     method.getReturnType().getName() + " ");
                // 显示方法名称
                System.out.println(method.getName() + "();");
            }
            System.out.println("}");
        }
        catch(ArrayIndexOutOfBoundsException e) {
            System.out.println("没有指定类别");
        }
        catch(ClassNotFoundException e) {
            System.out.println("找不到指定类别");
        }
    }
}
```

执行结果：

    package java.util;
    public class java.util.ArrayList {
            private static final long serialVersionUID;
            private transient [Ljava.lang.Object; elementData;
            private int size;
            public java.util.ArrayList();
            public java.util.ArrayList();
            public java.util.ArrayList();
            public boolean add();
            public void add();
            public java.lang.Object clone();
            public void clear();
            public boolean contains();
            public int indexOf();
            略...
    }

一些类别查看器的实作原理基本上就是范例 16.10 所示范的，当然还可以取得更多的信息，您可以参考 Class 的在线 API 文件得到更多的讯息。

### 16.1.4 简介类别加载器

Java 在需要使用类别的时候，才会将类别加载，Java 的类别载入是由类别加载器（Class loader）来达到的。

当您在文本模式下执行 java XXX 指令后，java 执行程序会尝试找到 JRE 安装的所在目录，然后寻找 jvm.dll（默认是在JRE目录下bin\client目录中），接着启动 JVM 并进行初始化动作，接着产生 Bootstrap Loader，Bootstrap Loader 会加载 Extended Loader，并设定 Extended Loader 的 parent 为 Bootstrap Loader，接着 Bootstrap Loader 会加载 System Loader，并将 System Loader 的 parent 设定为 Extended Loader。

Bootstrap Loader 通常由 C 撰写而成；Extended Loader 是由 Java 所撰写而成，实际是对应于 sun.misc.Launcher\$ExtClassLoader（Launcher 中的内部类别）；System Loader 是由 Java 撰写而成，实际对应于sun.misc. Launcher\$AppClassLoader（Launcher 中的内部类别）。

图 16.2 是 java 程序启动与加载类别的顺序图，也就是所谓的「类别加载器阶层架构」。

![Java 类别加载器阶层架构](../images/img16-02.png)

图 16.2 Java 类别加载器阶层架构

Bootstrap Loader 会搜寻系统参数 sun.boot.class.path 中指定位置的类别，默认是 JRE  classes 下之  档案，或 lib 目录下 .jar 档案中（例如 rt.jar）的类别并加载，您可以使用 System.getProperty("sun.boot.class.path") 陈述来显示 sun.boot.class.path 中指定的路径，例如在我的计算机中显示的是以下的路径：

    C:\Program Files\Java\jre1.5.0_03\lib\rt.jar;
    C:\Program Files\Java\jre1.5.0_03\lib\i18n.jar;
    C:\Program Files\Java\jre1.5.0_03\lib\sunrsasign.jar;
    C:\Program Files\Java\jre1.5.0_03\lib\jsse.jar;
    C:\Program Files\Java\jre1.5.0_03\lib\jce.jar;
    C:\Program Files\Java\jre1.5.0_03\lib\charsets.jar;
    C:\Program Files\Java\jre1.5.0_03\classes

Extended Loader（sun.misc.Launcher$ExtClassLoader）是由 Java 撰写而成，会搜寻系统参数 java.ext.dirs 中指定位置的类别，默认是 JRE 目录下的 lib\ext\classes 目录下的 .class 档案，或 lib\ext 目录下的 .jar 档案中（例如 rt.jar）的类别并加载，您可以使用 System.getProperty("java.ext.dirs") 陈述来显示  中指定的路径，例如在我的计算机中显示的是以下的路径：

    C:\Program Files\Java\jre1.5.0_03\lib\ext
    
System Loader（sun.misc.Launcher$AppClassLoader）是由 Java 撰写而成，会搜寻系统参数 java.class.path 中指定位置的类别，也就是 Classpath 所指定的路径，默认是目前工作路径下的 .class 档案，您可以使用 System.getProperty("java.class.path") 陈述来显示 java.class.path 中指定的路径，在使用 java 执行程序时，您也可以加上 -cp 来覆盖原有的 Classpath 设定，例如：

    java –cp ./classes SomeClass
    
Bootstrap Loader 会在 JVM 启动之后产生，之后它会加载 Extended Loader 并将其 parent 设为 Bootstrap Loader，然后 Bootstrap Loader 再加载 System Loader 并将其 parent 设定为 ExtClassLoader，接着 System Loader 开始加载您指定的类别，在加载类别时，每个类别加载器会先将加载类别的任务交由其 parent，如果 parent 找不到，才由自己负责加载，所以在加载类别时，会以 Bootstrap Loader→Extended Loader→System Loader 的顺序来寻找类别，如果都找不到，就会丢出 NoClassDefFoundError。

类别加载器在 Java 中是以 java.lang.ClassLoader 型态存在，每一个类别被载入后，都会有一个 Class 的实例来代表，而每个 Class 的实例都会记得自己是由哪个 ClassLoader 加载的，可以由 Class 的 getClassLoader() 取得加载该类别的 ClassLoader，而从 ClassLoader 的 getParent() 方法可以取得自己的 parent，图 16.3 显示了一个自定义的 SomeClass 实例与 Class、ClassLoader 及各 parent 的关系。

![对象、Class、ClassLoader 与 parent 的关系](../images/img16-03.png)

图 16.3 对象、Class、ClassLoader 与 parent 的关系

范例 16.11 示范了图 16.3 的一个实际例子。

#### **范例 16.11  SomeClass.java**
```java
package onlyfun.caterpillar;

public class SomeClass {
    public static void main(String[] args) {
        // 建立SomeClass实例
        SomeClass some = new SomeClass();
        // 取得SomeClass的Class实例
        Class c = some.getClass();
        // 取得ClassLoader
        ClassLoader loader = c.getClassLoader();
        System.out.println(loader);
        // 取得父ClassLoader
        System.out.println(loader.getParent());
        // 再取得父ClassLoader
        System.out.println(loader.getParent().getParent());
    }
} 
```

执行结果：

    sun.misc.Launcher$AppClassLoader@82ba41
    sun.misc.Launcher$ExtClassLoader@923e30
    null

onlyfun.caterpillar.SomeClass 是个自定义类别，您在目前的工作目录下执行程序，首先 AppClassLoader 会将加载类别的任务交给 ExtClassLoader，而 ExtClassLoader 会将加载类别的任务交给 Bootstrap Loader，由于 Bootstrap Loader 在它的路径设定（sun.boot.class.path）下找不到类别，所以由 ExtClassLoader 来试着寻找，而 ExtClassLoader 在它的路径设定（java.ext.dirs）下也找不到类别，所以由 AppClassLoader 来试着寻找，AppClassLoader 最后在 Classpath（java.class.path）设定下找到指定的类别并加载。

在执行结果中可以看到，加载 SomeClass 的 ClassLoader 是 AppClassLoader，而 AppClassLoader 的 parent 是 ExtClassLoader，而 ExtClassLoader 的 parent 是 null，null 并不是表示 ExtClassLoader 没有设定 parent，而是因为 Bootstrap Loader 通常由 C 所撰写而成，在 Java 中并没有一个实际的类别来表示它，所以才会显示为 null。

如果把 SomeClass 的 .class 档案移至 JRE 目录下的 lib\ext\classes下（由于设定了套件，所以实际上 SomeClass.class 要放置在 JRE 目录下的 lib\ext\classes\onlyfun\caterpillar下），并重新（于任何目录下）执行程序，您会看到以下的讯息：

    sun.misc.Launcher$ExtClassLoader@923e30
    null
    Exception in thread "main" java.lang.NullPointerException
            at onlyfun.caterpillar.SomeClass.main(SomeClass.java:15)

由于 SomeClass 这次可以在 ExtClassLoader 的设定路径下找到，所以会由 ExtClassLoader 来加载 SomeClass 类别，而 ExtClassLoader 的 parent 显示为 null，指的是它的 parent 是由 C 撰写而成的 Bootstrap Loader，因为没有实际的 Java 类别而表示为 null，所以再由 null 上尝试呼叫 getParent() 方法就会丢出 NullPointerException 例外。

如果再把 SomeClass 的 .class 档案移至 JRE 目录下的 classes 目录下（由于设定了套件，所以实际上 SomeClass.class 要放置在 JRE 目录下的 classes/onlyfun/caterpillar下），并重新（于任何目录下）执行程序，您会看到以下的讯息：

    null
    Exception in thread "main" java.lang.NullPointerException
            at onlyfun.caterpillar.SomeClass.main(SomeClass.java:13)

由于 SomeClass 这次可以在 Bootstrap Loader 的设定路径下找到，所以会由 Bootstrap Loader 来加载 SomeClass 类别，Bootstrap Loader 通常由 C 撰写而成，在 Java 中没有一个实际的类别来表示，所以显示为 null，因为表示为 null，所以再 由 null 上尝试呼叫 getParent() 方法就会丢出 NullPointerException 例外。

取得 ClassLoader 的实例之后，您可以使用它的 loadClass() 方法来加载类别，使用 loadClass() 方法加载别时，不会执行静态区块，静态区块的执行会等到真正使用类别来建立实例时，例如您可以改写范例 16.7 为范例 16.12。

#### **范例 16.12  ForNameDemoV3.java**
```java
package onlyfun.caterpillar;
 
public class ForNameDemoV3 {
    public static void main(String[] args) { 
        try {
            System.out.println("载入TestClass2");
            ClassLoader loader = ForNameDemoV3.class.getClassLoader();
            Class c = loader.loadClass("onlyfun.caterpillar.TestClass2");

            System.out.println("使用TestClass2宣告参考名称");
            TestClass2 test = null;

            System.out.println("使用TestClass2建立对象");
            test = new TestClass2();
        }
        catch(ClassNotFoundException e) {
            System.out.println("找不到指定的类别");
        }
    }
}
```

从执行结果中可以看到，loadClass() 不会在加载类别时执行静态区块，而会在使用类别新建对象时才执行静态区块，结果如下所示：

    载入TestClass2
    使用TestClass2宣告参考名称
    使用TestClass2建立对象
    [执行静态区块]
    
### 16.1.5 使用自己的 ClassLoader

ExtClassLoader 与 AppClassLoader 都是 java.net.URLClassLoader 的子类别，您可以在使用 java 启动程序时，使用以下的指令来指定 ExtClassLoader 的搜寻路径：

    java -Djava.ext.dirs=c:\workspace\ YourClass
    
可以在使用 java 启动程序时，使用 -classpath 或 -cp 来指定 AppClassLoader 的搜寻路径，也就是设定 Classpath：

    java -classpath c:\workspace\ YourClass

ExtClassLoader 与 AppClassLoader 在程序启动后会在虚拟机中存在一份，您在程序运行过程中就无法再改变它的搜寻路径，如果在程序运行过程中，打算动态决定从其它的路径加载类别，就要产生新的类别加载器。

您可以使用 URLClassLoader 来产生新的类别加载器，它需要 java.net.URL 作为其参数来指定类别加载的搜寻路径，例如：

    URL url = new URL("file:/d:/workspace/");
    ClassLoader urlClassLoader = 
                        new URLClassLoader(new URL[] {url});
    Class c = urlClassLoader.loadClass("SomeClass");
    
由于 ClassLoader 是 Java SE 的标准API之一，可以在 rt.jar 中找到，因而会由 Bootstrap Loader 来载入 ClassLoader 类别，在新增了 ClassLoader 实例后，您可以使用它的 loadClass() 方法来指定要加载的类别名称，在新增 ClassLoader 时，会自动将新建的 ClassLoader 的 parent 设定为 AppClassLoader，并在每次加载类别时，先委托 parent 代为搜寻，所以上例中搜寻 SomeClass 类别时，会一路往上委托至 Bootstrap Loader 先开始搜寻，接着是 ExtClassLoader、AppClassLoader，如果都找不到，才使用新建的 ClassLoader 搜寻。

Java 的类别加载器阶层架构除了可以达到动态加载类别目的之外，还有着安全上的考虑，首先，因为每次寻找类别时都是委托 parent 开始寻找，所以除非有人可以侵入您的计算机，置换掉标准 Java SE API 与您自己安装的延伸套件，否则是不可能藉由撰写自己的类别加载器来载入恶意类别，以置换掉标准 Java SE API与您自己安装的延伸套件。

由于每次的类别载入是由子 ClassLoader 委托父 ClassLoader 先尝试加载，但父 lassLoader 看不到子 ClassLoader，所以同一阶层的子 ClassLoader 不会被误用，从而避免了加载错误类别的可能性，例如在图 16.4 中，您想从 YourClassLoader 来加载类别的话，类别加载器阶层不会看到 MaliciousClassLoader。

![类别加载器阶层的安全设计](../images/img16-04.png)

图 16.4 类别加载器阶层的安全设计

由同一个 ClassLoader 加载的类别档案，会只有一份Class实例，如果同一个类别档案是由两个不同的ClassLoader 载入，则会有两份不同的 Class 实例。注意这个说法，如果有两个不同的 ClassLoader 搜寻同一个类别，而在 parent 的 AppClassLoader 搜寻路径中就可以找到指定类别的话，则 Class 实例就只会有一个，因为两个不同的 ClassLoader 都是在委托父 ClassLoader 时找到该类别的，如果父 ClassLoader 找不到，而是由各自的 ClassLoader 搜寻到，则 Class 的实例会有两份。

范例 16.13 是个简单的示范，可用来测试加载路径与Class实例是否为同一对象。

#### **范例 16.13  ClassLoaderDemo.java**
```java
package onlyfun.caterpillar;

import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLClassLoader;

public class ClassLoaderDemo {
    public static void main(String[] args) {
        try {
            // 测试路径
            String classPath = args[0];
            // 测试类别
            String className = args[1];

            URL url1 = new URL(classPath);
            // 建立ClassLoader
            ClassLoader loader1 = 
                      new URLClassLoader(new URL[] {url1});
            // 加载指定类别
            Class c1 = loader1.loadClass(className);
            // 显示类别描述
            System.out.println(c1);
        
            URL url2 = new URL(classPath);
            ClassLoader loader2 = 
                      new URLClassLoader(new URL[] {url2});
            Class c2 = loader2.loadClass(className);
        
            System.out.println(c2);
        
            System.out.println("c1 与 c1 为同一实例？" 
                                     + (c1 == c2));
        }
        catch(ArrayIndexOutOfBoundsException e) {
            System.out.println("没有指定类别加载路径与名称");
        }
        catch(MalformedURLException e) {
            System.out.println("加载路径错误");
        }
        catch(ClassNotFoundException e) {
            System.out.println("找不到指定的类别");
        }
    }
}
```

您可以任意设计一个类别，例如 TestClass，其中 classPath 可以输入不为 ExtClassLoader 或 AppClassLoader 的搜寻路径，例如 file:/d:/workspace/，这样同一个类别会分由两个 ClassLoader 载入，结果会有两份 Class 实例，则测试 c1 与 c2 是否为同一实例时，则结果会显示 false，一个执行结果如下：

    java onlyfun.caterpillar.ClassLoaderDemo file:/d:/workspace/ TestClass
    class TestClass
    class TestClass
    c1 与 c1 为同一实例？false

如果您在执行程序时，以 -cp 将 file:/d:/workspace/ 加入为 Classpath 的一部份，由于两个 ClassLoader 的 parent 都是 AppClassLoader，而 AppClassLoader 会在 Classpath 中找到指定的类别，所以最后会只有一个指定的类别之 Class 实例，则测试 c1 与 c2 是否为同一实例时，结果会显示 true，一个执行结果如下：

    java -cp .;d:\workspace onlyfun.caterpillar.ClassLoaderDemo file:/d:/workspace/ TestClass
    class TestClass
    class TestClass
    c1 与 c1 为同一实例？true

使用 -cp 指定 Classpath 时，会覆盖原有的 Classpath 定义，也就是连现行工作目录的路径也覆盖了，由于我的 ClassLoaderDemo 类别是在现行工作目录下，所以使用 -cp 时，也包括了现行工作目录，记得组合多个 Classpath 路径时，可以使用「;」。

## 16.2 使用反射生成与操作对象

使用反射机制，您可以于执行时期动态加载类别并生成对象，操作对象上的方法、改变类别成员的值，甚至连私用（private）成员的值也可以改变。

### 16.2.1 生成物件

您可以使用 Class 的 newInstance() 方法来实例化一个对象，实例化的对象是以 Object 型态传回，例如：

    Class c = Class.forName(className);
    Object obj = c.newInstance();
    
范例 16.14 是个简单的示范，您可以动态加载实现了 List 接口的类别。

#### **范例 16.14  NewInstanceDemo.java**
```java
package onlyfun.caterpillar;

import java.util.*;

public class NewInstanceDemo {
    public static void main(String[] args) { 
        try {
            Class c = Class.forName(args[0]);
            List list = (List) c.newInstance();
            
            for(int i = 0; i < 5; i++) {
                list.add("element " + i);
            }
            
            for(Object o: list.toArray()) {
                System.out.println(o);
            }
        }
        catch(ClassNotFoundException e) {
            System.out.println("找不到指定的类别");
        } catch (InstantiationException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }
    }
}
```

执行结果：

    java onlyfun.caterpillar.NewInstanceDemo java.util.ArrayList
    element 0
    element 1
    element 2
    element 3
    element 4

实际上如果想要使用反射来动态加载类别，通常是对对象的接口或类型都一无所知，也就无法像范例 16.14 中对 newInstance() 传回的对象进行接口转换动作，稍后会介绍如何以反射来呼叫方法以操作 newInstance() 所传回的对象。

如果加载的类别中具备无参数的建构方法，则可以无参数的 newInstance() 来建构一个不指定初始自变量的对象，如果您要在动态加载及生成对象时指定对象的初始化自变量，则要先指定参数型态、取得 Constructor 对象、使用 Constructor 的 newInstance() 并指定参数的接受值。

以一个例子来说明，首先定义一个 Student 类。

#### **范例 16.15  Student.java**
```java
package onlyfun.caterpillar;

public class Student {
    private String name;
    private int score; 

    public Student() {
        name = "N/A"; 
    } 

    public Student(String name, int score) { 
        this.name = name; 
        this.score = score; 
    } 

    public void setName(String name) {
        this.name = name;
    }
    
    public void setScore(int score) {
        this.score = score;
    }

    public String getName() { 
        return name; 
    } 

    public int getScore() { 
        return score; 
    } 

    public String toString() {
        return name + ":" + score;
    }
} 
```

您可以用 Class.forName() 来加载 Student 类别，并使用第二个有参数的建构方法来建构 Student 实例，如范例 16.16 所示。

#### **范例 16.16  NewInstanceDemo2.java**
```java
package onlyfun.caterpillar;
 
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
 
public class NewInstanceDemo2 {
    public static void main(String[] args) {
        try {
            Class c = Class.forName(args[0]);
            
            // 指定参数型态
            Class[] params = new Class[2];
            // 第一个参数是String
            params[0] = String.class;
            // 第二个参数是int
            params[1] = Integer.TYPE;

            // 取得对应参数列的建构方法            
            Constructor constructor = 
                             c.getConstructor(params);
            
            // 指定自变量内容
            Object[] argObjs = new Object[2];
            argObjs[0] = "caterpillar";
            argObjs[1] = new Integer(90);
            
            // 给定自变量并实例化
            Object obj = constructor.newInstance(argObjs);
            // 呼叫toString()来观看描述
            System.out.println(obj);
        } catch (ClassNotFoundException e) {
            System.out.println("找不到类别");
        } catch (SecurityException e) {
            e.printStackTrace();
        } catch (NoSuchMethodException e) {
            System.out.println("没有所指定的方法");
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        } catch (InstantiationException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
    }
}
```

注意在指定基本型态时，要使用对应的包裹类别（Wrapper）并使用 .TYPE，例如指定 int 型态时，则使用 Integer.TYPE，如果要指定 Integer 型态的参数的话，才是使用 Integer.class，范例 16.16 会根据指定的自变量呼叫对应的建构方法，加载 onlyfun.caterpillar.Student 的执行结果如下：

    java onlyfun.caterpillar.NewInstanceDemo2 onlyfun.caterpillar.Student
    caterpillar:90

### 16.2.2 呼叫方法

使用反射可以取回类别上方法的对象代表，方法的对象代表是 java.lang.reflect.Method 的实例，您可以使用它的 invoke() 方法来动态呼叫指定的方法，例如呼叫范例 16.15 的 Student 类别上之 setName() 等方法，这边直接以范例 16.17 作为示范。

#### **范例 16.17  InvokeMethodDemo.java**
```java
package onlyfun.caterpillar;

import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class InvokeMethodDemo {
    public static void main(String[] args) {
        try {
            Class c = Class.forName(args[0]);
            // 使用无参数建构方法建立对象
            Object targetObj = c.newInstance();
            // 设定参数型态
            Class[] param1 = {String.class};
            // 根据参数型态取回方法对象
            Method setNameMethod = c.getMethod("setName", param1);
            // 设定自变量值 
            Object[] argObjs1 = {"caterpillar"};
            // 给定自变量呼叫指定对象之方法
            setNameMethod.invoke(targetObj, argObjs1);
            
            
            Class[] param2 = {Integer.TYPE};
            Method setScoreMethod = 
                     c.getMethod("setScore", param2);
            
            Object[] argObjs2 = {new Integer(90)};
            setScoreMethod.invoke(targetObj, argObjs2);
            // 显示对象描述
            System.out.println(targetObj);
            
        } catch (ClassNotFoundException e) {
            System.out.println("找不到类别");
        } catch (SecurityException e) {
            e.printStackTrace();
        } catch (NoSuchMethodException e) {
            System.out.println("没有这个方法");
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        } catch (InstantiationException e) {
            e.printStackTrace();
        }
    }
}
```

范例 16.17 可以指定加载 Student 类别并生成实例，接着可以动态呼叫 setName() 与 setScore() 方法，范例中参数型态与自变量值的设定与范例 16.16 是类似的，由于呼叫 setName() 与 setScore() 所给定的自变量是 "caterpillar" 与 90，所以执行的结果与范例 16.16 是相同的。

在很少的情况下，您会需要突破 Java 的存取限制来呼叫受保护的（protected）或私有（private）的方法（例如您拿到一个组件（Component），但您没法修改它的原始码来改变某个私有方法的权限，而您又一定要呼叫某个私有方法），这时候您可以使用反射机制来达到您的目的，一个存取私有方法的例子如下：

    Method privateMethod = 
                c.getDeclaredMethod("somePrivateMethod", new Class[0]);
    privateMethod.setAccessible(true);
    privateMethod.invoke(targetObj, argObjs);
    
使用反射来动态呼叫方法的实际例子之一是在 JavaBean 的设定，例如在 JSP/Servlet 中，可以根据使用者的请求名称与 JavaBean 的属性名称自动比对，将字符串请求值设定至指定的 JavaBean 上，并自动根据参数型态作型态转换（详细说明请见本章后网络索引）。范例 16.18 是个简单的示范，您可以给 CommandUtil 工具类别一个 Map 对象与类别名称，然后取得一个更新了值的实例，其中参数 Map 对象的「键」（Key）为要呼叫的 setter 方法名称（不包括set开头的名称，例如 setName() 方法的话，只要给定键为 name 即可），而「值」（Value）为要设定给 setter 的自变量。

#### **范例 16.18  CommandUtil.java**
```java
package onlyfun.caterpillar;

import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
import java.util.Map;

public class CommandUtil {
    // 给定Map对象及要产生的Bean类别名称
    // 可以取回已经设定完成的对象
    public static Object getCommand(Map requestMap, 
                                    String commandClass) 
                                      throws Exception {
        Class c = Class.forName(commandClass);
        Object o = c.newInstance();
    
        return updateCommand(requestMap, o);
    }

    // 使用reflection自动找出要更新的属性
    public static Object updateCommand(
                           Map requestMap, 
                           Object command) 
                              throws Exception {
        Method[] methods = 
                   command.getClass().getDeclaredMethods();
    
        for(int i = 0; i < methods.length; i++) {
            // 略过private、protected成员
            // 且找出必须是set开头的方法名称
            if(!Modifier.isPrivate(methods[i].getModifiers()) &&
               !Modifier.isProtected(methods[i].getModifiers()) &&  
               methods[i].getName().startsWith("set")) {
                // 取得不包括set的名称
                String name = methods[i].getName()
                                        .substring(3)
                                        .toLowerCase();
                // 如果setter名称与键值相同
                // 呼叫对应的setter并设定值
                if(requestMap.containsKey(name)) {
                    String param = (String) requestMap.get(name);
                    Object[] values = findOutParamValues(
                                        param, methods[i]);
                    methods[i].invoke(command, values);
                }
            }
        }
        return command;  
    }
  
    // 转换为对应型态的值
    private static Object[] findOutParamValues(
                     String param, Method method) {
        Class[] params = method.getParameterTypes();
        Object[] objs = new Object[params.length];
    
        for(int i = 0; i < params.length; i++) {
            if(params[i] == String.class) {
                objs[i] = param;
            }
            else if(params[i] == Short.TYPE) {
                short number = Short.parseShort(param);
                objs[i] = new Short(number);
            }
            else if(params[i] == Integer.TYPE) {
                int number = Integer.parseInt(param);
                objs[i] = new Integer(number);
            }
            else if(params[i] == Long.TYPE) {
                long number = Long.parseLong(param);
                objs[i] = new Long(number);
            }
            else if(params[i] == Float.TYPE) {
                float number = Float.parseFloat(param);
                objs[i] = new Float(number);
            }
            else if(params[i] == Double.TYPE) {
                double number = Double.parseDouble(param);
                objs[i] = new Double(number);
            }
            else if(params[i] == Boolean.TYPE) {
                boolean bool = Boolean.parseBoolean(param);
                objs[i] = new Boolean(bool);
            }
        }    
        return objs;
    }
}
```

CommandUtil 可以自动根据方法上的参数型态，将 Map 对象中的「值」对象转换为属性上的对应型态，目前它可以转换基本型态与 String 型态的属性，一个使用 CommandUtil 类别的例子如范例 16.19 所示。

#### **范例 16.19  CommandUtilDemo.java**
```java
package onlyfun.caterpillar;

import java.util.*;

public class CommandUtilDemo {
    public static void main(String[] args) throws Exception {
        Map<String, String> request = 
                  new HashMap<String, String>();
        request.put("name", "caterpillar");
        request.put("score", "90");
        Object obj = CommandUtil.getCommand(request, args[0]);
        System.out.println(obj);
    }
}
```

您可以使用范例 16.19 来加载 Student 类别，使用 CommandUtil.getCommand() 方法可以返回一个设定好值的 Student 实例，虽然您设定给 request 的「值」是字符串型态，但 CommandUtil 会使用反射机制来自动转换为属性上的对应型态，一个执行的范例如下所示：

    java onlyfun.caterpillar.CommandUtilDemo onlyfun.caterpillar.Student
    caterpillar:90
    
> **良葛格的话匣子** 不知道方法的名称如何呼叫？其实范例 16.17 就给出了答案，透过规范方法的命名方式，之后就可以透用反射机制加上方法名称的比对，以正确呼叫对应的方法。

### 16.2.3 修改成员值

尽管直接存取类别的数据成员（Field）是不被鼓励的，但您仍是可以直接存取公开的（public）数据成员，而您甚至也可以透过反射机制来存取私用数据成员，以一个实例来说明，首先撰写个 TestedField 类别。

#### **范例 16.20  TestField.java**
```java
package onlyfun.caterpillar;

public class TestField {
    public int testInt;
    public String testString;
    
    public String toString() {
        return testInt + ":" + testString;
    }
}
```

范例 16.21 则利用反射机制动态加载类别来存取数据成员。

#### **范例 16.21  AssignFieldDemo.java**
```java
package onlyfun.caterpillar;
 
import java.lang.reflect.Field; 
 
public class AssignFieldDemo {
    public static void main(String[] args) {
        try {
            Class c = Class.forName(args[0]);
            Object targetObj = c.newInstance();
            
            Field testInt = c.getField("testInt");
            testInt.setInt(targetObj, 99);
            
            Field testString = c.getField("testString");
            testString.set(targetObj, "caterpillar");
            
            System.out.println(targetObj);
        } catch(ArrayIndexOutOfBoundsException e) {
            System.out.println("没有指定类别");
        } catch (ClassNotFoundException e) {
            System.out.println("找不到指定的类别");
        } catch (SecurityException e) {
            e.printStackTrace();
        } catch (NoSuchFieldException e) {
            System.out.println("找不到指定的数据成员");
        } catch (InstantiationException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }       
    }
}
```

您可以加载 TestField 类别来看看执行的结果，如下所示：

    java onlyfun.caterpillar.AssignFieldDemo onlyfun.caterpillar.TestField
    99:caterpillar

如果有必要的话，您也可以透过反射机制来存取私有的数据成员，例如：

    Field privateField = c.getDeclaredField("privateField"); 
    privateField.setAccessible(true);
    privateField.setInt(targetObj, 99);

### 16.2.4 再看数组对象

在 Java 中数组也是一个对象，也会有一个 Class 实例来表示它，范例 16.22 显示几个基本型态以及 String 数组的类别名称描述。

## **范例 16.22  ArrayDemo.java**
```java
package onlyfun.caterpillar;

public class ArrayDemo {
    public static void main(String[] args) {
        short[] sArr = new short[5];
        int[] iArr = new int[5];
        long[] lArr = new long[5];
        float[] fArr = new float[5];
        double[] dArr = new double[5];
        byte[] bArr = new byte[5];
        boolean[] zArr = new boolean[5];
        String[] strArr = new String[5];

        System.out.println("short 数组类别：" + sArr.getClass());
        System.out.println("int 数组类别：" + iArr.getClass());
        System.out.println("long 数组类别：" + lArr.getClass());
        System.out.println("float 数组类别：" + fArr.getClass());
        System.out.println("double 数组类别：" + dArr.getClass());
        System.out.println("byte 数组类别：" + bArr.getClass());
        System.out.println("boolean 数组类别：" + zArr.getClass());
        System.out.println("String 数组类别：" + strArr.getClass());
    }
}
```

使用 toString() 来显示数组对象的类别名称描述时，会以 "class [" 作为开始，之后跟随着一个型态表示字符，执行结果如下所示：

    short 数组类别：class [S
    int 数组类别：class [I
    long 数组类别：class [J
    float 数组类别：class [F
    double 数组类别：class [D
    byte 数组类别：class [B
    boolean 数组类别：class [Z
    String 数组类别：class [Ljava.lang.String;

要使用反射机制动态生成数组的话，可以使用 java.lang.reflect.Array 来协助，范例 16.23 简单的示范了如何生成 String 数组。

#### **范例 16.23  NewArrayDemo.java**
```java
package onlyfun.caterpillar;

import java.lang.reflect.Array;
 
public class NewArrayDemo {
    public static void main(String[] args) {
        Class c = String.class;
        Object objArr = Array.newInstance(c, 5);
        
        for(int i = 0; i < 5; i++) {
            Array.set(objArr, i, i+"");
        }
        
        for(int i = 0; i < 5; i++) {
            System.out.print(Array.get(objArr, i) + " ");
        }
        System.out.println();

        String[] strs = (String[]) objArr;
        for(String s : strs) {
            System.out.print(s + " ");
        }
    }
}
```

Array.newInstance() 的第一个参数是指定元素型态，而第二个参数是用来指定数组长度，执行结果如下：

    0 1 2 3 4
    0 1 2 3 4

Array.newInstance() 还有另一个版本，可用于建立二维数组，只要用一个表示二维数组的两个维度长度的 int 数组，传递给第二个参数，范例 16.24 是个简单示范。

#### **范例 16.24  NewArrayDemo2.java**
```java
package onlyfun.caterpillar;
 
import java.lang.reflect.Array;
 
public class NewArrayDemo2 {
    public static void main(String[] args) {
        Class c = String.class;
        
        // 打算建立一个3*4数组
        int[] dim = new int[]{3, 4};
        Object objArr = Array.newInstance(c, dim);
        
        for(int i = 0; i < 3; i++) {
            Object row = Array.get(objArr, i);
            for(int j = 0; j < 4; j++) {
                Array.set(row, j, "" + (i+1)*(j+1));
            }
        }
        
        for(int i = 0; i < 3; i++) {
            Object row = Array.get(objArr, i);
            for(int j = 0; j < 4; j++) {
                System.out.print(Array.get(row, j) + " ");
            }
            System.out.println();
        }
    }
}
```

执行结果如下：

    1 2 3 4
    2 4 6 8
    3 6 9 12

如果想要得知数组元素的型态，可以在取得数组的 Class 实例之后，使用 Class 实例的 getComponentType() 方法，所取回的是元素的 Class 实例，例如：

    int[] iArr = new int[5];
    System.out.println(iArr.getClass().getComponentType());

### 16.2.5 Proxy 类别

Java 在 J2SE 1.3 之后加入 java.lang.reflect.Proxy 类别，可协助您实现动态代理功能，举个实际应用的例子，假设今天您打算开发一个 HelloSpeaker 类别，当中有一个 hello() 方法，而您想要在这个 hello() 呼叫前后加上记录（log）的功能，但又不想将记录的功能写到 HelloSpeaker 类别中，这时您可以使用 Proxy 类别来实现动态代理。
要实现动态代理，首先要定义所要代理的接口，范例 16.25 为定义了有 hello() 方法的 IHello 接口。

#### **范例 16.25 IHello.java**
```java
package onlyfun.caterpillar;

public interface IHello {
    public void hello(String name);
}
```

您的 HelloSpeaker 类别实现了 IHello 接口，如范例 16.26 所示。

#### **范例 16.26  HelloSpeaker.java**
```java
package onlyfun.caterpillar;

public class HelloSpeaker implements IHello { 
    public void hello(String name) { 
        System.out.println("Hello, " + name); 
    } 
}
```

您可以实作一个处理记录（log）的处理者（Handler），让处理者在呼叫 hello() 方法的前后进行记录的动作，一个处理者必须实现 java.lang.reflect.InvocationHandler 接口，InvocationHandler 有一个 invoke() 方法必须实现，范例 16.27 是个简单的实现。

#### **范例 16.27  LogHandler.java**
```java
package onlyfun.caterpillar;

import java.util.logging.*; 
import java.lang.reflect.*; 

public class LogHandler implements InvocationHandler { 
    private Logger logger = 
               Logger.getLogger(this.getClass().getName()); 
    private Object delegate; 

    // 绑定要代理的对象
    public Object bind(Object delegate) { 
        this.delegate = delegate;
        // 建立并传回代理对象
        return Proxy.newProxyInstance(
                 delegate.getClass().getClassLoader(),
                 // 要被代理的接口
                 delegate.getClass().getInterfaces(), 
                 this); 
    }

    // 代理要呼叫的方法，并在其前后增加行为
    public Object invoke(Object proxy, 
                         Method method, 
                         Object[] args) throws Throwable {
        Object result = null; 
        try { 
            logger.log(Level.INFO, 
                         "method starts..." + method.getName()); 
            result = method.invoke(delegate, args); 
            logger.log(Level.INFO, 
                         "method ends..." + method.getName()); 
        } catch (Exception e){ 
            logger.log(Level.INFO, e.toString()); 
        } 
        return result; 
    } 
}
```

主要的概念是使用 Proxy.newProxyInstance() 方法建立一个代理对象，建立代理对象时必须告知所要代理的操作接口，之后您可以操作所建立的代理对象，在每次操作时会呼叫 InvocationHandler 的 invoke() 方法，invoke() 方法会传入被代理对象的方法名称与执行自变量，实际上要执行的方法交由 method.invoke()，您在 method.invoke() 前后加上记录动作，method.invoke() 传回的对象是实际方法执行过后的回传结果，先从范例 16.28 来看看一个执行的例子。

#### **范例 16.28  ProxyDemo.java**
```java
package onlyfun.caterpillar;

public class ProxyDemo {
    public static void main(String[] args) {
        LogHandler handler  = new LogHandler(); 
        IHello speaker = new HelloSpeaker();

        // 代理speaker的对象
        IHello speakerProxy = 
                 (IHello) handler.bind(speaker);

        speakerProxy.hello("Justin");        
    }
}
```

执行结果如下：

    2005/6/4 上午 09:39:11 onlyfun.caterpillar.LogHandler invoke
    信息: method starts...hello
    Hello, Justin
    2005/6/4 上午 09:39:11 onlyfun.caterpillar.LogHandler invoke
    信息: method ends...hello

透过代理机制，在不将记录动作写入为 HelloSpeaker 类别程序代码的情况下，您可以为其加入记录的功能，这并不是什么魔法，只不过是在 hello() 方法前后由代理对象 speakerProxy 先执行记录功能而已，而真正执行 hello() 方法时才使用 speaker 对象。

> **良葛格的话匣子** 这边的例子是「Proxy 模式」的实现，您可以进一步参考：
> 
> - [Proxy 模式（一）](http://openhome.cc/Gossip/DesignPattern/ProxyPattern.htm)
> - [Proxy 模式（二）](http://openhome.cc/Gossip/DesignPattern/ProxyPattern2.htm)

## 16.3 接下来的主题

每一个章节的内容由浅至深，初学者该掌握的深度要到哪呢？在这个章节中，对于初学者我建议至少掌握以下几点内容：

- 了解 Class 实例与类别的关系
- 会使用 Class.forName() 加载类别并获得类别信息
- 会使用 Class 建立实例
- 会使用反射机制呼叫对象上的方法

下一个章节要来介绍 J2SE 5.0 中新增的 Annotation 功能，Annotation 是 J2SE 5.0 对 metadata 的支持，metadata 简单的说就是「数据的数据」（Data about data），您可以使用 Annotation 对程序代码作出一些说明，以利一些程序代码分析工具来使用这些信息。



