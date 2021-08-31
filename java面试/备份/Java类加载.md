![image-20210811145151309](E:\学习笔记\img\java类加载1.png)

## 1.Java的类加载的全过程是什么样的？

Java的类加载器：AppClassLoader -> ExtClassLoader -> BootStrap ClassLoader   (parent属性,并非是继承关系)

Java 的类加载器的继承关系：AppClassLoader , ExtClassLoader  ->   URLClassLoader  ->  SecureClassLoader ->  ClassLoader

类加载过程：  加载  ->  连接   ->  初始化 

- 加载：把 Java的字节码数据加载到JVM内存中，并映射成JVM认可的数据结构。
- 连接：分为三个小阶段
  1. 验证：检查加载到的字节信息是否符合JVM规范。
  2. 准备：创建类或者接口的静态变量，并赋予初始值。
  3. 解析：把符号引用转为直接引用
- 初始化：对静态变量、静态代码块执行初始化工作。

> 类加载器就是寻找类或者字节码文件进行解析并构造成JVM内部对象的一个组件。就是将类装入JVM。

## 2.双亲委托机制是什么?

<img src="E:\学习笔记\img\java类加载2.png" alt="img" style="zoom:50%;" />

每个类加载器对加载过得类，会存入缓存中，当要加载类的时候，会去缓存中查询是否已经加载过。

双亲委托机制：向上委托查找，向下委托加载。作用：保护Java底层的类不会被应用程序覆盖。



