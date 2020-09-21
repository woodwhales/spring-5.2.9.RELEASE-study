# spring-5.2.9.RELEASE-study

## 安装 spring-5.2.9-RELEASE 源码步骤

### 步骤一

在项目根目中找到`build.gradle`文件，在大约 280 行处的 repositories 配置里增加：`maven { url 'https://maven.aliyun.com/nexus/content/groups/public/' }`和`maven { url 'https://maven.aliyun.com/nexus/content/repositories/jcenter'}`。

```groovy
repositories {
    maven { url 'https://maven.aliyun.com/nexus/content/groups/public/' }
	maven { url 'https://maven.aliyun.com/nexus/content/repositories/jcenter'}
    mavenCentral()
    maven { url "https://repo.spring.io/libs-spring-framework-build" }
    maven { url "https://repo.spring.io/milestone" } // Reactor
}
```

### 步骤二

在项目根目中找到`settings.gradle`文件，在第 1 行处的 pluginManagement 配置里增加：`maven { url 'https://maven.aliyun.com/repository/gradle-plugin' }`和`maven { url "https://maven.aliyun.com/repository/public" }`。

```groovy
pluginManagement {
	repositories {
		maven { url 'https://maven.aliyun.com/repository/gradle-plugin' }
        maven { url "https://maven.aliyun.com/repository/public" }
		gradlePluginPortal()
		maven { url 'https://repo.spring.io/plugins-release' }
	}
}
```

### 步骤三

修改`gradle.properties`文件，设置`org.gradle.jvmargs`参数值为：-Xmx2048M

```properties
version=5.2.9.RELEASE
## 设置此参数主要是编译下载包会占用大量的内存，可能会内存溢出
org.gradle.jvmargs=-Xmx2048M
## 开启 Gradle 缓存
org.gradle.caching=true
## 开启并行编译
org.gradle.parallel=true
## 启用新的孵化模式
org.gradle.configureondemand=true
## 开启守护进程 通过开启守护进程，下一次构建的时候，将会连接这个守护进程进行构建，而不是重新fork一个gradle构建进程
org.gradle.daemon=true
```

### 步骤四

在项目根目录的文件资源目录框中输入：cmd，在当前项目根目录下创建一个 cmd 窗口，执行：

```cmd
gradlew :spring-oxm:compileTestJava
```

命令，当出现如下字样时：

```cmd
Downloading https://services.gradle.org/distributions/gradle-6.6.1-bin.zip
..
```

按 ctrl + c 停止该下载任务，将 gradle 包地址在浏览器中输入，浏览器会自动下载 gradle 包。

将下载好的 gradle 包放到：%GRADLE_USER_HOME%\wrapper\dists\gradle-6.6.1-bin\du4tvj86lhti6iga1v8h7pckb 文件夹目录下。在这个文件夹里有：上述下载任务时创建的，进入该目录下，将里面的未下载完成文件删除。

> GRADLE_USER_HOME 是在系统的环境变量里配置的，笔者配置的值就是maven本地仓库的根目录。

再次执行`gradlew :spring-oxm:compileTestJava`命令编译源码。

### 步骤五

使用超级管理员模式启动 windows terminal 程序，执行：`./gradlew :spring-oxm:compileTestJava`命令，耐心等待编译完成。

### 步骤六

执行 java -jar aspectj-1.9.5.jar 将 aspectj-1.9.5.jar 安装到本地某个目录。并在 IDEA 中安装 Aspectj weaver 插件。

在 IDEA 中出现 aop 模块相关报错，可以参考：https://www.cnblogs.com/qubo520/p/13264036.html?utm_source=tuicool

参考资料：

https://www.cnblogs.com/qubo520/p/13264036.html

https://www.cnblogs.com/liuyangfirst/p/13526619.html

https://gitee.com/zhong96/spring-framework-analysis

https://gitee.com/zhong96/spring-framework-analysis/blob/master/docs/Spring%E6%BA%90%E7%A0%81%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA.md