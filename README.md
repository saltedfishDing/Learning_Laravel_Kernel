# Learning_Laravel_Kernel

Laravel核心代码学习

## 前言

我16年才开始接触Laravel框架, 算是比较晚的。之前几年一直都是在用ZendFramework和Codeigniter，尤其Codeigniter这个小巧但是功能强大的框架在前几年很流行，当时我也非常喜欢Codeigniter的轻量级和灵活，写了很多Codeigniter的libraries，甚至为了能更好的在Codeigniter核心的基础上扩展出自己想要的功能通读了它的源码。Codeigniter的源码相对Laravel来说还是很容易读懂的，因为它是上一个时代的PHP框架并没有用到后来PHP才有的命名空间、性状这些特性，所以当时在学习源码时也没有刻意觉得要把这些东西梳理到文档里来帮助自己理解。 后来随着项目越做越成熟由于在Codeigniter里扩展了太多的自已写的libraries明显感觉代码维护难度较项目早期高了很多，也觉得老用一种思路进行软件开发慢慢会限制自己的进步，所以在16年下半年才开始接触Laravel, 试着用laravel重构公司里的一个管理后台。当时学习的方法就是在照着文档里写，一边开发一边看文档慢慢的把文档看了几遍使用起来就顺手多了，也从Google上找到了很多问题在Laravel里的最佳实践。在使用的过程中慢慢地也就对“依赖注入”、“控制反转”、“服务容器”、“服务提供者”和“中间件”这些东西有了些概念。后来17年换工作后部门主要应用的就是Laravel, 应用场景一多起来之后自然使用的就越发熟练。由于我一直以来都坚信做开发的不光要知其然还要知其所以然，所以一直对laravel里面的依赖注入、服务绑定、服务解析等等这些东西很好奇，再一个我觉得只有理解了一个框架的核心代码才能真正把一个框架用好才能写出最佳实践。之前在开发的时候已经零敲碎打的看了很多Laravel核心部分的源码了也看了不少相关的文章对Laravel的这些核心组件是怎么实现的有了一定的印象，但时间久了很多东西就忘了遇到不知道怎么解决的问题后还是得去一遍遍的看源码。所以进入18年后给自己的目标就是好好梳理一下Laravel核心的代码把他们用文字记录起来慢慢地梳理成体系，这样以后遇到问题可以节省不少看源码的时间，梳理成体系后也更有利于把这些知识分享给其他人共同进步。

## 面向的人群

要想很好地理解文章的内容你需要具备一定的PHP基础和Laravel的知识，我并不会解释核心里的每一行代码，更多的是通过梳理代码流程来解释Laravel核心模块里最典型功能的设计思路和具体实现。所以我希望读者可以将文章内容看作是源代码的导读，跟随文章自己逐步地去看一遍Laravel每个核心组件的代码，如果遇到理解起来比较困难的地方就去补齐那里用到的知识再来继续阅读，我也希望读者在理解了文章里说的那些典型功能后能够自己再去举一三地看看模块里其他功能的源代码。相信看完Laravel核心的代码后你不仅能更熟练地使用Laravel也能在其它基础知识方面有所提高。

## 涉及的内容

文章主要专注于Laravel核心的学习，包括:服务容器、服务提供器、中间件、路由、Facades、事件驱动系统、Auth用户认证系统以及作为核心服务的Database、Request、Response、Cookie和Session。Laravel里其它的部分也都是作为服务注册到服务容器里提供给应用使用的，当你理解了上面那些东西后再去看其它的服务也就会很容易理解了。在学习源码的过程中我会向读者解释关于这些核心模块的常见问题比如：使用`DB`或者`Model`操作数据库时Laravel是什么时候连接上数据库的？ 注册到容器的服务是怎么被解析出来的等等。

## 关于框架版本
在通过这个项目学习Laravel核心代码时请使用Laravel5.5版本，由于服务容器和中间件两篇文章成稿比较早那会还在使用5.2版本的Laravel做项目所以引用的代码也来自5.2版本，其余章节的代码均引用自Laravel5.5的核心，两个版本的核心代码差异很小我已经在这两篇文章中标注出差异的地方所以不影响读者使用这个项目来学习Laravel5.5版本的核心代码。

## 文章目录

- [类的反射和依赖注入](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/reflection.md)
- [服务容器(IocContainer)](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/IocContainer.md)
- [服务提供器(ServiceProvider)](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/ServiceProvider.md)
- [外观模式](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/FacadePattern.md)
- [Facades](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Facades.md)
- [路由](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Route.md)
- [装饰模式(Decorator Pattern)](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/DecoratorPattern.md)
- [中间件](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Middleware.md)
- [控制器](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Controller.md)
- [Request](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Request.md)
- [Response](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Response.md)
- [Database 基础介绍](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Database1.md)
- [Database 查询构建器](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Database2.md)
- [Database 模型CRUD](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Database3.md)
- [Database 模型关联](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Database4.md)
- [观察者模式](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Observer.md)
- [事件系统](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Event.md)
- [用户认证系统(基础介绍)](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Auth1.md)
- [用户认证系统(实现细节)](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Auth2.md)
- [扩展用户认证系统](https://github.com/kevinyan815/Learning_Laravel_Kernel/blob/master/aritcles/Auth3.md)


## 其他推荐

- [Laravel最佳实践](https://github.com/kevinyan815/laravel_best_practices_cn) 
