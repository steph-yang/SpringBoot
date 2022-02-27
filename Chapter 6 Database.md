## Chapter 6 Database

### 声明式数据库
@Transactional: 底层启用AOP

### 隔离级别
#### 数据库事务的特征
1. Atomic：事务中包含的操作要么全部成功，要么全部失败、
2. Consistency：事务完成时，所有的数据保持一致的状态
3. Isolation
· 第一类丢失更新：一个线程回滚导致
· 第二类丢失更新：多线程提交导致
4. Durality：事务结束后，所有的数据会固化到一个地方

#### 隔离级别
1. 读未提交 read uncommitted：允许一个事务读取另一个事务没有提交的数据
· 引发脏读：回滚到另一线程已提交的内容
2. 读已提交 read committed：只允许一个事务读取另一个事务已经提交的数据
· 不可重读：一个事务先提交，导致另一事务提交失败
3. 可重复读：阻塞其他事务读取，必须等到第一个事务提交完毕
· 幻读
4. 串行化：严格按照顺序执行

``` {java}
@Transactional(isolation = Isolation.SERIALIZABLE)
```

### 传播行为






