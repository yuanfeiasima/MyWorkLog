1. @Resource的作用相当于@Autowired，只不过@Autowired按byType自动注入，而@Resource默认按 byName自动注入罢了。@Resource有两个属性是比较重要的，分是name和type，Spring将@Resource注解的name属性解析为bean的名字，而type属性则解析为bean的类型。所以如果使用name属性，则使用byName的自动注入策略，而使用type属性时则使用byType自动注入策略。如果既不指定name也不指定type属性，这时将通过反射机制使用byName自动注入策略。 　　@Resource装配顺序 　　1. 如果同时指定了name和type，则从Spring上下文中找到唯一匹配的bean进行装配，找不到则抛出异常 　　2. 如果指定了name，则从上下文中查找名称（id）匹配的bean进行装配，找不到则抛出异常 　　3. 如果指定了type，则从上下文中找到类型匹配的唯一bean进行装配，找不到或者找到多个，都会抛出异常 　　4. 如果既没有指定name，又没有指定type，则自动按照byName方式进行装配；如果没有匹配，则回退为一个原始类型进行匹配，如果匹配则自动装配；

2. dispatchler[http://sishuok.com/forum/blogPost/list/5188.html](http://sishuok.com/forum/blogPost/list/5188.html)

3. 事务处理[https://my.oschina.net/u/1415809/blog/209075](https://my.oschina.net/u/1415809/blog/209075)

4. 整体处理流程[http://www.cnblogs.com/plxx/p/5400467.html](http://www.cnblogs.com/plxx/p/5400467.html)

5. core 是啥作用 beans的bean加载过程

6. springmvc里面自动转化json靠什么？

7. aop怎么实现的 串这aspectJ 可能考察切面表达式

8. requestMapping的用法 例如矩阵参数 可变参数 必填参数

9. springEL在bean装载的时候怎么找对象的属性

10. controller 与context的注解分开来扫



