# Core knowledgr of SSM
__SpringMVC: DispatcherServlet__
`DispatcherServlet` Controls the front end. It captures the request and assign to corresponding Controllers and return the response.

__Spring: IOC and AOP__
`IOC`: Spring controls every objects. The creation and destruction and the dependency are all controlled by Spring. 

首先想说说IoC（Inversion of Control，控制倒转）。这是spring的核心，贯穿始终。所谓IoC，对于spring框架来说，就是由spring来负责控制对象的生命周期和对象间的关系。
Spring所倡导的开发方式就是如此，所有的类都会在spring容器中登记，告诉spring你是个什么东西，你需要什么东西，然后spring会在系统运行到适当的时候，把你要的东西主动给你，同时也把你交给其他需要你的东西。所有的类的创建、销毁都由spring来控制，也就是说控制对象生存周期的不再是引用它的对象，而是spring。对于某个具体的对象而言，以前是它控制其他对象，现在是所有对象都被spring控制，所以这叫控制反转。

IoC的一个重点是在系统运行中，动态的向某个对象提供它所需要的其他对象。这一点是通过DI（Dependency Injection，依赖注入）来实现的。比如对象A需要操作数据库，以前我们总是要在A中自己编写代码来获得一个Connection对象，有了spring我们就只需要告诉spring，A中需要一个Connection，至于这个Connection怎么构造，何时构造，A不需要知道。在系统运行时，spring会在适当的时候制造一个Connection，然后像打针一样，注射到A当中，这样就完成了对各个对象之间关系的控制。A需要依赖Connection才能正常运行，而这个Connection是由spring注入到A中的，依赖注入的名字就这么来的。

`AOP`: Aspecet Oriented Programming
在软件业，AOP为Aspect Oriented Programming的缩写，意为：面向切面编程，通过预编译方
式和运行期动态代理实现程序功能的统一维护的一种技术。AOP是OOP的延续，是软件开发中的一个
热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑
的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高
了开发的效率。


__MyBatis: ORM__


什么是ORM

即Object-Relationl Mapping，它的作用是在关系型数据库和对象之间作一个映射，这样，我们在具体的操作数据库的时候，就不需要再去和复杂的SQL语句打交道，只要像平时操作对象一样操作它就可以了 。

 

为什么要做持久化和ORM设计(重要)

在目前的企业应用系统设计中，MVC，即 Model（模型）- View（视图）- Control（控制）为主要的系统架构模式。MVC 中的 Model 包含了复杂的业务逻辑和数据逻辑，以及数据存取机制（如 JDBC的连接、SQL生成和Statement创建、还有ResultSet结果集的读取等）等。将这些复杂的业务逻辑和数据逻辑分离，以将系统的紧耦 合关系转化为松耦合关系（即解耦合），是降低系统耦合度迫切要做的，也是持久化要做的工作。MVC 模式实现了架构上将表现层（即View）和数据处理层（即Model）分离的解耦合，而持久化的设计则实现了数据处理层内部的业务逻辑和数据逻辑分离的解耦合。 而 ORM 作为持久化设计中的最重要也最复杂的技术，也是目前业界热点技术。

简单来说，按通常的系统设计，使用 JDBC 操作数据库，业务处理逻辑和数据存取逻辑是混杂在一起的。
一般基本都是如下几个步骤：
1、建立数据库连接，获得 Connection 对象。
2、根据用户的输入组装查询 SQL 语句。
3、根据 SQL 语句建立 Statement 对象 或者 PreparedStatement 对象。
4、用 Connection 对象执行 SQL语句，获得结果集 ResultSet 对象。
5、然后一条一条读取结果集 ResultSet 对象中的数据。
6、根据读取到的数据，按特定的业务逻辑进行计算。
7、根据计算得到的结果再组装更新 SQL 语句。
8、再使用 Connection 对象执行更新 SQL 语句，以更新数据库中的数据。
7、最后依次关闭各个 Statement 对象和 Connection 对象。

由上可看出代码逻辑非常复杂，这还不包括某条语句执行失败的处理逻辑。其中的业务处理逻辑和数据存取逻辑完全混杂在一块。而一个完整的系统要包含成 千上万个这样重复的而又混杂的处理过程，假如要对其中某些业务逻辑或者一些相关联的业务流程做修改，要改动的代码量将不可想象。另一方面，假如要换数据库 产品或者运行环境也可能是个不可能完成的任务。而用户的运行环境和要求却千差万别，我们不可能为每一个用户每一种运行环境设计一套一样的系统。
所 以就要将一样的处理代码即业务逻辑和可能不一样的处理即数据存取逻辑分离开来，另一方面，关系型数据库中的数据基本都是以一行行的数据进行存取的，而程序 运行却是一个个对象进行处理，而目前大部分数据库驱动技术（如ADO.NET、JDBC、ODBC等等）均是以行集的结果集一条条进行处理的。所以为解决 这一困难，就出现 ORM 这一个对象和数据之间映射技术。

举例来说，比如要完成一个购物打折促销的程序，用 ORM 思想将如下实现（引自《深入浅出Hibernate》）：
业务逻辑如下：
public Double calcAmount(String customerid, double amount) 
{
    // 根据客户ID获得客户记录
    Customer customer = CustomerManager.getCustomer(custmerid); 
    // 根据客户等级获得打折规则
    Promotion promotion = PromotionManager.getPromotion(customer.getLevel()); 
    // 累积客户总消费额，并保存累计结果
    customer.setSumAmount(customer.getSumAmount().add(amount); 
    CustomerManager.save(customer); 
    // 返回打折后的金额
    return amount.multiply(protomtion.getRatio()); 
}
这 样代码就非常清晰了，而且与数据存取逻辑完全分离。设计业务逻辑代码的时候完全不需要考虑数据库JDBC的那些千篇一律的操作，而将它交给 CustomerManager 和 PromotionManager 两个类去完成。这就是一个简单的 ORM 设计，实际的 ORM 实现框架比这个要复杂的多。