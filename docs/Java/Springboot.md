### <font size=3pt face="MV Boli" color="gray">By Ruicheng Zhang</font>





基础框架&插件：

-   Websocket：多端即时通讯
-   Shiro：用户登录和权限校验
-   Mybatis：数据持久化
-   ActiveMq：消息队列





# 注解：

-   `@Autowired`

    

-   `@Repository`（存储层Bean）

    将数据访问层（DAO）的类标识为Spring Bean

-   `@Service`（业务层Bean）

    一个组件，作用在业务层

-   `@Controller`（展示层Bean）

    一个组件，作用在控制层

-   `@Component`

    一个组件，可以作用在任何层次

    

`@Mapper`和`@Repository`的区别：

  1、使用`@Mapper`后，不需要在spring配置中设置扫描地址，通过mapper.xml里面的namespace属性对应相关的mapper类，spring将动态的生成Bean后注入到ServiceImpl中。

  2、`@Repository`则需要在Spring中配置扫描包地址，然后生成dao层的bean，之后被注入到ServiceImpl中





# 参数校验 Validator

**引入依赖**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

message属性：对应的业务提示

**约束注解**

| 注解|  功能    |
| ----------------- | --- |
| `@AssertFalse` / `@AssertTrue` | 必须为Null或False / True |
| `@DecimalMax` / `@DecimalMin` | 设置不能超过最大值 / 最小值 |
| `@Digits` | 必须是数字且数字整数的位数和小数的位数必须在指定范围内 |
| `@Future` / `@Past` | 日期必须在当前日期的未来 / 过去 |
| `@Max` / `@Min` | 最大 / 最小值 |
| `@NotNull` / `@Null` | 不能 / 必须是Null |
| `@Pattern` | 满足指定的正则表达式 |
| `@Size` | 集合、数组、map等的size()必须在指定范围内 |
| `@Email` | 必须是Email格式 |
| `@Length` | 长度在指定范围内 |
| `@NotBlank` | 字符串不能为Null或“” |
| `@NotEmpty` | 不能为Null，size不能为0，字符串不能为“” |
| `@Range` | 值在指定范围内 |
| `@URL` | 必须是URL |

-   自定义校验

-   分组校验

    某些字段在不同场景 必填/非必填 要求不同

    -   第一步：定义分组接口
    -   第二步：在模型中给参数分配分组
    -   第三步：给需要参数校验的方法指定分组

