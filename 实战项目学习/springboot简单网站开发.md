# SpringBoot Web开发

- 导入静态资源
- 首页
- jsp, 模板引擎Thymeleaf
- 装配扩展SpringMVC
- 增删改查
- 拦截器
- 国际化

## 静态资源

1. 创建项目, 选中web模块

> 1. 用webjar方式导入静态资源

以maven的方式导入webjar包(js, jquery等) 到/META-INF/resources/webjars/下

地址栏输入/webjars/**就可以访问到

> 2. 五个位置

这里的classpath=项目/resources

classpath:/META-INF/resources/, classpath:/resources/, classpath:/static/, classpath:/public/ 这五个位置都支持导入静态资源

地址输入/**就可以访问

如果重名资源, 访问优先级: resources> static(默认)> public

> 3. 自定义静态资源位置

在application.properties中定义spring.mvc.static-path-pattern=/xxx

前面两种都失效, 只会走第三种

## 首页定制

放在静态资源目录下, index.html

也可以放在templates目录下, 这个目录下的首页只能用controller访问, 需要模板引擎的支持

**定制图标**: springboot2.x之后的图标定义只能在网页内修改了

## 模板引擎 Thymeleaf

Template中的html, 数据是用${}取的, 加上返回的Data, 通过模板引擎渲染成正常的html页面

1. 导入thymeleaf依赖, 基于3.x开发

```
thymeleaf-spring5, thymeleaf-extras-java8time
```

2. 页面都写在templates下, html结尾的网页
3. thymeleaf页面要使用这个模板引擎的语法要导入对应的约束

```java
@Controller
public class HelloController{
	@RequestMapping("/test")
	public String test(Model model){
		model.addAttribute("msg","test");
		return "test";//这里返回的字符串会拼接localhost的地址和html的后缀
	}
}
```

## MVC配置

1. 新建config包, 下新建MyMvcConfig, 作用是扩展mvc
2. 编辑这个配置类, 要用到自动配置的话不要加@EnableWebMvc 这个注解

```java
//这个配置类, 如果想要定制一些功能 , 只要重写这个组件, 然后放入bean中交给springboot去管理就可以
@Configuration
public class MyMvcConfig implements WebMvcConfigurer{
    //重写WebMvcConfigurer的方法
    //如果要自定义视图解析器, 需实现视图解析器的接口, 然后将这个类放入bean容器中
    //Format组件去读去properties类, properties类默认日期格式是dd/MM/yyyy, 可以到application.properties中配置格式:spring.mvc.date-format=""
    @Override
    public void addViewControllers(ViewControllerRegistry registry){
        registry.addViewController("/kuagn").setViewName("test");
    }
    
}
```

## 项目开始

1. 导入静态资源, 页面放入templates下, 静态资源放入static
2. 导入lombok依赖和安装lombok插件
3. 数据使用伪造数据, 在pojo下的实体类中伪造数据

```java
@Data
@AllArgsConstructor

```



