## spring学习笔记

### 6.29

新建maven项目——勾选Createformarchetype的单选框，选中quickstart——设置Maven后还需添加个archetypeCatalog-internal——通过maven配置spring的jar包

 <!--引入spring框架-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.2.6.RELEASE</version>
    </dependency>



报错

Internal Error occurred. org.junit.platform.commons.JUnitException: TestEngine with ID 'junit-vintage' failed to discover....

junit的版本问题，由4.1.1更新到4.1.2就可以了（注意看报错说明）

### 7.1

ApplicationContext的主要实现类是ClassPathXmlApplicationContext和FileSystemXmlApplicationContext，前者默认从类路径加载配置文件，后者默认从文件系统中装载配置文件



#### Bean管理两种方式

##### 1.基于xml配置文件方式实现

（1）在spring配置文件中，使用bean标签，标签里面添加对应属性，就可以实现对象创建。

（2）在bean标签有很多属性，介绍常用的属性

id属性：唯一标识

class属性：类全路径（包类路径）

（3）创建对象时，默认执行无参数构造方法完成对象创建

##### 2.基于注解方式实现

（1）DI：是IOC的具体体现，依赖注入

##### 3.第一种注入方式：使用set方法进行注入

（1）创建类，定义属性和对应的set方法

（2）在spring配置文件配置对象创建，配置属性注入

![image-20210701172103150](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210701172103150.png)

##### 4.第二种注入方式，使用有参数构造进行注入

（1）创建类，定义属性，创建属性对应有参数构造方法

![image-20210701172333241](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210701172333241.png)

（2）在spring配置文件中进行配置

![image-20210701172641353](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210701172641353.png)

5.p名称空间注入

（1）使用p名称空间注入，可以简化xml配置方式

第一步 添加p名称空间在配置文件中

![image-20210701174107181](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210701174107181.png)

第二步 进行属性注入，在bean标签里面进行操作

![image-20210701174716743](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210701174716743.png)

#### IOC操作bean管理

##### 1.字面量

（1）null值

![image-20210701175151188](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210701175151188.png)

（2）属性值包含特殊符号

![image-20210701180620594](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210701180620594.png)

### 7.2

##### 2.注入属性-外部bean

（1）创建两个类service类和dao类

（2）在service调用dao里面的方法

（3）在spring配置文件中进行配置

![image-20210702105719795](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702105719795.png)

![image-20210702105739996](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702105739996.png)

##### 3.注入属性-内部bean和级联赋值

（1）一对多关系：部门和员工

一个部门有多个员工，一个员工属于一个部门

部门是一，员工是多

（2）在实体类表示一对多关系，员工表示所属部门，使用对象类型属性进行表示

![image-20210702111935935](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702111935935.png)

![image-20210702112007189](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702112007189.png)

（3）在spring中进行配置

![image-20210702113334641](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702113334641.png)

##### 4.注入属性-级联赋值

（1）第一种写法

![image-20210702140314904](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702140314904.png)

(2)第二种写法

![image-20210702140631500](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702140631500.png)



#### IOC操作Bean管理（xml注入集合属性）

##### 1.注入数组类型属性

##### 2.注入List集合类型属性

##### 3.注入Map集合类型属性

##### 4.注入set集合类型属性

(1)创建类，定义数组、List、Map、Set类型属性，生成对应的set方法

![image-20210702144039131](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702144039131.png)

![image-20210702144051627](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702144051627.png)

（2）在spring配置文件进行配置

![image-20210702145119186](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702145119186.png)

![image-20210702145133829](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702145133829.png)

##### 5.在集合里面设置对象类型值

![image-20210702151527104](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702151527104.png)



##### 6.把集合注入部分提取出来

（1）在spring配置文件中引入名称空间util

![image-20210702152643410](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702152643410.png)

（2）使用util标签完成list集合注入提取

![image-20210702153443171](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702153443171.png)

#### IOC操作bean管理（FactoryBean）

##### 1.spring有两种类型bean，一种普通bean，另外一种工厂bean（FactoryBean）

##### 2.普通bean：在配置文件中定义bean类型就是返回类型

##### 3.工厂bean：在配置文件定义bean类型可以和返回类型不一样

