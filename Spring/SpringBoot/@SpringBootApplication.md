## @SpringBootApplication

* 스프링 부트를 이용하여 처음 프로젝트를 생성하면 다음과 같은 코드를 볼 수 있다.

``` java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

* @SpringBootApplication은 자동 설정을 위한 어노테이션으로 org.springframework.boot.autoconfigure패키지에 들어 있다.


``` java
@Target(value = {ElementType.TYPE})
@Retention(value = RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
    @ComponentScan.Filter(type = FilterType.CUSTOM, classes = {TypeExcludeFilter.class}),
    @ComponentScan.Filter(type = FilterType.CUSTOM, classes = {AutoConfigurationExcludeFilter.class})})
public @interface SpringBootApplication {

    @AliasFor(annotation = EnableAutoConfiguration.class)
    public Class<?>[] exclude() default {};

    @AliasFor(annotation = EnableAutoConfiguration.class)
    public String[] excludeName() default {};

    @AliasFor(annotation = ComponentScan.class, attribute = "basePackages")
    public String[] scanBasePackages() default {};

    @AliasFor(annotation = ComponentScan.class, attribute = "basePackageClasses")
    public Class<?>[] scanBasePackageClasses() default {};

    @AliasFor(annotation = ComponentScan.class, attribute = "nameGenerator")
    public Class<? extends BeanNameGenerator> nameGenerator() default BeanNameGenerator.class;

    @AliasFor(annotation = Configuration.class)
    public boolean proxyBeanMethods() default true;
}
```
* @SpringBootApplication으로 들어가면 위와 같이 나온다.
* 위의 코드에서 @EnableAutoConfiguration, @ComponentScan이 중요하다.

### @ComponentScan
* @ComponentScan은 @component, @Service, @Repository, @Controller등의 어노테이션을 스캔하여 Bean으로 등록해주는 역할을 한다.

### @EnableAutoConfiguration
* @EnableAutoConfiguration은 사전에 정의한 라이브러리들을 Bean으로 등록해 준다.
* 미리 정의되어 있는 Bean들은 spring-boot-autoconfigure > META-INF > spring.factories에 위치한다.
