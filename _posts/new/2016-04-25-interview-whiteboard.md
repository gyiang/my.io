---

layout: post
title: Interview resources
category: 资源
tags: java,interview
description: java研发面试所需

---

- **update at 15/04/25** java
- **update at 15/04/28** 合并db


## Java基础

### 1 java与c/c++异同

- 解释型语言，C++编译型。
- 纯面向对象，除基本数据类型，所有类型都是类。
- 无指针，更安全。
- 不支持多重继承。
- 提供垃圾回收器.(finalize)
- 不支持自动强制类型转换。
- 平台无关性。
- 提供对注释文件的内建支持。


### 2 main()

- 必须public（任何类和对象可以访问） static（存储在静态存储区）
- 返回值必须 void
- 可以用final、synchronized修饰
- 只有与文件名相同类的main是入口

### 3 初始化顺序
当实例化对象时，只有所有类成员完成初始化，才会调用所在类的构造函数创建对象。

父类Ｂ静态代码块->子类Ａ静态代码块->父类Ｂ非静态代码块->父类Ｂ构造函数->子类Ａ非静态代码块->子类**Ａ构造函数**

- 静态代码块是随着类的创建而执行，所以父类静态代码块最先被执行
- 实例化子类对象要先调用父类的构造方法
- 调用父类构造方法前会先执行父类的非静态代码块
- 初始化静态成员变量和静态代码块时按照在程序中出现的顺序初始化


### 4 java文件中定义多个类

- 最多只能一个类被public修饰，且类名与文件名相同
- 无public时候，文件名随便是一个类的名字
- javac会对每个类生成.class

### 5 构造函数

用于在实例化时初始化对象的成员变量

- 构造函数必须与类名相同
- 不能有返回值
- 构造函数的参数可以为0
- 总伴随new操作一起调用，不能被其他方式调用，必须系统调用
- 默认构造器的修饰符只跟当前类的修饰符有关

### 6 标识接口

- 充当标识作用，仅用来表明属于特定类型
- 如Cloneable、Serizlizable等，常用instanceof来判断

### 7 参数传递

- 值传递：基本数据类型（int、char、double），传递的是输入**参数的复制**，因此方法中的改变参数的值，不会影响方法外
- 引用传递：其他类型的传递，引用类型传递的是对象的**地址**，指向了对象实例，对象在函数调用、“=”赋值都采用引用传递
- 使用clone方法复制对象
- 实现clone的类需要继承Cloneable接口，重写Object中的clone方法，在clone方法中调用super.clone()，并把浅复制（被复制对象所有变量都含有与原来对象相同的值所有对象引用指向原来对象）的引用指向原型对象新的克隆体，实现深复制（把复制对象所引用的对象也复制一遍）

### 8 反射机制

- 允许程序运行时候进行自我检查，并允许对内部成员进行操作
- 功能：得到一个对象所属的类；获取一个类的所有成员变量和方法；**在运行时创建对象**；在运行时调用对象的方法
- Class.forName("C").newInstance()

### 9 创建对象的方法

- new语句实例化
- 反射机制
- clone（）方法
- 反序列化

### 10 实现类似C函数指针功能

- 回调函数：指针函数先注册，将在稍后某个需要的时候被调用。
- 在java中利用接口与类实现。先定义接口，并声明要调用的方法，实习接口，把实现类的一个对象作为参数传递给调用程序，调用程序通过参数开调用指定的函数。

### 11 面向对象的特征

- 抽象，数据和过程抽象，忽略与主题无关的方面
- 继承，派生类可以从基类获得方法和实例变量，并且可以修改或增加新方法，代码复用方式，提高复用性和开发效率。（注意和组合的区别），is-a关系
- 封装，隐藏实现，只公开对外接口，隐藏其具体实现，通过访问控制实现（通过用Public将信息暴露，Private，Protected将信息隐藏）
- 多态，允许不同类的对象对同意消息做出响应,**同一消息可以根据发送对象的不同而采用多种不同的行为方式**。（发送消息就是函数调用）。

### 12 多态的实现机制

