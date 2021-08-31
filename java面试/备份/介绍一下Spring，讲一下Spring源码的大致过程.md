1. Spring是一个快速开发框架，Spring帮助程序员来管理对象
2. Spring的源码是非常优秀的，设计模式的应用、并发安全的实现、面向接口的设计等
3. 在创建Spring容器，也就是启动Spring时：
   1. 首先会进行扫描，扫描得到所有的BeanDefinition对象，并存在一个Map中。
   2. 然后筛选出非懒加载的单例BeanDefinition进行创建Bean，对于多例Bean不需要在启动过程中去进行创建，对于多例Bean会在每次获取Bean时利用BeanDefinition去创建
   3. 利用BeanDefinition创建Bean就是Bean的创建生命周期，这期间包括了合并BeanDefinition、推断构造方法、实例化、属性填充、初始化前、初始化、初始化后等步骤、其中AOP就是发生在初始化后这一步骤中
4. 单例Bean创建完了之后，Spring会发布一个容器启动事件
5. Spring启动结束
6. 在源码中会更加复杂，比如源码会提供一些模板方法，让子类实现，比如源码中还涉及到一些BeanFactoryPostProcessor和BeanPostProcessor的注册，Spring的扫描就是通过BeanFactoryPostProcessor来实现的，依赖注入就是通过BeanPostProcessor来实现的
7. 在Spring启动过程中还会去处理@Import等注解