第一步 创建类，让这个类作为工厂bean，实现接口FactoryBean

第二步 实现接口里面的方法，在实现的方法中定义返回的bean类型

![image-20210702163623629](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702163623629.png)

![image-20210702163701879](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702163701879.png)

#### IOC操作bean管理（bean作用域）

##### 如何设置是单实例还是多实例

（1）在spring配置文件bean标签里有属性（scope）用于设置单实例还是多实例

（2）scope属性值

第一个值：默认值，singleton，表示是单实例对象

第二个值：prototype，表示是多实例对象

##### ![image-20210702165517187](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702165517187.png)

![image-20210702165801606](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210702165801606.png)创建的对象不同



##### singleton和prototype区别

第一 singleton单实例，prototype多实例

第二 设置scope值是singleton时，加载spring配置文件时就会创建单实例对象

设置scope值是prototype时，不是在加载spring配置文件时候就创建对象，而是在调用getBean方法时创建多实例对象

### 7.3

#### IOC操作Bean管理（bean生命周期）

##### 1.生命周期

（1）从对象创建到销毁的过程

##### 2.bean生命周期

（1）通过构造器创建bean实例（无参数构造）

（2）为bean的属性设置值和对其他bean引用（调用set方法）

（把bean实例传递给bean后置处理器的方法）

（3）调用bean的初始化的方法（需要进行配置）

（把bean实例传递给bean后置处理器的方法）

（4）bean可以使用了（对象获取到了）

（5）当容器关闭时，调用bean的销毁的方法（需要进行配置销毁的方法）

##### 3.演示bean的生命周期

![image-20210703172051889](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703172051889.png)

![image-20210703172108592](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703172108592.png)

![image-20210703172125775](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703172125775.png)

![image-20210703172139662](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703172139662.png)

![image-20210703172152321](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703172152321.png)

##### 4.bean的后置处理器，bean的生命周期有七步

（1）通过构造器创建bean实例（无参数构造）

（2）为bean的属性设置值和对其他bean引用（调用set方法）

（3）把bean实例传递给bean后置处理器的方法postProcessBeforeInitialization

（4）调用bean的初始化的方法（需要进行配置）

（5）把bean实例传递给bean后置处理器的方法postProcessAfterInitialization

（6）bean可以使用了（对象获取到了）

（7）当容器关闭时，调用bean的销毁的方法（需要进行配置销毁的方法）

##### 5.演示添加后置处理器效果

（1）创建类，实现接口BeanPostProcessor，创建后置处理器

![image-20210703175053055](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703175053055.png)

![image-20210703175503935](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703175503935.png)

#### IOC操作Bean管理（xml自动装配）

##### 1.什么是自动装配

（1）根据指定装配规则（属性名称或者属性类型），spring自动将匹配的属性值进行注入

##### 2.演示自动装配过程

（1）根据属性名称自动注入

![image-20210703181153061](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703181153061.png)

（2）根据属性类型自动注入

![image-20210703181408680](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210703181408680.png)

#### IOC操作Bean管理（外部文件属性）

##### 1.自动配置数据库信息

（1）配置德鲁伊连接池

（2）引入德鲁伊连接池依赖jar包

### 7.5

#### IOC操作Bean管理（基于注解方式）

##### 1.什么是注解

（1）注解是代码特殊标记，格式：@注解名称（属性名称=属性值，属性名称=属性值...)

（2）使用注解，注解作用在类上面，方法上面，属性上面

（3）使用注解目的：简化xml配置

##### 2.Spring针对Bean管理中创建对象提供注解

(1)@Component

(2)@Service

(3)@Controller

(4)@Repository——dao

*上面四个注解功能是一样的，都可以用来创建bean实例

##### 3.基于注解方式实现对象创建

第一步 引入依赖

maven引入aop

第二步 开启组件扫描

![image-20210705164025204](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705164025204.png)

第三步 创建类，在类上面添加对象注解

![image-20210705165347675](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705165347675.png)

##### 4.开启组件扫描细节配置

![image-20210705174526440](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705174526440.png)

##### 5.基于注解方式实现属性注入

（1）@AutoWired：根据属性类型进行自动装配

第一步 把service和dao对象创建，在service和dao类添加创建对象注释

