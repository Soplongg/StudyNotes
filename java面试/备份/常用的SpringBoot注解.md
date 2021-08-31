1. SpringBootApplication注解：这个注解标识了一个SpringBoot工程，它实际上是三个注解的组合，分别是
   1. @SpringBootConfiguration：这个注解实际上就是一个@Configuration，表示启动类也是一个配置类
   2. @EnableAutoConfiguration：向Spring容器中导入了一个Selector，用来加载ClassPath下SpringFactories中所定义的自动配置类，将这些自动配置加载为配置Bean
   3. @ComponentScan：标识扫描路径，默认是没有配置实际扫描路径，所以SpringBoot扫描的路径是启动类所在的当前目录。
2. @Bean注解：用来定义Bean，类似于XML中的`<bean>`标签，Spring在启动时，会对加了@Bean注解的方法进行解析，将方法的名字做为beanName，并通过执行方法得到bean对象
3. @Controller、@Service、@ResponseBody、@Autowired等等

