title: 开始学习Spring 
date: 2015-07-14 18:08:50
tags:
---

#开始学习Spring 

##Spring 4 Configuration
Spring中核心IoC功能的补充：

- 管理bean的生命周期
- 使bean能够“Spring aware”
- 使用FactoryBeans
- JavaBeans PropertyEditors
- 使用Java类来配置
- 进阶配置
- 使用Groovy配置


##参考资料
《Pro Spring 4 Edition》


#《Spring in Action》
如何创建容器 -》 有了容器，如何装配Bean -》知道装配Bean，如果Bean很多，XML文件就很复杂 -》如何减少XML的配置

##Spring 应用上下文

- Spring 容器是什么，有什么用
- 如何创建 Spring 容器

Spring容器是Spring框架的核心，Spring自带了几种容器实现，可以归为两类：

- BeanFactory是最简单的容器，提供基础的依赖注入和Bean装配服务
- ApplicationContext 应用上下文（用的更多）
    * Spring通过应用上下文（Application Context）装载Bean的定义并把它们组装起来。Spring应用上下文全权负责对象的创建和组装。Spring自带了几种应用上下文的实现，它们之间主要的区别仅仅是如何加载它们的配置。用的最多的是3种：
        + ClassPathXmlApplicationContext，从类路径下的XML配置文件中加载上下文定义，把应用上下文文件当做类资源
        + FileSystemXmlApplicationContext，读取文件系统中的XML配置文件并加载上下文定义
        + XmlWebApplicationContext，读取Web应用下的XML配置文件并装载上下文定义
    * 通过现有的应用上下文引用，你可以调用应用上下文的getBean()方法从Spring容器中获取Bean。

在Spring应用中，Spring容器会创建相互协作的组件之间的关联。负责创建对象、装配（Wiring）对象、配置对象，管理对象的整个生命周期。

    创建应用组件之间协作的行为通常称为装配。在Spring中装配Bean最常见的方式是使用XML文件。


##Bean的实例化
在Spring中，默认情况下，所有的bean都是单例。ApplicationContext.getBean()总是返回同一个实例。

###Bean 的作用域
如果需要每次请求时都获得唯一的Bean实例，可以通过配置Bean的作用域 scope属性。
Spring有关单例的概念限于Spring上下文的范围内，不像真正的单例，在每个类加载器中保证只有一个实例。

###Bean 的生命周期
初始化和销毁，可以配置 init-method 和 destory-method，虽然Spring API也提供相应的接口，但会与其产生耦合。

在Java中singleton包含两个概念：单个实例的对象，单例模式。前者用singleton表示，后者用Singleton表示。
可以通过配置文件中的配置来修改“单例”的属性。
```Java中的单例模式
    package com.apress.prospring4.ch3;
    public class Singleton {
        private static Singleton instance;
        static {
            instance = new Singleton();
    }
        public static Singleton getInstance() {
            return instance;
    } }

```

##为Bean的属性和构造器参数装配多种类型的值
- 简单属性值，使用value属性
- 引用其他Bean的属性，使用ref属性
- Bean的属性是复数，比如集合，使用list set map props属性
    *  
    
```
    
    <bean id="hank"
                class="com.springinaction.springido1.OneManBand">
        <property name="instruments">
            <list>
                <ref bean="guitar" />
                <ref bean="cymbal" />
                <ref bean="harmonica" />
    </bean>
    
```
    
    
##疑问？
从《Spring in Action》中可以看到注入Bean属性实则就是setter方法注入，这种方式在setter方法上有@Autowired注解。那在属性上直接写@Autowired又是什么注入方式呢。


##如何减少XML的配置数量
Spring提供了以下方式：

- 自动装配 autowiring，减少甚至消除配置<property> <constructor-arg>元素，让Spring自动识别并装配Bean的依赖关系
- 自动检测 autodiscovery，比自动装配更进一步，让Spring自动识别哪些类需要被配置成Spring Bean，减少对<bean>元素的使用。

###自动装配Autowiring Bean 属性
Spring提供了4种自动装配策略：

- byName，把与Bean的属性具有相同名字的其他Bean自动装配到Bean的对应属性中
- byType，把与Bean的属性具有相同类型的其他Bean自动装配到Bean的对应属性中
- constructor，把与Bean的构造器入参具有相同类型的其他Bean自动装配到Bean构造器的对应入参中
- autodetect，首先尝试使用constructor进行自动装配，如果失败，再尝试使用byType进行自动装配

#### 使用注解自动装配Bean 属性
Spring容器默认禁用注解装配，所以在使用基于注解的自动装配前，我们需要在Spring配置中启用它。最简单的启用方式是使用：
<context:annotation-config />

这会告诉Spring我们打算使用基于注解的自动装配。

Spring 3 支持几种不同的用于自动装配的注解：

- Spring自带的 @Autowired 注解，这种方式下如果没有Bean可以装配到@Autowired所标注的属性或参数中，或者有多个Bean的时候，都会得到“NoSuchBeanDefinitionException”的异常
    * 可以标注Setter方法
    * 可以标注构造器
    * 可以标注属性，并删除setter方法
- JSR-330 的 @Inject 注解
    * 为了统一各种依赖注入框架的编程模型，JCP（Java Community Process）发布了Java依赖注入规范，JCP将其称为JSR-330，更常见的叫法是 at inject，该规范为Java带来了通用依赖注入模型。
    * @Inject 注解是JSR-330的核心部件，几乎可以完全替换Spring的 @Autowired 注解。
    * 和 @Autowired 一样，@Inject 可以用来自动装配属性、方法和构造器
    * 不一样的是，@Inject 没有 required 属性。因此 @Inject 注解所标注的依赖关系必须存在，如果不存在，则会抛出异常。
    * @Inject 可以注入一个provider
- JSR-250 的 @Resource 注解

###自动检测 Bean
我们希望使用<context:annotation-config>之后，Spring能对待我们定义的注解，并指导Bean的装配。
即使<context:annotation-config>有助于完全消除Spring配置中的<property> <constructor-arg>元素，我们仍需要使用<bean>元素显示定义Bean。

在Spring中<context:component-scan>除了完成<context:annotation-config>的工作，还允许Spring自动检测Bean和定义Bean。

为了配置Spring自动检测，需要使用<context:component-scan>元素来代替<context:annotation-config>元素。

#### <context:component-scan> 如何知道哪些类需要注册为Spring Bean？
默认情况下，<context:component-scan> 查找使用构造型（stereotype）注解所标注的类：

- @Component，通用的构造型注解，标识该类为Spring组件
- @Controller，标识将该类定义为Spring MVC Controller
- @Repository，标识将该类定义为数据仓库
- @Service，标识将该类定义为服务
- 使用 @Component 标注的任意自定义注解

当使用 <context:component-scan> 时，基于注解地自动检测只是一种扫描策略，还有其他扫描策略。

- 过滤组件扫描，比如 <context:include-filter>

##如果不喜欢XML，可以使用Spring创建基于Java的配置

仍然需要少量的XML来启用Java配置，在下面代码中，base-package告诉Spring在哪个包中查找使用@Configuration注解所标注的所有类：

```

    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans.xsd
              http://www.springframework.org/schema/context
              http://www.springframework.org/schema/context/spring-context.xsd">
    
        <context:component-scan
              base-package="com.springinactin.springido1"/>
    </beans>
```
###定义一个配置类
使用@Configuration注解的Java类，等价于XML配置中的<beans>元素。
@Configuration注解会告诉Spring，这个类将包含一个或多个Spring Bean的定义。

```

    @Configuration
    public Class SpringIdo1Config {
        // Bean declaration methods go here
    }

```


    