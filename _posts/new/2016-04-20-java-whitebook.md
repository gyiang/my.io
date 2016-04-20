---

layout: post
title: BlackBook
category: 资源
tags: java,job
description: java研发面试所需

---

#### 1 java与c/c++异同

- 解释型语言，C++编译型。
- 纯面向对象，除基本数据类型，所有类型都是类。
- 无指针，更安全。
- 不支持多重继承。
- 提供垃圾回收器.(finalize)
- 不支持自动强制类型转换。
- 平台无关性。
- 提供对注释文件的内建支持。


#### 2 main()

- 必须public（任何类和对象可以访问） static（存储在静态存储区）
- 返回值必须 void
- 可以用final、synchronized修饰
- 只有与文件名相同类的main是入口

#### 3 初始化顺序
当实例化对象时，只有所有类成员完成初始化，才会调用所在类的构造函数创建对象。

父类Ｂ静态代码块->子类Ａ静态代码块->父类Ｂ非静态代码块->父类Ｂ构造函数->子类Ａ非静态代码块->子类**Ａ构造函数**

- 静态代码块是随着类的创建而执行，所以父类静态代码块最先被执行
- 实例化子类对象要先调用父类的构造方法
- 调用父类构造方法前会先执行父类的非静态代码块
- 初始化静态成员变量和静态代码块时按照在程序中出现的顺序初始化


#### 4 java文件中定义多个类

- 最多只能一个类被public修饰，且类名与文件名相同
- 无public时候，文件名随便是一个类的名字
- javac会对每个类生成.class

#### 5 构造函数

用于在实例化时初始化对象的成员变量

- 构造函数必须与类名相同
- 不能有返回值
- 构造函数的参数可以为0
- 总伴随new操作一起调用，不能被其他方式调用，必须系统调用
- 默认构造器的修饰符只跟当前类的修饰符有关

#### 6 标识接口

- 充当标识作用，仅用来表明属于特定类型
- 如Cloneable、Serizlizable等，常用instanceof来判断

#### 7 参数传递

- 值传递：基本数据类型（int、char、double），传递的是输入**参数的复制**，因此方法中的改变参数的值，不会影响方法外
- 引用传递：其他类型的传递，引用类型传递的是对象的**地址**，指向了对象实例，对象在函数调用、“=”赋值都采用引用传递
- 使用clone方法复制对象
- 实现clone的类需要继承Cloneable接口，重写Object中的clone方法，在clone方法中调用super.clone()，并把浅复制（被复制对象所有变量都含有与原来对象相同的值所有对象引用指向原来对象）的引用指向原型对象新的克隆体，实现深复制（把复制对象所引用的对象也复制一遍）

#### 8 反射机制

- 允许程序运行时候进行自我检查，并允许对内部成员进行操作
- 功能：得到一个对象所属的类；获取一个类的所有成员变量和方法；**在运行时创建对象**；在运行时调用对象的方法
- Class.forName("C").newInstance()

#### 9 创建对象的方法

- new语句实例化
- 反射机制
- clone（）方法
- 反序列化

#### 10 实现类似C函数指针功能

- 回调函数：指针函数先注册，将在稍后某个需要的时候被调用。
- 在java中利用接口与类实现。先定义接口，并声明要调用的方法，实习接口，把实现类的一个对象作为参数传递给调用程序，调用程序通过参数开调用指定的函数。

#### 11 面向对象的特征

- 抽象，数据和过程抽象，忽略与主题无关的方面
- 继承，派生类可以从基类获得方法和实例变量，并且可以修改或增加新方法，代码复用方式，提高复用性和开发效率。（注意和组合的区别），is-a关系
- 封装，隐藏实现，只公开对外接口，隐藏其具体实现，通过访问控制实现（通过用Public将信息暴露，Private，Protected将信息隐藏）
- 多态，允许不同类的对象对同意消息做出响应,**同一消息可以根据发送对象的不同而采用多种不同的行为方式**。（发送消息就是函数调用）。

#### 12 多态的实现机制

- 覆盖(override)，子类重写了**父类**的同名方法，子类覆盖父类的方法，**方法名相同，参数类型相同**，返回类型和抛出异常要<=父类，访问权限要>=父类（两同两小一大原则）基类的方法不能为private（否则子类只是自己定义了方法），**运行时多态**（基类引用可以指向基类也可以指向子类的实例变量，程序调用的方法在运行期才动态绑定，引用变量指向具体的实例对象方法，在内存中的方法）
- 重载(overload)，指在**同一个类中**，允许存在多个同名方法，而这些方法的参数表不同（**个数**或**参数类型**不同，方法的返回类型、修饰符可以相同，也可不同），**编译时多态**（因为参数列表不同，编译时候确定）

#### 13 抽象类和接口

