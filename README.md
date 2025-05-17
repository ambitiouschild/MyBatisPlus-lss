# MyBatisPlus-lss

#### 介绍
MyBatisPlus-lss，是一个MyBatis的增强工具，在MyBatis的基础上只做增强不做改变，为简化开发、提高效率而生。MyBatis-Plus提供了通用的mapper和service，可以在不编写任何SQL语句的情况下，快速的实现对单表的CRUD、批量、逻辑删除、分页等操作。

MyBatis-Plus提供的优秀插件

#### 软件架构
MySQL数据库为案例

Idea为IDE

Maven为构建工具

Spring Boot展示MyBatis-Plus的各个功能



BaseMapper：泛型接口汇聚了各种数据库操作，包括插入、更新、删除和查询等功能。借助`BaseMapper`，我们能够毫不费力地构建个性化的 Mapper接口，而无需繁琐地编写SQL语句。



IService：自定义定义各种业务方法，无需亲自编写插入数据库的SQL语句。这种高层次的抽象，让我们在面对复杂的数据操作时，能够以更加清晰、简洁的方式表达业务需求。



ServiceImpl：可谓 Mybatis-Plus 高效魔法的完美体现，它是 `IService` 接口的默认实现。在 `ServiceImpl` 中，不仅实现了 `IService` 中定义的各种基本业务方法，还额外赋予了一些更加高级的查询操作，如 `lambdaQuery`、`page` 等。通过继承 `ServiceImpl`，我们能够轻松地编写出贴合业务需求的 Service 实现类。






#### 安装教程

1.  MyBatis-Plus官网

https://baomidou.com/



1.  xxxx
2.  xxxx

#### 使用说明

### 1.BaseMapper： 数据操作的多功能工具

### 2.Service： 拥抱业务逻辑的抽象境界

### 3.ServiceImpl： 业务逻辑的娴熟演绎

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request


## **快速理解Mybatis-plus中BaseMapper、IService和ServiceImpl**

1.  `Mybatis-Plus`是一个强大且富有表现力的持久层框架，它在`Mybatis`的基础上提供了更多的便利和功能。在使用Mybatis-Plus时，你会遇到几个重要的接口：`BaseMapper`、`IService`和`ServiceImpl`。这些接口是`Mybatis-Plus`的核心组成部分，它们为我们简化了数据访问层的开发，让我们可以更专注于业务逻辑的实现。

### 1.BaseMapper： 数据操作的多功能工具

>  在 `Mybatis-Plus` 这个高效而又灵活的持久层框架中，`BaseMapper` 可以被视为一把数据操作的多功能瑞士军刀。这个泛型接口汇聚了各种数据库操作，包括插入、更新、删除和查询等功能。借助`BaseMapper`，我们能够毫不费力地构建个性化的 Mapper接口，而无需繁琐地编写SQL语句。`Mybatis-Plus`巧妙地运用命名规范，自动生成SQL，这为我们的数据操作代码带来了前所未有的便捷性。

让我们用一个例子来说明，假设我们有一个 User 实体类，而我们希望进行查询操作。只需要定义一个继承自 BaseMapper 的接口，我们就能够轻松调用 BaseMapper 提供的各种查询方法，如 selectList、selectById 等。这意味着我们能够愉快地进行数据的增、删、改、查操作，大大减少了琐碎的SQL编写过程。

**充分利用命名规范的妙处**

`Mybatis-Plus 的 BaseMapper` 并非单纯地提供了一套预设的增删改查操作，而是根据实体类和数据库表的命名规范，智能地生成相应的SQL语句。这就意味着，你无需将大量时间浪费在手动编写和优化SQL上，而是专心构建数据访问逻辑和业务逻辑。

继续以前述的 `User` 实体类为例，如果我们在数据库中拥有名为 `user` 的表，那么 `Mybatis-Plus` 会自动将这两者关联起来，为我们生成合适的SQL。这种智能化的匹配，使得我们的代码更加简洁、易读，同时也避免了一些潜在的错误。



```
// 假设我们有一个 User 实体类

// 定义一个继承 BaseMapper 的自定义 Mapper 接口
public interface UserMapper extends BaseMapper<User> {
    // 无需手写SQL，Mybatis-Plus 根据命名规范自动生成SQL
}

// 在业务逻辑中使用 BaseMapper 进行数据操作
public class UserService {
    @Autowired
    private UserMapper userMapper;

    public List<User> getUsersByName(String name) {
        QueryWrapper<User> queryWrapper = new QueryWrapper<>();
        queryWrapper.eq("name", name);
        return userMapper.selectList(queryWrapper);
    }

    // ...其他业务方法
}
```



**小结**

`BaseMapper` 是 `Mybatis-Plus` 中的一颗明珠，它简化了数据操作的复杂性，通过智能的SQL生成机制，让开发者能够更专注于业务逻辑的编写。借助命名规范，我们能够在编写数据操作代码时获得更多的自动化支持，减少了重复性的劳动，提升了开发效率。无论是初学者还是有经验的开发者，都能够从 `BaseMapper` 中受益，更轻松地构建出高效、可维护的应用。



### 2.Service： 拥抱业务逻辑的抽象境界

