---
title: 'O2O: Project Structure and Configuration'
date: 2019-08-01T06:24:45.843Z
tags: ['Database', 'Java', 'Tomcat', 'Maven', 'Spring', 'MyBatis', 'MySQL', 'Web', 'O2O']
categories: ['CS']
---

# Notes of O2O projcet

## Tech stack
1. SSM: Spring, SpringMVC, MyBatis
## Project Structure
### General Structure
#### Front End
![Notes-2019-7-30-21-48-14.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-48-14.png)

#### Shop
![Notes-2019-7-30-21-48-32.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-48-32.png)

![Notes-2019-7-30-21-49-14.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-49-14.png)

#### Administrator
![Notes-2019-7-30-21-49-0.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-49-0.png)

#### Product

![Notes-2019-7-30-21-50-17.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-50-17.png)

### Concrete Class
![Notes-2019-7-29-17-21-23.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-29-17-21-23.png)
#### Area
![Notes-2019-7-29-17-22-14.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-29-17-22-14.png)
__1. Build the class in Java__
![Notes-2019-7-29-17-50-54.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-29-17-50-54.png)

__1. Build the table in database__
![Notes-2019-7-29-17-52-58.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-29-17-52-58.png)

![Notes-2019-7-29-19-47-45.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-29-19-47-45.png)

__Q: Why do we use DateTime rather than TimeStamp in mySQL?__
__A: Because DateTime has a larger range of 0000 -> 9999 year, while TimeStamp can only varies between 1970 and 2037. However, TimeStamp can automatically adjust to the current time zone.__

__Q: What's the difference between InnoDB and MYISAM?__
__A: MYISAM has a table lock that doesn't allow multiple threads modifying the table while current thread working on it. InnoDB is locked by row. Also, MYISAM has a better read performance, while InnoDB has a better write performance.__

#### PersonInfo

![Notes-2019-7-29-19-48-53.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-29-19-48-53.png)

![Notes-2019-7-29-19-51-51.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-29-19-51-51.png)

![Notes-2019-7-30-16-10-28.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-16-10-28.png)

![Notes-2019-7-30-16-10-50.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-16-10-50.png)

#### WechatAuth and LocalAuth

![Notes-2019-7-30-16-12-50.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-16-12-50.png)

![Notes-2019-7-30-16-14-45.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-16-14-45.png)

![Notes-2019-7-30-16-16-31.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-16-16-31.png)

![Notes-2019-7-30-16-23-45.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-16-23-45.png)

![Notes-2019-7-30-16-57-58.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-16-57-58.png)

![Notes-2019-7-30-16-58-44.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-16-58-44.png)

> Here we should also change open_id in tb_wechat_auth into a unique key.

__Q: Why do we want to set username to be unique?__
__A: Because we want to improve the performance of lookup. __

#### HeadLine
![Notes-2019-7-30-17-8-50.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-17-8-50.png)

![Notes-2019-7-30-17-12-3.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-17-12-3.png)
![Notes-2019-7-30-17-15-35.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-17-15-35.png)

#### ShopCategory
![Notes-2019-7-30-17-19-17.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-17-19-17.png)

![Notes-2019-7-30-20-57-2.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-20-57-2.png)

> parentId is like a recurrence relation here. if the parent is null, that means the category is the root. Any child node can traverl all the way back to root.

#### Shop
![Notes-2019-7-30-21-5-5.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-5-5.png)

![Notes-2019-7-30-21-11-59.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-11-59.png)

![Notes-2019-7-30-21-12-20.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-12-20.png)

#### ProductCategory
![Notes-2019-7-30-21-15-54.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-15-54.png)

![Notes-2019-7-30-21-16-44.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-16-44.png)

#### ProductImg

![Notes-2019-7-30-21-22-37.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-22-37.png)

![Notes-2019-7-30-21-23-26.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-23-26.png)

#### Product
![Notes-2019-7-30-21-27-50.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-27-50.png)

![Notes-2019-7-30-21-33-45.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-33-45.png)

![Notes-2019-7-30-21-34-3.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-34-3.png)

![Notes-2019-7-30-21-34-24.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-30-21-34-24.png)

### Configurations
#### Packages of the projects
![Notes-2019-7-31-8-43-55.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-8-43-55.png)

#### Dependencies
1. Junit
> Has to be higher than 4.12, otherwise there's error. 
2. Logback
![Notes-2019-7-31-8-47-55.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-8-47-55.png)

> Here we want to remove \<scope>test\<scope>, since we also want it to appear in the actual scope.