- 覆盖(override)，子类重写了**父类**的同名方法，子类覆盖父类的方法，**方法名相同，参数类型相同**，返回类型和抛出异常要<=父类，访问权限要>=父类（两同两小一大原则）基类的方法不能为private（否则子类只是自己定义了方法），**运行时多态**（基类引用可以指向基类也可以指向子类的实例变量，程序调用的方法在运行期才动态绑定，引用变量指向具体的实例对象方法，在内存中的方法）
- 重载(overload)，指在**同一个类中**，允许存在多个同名方法，而这些方法的参数表不同（**个数**或**参数类型**不同，方法的返回类型、修饰符可以相同，也可不同），**编译时多态**（因为参数列表不同，编译时候确定）

### 13 抽象类和接口

- 抽象类：含有抽象方法，声明为abstract（只能修饰类和方法，不可以修饰属性）
- 接口：方法的集合，所有方法都没有方法体，声明为interface，成员变量全部是static final。
- 抽象类和接口**都不能被实例化**。
- 接口强调特定功能的实现，设计理念是“has-a”关系，抽象类是“is-a”
- 接口定义的成员变量默认为public static final，必须赋初值且不可修改，方法成员都是public abstract的，且只能被这两个关键词修饰
- 抽象类默认成员变量为defaultt(本包可见)，可以定义private、protected、public，成员变量可以在子类中被重新定义，也可以被重新赋值。抽象类中的抽象方法（abstract修饰）不能用private、static、synchronized、native等访问修饰符修饰，方法以分号结尾，不带{}。
- 当功能需要累积时，用抽象类；不需要累积时，用接口。
- 接口是一种特殊的抽象类，接口中的方法全部是抽象方法，接口中的方法只能是public和default

### 14 命名规则

- 只能字母（a~z，A~Z）、数字（0~9）、下划线（_）和$
- 第一个字母不能是数字

### 15 break、continue、return

- break 强制跳出当前循环，使用标识符+":",跳出多重循环
- continue 停止当此循环，回到循环起始处，进入下一次循环，也可以多重循环
- return 从一个方法返回，返回到调用的地方

### 16 final、finally、finalize

- **final**方法：不允许重写，final参数：参数在函数内部不允许修改，final类：不能被继承，所有方法不可重写。
final指的是**引用不可变**，指向初始时指向的那个对象，不关心所指对象的内容变化，被**final修饰的变量必须初始化**。可以在定义、初始化块（不可以在静态初始化块中初始化，静态final成员变量可以在静态初始化块中但不可在初始化块中）、在类的构造器中（静态final不可以）
- **finally**：异常处理中的finally必须在函数退出前执行，无论如何finally语句都要执行。try中没有异常时，但是有return等跳转语句，这样会引发程序控制流离开当前的try,自动完成finally中资源的释放。try中有异常时，**catch在获取到异常之前，进行finally执行，接着执行catch中的语句**
- **finalize**是Object的方法，在垃圾回收器执行前，会调用被回声对象的finalize（）方法，可以覆盖这个方法实现对资源的回收

### 17 static

- 为某特定数据类型或对象分配单一的存储空间，而与创建的个数无关
- 实现方法或属性与类而不是对象关联在一起（通过类直接调用或使用类的属性）
- static成员变量：全局效果，静态变量属于类，在内存中只有一个复制
- static成员方法：static方法是类方法，不需要创建就可以调用，static方法中不可以this、super，不能调用非static方法，只能访问所属类静态变量和成员方法
- static代码块，JVM在加载时候会执行static代码块，用来初始化静态变量，只会被执行一次
- 用来实现单例模式，隐藏构造函数（设为private）
- static final：全局常量

### 18 volatile

- 修饰被不同线程访问和修改的变量，让其每次从对应的内存中读取，而不是缓存
- 所有线程在任何时刻看到的变量值都是相同的
- private volatile Boolean flag

### 19 instanceof

- 二元操作符
- 判读一个引用类型的变量所指的对象是否是一个类（或接口、抽象类、父类）的实例
- object instanceof class

### 20 strictfp

- strict float point 精确浮点关键字
- 确保浮点运算的准确性
- 不同平台结果也一致

