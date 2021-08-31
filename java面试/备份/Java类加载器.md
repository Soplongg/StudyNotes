JDK自带三个类加载器：boostrap ClassLoader、ExtClassLoader、AppClassLoader

boostrap ClassLoader 是 ExtClassLoader的父类加载器，负责加载%JAVA_HOME%/lib下的jar包和class文件。

ExtClassLoader 是 APPClassLoader  的 父类加载器，负责加载%JAVA_HOME%/lib/ext下的jar包和class文件。

APPClassLoader 是 自定义加载器 的 父类加载器,负责加载classpath路径下的类文件同时还是系统加载器，线程上下文加载器。

自定义加载器的实现方法是继承ClassLoader。