第二步 在service注入dao对象，在service类添加dao类型属性，在属性上面使用注解

![image-20210705181914841](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705181914841.png)



（2）@Qualifier：根据属性名称进行注入

这个@Qualifier注解的使用，和上面@Autowired一起使用

![image-20210705182431394](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705182431394.png)



（3）@Resource：可以根据类型注入，可以根据名称注入

![image-20210705182850150](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705182850150.png)

（4）@Value：注入普通类型属性

![image-20210705183019428](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705183019428.png)

##### 6.完全注解开发

（1）创建配置类，替代xml配置文件

![image-20210705200252574](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705200252574.png)

（2）编写测试类

![image-20210705200842973](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210705200842973.png)









#### AOP(概念)

##### 1.什么是AOP

（1）面向切面编程，利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的[耦合度](https://baike.baidu.com/item/耦合度/2603938)降低，提高程序的可重用性，同时提高了开发的效率。

（2）通俗描述：不通过修改源代码的方式，在主干功能里面添加新功能

（3）使用登录例子说明AOP

### 7月7日

#### AOP（底层原理）

##### （1）有两种情况的动态代理

第一种 有接口情况，使用JDK动态代理

创建类实现类代理对象，增强类的方法

interface UserDao{

​	public void login();

}

JDK动态代理

1 创建UserDao接口实现类代理对象

代理对象

class UserDaoImpl implements UserDao{

​	public void login(){

​		//登录实现过程

​	}

}

JDK动态代理

1.创建UserDao接口实现类代理对象

##### 第二种 没有接口情况，使用CGLIB动态代理

Class User{

​	public void add(){

​		......

​	}

}



class Person extends User{

​	public void add(){

​		super.add();

​		//增强逻辑	

​	}

}

CGLIB动态代理	1.创建当前类子类的代理对象 

#### AOP（JDK动态代理）

##### 1.动态代理（dynamic proxy）

           利用Java的反射技术(Java Reflection)，在运行时创建一个实现某些给定接口的新类（也称“动态代理类”）及其实例（对象）,代理的是接口(Interfaces)，不是类(Class)，也不是抽象类。在运行时才知道具体的实现，spring aop就是此原理。

   public static Object newProxyInstance(ClassLoader loader,
                                          Class<?>[] interfaces,
                                          InvocationHandler h)
        throws IllegalArgumentException
调用newProxyInstance方法

方法有三个参数：

loader: 用哪个类加载器去加载代理对象

interfaces:动态代理类（增强方法所在的类）需要实现的接口

 InvocationHandler:动态代理方法在执行时，会调用h里面的invoke方法去执行，创建代理对象，写增强的方法

##### 2.编写JDK动态代理代码

（1）创建接口，定义方法

![image-20210709112716044](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210709112716044.png)

（2）创建接口实现类

![image-20210709112730798](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210709112730798.png)

（3）使用proxy类创建接口代理对象

```
public class JDKProxy {

    public static void main(String[] args) {
    //    创建接口实现类的代理对象
        Class[] interfaces = {UserDao.class};
        //Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new InvocationHandler() {
        //    @Override
        //    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //        return null;
        //    }
        //});
        //不改变原有代码条件下改变方法
        UserDaoImpl userDao = new UserDaoImpl();
        UserDao dao = (UserDao) Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new UserDaoProxy(userDao));
        int sum = dao.add(1,2);
        System.out.println(sum);

    }
}

//创建代理对象代码
class UserDaoProxy implements InvocationHandler {

    //1 把创建的是谁的代理对象，把谁传递过来
    //有参数构造传递
    private Object obj;
    public UserDaoProxy(Object obj){
        this.obj = obj;
    }
    //增强的逻辑
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

        //方法之前
        System.out.println("方法之前执行......" + method.getName() + ":传递的参数..." + Arrays.toString(args));

        //被增强的方法执行
        Object res = method.invoke(obj, args);

        //方法之后
        System.out.println("方法之后执行..." + obj);
        return null;
    }
}
```

### 7月9日

#### AOP(术语)

##### 1.连接点

类里面那些方法可以被增强，这些方法称为连接点

##### 2.切入点

实际被真正增强的方法，称为切入点

##### 3.通知（增强）

（1）实际增强的逻辑部分称为通知（增强）

（2）通知有多种类型

*前置通知

*后置通知

*环绕通知

*异常通知

*最终通知	finally

##### 4.切面

是动作

（1）把通知应用到切入点过程

AOP操作（准备）

1.spring框架一般都是基于AspectJ实现AOP操作

（1）什么是AspectJ

*AspectJ不是Spring组成部分，独立AOP框架，一般把AspectJ和Spring框架一起使用，进行AOP操作

2.基于AspectJ实现AOP操作

（1）基于xml配置文件实现

（2）基于注解方式实现(使用)

3.在项目工程里面引入AOP相关依赖

![image-20210709141601385](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210709141601385.png)

4.切入点表达式

（1）切入点表达式作用：知道对哪个类里面的哪个方法进行增强

（2）语法结构：

Execution（[权限修饰符] [返回类型] [类全路径] [方法名称]（[参数列表)]）