- 抽象类：含有抽象方法，声明为abstract（只能修饰类和方法，不可以修饰属性）
- 接口：方法的集合，所有方法都没有方法体，声明为interface，成员变量全部是static final。
- 抽象类和接口**都不能被实例化**。
- 接口强调特定功能的实现，设计理念是“has-a”关系，抽象类是“is-a”
- 接口定义的成员变量默认为public static final，必须赋初值且不可修改，方法成员都是public abstract的，且只能被这两个关键词修饰
- 抽象类默认成员变量为defaultt(本包可见)，可以定义private、protected、public，成员变量可以在子类中被重新定义，也可以被重新赋值。抽象类中的抽象方法（abstract修饰）不能用private、static、synchronized、native等访问修饰符修饰，方法以分号结尾，不带{}。
- 当功能需要累积时，用抽象类；不需要累积时，用接口。
- 接口是一种特殊的抽象类，接口中的方法全部是抽象方法，接口中的方法只能是public和default

#### 14 命名规则

- 只能字母（a~z，A~Z）、数字（0~9）、下划线（_）和$
- 第一个字母不能是数字

#### 15 break、continue、return

- break 强制跳出当前循环，使用标识符+":",跳出多重循环
- continue 停止当此循环，回到循环起始处，进入下一次循环，也可以多重循环
- return 从一个方法返回，返回到调用的地方

#### 16 final、finally、finalize

- **final**方法：不允许重写，final参数：参数在函数内部不允许修改，final类：不能被继承，所有方法不可重写。
final指的是**引用不可变**，指向初始时指向的那个对象，不关心所指对象的内容变化，被**final修饰的变量必须初始化**。可以在定义、初始化块（不可以在静态初始化块中初始化，静态final成员变量可以在静态初始化块中但不可在初始化块中）、在类的构造器中（静态final不可以）
- **finally**：异常处理中的finally必须在函数退出前执行，无论如何finally语句都要执行。try中没有异常时，但是有return等跳转语句，这样会引发程序控制流离开当前的try,自动完成finally中资源的释放。try中有异常时，**catch在获取到异常之前，进行finally执行，接着执行catch中的语句**
- **finalize**是Object的方法，在垃圾回收器执行前，会调用被回声对象的finalize（）方法，可以覆盖这个方法实现对资源的回收

#### 17 static

- 为某特定数据类型或对象分配单一的存储空间，而与创建的个数无关
- 实现方法或属性与类而不是对象关联在一起（通过类直接调用或使用类的属性）
- static成员变量：全局效果，静态变量属于类，在内存中只有一个复制
- static成员方法：static方法是类方法，不需要创建就可以调用，static方法中不可以this、super，不能调用非static方法，只能访问所属类静态变量和成员方法
- static代码块，JVM在加载时候会执行static代码块，用来初始化静态变量，只会被执行一次
- 用来实现单例模式，隐藏构造函数（设为private）
- static final：全局常量

#### 18 volatile

- 修饰被不同线程访问和修改的变量，让其每次从对应的内存中读取，而不是缓存
- 所有线程在任何时刻看到的变量值都是相同的
- private volatile Boolean flag

#### 19 instanceof

- 二元操作符
- 判读一个引用类型的变量所指的对象是否是一个类（或接口、抽象类、父类）的实例
- object instanceof class

#### 20 strictfp

- strict float point 精确浮点关键字
- 确保浮点运算的准确性
- 不同平台结果也一致

#### 21 基本数据类型

基本类型四类八种，其余全是引用类型

- 整数：byte（8 bit） short（16） int（32） long（64）
- 浮点数：float（32） double（64）
- 字符型：char（16）
- 逻辑性：boolean（true flase）

- 封装类型，默认null（Character、Boolean、Byte、Short、Integer、Long、Float、Double）
- 原始数据类型值传递，封装类型引用传递
- float初始化1.0f 或 f=（float）1.0， f=3.4是错的

#### 22 不可变类

- 创建实例后，不允许修改值
- 所有基本类型的包装类都是不可以变类（Integer）
- String 不可变类

#### 23 强制类型转换

- 涉及byte、short、char类型运算会强转为int类型，最后结果也是int
- short s1=（short）s0+1

#### 24 char存储中文汉字

- java默认是Unicode编码，每个字符占用2个字节
- String由char组成，更灵活，英文占用1个字符，中文占用2个字符

#### 25 字符串创建于存储机制

- new String("abc"),只要new总会生成新对象
- String s1="abc", String s2="abc" ,JVM存在常量池，共享使用
- 现在常量池中是否有相同的字符串被定义，如果存在，直接获取对其引用，不需要创建，如果没有定义，先创建，加入到常量池，在返回引用

#### 26 ==与equals

- “==”比较两个变量值是否相等，比较的是内存中所有存储的数值，比较两个基本类型的数据或者两个引用变量是否相等。
- equals，在没覆盖的情况下，equals=“==” 
- 通过覆盖equals让其比较引用而不是比较数据内容
- s1=new String("Hello") s2=new String("Hello") s1和s2引用地址不同，内容相同，用“==”不可以比较，String方法重写了equals方法，比较两个独立对象的内容是否相同。
- hashCode（）方法从Object继承而来，鉴定两个对象是否相等。返回值是对象在内存中地址转换为一个int值，任何对象的hashCode方法不同（没重写的情况）
- 覆盖equals方法时候也覆盖hashCode


