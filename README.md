# swagger-springmvc v1.0.2对应的前端swagger-ui页面
Swagger能成为最受欢迎的REST APIs文档生成工具之一，有以下几个原因：

 1. Swagger 可以生成一个具有互动性的API控制台，开发者可以用来快速学习和尝试API。
 2. Swagger 可以生成客户端SDK代码用于各种不同的平台上的实现。
 3. Swagger 文件可以在许多不同的平台上从代码注释中自动生成。
 4. Swagger 有一个强大的社区，里面有许多强悍的贡献者。

Swagger 文档提供了一个方法，使我们可以用指定的 JSON 或者 YAML 摘要来描述你的 API，包括了比如 names、order 等 API 信息。
你可以通过一个文本编辑器来编辑 Swagger 文件，或者你也可以从你的代码注释中自动生成。各种工具都可以使用 Swagger 文件来生成互动的 API 文档。

在【pom.xml】文件中添加swagger相关依赖

```xml
 <!-- swagger api接口文档 -->
        <dependency>
            <groupId>com.mangofactory</groupId>
            <artifactId>swagger-springmvc</artifactId>
            <version>1.0.2</version>
        </dependency>
```
新建配置文件【SwaggerConfig.java】

```java
@Configuration//交由srping管理
@EnableSwagger
public class SwaggerConfig {

    private SpringSwaggerConfig springSwaggerConfig;
    @Autowired
    public void setSpringSwaggerConfig(SpringSwaggerConfig springSwaggerConfig) {
        this.springSwaggerConfig = springSwaggerConfig;
    }
    @Bean
    public SwaggerSpringMvcPlugin customImplementation(){
       return  new SwaggerSpringMvcPlugin(this.springSwaggerConfig).apiInfo(apiInfo());
    }

    public  ApiInfo   apiInfo(){
        ApiInfo info= new ApiInfo("统一身份认证系统Api文档","提供所有后台接口",
                "联系开发者","email@qq.com",
                "","");
       return  info;
    }
}
```
在【springMvc.xml】配置文件中添加swagger配置文件

```xml
    <!-- 把Swagger配置文件类增加spring容器 -->
    <bean class="com.dc.base.config.SwaggerConfig"></bean>
    <!-- 防止spring拦截swagger接口aip。 -->
    <mvc:resources mapping="/swagger/**" location="/swagger/"/>
```

下载swagger-springmvc-v1.0.2对应的swagger-ui