### 21 基本数据类型

基本类型四类八种，其余全是引用类型

- 整数：byte（8 bit） short（16） int（32） long（64）
- 浮点数：float（32） double（64）
- 字符型：char（16）
- 逻辑性：boolean（true flase）

- 封装类型，默认null（Character、Boolean、Byte、Short、Integer、Long、Float、Double）
- 原始数据类型值传递，封装类型引用传递
- float初始化1.0f 或 f=（float）1.0， f=3.4是错的

### 22 不可变类

- 创建实例后，不允许修改值
- 所有基本类型的包装类都是不可以变类（Integer）
- String 不可变类

### 23 强制类型转换

- 涉及byte、short、char类型运算会强转为int类型，最后结果也是int
- short s1=（short）s0+1

### 24 char存储中文汉字

- java默认是Unicode编码，每个字符占用2个字节
- String由char组成，更灵活，英文占用1个字符，中文占用2个字符

### 25 字符串创建于存储机制

- new String("abc"),只要new总会生成新对象
- String s1="abc", String s2="abc" ,JVM存在常量池，共享使用
- 现在常量池中是否有相同的字符串被定义，如果存在，直接获取对其引用，不需要创建，如果没有定义，先创建，加入到常量池，在返回引用

### 26 ==与equals

- “==”比较两个变量值是否相等，比较的是内存中所有存储的数值，比较两个基本类型的数据或者两个引用变量是否相等。
- equals，在没覆盖的情况下，equals=“==” 
- 通过覆盖equals让其比较引用而不是比较数据内容
- s1=new String("Hello") s2=new String("Hello") s1和s2引用地址不同，内容相同，用“==”不可以比较，String方法重写了equals方法，比较两个独立对象的内容是否相同。
- hashCode（）方法从Object继承而来，鉴定两个对象是否相等。返回值是对象在内存中地址转换为一个int值，任何对象的hashCode方法不同（没重写的情况）
- 覆盖equals方法时候也覆盖hashCode


### 27 String、StringBuffer、StringBuilder和StringTokenizer

- Character单个字符操作
- String不可变类（一旦创建，值不可以改），StringBuffer可变类
- 当用String类型对字符串修改时，实现方法也是调用了StringBuffer（append等），最后to_string
- StringBuilder非线程安全、StringBuffer线程安全
- 执行效率方面：StringBuilder>StringBuffer>String
- 数据量小选择String，单线程大量操作：StringBuilder，多线程下大量数据：StringBuffer
- StringTokenizer用来分割字符串的工具=new StringTokenizer("Hello to")

### 28 try中return

- try-finally或者catch-finally中都有return，finally中的return语句会覆盖别处return语句，**最终返回**到调用者那里的是finally中return的值
- return在返回时，不是直接返回变量的值，而是**复制一份**，然后返回（）
- finally块中改变return的基本类型的值对返回值没有任何影响，而对引用类型的数据有影响try{r=2;return r}catch(EXception ex){}finally{r=3} ，返回2

### 29 运行时异常和普通异常

- 两种异常类，**Error和Excetion**，共同父类是Trowable
- Error表示在运行期出现了非常严重的错误，**该错误不可恢复**，JVM层次大错误，导致程序终止执行，编译器不会检查Error是否被处理，程序不推荐捕获Error类异常，运行时异常多是逻辑错导致的，属于应该解决的问题，OutOfMemoryError、ThreadDeath等
- Exception表示可以恢复的异常，是编译器可以捕获的，包含两种类型：检查异常（Checked exception）和运行时异常（runtime exception）
- （检查异常）：所有继承Exception非运行时的都是，在编译阶段，编译器强制程序去捕获此类一次。如IO、SQL
- （运行时异常）：如果不处理，由JVM处理，NullPointerException、ClassCastException、ArraryindexOutofBoundExcpetion、BufferOverflowExcetion、ArithmeticException等
- 出现运行时异常后，系统会把异常一直往上层抛出，直到遇到处理代码为止，多线程用Thread.run()抛出，单线程用main（）抛出。线程退出，主程序异常则程序退出