在 `Mybatis-Plus` 的舞台上，`IService` 接口宛如业务逻辑的一片宁静湖泊。这个接口将常见的业务操作抽象化，包括保存、删除、更新、查询等。通过继承 `IService` 接口，我们能够在 `Service` 层更专注于业务逻辑的实现，而不必过分纠结于底层的数据库操作细节。

------

假设我们拥有一个 `UserService` 接口，它继承了 `IService<User>` 接口。在这个 `UserService` 中，我们可以定义各种业务方法，如 `getUserByName、createUser` 等。这样一来，我们的注意力就可以更加集中于业务逻辑的构建，从而大幅提升代码的可读性和可维护性。

**解放业务逻辑**

透过 `IService` 这个抽象层，我们能够将业务逻辑从繁琐的数据库操作中解放出来。比如，你要实现一个用户注册的功能。借助 `IService`，你只需在 `UserService` 中定义一个 `createUser` 方法，无需亲自编写插入数据库的SQL语句。这种高层次的抽象，让我们在面对复杂的数据操作时，能够以更加清晰、简洁的方式表达业务需求。



```
// 定义一个继承 IService 的自定义 Service 接口
public interface UserService extends IService<User> {
    User getUserByName(String username);
    void createUser(User user);
    // ...其他业务方法
}

// 在业务逻辑实现中充分利用 IService 的便利
@Service
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements UserService {
    @Override
    public User getUserByName(String username) {
        // 调用 IService 提供的方法进行查询
        QueryWrapper<User> queryWrapper = new QueryWrapper<>();
        queryWrapper.eq("username", username);
        return this.getOne(queryWrapper);
    }
    
    @Override
    public void createUser(User user) {
        // 调用 IService 提供的方法进行插入
        this.save(user);
    }
    // ...其他业务方法的实现
}
```



**细致的业务构建**

通过抽象出 IService，我们能够更加深入地思考和构建业务逻辑。在 UserService 中，我们可以将业务操作切分为各个方法，从而提升代码的可维护性。这种方式，不仅让业务逻辑更具层次感，也使得团队协作变得更加流畅。

**小结**

`IService` 是 `Mybatis-Plus` 框架中的一颗明珠，它将业务逻辑与底层的数据库操作解耦，为我们提供了一个清晰而又高效的业务抽象层。通过继承 `IService`，我们能够更专注于业务逻辑的构建，让代码更加简洁易读。借助这个抽象，我们能够在项目中轻松创建出高度可维护和可扩展的业务层，为软件开发注入更多的便利与创造力。





### 3.ServiceImpl： 业务逻辑的娴熟演绎

`ServiceImpl` 可谓 Mybatis-Plus 高效魔法的完美体现，它是 `IService` 接口的默认实现。在 `ServiceImpl` 中，不仅实现了 `IService` 中定义的各种基本业务方法，还额外赋予了一些更加高级的查询操作，如 `lambdaQuery`、`page` 等。通过继承 `ServiceImpl`，我们能够轻松地编写出贴合业务需求的 Service 实现类。

**娴熟编织业务逻辑**

以一个例子来阐述，假设我们要实现一个 `UserService` 的实现类。我们只需要继承 `ServiceImpl<UserMapper, User>`，然后在其中娴熟地实现我们所定义的业务方法。通过这种简洁的方式，我们不必为基本的数据操作费心劳神，从而将更多精力投入到真正的业务逻辑编写中。

**充盈的高级查询功能**

除了基本的业务方法外，`ServiceImpl` 还附加了更多高级查询方法。以 `lambdaQuery` 为例，我们能够使用 Lambda 表达式编写更加优雅的查询条件，使得代码更具可读性。另外，`page` 方法能够让我们轻松实现分页查询，有效地处理大量数据的查询需求。

**事务管理的坚实后盾**

值得一提的是，`ServiceImpl` 对事务管理提供了坚实的支持。这使得我们的业务逻辑在执行多个数据操作时，能够保持数据一致性和可靠性。通过 `@Transactional` 注解，我们能够轻松地实现事务的控制，无需担心数据操作带来的风险。

**示例代码示范**

总结与展望： 解放开发者，提升效率

```
// 在业务逻辑实现中继承 ServiceImpl，轻松构建业务方法
@Service
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements UserService {
    @Override
    public User getUserByName(String username) {
        // 使用 lambdaQuery 方法编写更优雅的查询条件
        return this.lambdaQuery().eq(User::getUsername, username).one();
    }
    
    @Override
    public void createUser(User user) {
        // 调用 ServiceImpl 提供的方法进行插入
        this.save(user);
    }
    // ...其他业务方法的实现
}
```

**小结与展望**

`ServiceImpl` 是 Mybatis-Plus 这个高效持久层框架中的灵魂角色，它不仅为我们提供了 `IService` 的默认实现，还赋予了更多高级查询功能和事务管理的支持。通过 `ServiceImpl`，我们能够以更加清晰、简单的方式编写业务逻辑，摆脱了繁琐的数据操作细节。它是构建高度可靠、高效、易扩展的业务层的理想工具，为软件开发铺就了一条光明之路。

通过对这些核心接口的深入理解和灵活应用，我们可以更好地驾驭`Mybatis-Plus`这个工具，提升项目开发的效率和质量，为软件开发的未来铺平道路。