#### 27 String、StringBuffer、StringBuilder和StringTokenizer

- Character单个字符操作
- String不可变类（一旦创建，值不可以改），StringBuffer可变类
- 当用String类型对字符串修改时，实现方法也是调用了StringBuffer（append等），最后to_string
- StringBuilder非线程安全、StringBuffer线程安全
- 执行效率方面：StringBuilder>StringBuffer>String
- 数据量小选择String，单线程大量操作：StringBuilder，多线程下大量数据：StringBuffer
- StringTokenizer用来分割字符串的工具=new StringTokenizer("Hello to")

#### 28 try中return

- try-finally或者catch-finally中都有return，finally中的return语句会覆盖别处return语句，**最终返回**到调用者那里的是finally中return的值
- return在返回时，不是直接返回变量的值，而是**复制一份**，然后返回（）
- finally块中改变return的基本类型的值对返回值没有任何影响，而对引用类型的数据有影响try{r=2;return r}catch(EXception ex){}finally{r=3} ，返回2

#### 29 运行时异常和普通异常

- 两种异常类，**Error和Excetion**，共同父类是Trowable
- Error表示在运行期出现了非常严重的错误，**该错误不可恢复**，JVM层次大错误，导致程序终止执行，编译器不会检查Error是否被处理，程序不推荐捕获Error类异常，运行时异常多是逻辑错导致的，属于应该解决的问题，OutOfMemoryError、ThreadDeath等
- Exception表示可以恢复的异常，是编译器可以捕获的，包含两种类型：检查异常（Checked exception）和运行时异常（runtime exception）
- （检查异常）：所有继承Exception非运行时的都是，在编译阶段，编译器强制程序去捕获此类一次。如IO、SQL
- （运行时异常）：如果不处理，由JVM处理，NullPointerException、ClassCastException、ArraryindexOutofBoundExcpetion、BufferOverflowExcetion、ArithmeticException等
- 出现运行时异常后，系统会把异常一直往上层抛出，直到遇到处理代码为止，多线程用Thread.run()抛出，单线程用main（）抛出。线程退出，主程序异常则程序退出

#### 30 IO流实现机制

- 流的本质是数据传输，分为两类：字节流和字符流
- 字节流（8 bit）：InputStream、OutputStream
- 字符流（16 bit）：根据码表映射字符，一次可读多个字节，Reader和Writer，处理输入输出的时候用缓存
- IO类设计采用Decorator装饰者模式

#### 31 Socket

- 基于TCP的通信过程：Server端Listen指定的某个端口（>1024）是否有连接请求,Client端向Server端发出Connect（连接）请求，Server端向Clinet端发回Accept（接受）消息。一个连接建立，会话产生，Server端和Client端通过send和write等方法与对方通信
- ···代码···

#### 32 NIO

- NIO：Nonbloking IO,非阻塞IO
- Socket阻塞导致大量线程的上下文切换，效率低
- NIO通过Selector、Channel和Buffer来实现非阻塞IO操作
- NIO非阻塞实现主要采用了Reactor（反应器）设计模式，与Observer（观察者）模式类似，O只处理一个事件源，R可以出来多个事件源
- Channel双向非阻塞的通道，通道两边进行数据读写操作
- Selector实现用一个线程来管理多个通道，类似观察者。将要处理的Channel的IO事件（connect、read、write）注册给Selector。内部实现原理：对所有注册的Channel进行轮询访问，一旦轮询到Channel 1一个注册事件发生，通过SelectionKey方式通知开发人员对Channel1进行数据的读或写操作
- Key封装一个特定Channel 1和一个特定Selector之间的关系，
- 通过轮询方式处理多线程请求时不需要上下文切换，NIO较高的执行效率
- Buffer用来保存数据，可以存Channel1读取的数据，也可以存放使用Channel1进行发送的数据。 ByteBuffer、CharBuffer

#### 33 序列化

- 在分布式环境下，当进行远程通信时候，无论是何种类型的数据，都会以**二进制序列的形式在网络上传送**。 序列化是一种将对象以一连串的字节描述的过程，用于解决在对对象流进行读写操作时所引发的问题。序列化可以将对象的状态写在流里进行网络传输，或者保存到文件、数据库等系统容，并在需要时把该流读取出来重新构造一个相同的对象。
- 实现Srializable接口（java.lang）
- 使用输出流（FileOutputStream）来构造一个ObjectOutputStream（对象流）对象
- 使用该对象的writeObject（Object obj）将obj对象写出（即保存其状态），要恢复时，使用对应的输入流
- static（静态）代表类的成员、transient 代表对象的临时数据，不能序列化
- 


