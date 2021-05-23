1. 使用[https://start.spring.io/]创建一个SpringCloud项目，添加Eureka-Server组件
    
2. 添加模块[Module]-eureka
    1. 在子模块的pom.xml中追加，注释掉父模块的引用
    <dependencies>
        <!-- Eureka-Server -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
    </dependencies>
    2. 移动java及resources下文件到子模块中
        [CourseApplication.java]->[EurekaApplication.java]
    3. 删除父模块下src目录
    
3. 解决Eureka启动失败问题
    1. application.properties
       ```
        # 应用名称
        spring.application.name=eureka
        # eureka注册中心默认端口
        server.port=8761
        # 获取注册中心（因本模块是注册中心，所以设置成false）
        eureka.client.fetch-registry=false
        # 注册到eureka server（因本模块是注册中心，所以设置成false）
        eureka.client.register-with-eureka=false
       ```
    2. EurekaApplication.java
       ```
       @EnableEurekaServer //开启EurekaServer服务
       ```
4. 添加日志配置
    logback.xml
5. 添加System模块
    1. 将System模块注册到注册中心（eureka）。需要修改3个地方
        1. pom.xml
        2. application.properties
        3. SystemApplication.java
6. 添加Gateway模块
    1. 路由转发
        application.properties
        ```
        # 路由转发
        # System模块
        spring.cloud.gateway.routes[0].id=system
        spring.cloud.gateway.routes[0].uri=http://127.0.0.1:9001
        spring.cloud.gateway.routes[0].predicates[0].name=Path
        spring.cloud.gateway.routes[0].predicates[0].args[0]=/system/**
        ```
7. 
        