# java基础

基本数据类型

整型:byte 1, short 2, int 4, long 8

浮点: float 4, double 8 , 

字符: char 2 , 布尔型: boolean, 

字符串String , 枚举: enum 接口interface

流程: if(){}  for( ; ; ){}  while(){} do{}while()

switch(exp){

​	case x:

​	break;

}

重载: 同一个类中的相同方法名有不同的参数, 调用时根据参数判断出调用的具体方法

重写: 继承或接口关系的两个类, 子类有着与父类相同的名字的方法, 返回值相同,修饰词不能比父类更严格



java内存图

栈stack存放方法的局部变量, 存放方法, 存放对象的引用(指针)

堆Heap存放对象, new出来的实体对象(不包括成员方法) , 常量池:基本类型的常量

方法区 存储class信息, 包括方法的信息

本地方法栈 与操作系统相关

寄存器与cpu相关



关键字

static 静态, 在静态方法区中独有的一份, 

代码块调用顺序: 静态代码块, 构造代码块, 构造方法, 普通方法

this在构造方法中必须在第一行

super在构造方法中必须在第一行

final修饰全局变量声明的时候必须赋值且只能赋值一次, 修饰局部变量不能赋值



面向对象三大特性

封装, 继承, 多态

多态体现: 编译多态: 向上转型 , 重载方法; 运行多态: 向下转型: 直接强转



抽象类abstract



equals比较的是地址, 底层是==, ==比较的是基本数据类型, 比较的是内容



内部类: 成员内部类, 静态内部类, 局部内部类, 匿名内部类

成员内部类与静态内部类: 有无static

局部内部类: 在方法中声明的类, 不能加修饰词, 不能离开这个方法调用这个内部类任何东西, 调用方法时内部类才被创建

匿名内部类: 使用一次, 父类或接口名 对象名 = new 父类或接口名(参数){}



设计模式

单例模式, 简单工厂模式, 建造者模式, 装饰者模式



数组声明 int a[]或  int[] a

初始化: a=new int[2];  a=new b[]{3,4};  int[] c = {5,6};

数组常用方法: 

1. 打印: Arrays.toString(a);
2. 从数组创建ArrayList: new ArrayList<>(Arrays.asList(a));
3. 检查是否包含值: Arrays.asList(a).contains();
4. 合并:  int[] c = ArrayUtils.addAll(a,b);
5. 把ArrayList转数组: arrayList.toArray(a);
6. 数组转set: new HashSet<>(Arrays.asList(a));
7. 反转数组: ArrayUtils.reverse(a);
8. 根据分割符拼接数组: StringUtils.join(new String[]{"a","b"},",");
9. 删除数组元素: ArrayUtils.removeElement(a, 3);
10. 数组复制: Arrays.copyOf();



常用类

Integer

compareTo(); 比较大小

toBinaryString() 十进制转二进制, 返回String字符串, Ascall码转字符

Integer.valueOf(  ) 转为Integer类型

parseInt将Integer转int

intValue()  将Integer转int



String常用方法

==比较地址,  .equals()  比较字符,  .equalsIgnoreCase() 忽略大小写比较

.charAt() 取出对应下标的字符,  .compareTo(); 比较大小,  str.concat(str2) 将str2连接到str后面

.contains() 是否包含,  .startsWith(前缀, 开始位置) 检测字符串是否以指定前缀开头

.indexOf("/").indexOf("/",3).lastIndexOf("/")  找出字符出现的位置

substring(开始位置, 结束位置),  . replace("a","b") 替换a为b

.toUpperCase().toLowerCase() 转换大小写

.trim() 去掉字符串前后的空格



StringBuffer

.append("a") .insert(2,"b") .delete(开始位置, 结束位置)左闭右开  .reverse() 逆序



Character

Character.isLetter('a') 判断是否为a



时间类



finally与finalize的区别

当一个对象被虚拟机宣告死亡时会先调用它finalize()方法,这是Object的方法

finalize又系统调用, 垃圾回收器回收之前做的一些清理工作



# 集合类



# 枚举



# lambda表达式, 函数式接口, 流式计算