### 30 IO流实现机制

- 流的本质是数据传输，分为两类：字节流和字符流
- 字节流（8 bit）：InputStream、OutputStream
- 字符流（16 bit）：根据码表映射字符，一次可读多个字节，Reader和Writer，处理输入输出的时候用缓存
- IO类设计采用De
- ator装饰者模式

### 31 Socket

- 基于TCP的通信过程：Server端Listen指定的某个端口（>1024）是否有连接请求,Client端向Server端发出Connect（连接）请求，Server端向Clinet端发回Accept（接受）消息。一个连接建立，会话产生，Server端和Client端通过send和write等方法与对方通信
- ···代码···

### 32 NIO

- NIO：Nonbloking IO,非阻塞IO
- Socket阻塞导致大量线程的上下文切换，效率低
- NIO通过Selector、Channel和Buffer来实现非阻塞IO操作
- NIO非阻塞实现主要采用了Reactor（反应器）设计模式，与Observer（观察者）模式类似，O只处理一个事件源，R可以出来多个事件源
- Channel双向非阻塞的通道，通道两边进行数据读写操作
- Selector实现用一个线程来管理多个通道，类似观察者。将要处理的Channel的IO事件（connect、read、write）注册给Selector。内部实现原理：对所有注册的Channel进行轮询访问，一旦轮询到Channel 1一个注册事件发生，通过SelectionKey方式通知开发人员对Channel1进行数据的读或写操作
- Key封装一个特定Channel 1和一个特定Selector之间的关系，
- 通过轮询方式处理多线程请求时不需要上下文切换，NIO较高的执行效率
- Buffer用来保存数据，可以存Channel1读取的数据，也可以存放使用Channel1进行发送的数据。 ByteBuffer、CharBuffer

### 33 序列化

- 在分布式环境下，当进行远程通信时候，无论是何种类型的数据，都会以**二进制序列的形式在网络上传送**。 序列化是一种将对象以一连串的字节描述的过程，用于解决在对对象流进行读写操作时所引发的问题。序列化可以将对象的状态写在流里进行网络传输，或者保存到文件、数据库等系统容，并在需要时把该流读取出来重新构造一个相同的对象。
- 实现Srializable接口（java.lang）
- 使用输出流（FileOutputStream）来构造一个ObjectOutputStream（对象流）对象
- 使用该对象的writeObject（Object obj）将obj对象写出（即保存其状态），要恢复时，使用对应的输入流
- static（静态）代表类的成员、transient 代表对象的临时数据，不能序列化
- java提供多个对象序列化接口，包括OnjectOutput、ObjectInput、ObjectOutputStream、ObjectInputStream
- 序列化使用会影响系统性能（网络发生、深复制时候用）
- 反序列化：将流转换我对象
- serialVersionUID判定类兼容性，显示声明，提高运行效率、不同平台兼容性、版本兼容性
- 


### 34 java平台独立性

- 中间码，java虚拟机。由JVM负责把“中间码”翻译成硬件平台能执行的代码
- 字节码执行方式：编译方式与解释执行（每次解释并执行一小段代码）方式


