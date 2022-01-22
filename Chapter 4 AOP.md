## Chapter 4 AOP

### ProxyBean
代理
```java
public static Object newProxyInstance(ClassLoader classLoader,
                                    Class<?>[] interfaces,
                                    InvocationHandler invocationHandler)
```
- ClassLoader: 类加载器
- interfaces：绑定的接口
- invocationHandler：绑定代理的逻辑实现对象
- 


### AOP的术语和流程
- joint point：具体被拦截的对象
- point cut：切面应用于多个类的不同方法时，用正则式和指示器定义的连接点
- advice：按照约定的流程下的方法，被分为before advice, after advice, around advice, afterRounding advice, afterThrowing advice

### 开发
```java
@Aspect
public class MyAspect {
    // 定义切点
    @PointCut("execution(* UserServiceImpl.printUser(..))")
    public void pointCut(){}
    
    // 可以携带参数
    @Before("ponitCut() && args (user)")
    public void before(JointPoint jp, User user) { do something... }
}

```