举例1：对com.dao.BookDao类里面的add进行增强

execution(*com.dao.BookDao.add(..))

举例2：对com.dao.BookDao类里面的所有的方法进行增强

execution(*com.dao.BookDao. *(..))	(空格不需要)

举例3：对com.dao.包里面所有类，类里面的所有的方法进行增强

execution(*com.dao. * .*(..))	(空格不需要)

#### AOP操作（AspectJ注解）

##### 1.创建类，在类里面定义方法

```
public class User {
    public void add(){
        //int i = 10 / 0;
        System.out.println("add......");
    }
}
```

##### 2.创建增强类（编写增强逻辑）

（1）在增强类里面，创建方法，让不同方法代表不同通知类型

```
public class User {
	public void before(){
    	System.out.println("before......");
	}
}
```

##### 3.进行通知的配置

（1）在spring配置文件中，开启注解扫描

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--开启注解扫描-->
    <context:component-scan base-package="org.example.aopanno"></context:component-scan>
```

（2）使用注解创建User和UserProxy对象

```
@Component
public class User {
```

```
//增强的类
@Component
public class UserProxy {
```

（3）在增强类上面添加注解@Aspect

```
//增强的类
@Component
@Aspect //生成代理对象
public class UserProxy {
```

（4）在spring配置文件中开启生成代理对象

```
<!--开启Aspect生成代理对象-->
<aop:aspectj-autoproxy></aop:aspectj-autoproxy>
```

##### 4.配置不同类型的通知

（1）在增强类的里面，在作为通知方法

```
//前置通知
//@Before注解表示作为前置通知
//@Before(value = "execution(* org.example.aopanno.User.add(..))")
@Before(value = "pointdemo()")
public void before(){

    System.out.println("before......");
}
```

```
//增强的类
@Component
@Aspect //生成代理对象
public class UserProxy {

    //前置通知
    //@Before注解表示作为前置通知
    @Before(value = "execution(* org.example.aopanno.User.add(..))")
    public void before(){
        System.out.println("before......");
    }

    //最终通知
    @After(value = "execution(* org.example.aopanno.User.add(..))")
    public void after(){
        System.out.println("after......");
    }

    //后置通知（返回通知）
    @AfterReturning(value = "execution(* org.example.aopanno.User.add(..))")
    public void afterReturning(){
        System.out.println("afterReturning......");
    }

    //异常通知
    @AfterThrowing(value = "execution(* org.example.aopanno.User.add(..))")
    public void afterThrowing(){
        System.out.println("afterThrowing......");
    }

    //环绕通知
    @Around(value = "execution(* org.example.aopanno.User.add(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable{
        System.out.println("环绕之前......");
        //被增强的方法执行
        proceedingJoinPoint.proceed();
        System.out.println("环绕之后......");
    }
}
```

##### 5.相同的切入点进行抽取

```
//相同切入点抽取
@Pointcut(value = "execution(* org.example.aopanno.User.add(..))")
public void pointdemo(){

}

//前置通知
//@Before注解表示作为前置通知
//@Before(value = "execution(* org.example.aopanno.User.add(..))")
@Before(value = "pointdemo()")
public void before(){
    System.out.println("before......");
}
```

##### 6.有多个增强类对同一个方法进行增强，设置增强类优先级

（1）在增强类上面注释@Order（数字类型值），数字类型值越小优先级越高

```
@Order(1)
public class PersonProxy {
```

##### 7.完全使用注解开发

（1）创建配置类，不需要创建xml配置文件

```
@Configuration
@ComponentScan(basePackages = {"org.example"})
@EnableAspectJAutoProxy(proxyTargetClass = true)
public class ConfigAop {
}
```

##### AOP操作（AspectJ配置文件）

##### 1.创建两个类，增强类和被增强类，创建方法

```
public class Book {
    public void buy(){
        System.out.println("buy......");
    }
}
```

```
public class BookProxy {

