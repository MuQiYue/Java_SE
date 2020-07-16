## spring框架

### 1、什么是框架？

框架就是整合了业务代码的脚手架，他可以帮助你整合你开发所需要的架构和相关规定

三层架构：

​	表现层：用于展示数据

​	业务层：处理业务需求

​	持久层：与数据库交互

Mac框架：为模型-视图-控制器的缩写，就是可以把业务逻辑整合在一个部件中，改进和完成代码时不需要改变业务逻辑，主要有：struts1，struts2，stringmvc。

持久层/数据访问层/DAL框架：用于访问数据库和对数据库的数据进行操作的框架，主要有mybatis,hibernate。

整合型框架：可以理解为把你开发要用的框架都整合在一起，让你不需要搞更多的配置；string

### 2、spring概述

* 一个开源框架
* 为简化企业级开发而生，你在EJB中使用繁琐的配置和复杂的代码可以通过spring优雅和简洁的实现
* spring的核心：IOC(DI)和AOP容器框架

特性：

* 非侵入式：基于spring开发的应用中的对象课不依赖spring的api
* 依赖注入：DI---Dependency Injection,反正控制（IOC）最经典的实现
* 面对切面编程：Aspect Oriented Prigramming---AOP;和OOP（面对对象编程）关系是补充OOP的有关缺陷
* 容器：spring是一个容器，它可以管理应用对象的生命周期
* 组件化：spring实现了使用简单的组件配置组成一个复杂的应用；在spring中可以使用xml和java注解组合这些对象；spring中组件就是spring所管理的对象。降低耦合。
* 一站式：在IOC和AOP的基础上可以整合各种整合开发企业应用的开源框架和优秀的第三方类课（实际上spring自身提供表述层的springmvc和持久层的spring jdbc）。

spring模块

底层ioc: Beans, Core, Context,SpEL

AOP:面向切面编程

持久层：JDBC, ORM, OXM, JMS, Transactlons

MVC层：websoclet, serviet, web, portlet