### 35 JVM加载class文件
- 由类加载器完成
- 隐式加载：new 显式加载：class.forName把需要的类加载到JVM中
- 类的加载时动态的，并不会一次性把所有类全部加载后再执行，只加载基础类
- Bootstrap Loader 负责加载**系统**类（jre/lib/rt.jar）
- ExtClass Loader 负责加载**扩展**类(jar/lib/ext/*.jar)
- AppClassLoader 负责加载**应用**类 (classpath指定目录或jar中的类)  
- 通过委托方法实现类加载，但需要类加载时，请求父类载入，父类会使用其自己的搜索路径来搜索需要被载入的类，如果搜索不到，才会由子类按照其搜索路径来搜索待加载的类
- 类加载主要步骤：（1）**装载**，根据查找路径找到对应的class文件然后导入（2）**链接**，可以分为3步骤：（检查）检查待加载文件的正确性，（准备）给类中的静态变量分配存储空间，（解析）将符号引用转换为直接引用 （3）**初始化**，对静态变量和静态代码块执行初始化工作

### 36 GC
 
- 分配内存、确保被引用对象的内存不被错误地回收
- 使用有向图来记录和管理堆内存中的所有对象，通过这个有向图可以识别哪些对象是“可达的”（有引用变量引用它就是“可达的”）

GC算法：

-  引用计数算法（Reference Counting Collerctor）：简单效率低，原理：堆中每个对象都有1个引用计数器，被引用+1，引用置空或离开作用域-1，但是无法解决相互引用问题。
-  追踪回收算法（Tracing Colletor）：利用JVM的对象图引用，从根结点开始遍历对象的应用图，同时标记遍历的对象。当遍历结束，未被标记的对象就是目前已不被使用的对象，可以被回收。
-  压缩回收算法（Compacting Colletor）：把堆中活动的对象移动到堆中一端，这样就会在堆中另外一端留出很大的一块空闲区域，相当于对堆中的碎片进行了处理。大大简化消除堆碎片的工作，但是每次处理都带来性能损失。
-  复制回收算法（Coping Colletor）：把堆分成两个大小相同的区域，在任何时刻，只有其中的一个区域被使用，知道这个被消耗为止，此时垃圾回收器会中断程序的执行，通过变量的方式吧所有活动的对象复制到另一个区域中，在复制的过程中它们你是紧挨着布置的，从而可以消除内存碎片。但是这也付出了很高的代价：对于指定大小的堆来说，需要两倍大小的内存空间，而且内存调整过程要中断程序的执行，影响效率按
-  代回收算法（Cenerational Colletor）：“程序创建的大部分对象的生命周期都很短，只有一部分对象有较长的生命周期”，把堆分成两个或多个子堆，每个子堆被视为一代。算法在运行的过程优先收集那些“年幼”的对象，如果一个对象经过多次收集仍然“存活”，那么久把这个对象转移到高一级的堆里，减少对其扫描次数。


- 成为垃圾的对象，只要在下次垃圾回收器运行时才会被回收，而不是马上被清理。
- 开发人员并不能实时的调用垃圾回收器对对象进行回收，System.gc()通知垃圾回收器运行。
- 不推荐频繁System.gc()，会停止所有响应，去检查是否有可回收的对象，对正在运行和性能影响很大。   


### 37 java内存泄漏

- 指不再被程序使用的对象或变量还在内测中占有存储空间
- 判断内存空间是否可以符合回收：（1）给对象赋予过空值null，以后再也没使用过（2）给对象赋予了新指，重新分配内存空间。
- 内存泄漏情况:（1）堆中申请的空间没有被释放（gc可以解决）（2） 对象不再被使用，但还仍然在内存中保留着

引起内存泄漏的原因：

- 静态集合类（eg.HashMap、Vector），容器为静态，生命周期与程序一致，容器中的对象在程序结束之前不能被释放
- 各种连接(eg.数据库连接，网络连接，IO)，只有显式close了才能被回收
- 监听器，释放对象的时候，没有删除对应的监视器
- 变量不合理的作用域，定义范围大于使用范围，造成内存泄漏，没有及时把对象设置为null

### 38 堆和栈

- 栈：**基本数据类型的变量**以及**对象的引用变量**（堆中对象内存的首地址），内存分配在栈上。变量出了作用域会自动释放，通过压栈和弹栈方式来操作完成，以栈帧为基本单位来管理程序的调用关系。栈主要用来执行程序。
- 堆：存放运行时创建的对象，通过new方式创建，每个实例唯一对应一个堆，多线程运行在一个JVM实例上，线程之间共享堆内存（多线程在访问堆中的数据时需要对数据进行同步）。存储引用类型的变量，其内存分配在堆上或者常量池（字符串常量和基本数据类型常量）。

### 39 Java Collections框架

- Collection接口:List、Queue、Set、Stack
- Set：集合，不重复。实现：TreeSet（有序）、SortedSet
- List：有序的COllection，保存进入顺序，实现：LinkedList、ArrayList、Vector
- Map接口：HashMap（基于散列表，采用对象HashMap）、TreeMap（基于红黑树，内部按需排列）、LinkedHashMap、WeakHashMap、IdentityHashMap


### 40 迭代器Iterator

- Iterator：遍历并选择序列中的对象，提供访问方法又不必暴露对象内部细节方法
- 容器的iterator（）返回Iterator，通过next方法遍历
- Iterator的hasNext方法判断是否有元素，remove删除
- ListItrator继承自Iterator，专门针对List，可以两个方法变量List，支持元素修改
- ConcurrentModificationException：在遍历时候，对容器做增加和删除操作或者由于多线程操作导致。在遍历的过程把要删除的对象保存到一个集合中，等遍历后用removeAll（）方法删除，或者使用iter.remove()方法
- 多线程中，JDK1.5引入线程安全的容器，比如ConcurrentHashMap、CopyOnWriteArrayList,或者遍历时候对容器的操作放到synchroized代码块中，但是并发程序比较高时，严重影响性能

### 41 ArrayList、Vector、LinkedList

- java.util包中
- ArrayList、Vector基于存储元素的Object[] array，连续空间存储，有初始化容量，自动扩充，Vector默认扩充2倍（扩充空间可设置），ArrayList默认扩充1.5倍（不可设）
- ArrayList线程不安全，Vector线程安全（性能差）
- LinkedList双向链表，对数据的索引从列表头开始遍历，随机访问效率低插入效率高，**非安全**


### 42 HashMap、HashTable、TreeMap、WeakHashMap

- Map的接口实现（java.util.Map）
- HashTable和HashMap的hash/rehash算法几乎一样，性能差异不大
- HashMap是HashTbale的轻量级实现（非线程安全），HashMap运行null的键
- HashMap不使用contans方法，使用containsValue和containsKey
- HashTable继承自Dictionary类，HashMap是Map接口实现
- HashTable方法线程安全，HashMap不支持线程同步（在多线程时候，额外同步机制）
- HashTable使用Enumeration、HashMap使用Iterator
- HashTbal的hash数组默认11（old*2+1）、HashMap默认16（一定是2的指数）
- hash值的使用不同，HashTable直接使用对象的hashCode
- TreeMap实现的SortMap接口，能够保存记录根据键排序，取出来的是排序后的键值对
- LinkedHashMap是HashMap的子类。输出顺序和输入顺序相同，可以按读取顺序来排列
- WeakHashMap与HashMap类似，键是“弱引用”，当key不再被外部引用，GC可以回收。（HashMap需要key删除）
- HashMap可以荣光Map m=Collections.syschronizedMap(new HashMap())方式达到同步（在一个时间点只能有一个线程可以修改hash表）效果，该方法返回一个同步的Map，该Map封装了底层的HashMap的所有方法，使得底层的HashMap即使是多线程的环境也是安全的。
- HashMap中，添加key时候，先调用key的hashCode方法生成一个hash值h1，如果h1在HashMap中已经存在，找出所有key，然后equals()方法返回true，说明已经存在，那么HashMap会使用新的value值覆盖旧的value，返回false说明不存在key，创建映射关系。HashMap采用链地址法纪解决冲突。
- 使用自定义HashMap的key时候，要重写hashCode方法和equals方法

### 43 多线程

- 进程：一段正在执行的程序，在操作系统级别上的单位
- 线程：程序执行过程中，能够执行程序代码的一个执行单元，轻量级进程。各个线程之间共享程序的内存空间（代码段、数据段和堆空间）以及一些进程级的资源（打开的文件），各个线程拥有自己的栈空间。线程的创建和切换开销更小，数据共享方面效率高，提高CPu的利用率，简化程序的结构
- （在java中）线程有4中状态：运行、就绪、挂起、结束


### 44 同步和异步

- 同步：数据共享问题（当多个线程需要访问同一个资源时），保证资源的安全（某一时刻只能被一个线程使用）。需要获得每一个对象的锁（访问互斥资源的代码块），并且在这个锁被释放之前，其他线程就不能再进入这个临界区。**Synchronized**关键字实现同步，很大的系统开销。同步：利用同步代码库，利用同步方法
- 异步：与非阻塞类似。每个线程都包含了运行时自身所需要的数据或方法，不必关系其他线程的状态或行为
- 举个例子：同步就是你喊我去吃饭，如果听到了，我就和你去吃饭，如果我没有听到，你就不停的喊，知道我告诉你听到了，然后一起去吃。异步就是你喊我，然后自己去吃饭，我得到消息后可能立即走，也可能等到下班次才去吃饭。

### 45 Java实现多线程

- 继承Thread类，重写run（）方法。Thread本质上实现了Runnable接口的一个实例，启动方式通过start（）方法，调用后，不是立即持续多线程的代码，而是该线程变为可运行态（Runnable），什么时候运行多线程代码是由操作系统决定的。
- 实现Runnable接口，并试下该接口的run（）方法。 **Thread t=new Thread(thread implements Runnable)**，t.start();
- 实现Callable接口，重写call（）方法，属于Executor框架中的功能类，Callable可以在任务结束后提供一个返回值（Runnable不可以），call（）方法可以抛出异常（Runnable不可以），运行Callable可以拿到一个Future对象，Future对象表示异步计算的结果，提供检查计算是否完成的方法（Future监视目标线程调用call（）方法的情况）。ExecutorService threadPool=Executors.newSingleThreadExecutor(); Future<String> future=threadPool.submit(new CallableTes()); future.get();  (public String call() throws Exception{ return "1111"})
- 如果不需要改写Thread中的其他方法，使用Runnable接口
- 只有通过调用线程类的start（）方法才能真正达到多线程的目的（将线程处于就绪状态）。run（）方法当普通函数调用（同步）。

### 46 多线程同步的实习方法

- synchronized关键字，对象锁（任何时候只允许被一个线程拥有），（获取锁-执行代码-释放锁），synchronized方法（public synchronized void mutilThreadAccess）和synchronized块（Synchronized（SyncObject））{// 访问syncObject代码}。在synchronized代码被执行期间，线程可以调用对象的wait（）方法，释放对象锁，进入等待状态，并且调用notify（）（唤醒第一个等待线程）方法或notifyAll（）方法通知正在等待的其他线程。
- lock（JDK 5）：Lock接口，和实现类ReentranLock（重入锁）。（1）lock（）以阻塞方法获取锁（如果获得锁，立即返回，如果别的线程持有锁，当前线程等待，直到获取锁后返回）。 （2）tryLock（），以非阻塞方法获取锁（尝试获取，获得返回true）。（3）tryLock(long timeout,TimeUbit unit),如果获取锁，立即返回true，否则等待参数单元。
（4）lockInterruptibly（），获取锁，立即返回，没有则处于休眠，直到获得锁或者当前线程被别的线程中断（interruptedException）（非lock()的阻塞方式.lock会忽略InterruptException,lock.lock()不会抛异常）。
final Lock lock=new ReetranLock();
public void run(){try{lock.lockInterruptibly();}catch(InterruptException e){sout("intrrupted!")}} 

### 47 sleep()和wait()方法

- sleep（）使线程暂停执行一段时间的方法（阻塞状态）。wait（）（Thread.wait()）会使线程进入等待状态，直到唤醒或等待超时。
- sleep（）是Thread类的静态方法，线程用来控制自身流程的，使线程暂停执行一段时间，把执行机会给其他线程，等到计时时间一到，线程自动“唤醒”（处于可运行状态，等待CPU调度）。 wait（）方法是Object类的方法，用于线程间的通信，会使当前拥有该对象锁的进程等待，知道其他线程调用notify（）方法，也可以设置时间自动“醒”来。
- sleep（）方法不涉及线程间的通信，不会释放锁。wait（）会释放锁，而使线程所在对象中的其他synchronized数据可被其他线程使用。.
- wait（）必须放在同步控制方法或者同步语句块中使用，sleep任何地方（必须捕获异常，可以被Interrupt，不释放锁容易导致死锁，不推荐使用）

### 48 线程终止方法

- stop()和suspend()，Thread.stop（）释放所有监视资源（导致对象处于不一致状态），supend（）容易导致死锁（不会释放锁）。现在不推荐使用了
- (1)通过对run（）方设置flag标志控制循环执行，让线程立刻run（）方法从而终止线程。  while（flag}{//...}(2)通过在run方法中捕获异常，让线程安全退出 thread.interrupt（）;

### 49 synchronized和Lock

- 资源同步的两种锁机制
- synchronized使用Object对象本身的notify、wait、notfiyALl调度机制，Lock使用Condition进行线程之间的调度
- Lock需要显示的指定开始和结束位置，synchronized是托管给JVM执行的，Lock的锁定通过代码实现，更精准的线程语义。
- ReentrantLock（Lock实现），有锁投票、定时锁、等候和重点锁。竞争一般情况下synchronzied性能优于Reentrantlock，竞争激烈时候synchronized性能下降很快，ReentrantLock基本保持不变
-  锁机制不同，synchronized自动解锁，lock需要在finally中释放（否则死锁）


### 50 守护线程

- 服务进程或后台线程，较低的优先级
- 在start（）前，使用thread.setDaemon(true)方法
- 守护线程产生的线程默认也是守护线程
- 当程序中只有守护线程时候，JVM是可以退出的
- 例子：GC

### 51 join方法

- join方法作用是让调用该方法的线程在执行完run（）的线程后，再执行join方法后面的代码，将两个线程合并，实习同步功能
- join（2000），最多等待两秒
 

## db(数据库)基础

### 1 范式

- 第一范式（1NF）字段具有**原子性**不可再分。

- 第二范式（2NF）在1NF的基础上，数据库表中的每个实例或行必须可以被**唯一地区分**，拥有唯一属性列（主关键字或**主键**），每一行都能区分 。 2NF要求实体的属性**完全依赖**于主关键字。

- 第三范式（3NF）必须先满足第二范式2NF，3NF要求一个数据库表中**不包含**已在其它表中已包含的非主关键字信息。否则造成**数据冗余**。

### 2 ACID
数据库事务正确执行的四个基本要素：
[acid-database](http://www.jdon.com/concurrent/acid-database.html)

- Atomic，**原子性**: 一个事务的所有系列操作步骤被看成是一个动作，所有的步骤要么全部完成要么一个也不会完成，如果事务过程中任何一点失败，将要被改变的数据库记录就不会被真正被改变。
 
- Consistent，**一致性**: 在事务开始之前和事务结束以后，数据库的完整性约束没有被破坏。数据库的约束级联和触发机制Trigger都必须满足事务的一致性。也就是说，通过各种途径包括外键约束等任何写入数据库的数据都是有效的，不能发生表与表之间存在外键约束，但是有数据却违背这种约束性。所有改变数据库数据的动作事务必须完成，没有事务会创建一个无效数据状态，这是不同于CAP理论的一致性"consistency"。

- Isolated，**隔离性**: 主要用于实现并发控制, 隔离能够确保并发执行的事务能够顺序一个接一个执行，通过隔离，一个未完成事务不会影响另外一个未完成事务。串行化，防止事务操作间的混淆，**同一时间仅有一个请求用于同一数据**。
- Durable，**持久性**: 一旦一个事务被提交，它应该持久保存，不会因为和其他操作冲突而取消这个事务。很多人认为这意味着事务是持久在磁盘上，但是规范没有特别定义这点。

实现ACID：（1）Write ahead logging（2）Shadow paging

### 3 CAP

- C:Consistency **一致性**,更新操作成功并返回客户端完成后,分布式的所有节点在同一时间的数据完全一致
- A: Availability **可用性**,所有在分布式系统活跃的节点都能够处理操作且能响应查询，读和写操作都能成功 
- P: Partition Tolerance **分区容错性**，再出现网络故障导致分布式节点间不能通信时，系统能否继续服务。


### 4 内连接和外连接

- 内连接：（inner join）自然连接，只有两个表相匹配的行才能在结果集中出现，返回结果集中所有相匹配的数据。

- 外连接，还包含不匹配的行，左外连接（left outer join）、右外连接（right outer join)


