# Jackson

## 介绍
这个工程基于常见的MVC架构，展示了Jackson（the Java JSON library）的使用。学习这个工程之前，需要同学们对MVC有一定的了解。

## 运行
### Maven
同学们直接输入下面的命令就可以运行工程了
```
mvn spring-boot:run
```


### 获取不同视图
如果程序没有报错就可以登陆链接，打开浏览器输入网址。没有浏览器的同学可以使用curl命令获取网页内容。


这里先解释一下什么是视图（View）。视图决定了哪些数据序列化。举例来说，就是在将一个数据使用Jackson序列化的时候，视图A只对重要信息进行序列化，而视图B则可以对所有的信息进行序列话。不同的视图针对不同的场景。同学们可以看下面的内容来学习。

#### 获得简单视图

```
http://127.0.0.1:8080
curl http://127.0.0.1:8080
```

同学们会得到下面的输出内容，这个是本工程中的“Summary”样式，仅输出了重要的内容，没有输出数据中Recipients。
```
[ {
  "id" : 1,
  "title" : "Info",
  "author" : {
    "id" : 1,
    "firstname" : "Brian",
    "lastname" : "Clozel"
  }
}, {
  "id" : 2,
  "title" : "Warning",
  "author" : {
    "id" : 2,
    "firstname" : "Stéphane",
    "lastname" : "Nicoll"
  }
}, {
  "id" : 3,
  "title" : "Alert",
  "author" : {
    "id" : 3,
    "firstname" : "Rossen",
    "lastname" : "Stoyanchev"
  }
} ]
```

#### 获得详尽视图

使用下面的命令来获取详尽视图。
```
http://127.0.0.1:8080/with-recipients
curl http://127.0.0.1:8080/with-recipients
```

同学们会得到下面的输出内容，这个是本工程中的“SummaryWithRecipients”样式，还输出了Recipients。
```
[ {
  "id" : 1,
  "title" : "Info",
  "author" : {
    "id" : 1,
    "firstname" : "Brian",
    "lastname" : "Clozel"
  },
  "recipients" : [ {//第一个用户的Recipients，这一部分是这个视图跟上一个视图的不同
    "id" : 2,
    "firstname" : "Stéphane",
    "lastname" : "Nicoll"
  }, {
    "id" : 3,
    "firstname" : "Rossen",
    "lastname" : "Stoyanchev"
  } ]
}, {
  "id" : 2,
  "title" : "Warning",
  "author" : {
    "id" : 2,
    "firstname" : "Stéphane",
    "lastname" : "Nicoll"
  },
  "recipients" : [ {//第二个用户的Recipients，这一部分是这个视图跟上一个视图的不同
    "id" : 3,
    "firstname" : "Rossen",
    "lastname" : "Stoyanchev"
  } ]
}, {
  "id" : 3,
  "title" : "Alert",
  "author" : {
    "id" : 3,
    "firstname" : "Rossen",
    "lastname" : "Stoyanchev"
  },
  "recipients" : [ {//第三个用户的Recipients，这一部分是这个视图跟上一个视图的不同
    "id" : 1,
    "firstname" : "Brian",
    "lastname" : "Clozel"
  } ]
} ]
```

### 文件读写
这一部分向大家展示Jackson向文件的读写功能。

#### 写入文件
使用下面的命令来获取将内容写到文件中。其中"file=Messages.json"用来指定将文件写到Messages.json中。
```
http://127.0.0.1:8080/save?file=Messages.json
curl http://127.0.0.1:8080/save?file=Messages.json
```

同学们会得到下面的输出内容，证明成功了。
```
save successfully
```