3. spring 
```xml
<properties>
    <spring.version>4.3.7.RELEASE</spring.version>
</properties>

<dependencies>
    <!-- Spring -->
    <!-- 1)包含Spring 框架基本的核心工具类。Spring 其它组件要都要使用到这个包里的类，是其它组件的基本核心 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- 2)这个jar 文件是所有应用都要用到的，它包含访问配置文件、创建和管理bean 以及进行Inversion of Control
      / Dependency Injection（IoC/DI）操作相关的所有类。如果应用只需基本的IoC/DI 支持，引入spring-core.jar
      及spring-beans.jar 文件就可以了。 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- 3)这个jar 文件为Spring 核心提供了大量扩展。可以找到使用Spring ApplicationContext特性时所需的全部类，JDNI
      所需的全部类，instrumentation组件以及校验Validation 方面的相关类。 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- 4) 这个jar 文件包含对Spring 对JDBC 数据访问进行封装的所有类。 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- 5) 为JDBC、Hibernate、JDO、JPA等提供的一致的声明式和编程式事务管理。 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- 6)Spring web 包含Web应用开发时，用到Spring框架时所需的核心类，包括自动载入WebApplicationContext特性的类、Struts与JSF集成类、文件上传的支持类、Filter类和大量工具辅助类。 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- 7)包含SpringMVC框架相关的所有类。 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- 8)Spring test 对JUNIT等测试框架的简单封装 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${spring.version}</version>
      <scope>test</scope>
</dependencies>

```

4. Servlet
Servlet serevice dependency
```xml
    <!-- Servlet web -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
    </dependency>
```

5. json support for front-end
```xml
    <!-- json解析 -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.9.9</version>
    </dependency>
```

6. spring-core dependency
```xml
    <!-- Map工具类 对标准java Collection的扩展 spring-core.jar需commons-collections.jar -->
    <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
      <version>3.2.2</version>
    </dependency>
```

7. mybatis dependency
```xml
    <!-- DAO: MyBatis -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.1</version>
    </dependency>
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>2.0.1</version>
    </dependency>
```

8. mysql
mysql-connector-java supports sql api
com.mchange supports connection pool

```xml
<!-- 数据库 -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.16</version>
</dependency>
<!-- https://mvnrepository.com/artifact/com.mchange/c3p0 -->
<dependency>
    <groupId>com.mchange</groupId>
    <artifactId>c3p0</artifactId>
    <version>0.9.5.4</version>
</dependency>
```

```
什么是连接池
数据库连接池负责分配、管理和释放数据库连接，它允许应用程序重复使用一个现有的数据库连接，而不是再重新建立一个。

为什么要使用连接池
 数据库连接是一种关键的有限的昂贵的资源，这一点在多用户的网页应用程序中体现得尤为突出。  一个数据库连接对象均对应一个物理数据库连接，每次操作都打开一个物理连接，使用完都关闭连接，这样造成系统的 性能低下。 数据库连接池的解决方案是在应用程序启动时建立足够的数据库连接，并讲这些连接组成一个连接池(简单说：在一个“池”里放了好多半成品的数据库联接对象)，由应用程序动态地对池中的连接进行申请、使用和释放。对于多于连接池中连接数的并发请求，应该在请求队列中排队等待。并且应用程序可以根据池中连接的使用率，动态增加或减少池中的连接数。 连接池技术尽可能多地重用了消耗内存地资源，大大节省了内存，提高了服务器地服务效率，能够支持更多的客户服务。通过使用连接池，将大大提高程序运行效率，同时，我们可以通过其自身的管理机制来监视数据库连接的数量、使用情况等。 
--------------------- 
作者：CrankZ 
来源：CSDN 
原文：https://blog.csdn.net/crankz/article/details/82874158 
版权声明：本文为博主原创文章，转载请附上博文链接！
```

#### Configurations
1. jdbc
File name is __jdbc.properties__, save it under src/main/resources
```js
jdbc.driver = com.mysql.jdbc.Driver
jdbc.url = jdbc:mysql://localhost:3306/o2o?useUnicode=true&characterEncoding=utf8
jdbc.username = root
#jdbc.password = password
```

2. mybatis
File name is __mybatis-config.xml__, save it under src/main/resources
```xml
<!-- 使用jdbc的getGeneratedKeys获取数据库自增主键值 -->
<setting name="useGeneratedKeys" value="true" />

<!-- 使用列标签替换列别名 默认:true -->
<setting name="useColumnLabel" value="true" />

<!-- 开启驼峰命名转换:Table{create_time} -> Entity{createTime} -->
<setting name="mapUnderscoreToCamelCase" value="true" />
```

3. spring
__spring-dao.xml__
```xml
<!-- 配置整合mybatis过程 -->
  <!-- 1.配置数据库相关参数properties的属性：${url} -->
  <!-- 2.配置连接池属性 -->
  <!-- 3.配置SqlSessionFactory对象 -->
  <!-- 4.配置扫描Dao接口包，动态实现Dao接口，注入到spring容器中 -->
```
__spring-service.xml__

```xml
  <!-- 扫描service包下所有使用注解的类型 -->
    <!-- 配置事务管理器 -->
        <!-- 注入数据库连接池 -->
  <!-- 配置基于注解的声明式事务 -->

```
__spring-web.xml__
```xml
  <!-- 配置SpringMVC -->
  <!-- 1.开启SpringMVC注解模式 -->
    <!-- 2.静态资源默认servlet配置 (1)加入对静态资源的处理：js,gif,png (2)允许使用"/"做整体映射 -->
  <!-- 3.定义视图解析器 -->
  <!-- 4.扫描web相关的bean -->

```