    public void before(){
        System.out.println("before......");
    }
}
```

##### 2.在spring配置文件中创建两个类对象

```
<!--创建对象-->
<bean id="book" class="org.example.aopxml.Book"></bean>
<bean id="bookProxy" class="org.example.aopxml.BookProxy"></bean>
```

##### 3.在spring配置文件中配置切入点

```
<!--配置aop增强-->
<aop:config>
    <!--切入点-->
    <aop:pointcut id="p" expression="execution(* org.example.aopxml.Book.buy(..))"/>

    <!--配置切面-->
    <aop:aspect ref="bookProxy">
        <!--增强作用在具体的方法上-->
        <aop:before method="before" pointcut-ref="p"/>
    </aop:aspect>
</aop:config>
```

#### JdbcTemplate(概念和准备)

##### 1.什么是JdbcTemplate

（1）Spring框架对JDBC进行封装，使用JdbcTemplate方便实现对数据库操作

2.准备工作

（1）引入相关jar包

![image-20210712181827682](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210712181827682.png)

（2）在spring配置文件配置数据库连接池

```
<!--数据库连接池-->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
      destroy-method="close">
    <property name="url" value="jdbc:mysql:///user_db"/>
    <property name="username" value="root"/>
    <property name="password" value="123456"/>
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
</bean>
```

（3）配置JdbcTemplate对象，注入DataSource

```
<!--JdbcTemplate对象-->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <!--注入dataSource-->
    <property name="dataSource" ref="dataSource"></property>
</bean>
```

（4）创建service类，创建dao类，在dao注入jdbcTemplate对象

```
<!--组件扫描-->
<context:component-scan base-package="org.example"></context:component-scan>
```

Service

```
@Service
public class BookService {

    //注入dao
    @Autowired
    private BookDao bookDao;
}
```

Dao

```
@Repository
public class BookDaoImpl implements BookDao{

    //进入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;

}
```

### 7月12日

#### JdbcTemplate操作数据库（添加）

##### 1.创建实体类

```
public class User {
    private String userId;
    private String username;
    private String ustatus;

    public String getUserId() {
        return userId;
    }

    public void setUserId(String userId) {
        this.userId = userId;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getUstatus() {
        return ustatus;
    }

    public void setUstatus(String ustatus) {
        this.ustatus = ustatus;
    }
}
```

2.编写service和dao

（1）在dao进行数据库添加操作

（2）调用JdbcTemplate对象里面update方法实现添加操作

![image-20210712183924247](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210712183924247.png)

有两个参数

第一个参数：sql语句

第二个参数：可变参数，设置sql语句值3.

```
@Repository
public class BookDaoImpl implements BookDao{

    //进入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public void add(Book book) {
        //1 创建sql语句
        String sql = "insert into t_book values(?,?,?)";
        //2 调用方法实现
        Object[] args = {book.getUserId(), book.getUsername(), book.getUstatus()};
        int update = jdbcTemplate.update(sql, book.getUserId(), book.getUsername(), book.getUstatus());
        System.out.println(update);
    }
}
```

3.测试类

```
@Test
public void testJdbcTemplate(){
    ApplicationContext context = new ClassPathXmlApplicationContext("datasource.xml");
    BookService bookService = context.getBean("bookService", BookService.class);

    Book book = new Book();
    book.setUserId("1");
    book.setUsername("hcs");
    book.setUstatus("java滴神");
    bookService.addBook(book);
}
```

![image-20210712202130513](C:\Users\Xpeng\AppData\Roaming\Typora\typora-user-images\image-20210712202130513.png)