()-{},多参数必须使用(), 多语句必须使用{}, 用在函数式接口

# javaIO



# 多线程

线程创建: 三种方法: 1. 继承Thread,重写run方法, 调用start开启  2. 实现Runnable接口, 重写run方法, new线程, 丢入runnable接口实现类, 调用start方法  3. 实现Callable接口, 重写call方法, 创建线程对象, 创建执行服务, 提交执行, 获取结果, 关闭服务

线程状态: 创建new, 就绪start, 阻塞sleep, wait, 运行, 死亡

线程方法: setPriority()设置优先级, sleep()指定睡眠, join() 等待该线程终止, yield()暂停该线程转其他线程, isAlive()测试线程是否处于活动

线程停止: 使用标志位当flag=false时终止:  while(flag){...

线程休眠: sleep, 不会释放对象锁,时间到进入就绪

线程礼让: yield, Thread.yield();

合并线程: (插队) Join,等此线程执行完才执行别的,其他阻塞

线程状态观测: Thread.State

设置优先级: setPriority(), 最大10默认5最小1

守护线程Daemon: thread.setDaemon(true);(后台日志, 监控, gc)

线程同步:锁机制synchronized,  加在方法上, 降低性能,     同步块:synchronized(obj){...}

死锁条件: 1. 互斥条件, 2. 请求与保持请求,3. 不剥夺 4. 循环等待

Lock锁(显式定义同步锁): 性能更好,   try{  加锁:lock.lock();....}  finally{解锁lock.unlock();}

线程协作: 同步代码块内使用wait(), notify/notifyAll()

生产者消费者: 管程法, 信号灯法

线程池: ExcutorService service = Executors.newFixedThreadPool(10);

service.execute(new Thread());

service.shutdown();



JUC

并发: 多线程操作同一资源, 并行: 多核心同时运行

获取cpu核心数: Runtime.getRuntime(),availableProcessors()

线程状态:六个: new, runnable, blocked, waiting, timed_waiting有限等待, terminated终止

wait与sleep区别: 1. 来自不同类,2. wait会释放锁, sleep不会, 3, wait必须在同步代码块中使用,4, wait不需要捕获异常

创建多线程: 1.创建资源类, 2. new Thread(lambda表达式).start();

获取当前线程名: Thread.currentThread()

Lock锁: Lock lock = new ReentrantLock();...try{ lock.lock();}...finally{ lock.unlock();}

synchronized与lock的区别: 

1. synchronized是关键字, lock是锁
2. lock可以判断是否获取到了锁
3. lock必须手动释放锁
4. lock不会一直等待
5. lock可重入,可判断锁, 非公平锁
6. lock适合大量同步代码

锁的对象是?锁类, 锁对象

生产者消费者问题:synchronized版和lock版

8锁问题

线程池:三大方法,七大参数, 四种拒绝策略

三大方法: ExcutorService threadPool = Executors.newSingleThreadExecutor();//单线程-池

Executors.newFixedThreadPool(5);//创建固定大小线程池

Executors.newCachedThreadPool();//可伸缩的变动线程池

七大参数: 三大方法的本质:  new ThreadPoolExecutor()

​	corePoolSize线程池大小,  maximumPoolSize最大核心线程池大小,  keepAliveTime超时释放

​	unit超时单位, workQueue阻塞队列,  threadFactory线程工程,创建线程用的一般不用改,

​	handle 拒绝策略

四种拒绝策略: 

​	AbortPolicy()//满人抛异常,  CallerRunsPolicy()哪来回哪去(回主线程) 

​	DiscardPolicy()//满了丢任务, 不抛出异常,  DiscardOldestPolicy()//满了与早前的竞争, 不抛异常

最大线程设置规则: cpu密集型任务: 几核就几条线程,  IO密集型: 判断程序中十分消耗IO的线程数量来设置大于这个数的线程数



ForkJoin: 并行任务, 大任务变小任务, 特点: 工作窃取

异步回调  Future

JMM: 对Volatile的理解: Volatile是轻量级的同步机制

JMM的一些同步约定: 1. 线程解锁前必须把共享变量写回主存  2. 线程加锁前必须从主存读入最新值到工作内存,  3.加锁和解锁是同一把锁 

Volatile三个特性: 1. 保证可见性: 当一个线程修改了某个共享变量值,其他的线程能立即看到修改的值  2. 不保证原子性,synchronized加锁可以保证原子性 (使用原子类也可以解决原子性问题)  3. 禁止指令重排:多并发下的单例懒汉模式有指令重排导致非单例的风险

CAS: 



# jvm及调优

### 加载器, 内存图, 堆结构,堆调优, gc算法,JMM

java-class-classloader

虚拟机栈(方法的栈帧)=栈内存        本地方法栈(native方法)             方法区  堆           程序计数器

​                                                         本地方法接口<--本地方法库           执行引擎

类加载器: 1. 虚拟机自带加载器, 2. 启动类根加载器rt.jar  3. 扩展类加载器ExtClassLoader  4. 系统加载器/应用程序加载器AppClassLoader

双亲委派机制, 往上找包,上层有包不加载下层, 查看当前类的加载器: 对象.getClass(),getClassLoader();

沙箱安全机制

沙箱组件: 字节码校验器, 类装载器, 存取控制器, 安全管理器, 安全软件包

Native关键字: 进入本地方法栈, 从本地方法栈调用本地接口JNI, c写的

PC寄存器=程序计数器, 指向方法区方法

方法区: 被所有线程共享, 所有定义方法的信息都保存在这, static, final, 构造, 接口定义, 常量池

栈: 没有垃圾回收的问题 , 存: 八大基本类型, 对象引用, 实例方法, 运行原理: 栈帧

三种JVM: HotSpot, JRockit, JIT

堆: 一个jvm只有一个堆内存,可调节,再分三个区: 新手区young=伊甸园区, (幸存区0区, 幸存区1区) 轻gc;   养老区old , 重gc, 永久区Prem(元空间)

gc回收主要在伊甸园区和养老区

新生区: 新建实例存入这里, 进过垃圾回收机制后存活的进入幸存区, 幸存区满后重gc进入老年区

jdk8元空间MetaSpace: 存放java运行环境, 不做gc

OOM: 1. 扩大堆内存:  -Xms1024m -Xmx1024m -XX:+PrintGCDetails, -Xms初始1/64, -Xmx最大分配内存1/4

2. 分析内存: MAT, Jprofiler分析Dump文件: VM设置: -XX:+HeapDumpOnOutOfNemoryError

​        

1、字符串存在永久代中，容易出现性能问题和内存溢出。

　　2、类及方法的信息等比较难确定其大小，因此对于永久代的大小指定比较困难，太小容易出现永久代溢出，太大则容易导致老年代溢出。

　　3、永久代会为 GC 带来不必要的复杂度，并且回收效率偏低。

　　4、Oracle 可能会将HotSpot 与 JRockit 合二为一。



堆内存调优



GC: 

GC算法: 

引用计数法: 给每个对象设置引用数值, 为0清除

复制算法: eden轻gc将幸存的移入幸存区to区, from区内容移入to区, from区变to区, to区变from区

​	好处无内存碎片,坏处浪费空间, 适用: 对象存活度较低的区比如新生区

标记清除法: 两轮: 标记, 清除 坏处: 大量内存碎片

标记压缩: (标记清除压缩算法) 标记, 清除, 压缩, (三轮)

年轻代用复制算法, 老年代用标记清除压缩



JMM: java内存模型

干什么的:缓存一致性协议，用于定义数据读写规则

主内存(物理内存) 工作内存(高速缓存), 工作内存是每个线程独自拥有的, 是主内存变量的拷贝, 线程只操作工作内存

内存交互8种: 每一个都是原子的: 锁定, 解锁, (读取, 载入) 使用, 赋值, (存储, 写入)

模型特征: 原子性, 可见性, 有序性

# 设计模式



# java网络编程



# 反射



# servlet



# mysql数据库



# 408



# redis



# spring



# springboot



# mybatis



# 熟悉项目



# linux命令



# restful



# rabbitMQ