4. web.xml
Integrate the configuration of Spring
```xml
  <servlet>
    <servlet-name>spring-dispatcher</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:spring/spring-*.xml</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>spring-dispatcher</servlet-name>
<!--    默认匹配所有的请求 -->
    <url-pattern>/</url-pattern>
  </servlet-mapping>
```

5. Review
![Notes-2019-7-31-10-7-2.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-10-7-2.png)


### Test for DAO

Take Area class as an example, we try to implement its DAO. 

__Q: What is DAO?__
__A: DAO是Data Access Object数据访问接口，数据访问：顾名思义就是与数据库打交道。In computer software, a data access object (DAO) is an object that provides an abstract interface to some type of database or other persistence mechanism. By mapping application calls to the persistence layer, the DAO provides some specific data operations without exposing details of the database. This isolation supports the single responsibility principle. It separates what data access the application needs, in terms of domain-specific objects and data types (the public interface of the DAO), from how these needs can be satisfied with a specific DBMS, database schema, etc. (the implementation of the DAO).__

We first implement the interface of user's operation(such as insertion, deletion, update, query), and then map the DAO in the myBatis (mapper package) to the entity class. There we define the type of the operation and return type, then we can write SQLs to execute the actual queries.

Step:
1. create interface AreaDao in o2o.dao
2. create config file AreaDao.xml in resources.mapper
> Here we don't need to implement the actual AreaDao class but simply provide an interface is enough. MyBatis will do the job for us. We just need to map it to MyBatis.
3. Specify the namespace, id, and resultType
![Notes-2019-7-31-16-18-3.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-16-18-3.png)
4. Write the test for the dao.

First, create a BaseTest class in test/.../o2o/, which is used to initialize Spring and Junit configuration

![Notes-2019-7-31-21-9-26.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-21-9-26.png)
> @RunWith and @ContextConfiguratiion are often used together. First one indicate what test runner we want to use for junit. @ContextConfiguration indicates the Config file of Spring DAO.

Then create a concrete test class AreaDaoTest in ~/o2o.dao extending the BaseTest.

![Notes-2019-7-31-21-12-11.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-21-12-11.png)

> @Autowired is used to assemble the DAO class by Spring. Every time we declare an interface with @Autowired, Spring will automatically use its implementation class.

5. Debug.

+ in `jdbc.properties`, password line cannot be omitted
+ jdbc.driver is deprecated, shoule be changed to `com.mysql.cj.jdbc.Driver`
+ Add `&serverTimezone=UTC` to jdbc url
+ Make sure all paths are configured correctly.

### Test for Service
1. Create `AreaService` interface in service package, which has a getAreaList API. 
2. Create `AreaServiceImpl` class in service.impl package, create a DAO and implement the API. Just simply return the DAO's queryArea() API.

![Notes-2019-7-31-21-34-33.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-21-34-33.png)

3. Create `serevice.AreaServiceTest` in test package, and add config file to the BaseTest.
``` java
@ContextConfiguration({"classpath:spring/spring-dao.xml", "classpath:spring/spring-service.xml"})
```

4. Same as testDao, test the getAreaList() API we defined in interface AreaService. Here we changed a way to test it. Notice that since we configure the mapper with AreaDao.xml, we know that the result return from the database is exactly the field we defined in entity class Area.

![Notes-2019-7-31-21-46-58.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-21-46-58.png)

### Test for Controller

1. Since we use a super admin to control the Area, we create a superadmin package to manage related behaviour. Create `web.superadmin.AreaController`.
2. Implement this class.

`@Controller` tag means this is an implementation class of Controller(just like `@Service`). Here we don't have a Controller interface. 

`@RequestMapping` means when we have a request calling `superadmin`, we direct it to our current class `AreaController`. Same as the following. Notice that we use lower case here for url.

`@ResponseBody` is used to write the data we have in controller to the body of response. Could be html, json or xml. In this case, we return `json`.

The reason why we use a Map<String, Object> here is because this data structure is like a json. We can put whatever we want as the value of a certain String, including error message.

![Notes-2019-7-31-22-3-49.png](https://raw.githubusercontent.com/Luorinz/images/master/Notes-2019-7-31-22-3-49.png)

We can test it at http://localhost:8080/superadmin/listarea


and get something like

```json
{"total":2,"rows":[{"areaId":2,"areaName":"Chicago","priority":2,"createTime":null,"lastEditTime":null},{"areaId":1,"areaName":"Seattle","priority":1,"createTime":null,"lastEditTime":null}]}
```

> Debug: There's a serious bug about bean multipartResolver. Annotate it will be fine.

### Review

1. Create the interface in DAO, and create certain APIs
2. Create config file in mapper for this DAO, and Use SQL to execute operations on Database.
3. Call DAO API in Service
4. Call Service API in Controller and return it to front end(write to response).