其中Messages.json中的内容为序列化后的字符串。
```
[ {
  "id" : 1,
  "title" : "Info",
  "author" : {
    "id" : 1,
    "firstname" : "Brian",
    "lastname" : "Clozel",
    "email" : "bclozel@pivotal.io",
    "address" : "1 Jaures street",
    "postalCode" : "69003",
    "city" : "Lyon",
    "country" : "France"
  },
  "recipients" : [ {
    "id" : 2,
    "firstname" : "Stéphane",
    "lastname" : "Nicoll",
    "email" : "snicoll@pivotal.io",
    "address" : "42 Obama street",
    "postalCode" : "1000",
    "city" : "Brussel",
    "country" : "Belgium"
  }, {
    "id" : 3,
    "firstname" : "Rossen",
    "lastname" : "Stoyanchev",
    "email" : "rstoyanchev@pivotal.io",
    "address" : "3 Warren street",
    "postalCode" : "10011",
    "city" : "New York",
    "country" : "USA"
  } ],
  "body" : "This is an information message"
}, {
  "id" : 2,
  "title" : "Warning",
  "author" : {
    "id" : 2,
    "firstname" : "Stéphane",
    "lastname" : "Nicoll",
    "email" : "snicoll@pivotal.io",
    "address" : "42 Obama street",
    "postalCode" : "1000",
    "city" : "Brussel",
    "country" : "Belgium"
  },
  "recipients" : [ {
    "id" : 3,
    "firstname" : "Rossen",
    "lastname" : "Stoyanchev",
    "email" : "rstoyanchev@pivotal.io",
    "address" : "3 Warren street",
    "postalCode" : "10011",
    "city" : "New York",
    "country" : "USA"
  } ],
  "body" : "This is a warning message"
}, {
  "id" : 3,
  "title" : "Alert",
  "author" : {
    "id" : 3,
    "firstname" : "Rossen",
    "lastname" : "Stoyanchev",
    "email" : "rstoyanchev@pivotal.io",
    "address" : "3 Warren street",
    "postalCode" : "10011",
    "city" : "New York",
    "country" : "USA"
  },
  "recipients" : [ {
    "id" : 1,
    "firstname" : "Brian",
    "lastname" : "Clozel",
    "email" : "bclozel@pivotal.io",
    "address" : "1 Jaures street",
    "postalCode" : "69003",
    "city" : "Lyon",
    "country" : "France"
  } ],
  "body" : "This is an alert message"
} ]
```
#### 从文件中读取
我们从only3.json中读取Messages，其中only3.json中只有上文中的id=3的那个用户的数据，如果读取成功，那么用户则只能请求到id=3的用户数据。
```
http://127.0.0.1:8080/load?file=only3.json
curl http://127.0.0.1:8080/load?file=only3.json
```

读取成功的输出如下。
```
load successfully
```


此时我们请求用户数据就会得到
```
http://127.0.0.1:8080/
curl http://127.0.0.1:8080/
```

输出如下。发现仅有id为3的用户了。证明数据读取成功。
```
[ {
  "id" : 3,
  "title" : "Alert",
  "author" : {
    "id" : 3,
    "firstname" : "Rossen",
    "lastname" : "Stoyanchev"
  }
} ]
```

## 代码解读

本项目的工程结构如下。

视图的不同可以通过“手动写逻辑”的方式来实现，但是在Spring Boot中，我们仅仅需要定义视图类、数据标注、API标注就更简便地达到相同的效果。


```
.
├── README.md
├── only3.json
├── pom.xml
└── src
    └── main
        ├── java
        │   └── demo
        │       └── jacksonDemo
        │           ├── Application.java//SpringBoot入口，main函数
        │           ├── DO//数据对象。数据对象的视图在每个对象中定义。
        │           │   ├── Message.java//数据结构标注
        │           │   └── User.java//数据结构标注
        │           ├── controller//Controller，接收前端的映射
        │           │   └── MessageController.java//API标注
        │           ├── service//接口与实现分离的服务
        │           │   ├── MessageService.java
        │           │   └── impl
        │           │       └── MessageServiceImpl.java
        │           └── view//视图类的定义
        │               └── View.java//视图类
        └── resources
            └── application.properties//各种配置选项

11 directories, 15 files
```

## 延伸阅读
* Jackson Homepage： https://github.com/FasterXML/jackson
* Jackson教程：https://www.baeldung.com/category/json/jackson/
* Java工程脚手架： https://start.aliyun.com


## pom.xml备份
这部分对pom.xml的内容进行了备份。

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.test</groupId>
    <artifactId>spring-jackson-demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>Spring Jackson demo</name>
    <description>Demo project for latest Spring + Jackson functionalities</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.2.0.RC2</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.dataformat</groupId>
            <artifactId>jackson-dataformat-xml</artifactId>
        </dependency>
        <dependency>
            <groupId>org.codehaus.woodstox</groupId>
            <artifactId>woodstox-core-asl</artifactId>
            <version>4.4.1</version>
        </dependency>
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
            <version>2.6</version>
        </dependency>
        <dependency>
            <groupId>javax.xml.bind</groupId>
            <artifactId>jaxb-api</artifactId>
            <version>2.3.0</version>
        </dependency>
        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-impl</artifactId>
            <version>2.3.0</version>
        </dependency>
        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-core</artifactId>
            <version>2.3.0</version>
        </dependency>
        <dependency>
            <groupId>javax.activation</groupId>
            <artifactId>activation</artifactId>
            <version>1.1.1</version>
        </dependency>
    </dependencies>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <start-class>com.demo.jacksonDemo.Application</start-class>
        <java.version>1.8</java.version>
    </properties>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

    <repositories>
        <repository>
            <id>spring-snapshots</id>
            <name>Spring Snapshots</name>
            <url>http://repo.spring.io/snapshot</url>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
        <repository>
            <id>spring-milestones</id>
            <name>Spring Milestones</name>
            <url>http://repo.spring.io/milestone</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-snapshots</id>
            <name>Spring Snapshots</name>
            <url>http://repo.spring.io/snapshot</url>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </pluginRepository>
        <pluginRepository>
            <id>spring-milestones</id>
            <name>Spring Milestones</name>
            <url>http://repo.spring.io/milestone</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </pluginRepository>
    </pluginRepositories>

</project>
```

