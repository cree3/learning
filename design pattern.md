
## [设计原则](http://www.uml.org.cn/sjms/201211023.asp)
- 单一职责原则：一个类只负责一项职责
- 依赖倒转原则：使用接口或者抽象类的目的是制定好规范和契约，而不去涉及任何具体的操作，把展现细节的任务交给他们的实现类去完成
- 里氏替换原则：子类可以扩展父类的功能，但不能改变父类原有的功能。
- 接口隔离原则：为各个类建立专用的接口，而不要试图去建立一个很庞大的接口供所有依赖它的类去调用
- 开闭原则：类、模块和函数应该对扩展开放，对修改关闭
- 迪米特原则：每个对象都会与其他对象有耦合关系。耦合的方式有依赖、关联、组合、聚合等。陌生的类最好不要作为局部变量的形式出现在类的内部。
### 1.  适配模式
[适配器模式详解](http://www.runoob.com/design-pattern/adapter-pattern.html)

**意图**：适配器继承或依赖已有对象，实现想要的目标接口


**举例**：美国电器 110V，中国 220V，就要有一个适配器将 110V 转化为 220V

**优点**： 
1、可以让任何两个没有关联的类一起运行。
2、提高了类的复用。 3、增加了类的透明度。 4、灵活性好。 

**缺点**：过多地使用适配器，会让系统非常零乱，不易整体进行把握。比如，明明看到调用的是 A 接口，其实内部被适配成了 B 接口的实现

**实现**：有一个 MediaPlayer 接口和一个实现了 MediaPlayer 接口的实体类 AudioPlayer。默认情况下，AudioPlayer 可以播放 mp3 格式的音频文件。

我们还有另一个接口 AdvancedMediaPlayer 和实现了 AdvancedMediaPlayer 接口的实体类。该类可以播放 vlc 和 mp4 格式的文件。

我们想要让 AudioPlayer 播放其他格式的音频文件。为了实现这个功能，我们需要创建一个实现了 MediaPlayer 接口的适配器类 MediaAdapter，并使用 AdvancedMediaPlayer 对象来播放所需的格式。

AudioPlayer 使用适配器类 MediaAdapter 传递所需的音频类型，不需要知道能播放所需格式音频的实际类。AdapterPatternDemo，我们的演示类使用 AudioPlayer 类来播放各种格式。

![适配器模式类图](https://github.com/cree3/learning/blob/picture/adapter_pattern_uml_diagram.jpg)

### 2.  工厂模式
[工厂模式详解](http://www.runoob.com/design-pattern/service-locator-pattern.html)

**意图**：定义一个创建对象的接口，让子类自己决定实例化哪个工厂类

**举例**：Hibernate 换数据库只需换方言和驱动就可以

**优点**：1、一个调用者想创建一个对象，只要知道其名称就可以了。 2、扩展性高，如果想增加一个产品，只要扩展一个工厂类就可以。 3、屏蔽产品的具体实现，调用者只关心产品的接口。


**缺点**：每次增加一个产品时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂度，同时也增加了系统具体类的依赖。

**实现**：![工厂类类图](https://github.com/cree3/learning/blob/picture/factory_pattern_uml_diagram.jpg)
### 3. 抽象工厂例模式
**抽象工厂 VS 简单工厂**：
抽象工厂有多个工厂且工厂里有多个生产线；
简单工厂里一个工厂一条生产线
![抽象工厂类图](https://github.com/cree3/learning/blob/picture/abstractfactory_pattern_uml_diagram.jpg)
### 4.  状态模式
[状态模式详解](http://www.runoob.com/design-pattern/state-pattern.html)

**意图**：类的行为是基于它的状态改变的

**举例**:打篮球的时候运动员可以有正常状态、不正常状态和超常状态

**优点**: 1、封装了转换规则。 2、枚举可能的状态，在枚举状态之前需要确定状态种类。 3、将所有与某个状态有关的行为放到一个类中，并且可以方便地增加新的状态，只需要改变对象状态即可改变对象的行为。 4、允许状态转换逻辑与状态对象合成一体，而不是某一个巨大的条件语句块。 5、可以让多个环境对象共享一个状态对象，从而减少系统中对象的个数。

**实现**：
![image](https://github.com/cree3/learning/blob/picture/state_pattern_uml_diagram.jpg)
### 5.  单例模式
**注意**：
- 1、单例类只能有一个实例。
- 2、单例类必须自己创建自己的唯一实例。
- 3、单例类必须给所有其他对象提供这一实例。

**意图**：保证一个类仅有一个实例，并提供一个访问它的全局访问点。
**举例**：设备管理器常常设计为单例模式，比如一个电脑有两台打印机，在输出的时候就要处理不能两台打印机打印同一个文件。 

**优点**
- 1、在内存里只有一个实例，减少了内存的开销，尤其是频繁的创建和销毁实例。
- 2、避免对资源的多重占用（比如写文件操作）。

**缺点**：没有接口，不能继承，与单一职责原则冲突，一个类应该只关心内部逻辑，而不关心外面怎么样来实例化。

**实现方式**
- 懒汉式，线程不安全
```
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}  
  
    public static Singleton getInstance() {  
    if (instance == null) {  
        instance = new Singleton();  
    }  
    return instance;  
    }  
} 
```
- 懒汉式，线程安全
```
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}  
    public static synchronized Singleton getInstance() {  
    if (instance == null) {  
        instance = new Singleton();  
    }  
    return instance;  
    }  
} 
```
- 饿汉式，线程安全
```
public class Singleton {  
    private static Singleton instance = new Singleton();  
    private Singleton (){}  
    public static Singleton getInstance() {  
    return instance;  
    }  
}  
```
- 双重校验锁，线程安全

```
public class Singleton {  
    private volatile static Singleton singleton;  
    private Singleton (){}  
    public static Singleton getSingleton() {  
    if (singleton == null) {  
        synchronized (Singleton.class) {  
        if (singleton == null) {  
            singleton = new Singleton();  
        }  
        }  
    }  
    return singleton;  
    }  
}  
```

- 静态内部类，线程安全

```
public class Singleton {  
    private static class SingletonHolder {  
    private static final Singleton INSTANCE = new Singleton();  
    }  
    private Singleton (){}  
    public static final Singleton getInstance() {  
    return SingletonHolder.INSTANCE;  
    }  
} 
```

- 枚举，线程安全

```
public enum Singleton {  
    INSTANCE;  
    public void whateverMethod() {  
    }  
}  
```

### 6.  MVC模式
- Model（模型） - 模型代表一个存取数据的对象或 JAVA POJO。它也可以带有逻辑，在数据变化时更新控制器。
- View（视图） - 视图代表模型包含的数据的可视化。
- Controller（控制器） - 控制器作用于模型和视图上。它控制数据流向模型对象，并在数据变化时更新视图。它使视图与模型分离开。


**实现**：创建一个作为模型的 Student 对象。StudentView 是一个把学生详细信息输出到控制台的视图类，StudentController 是负责存储数据到 Student 对象中的控制器类，并相应地更新视图 StudentView。
![image](https://github.com/cree3/learning/blob/picture/mvc_pattern_uml_diagram.jpg)
