---
title: powermock
copyright: true
top: 0
date: 2018-09-16 16:51:53
tags:
 - mock
categories:
  - 技术
  - 后端
password:
---



# 特性
首先mockito框架，可以mock,也可以spy,但是不能mock静态方法，和私有方法，
然而powermock支持;
[mockito中文文档][1]

# maven 依赖
```xml
    <properties>
        <powermock.version>1.7.1</powermock.version>
        <mockito1.version>1.10.19</mockito1.version>
    </properties>
    <dependencies>
            <!-- 依赖 -->
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-test</artifactId>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.12</version>
            </dependency>
            <dependency>
                <groupId>org.mockito</groupId>
                <artifactId>mockito-core</artifactId>
                <version>${mockito1.version}</version>
                <scope>test</scope>
            </dependency>
            <dependency>
                <groupId>org.powermock</groupId>
                <artifactId>powermock-module-junit4</artifactId>
                <version>${powermock.version}</version>
                <scope>test</scope>
            </dependency>
            <dependency>
                <groupId>org.powermock</groupId>
                <artifactId>powermock-api-mockito</artifactId>
                <version>${powermock.version}</version>
                <scope>test</scope>
            </dependency>
            <dependency>
                <groupId>org.powermock</groupId>
                <artifactId>powermock-module-junit4-rule-agent</artifactId>
                <version>${powermock.version}</version>
                <scope>test</scope>
            </dependency>
    </dependencies>
    <build>
            <!-- 插件配置 -->
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <configuration>
                    <argLine>-javaagent:${settings.localRepository}/org/powermock/powermock-module-javaagent/1.7.1/powermock-module-javaagent-1.7.1.jar -XX:-UseSplitVerifier</argLine>
                </configuration>
            </plugin>
        </plugins>
    </build>

```

# 测试用例
```java
@WebAppConfiguration
@SpringBootApplication
@ContextConfiguration(locations = {"classpath:spring-application.xml"})
@RunWith(SpringJUnit4ClassRunner.class)
@PrepareForTest(HttpPayUtil.class)//准备静态类
public class ControllerTest {

    protected MockMvc mockMvc;

    @Rule
    public PowerMockRule rule = new PowerMockRule();

    @Autowired
    protected WebApplicationContext webApplicationContext;


    @Before
    public void setUp() throws Exception {
        PropertyConfigurator.configure(new FileInputStream(ResourceUtils.getFile(ResourceUtils.CLASSPATH_URL_PREFIX+"log4j.properties")));
        mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext).build();
    }

    /**
     *
     * @throws Exception
     */
    @Test
    public void test()throws Exception{
    //mock静态类
        PowerMockito.mockStatic(HttpPayUtil.class);
        //录制脚本
        PowerMockito.when(HttpPayUtil.queryOrderDetail("1", PayConstants.PaySource.WEAPP))
        .thenReturn(new String[]{"2","3"});

        String[] stss = HttpPayUtil.queryOrderDetail("1", PayConstants.PaySource.WEAPP);
        System.out.println(stss[0]);
        System.out.println(stss[1]);

    }
}

```

# 运行测试
```shell
mvn test
```

---

[1]: https://github.com/hehonghui/mockito-doc-zh/blob/master/mr.simple.md