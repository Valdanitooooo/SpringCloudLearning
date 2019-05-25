- 服务的注册与发现Eureka

  - 创建一个主Maven工程

    在其pom文件引入依赖，spring Boot版本为2.0.3.RELEASE，Spring Cloud版本为Finchley.RELEASE
    
    `File -> New -> Project -> Maven -> Next -> 输入group & artifactId -> Next ->选择存储目录`

   - 创建服务注册中心(eureka server)

        `工程上右键 -> New -> Module -> 选择spring initializr -> Next -> 输入group  & artifact -> Next -> 选择Cloud Discovery -> 选择Eureka Server -> Next -> 输入Module名称 选择存储位置`

        创建完成后的Module需要继承父pom文件

        启动一个服务注册中心，只需要一个注解@EnableEurekaServer

        eureka是一个高可用的组件，它没有后端缓存，每一个实例注册之后需要向注册中心发送心跳（因此可以在内存中完成），在默认情况下erureka server也是一个eureka client ,必须要指定一个 server。
        
        eureka server的配置文件appication.yml 通过eureka.client.registerWithEureka：false和fetchRegistry：false来表明自己是一个eureka server.

        启动后通过http://localhost:8761访问，这是应该显示No application available 没有服务被发现

   - 创建一个服务提供者 (eureka client)
   
        当client向server注册时，它会提供一些元数据，例如主机和端口，URL，主页等。Eureka server 从每个client实例接收心跳消息。 如果心跳超时，则通常将该实例从注册server中删除。

        `工程上右键 -> New -> Module -> 选择spring initializr -> Next -> 输入group  & artifact -> Next -> 选择Cloud Discovery -> 选择Eureka Discovery -> Next -> 输入Module名称 选择存储位置`

        通过注解@EnableEurekaClient 表明自己是一个eurekaclient。

        还需要在配置文件中注明自己的服务注册中心的地址，application.yml中需要指明spring.application.name,这个很重要，这在以后的服务与服务之间相互调用一般都是根据这个name。
   
        启动工程，打开http://localhost:8761, 即eureka server的网址, 看到一个服务已经注册了。

原文地址：https://blog.csdn.net/forezp/article/details/81040925