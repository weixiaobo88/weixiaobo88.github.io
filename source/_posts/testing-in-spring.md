title: Testing in Spring
date: 2015-08-05 10:00:41
tags: spring test
---

## 单元测试

### Spring Framework 提供的 Mock Objects

- Environment, org.springframework.mock.env package, MockEnvironment and MockPropertySource
- JNDI, org.springframework.mock.jndi, JNDI SPI
- Servlet API, org.springframework.mock.web, 测试 web contexts, controllers, filters
    * Spring MVC and REST Controllers 的集成测试可以参考 [Spring MVC Test Framework](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/integration-testing.html#spring-mvc-test-framework)
- Portlet API

## 集成测试

Spring 2.5 以后，在 Spring TestContext Framework 中提供了基于注解的单元测试和集成测试。
 
Spring 对于集成测试的支持有以下几个主要目标：

- 测试执行过程中管理 Spring IoC 容器缓存
- 提供测试夹具（test fixture）实例的依赖注入(Dependency Injection)
- 提供集成测试中的事务管理
- 提供写集成测试中需要的特定的 Spring 基类

### JDBC 测试

使用 JdbcTestUtils

### 注解


## Spring MVC 测试框架

建立在 spring-test 模块中的 Servlet API mock objects 之上，所以不需要一个运行的 Servlet 容器，它会使用 DispatcherServlet，提供所有的 Spring MVC 的支持，使用 TestContext 框架可以选择性的加载实际的 Spring 配置文件，

Spring MVC 测试提供了 client-side 的测试，使用 RestTemplate 来测试。Client-side 的测试会 mock 服务器的响应，并不需要一个运行的服务器。

### Server-Side 服务器端测试

#### 配置项 Setup Options

有两种方式来创建 MockMvc的实例
- 通过 TestContext 框架来加载 Spring MVC 的配置
- 手动创建 controller 的实例，不用加载 Spring 的配置

```bash
// 通过 TestContext 框架来加载 Spring MVC 的配置
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration("test-servlet-context.xml")
public class ExampleTests {

    @Autowired
    private WebApplicationContext wac;

    private MockMvc mockMvc;

    @Before
    public void setup() {
        this.mockMvc = MockMvcBuilders.webAppContextSetup(this.wac).build();
    }

    @Test
    public void getAccount() throws Exception {
        this.mockMvc.perform(get("/accounts/1").accept(MediaType.parseMediaType("application/json;charset=UTF-8")))
            .andExpect(status().isOk())
            .andExpect(content().contentType("application/json"))
            .andExpect(jsonPath("$.name").value("Lee"));
    }

}
```

```bash
// 手动创建 controller 的实例
public class MyWebTests {

    private MockMvc mockMvc;

    @Before
    public void setup() {
        this.mockMvc = MockMvcBuilders.standaloneSetup(new AccountController()).build();
    }

    // ...

}
```

##### 选择哪一种？

- "webAppContextSetup"
    * "webAppContextSetup" 加载实际的 Spring MVC 配置，能够提供一个更完整的集成测试。
    * 而且 TestContext 框架能够缓存加载的 Spring 配置，保证测试能够快速运行。 
    * 另外，你还可以通过 Spring 的配置，在 controller 中注入 mock 的 services，这样可以把关注点放在测试 web 层。

```bash
// 使用 Mockito 声明一个 mock 的 service 
<bean id="accountService" class="org.mockito.Mockito" factory-method="mock">
    <constructor-arg value="org.example.AccountService"/>
</bean>

// 在测试中就可以使用这个 mock 的 service
@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration("test-servlet-context.xml")
public class AccountTests {

    @Autowired
    private WebApplicationContext wac;

    private MockMvc mockMvc;

    @Autowired
    private AccountService accountService;

    // ...

}
```

- "standaloneSetup" 
    * "standaloneSetup" 更像单元测试，每次测一个 controller，controller 可以用 mock 的依赖手动注入，不需要加载 Spring 配置。
    * 可以很容易的看到是在测是哪一个 controller
    * 对于写 ad-hoc 测试来验证行为或者 debug 的时候很方便
    * 要写 “webAppContextSetup” 测试来验证 Spring MVC 配置
    

#### 执行请求 Performing Requests

- 用 HTTP 方法
- 用 file upload 请求
 
#### 定义 Expectations

有两种类型
- 验证 response 的属性，比如 response 的 status, headers, content
- 验证 Spring MVC 具体的事情，比如哪个 controller 的方法处理了这个请求，是否有 exception 抛出和处理，model 的内容是什么，选择了哪个 view 等。


## 与端到端基础测试的区别

- blank MockHttpServletRequest
 

     
     




