### <font size=3pt face="MV Boli" color="gray">By Ruicheng Zhang</font>





基础框架&插件：

-   Websocket：多端即时通讯
-   Shiro：用户登录和权限校验
-   Mybatis：数据持久化
-   ActiveMq：消息队列





# 注解：

-   @Autowired

    

-   @Repository（存储层Bean）

    将数据访问层（DAO）的类标识为Spring Bean

-   @Service（业务层Bean）

    一个组件，作用在业务层

-   @Controller（展示层Bean）

    一个组件，作用在控制层

-   @Component

    一个组件，可以作用在任何层次

    

@Mapper和@Repository的区别：

  1、使用@mapper后，不需要在spring配置中设置扫描地址，通过mapper.xml里面的namespace属性对应相关的mapper类，spring将动态的生成Bean后注入到ServiceImpl中。

  2、@repository则需要在Spring中配置扫描包地址，然后生成dao层的bean，之后被注入到ServiceImpl中

