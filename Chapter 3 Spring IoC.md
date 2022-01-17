# Chapter 3 Spring IoC
[toc]
## IoC容器
通过描述来生成或获取对象的技术
### 两个基本功能：
1. 通过描述管理Bean，包括发布和获取bean
2. 通过描述完成Bean之间的依赖关系

### BeanFactory接口源码
##### 获取Bean
```java
// 按名称获取bean
Object getBean(String name)
// 按照名称和类型获取
<T> T getBean(String name, Class<T> requiredType)
// 按类型获取bean
<T> T getBean(Class<T> requiredType)
```

##### 获取Bean的类型
Spring IoC中，bean默认以单例存在，即getBean方法返回的都是同一个**对象**。
isPrototype为true时，getBean会创建一个新Bean
```java
// 是否是单例
boolean isSingleton(String name)
// 是否是原型
boolean isPrototype(String name)
```


##### 配置文件
@Configuration: 配置文件
name为Bean的名称，如果没有就用方法名代替
```java
@Configuration
public class AppConfig {
    @Bean(name = "user")
    public User initUser(){
        return new User();
    }
}
```

##### AnnotationConfigApplicationContext

将AppConfig传递给AnnotationConfigApplicationContext构造方法
```java
ApplicationContext cxt = AnnotationConfigApplicationContext(AppConfig.class)
```

### 装配Bean

##### @Component：标明哪个类被扫入IoC
这个类将被IoC容器扫描装配
```java
@Component("user")
public class User() {
    @Value("name")
    public static final String name;
}

```
@ComponentScan：标明用何种策略去扫描装配Bean
只会扫描AppConfig所在的包和子包，将User移入当前包
```java
@Configuration
@ComponentScan
public class AppConfig {}
```
@ComponentScan配置项
basePackages：读取输入包中的类
```java
@Configuration
@ComponentScan(basePackages={"com.springboot.pojo"})
```

basePackageClasses：读取对应类型的类
```java
@Configuration
@ComponentScan(basePackageClasses={User.class})
```

excludeFilters
```java
@ComponentScan(basePackages = "com.springboot.chapter2.*",
                excludeFilters = {@Filter(classes = {UserService.class})})
```

### 依赖注入
@Autowired：根据属性找到对应的Bean进行注入
先根据属性，属性不唯一，根据名字。
```java
@Autowired(required = false)
```

#### 消除歧义性
@Primary：当出现多个Bean时，优先使用带有@Primary注解的bean
@Qualifier("dog")
```java
public Person (@Autowired @Qualifier("dog") Animal animal) {
    this.animal = animal;
}

````









