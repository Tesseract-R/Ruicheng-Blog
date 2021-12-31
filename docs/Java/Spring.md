### <font size=3pt face="MV Boli" color="gray">By Ruicheng Zhang</font>



## 注解

####   ① `@Component` , `@Bean`的区别

1.   作用对象：`@Component`作用于类，`@Bean`作用于方法
2.   `@Component`通过路径扫描自动侦测、自动装配到`Spring`容器中；`@Bean`告诉`Spring`这是某个类的实例。在标有该注解的方法中定义产生这个bean

####   ② `@Autowire`, `@Resource`的区别

1.   都可以用来装配bean，都可以用于字段或setter方法
2.   `@Autowire`默认按类型装配，`@Resource`默认按名称装配

####   ③ 将一个类声明为bean的注解

-   `@Component`：通用
-   `@Repository`：持久层（DAO层）
-   `@Service`：服务层
-   `@Controller`：Spring MVC控制层
-   `@Configuration`：配置类

####   ④ `@Configuration`配置类

一个类里可以声明一个或多个`@Bean`方法
约束：
- 配置类必须以类的方式提供
- 配置类必须是非final的
- 配置类必须是非本地的
- 任何嵌套的配置类必须声明为static
- `@Bean`方法可能不会反过来创建更多的配置类
