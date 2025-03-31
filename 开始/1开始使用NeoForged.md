## 开始使用NeoForged

这一章节将包含如何创建NeoForged的开发环境，以及如何运行，测试你的模组。

## 先决条件

1. 熟悉JAVA，尤其是面向对象，多态，泛型，函数式编程等。
2. 安装Java 21开发工具包（JDK）和64位Java虚拟机（JVM）。NeoForged推荐 [微软的OpenJDK](https://learn.microsoft.com/en-us/java/openjdk/download#openjdk-21)，不过其他的JDK也可以正常使用。

__警告__
确保你使用的是64位的jvm，一种检验的方式就是在你的终端中输入`java --version`(~~译：真的还有32位的JVM吗~~)

3. 选择你熟悉的ide
	* NeoForge推荐使用IntelliJ IDEA和Eclipse，两者都集成了Gradle支持。不过任何IDE都行，从Netbeans Visual Studio Code 到Vim Emacs。
4. 熟悉Git和GitHub。这项技能不是必要的，但它能让你的生活更轻松。

---

## 设置开发环境
打开github仓库上的 模组开发者工具包 (Mod Developer Kit/MDK)(ModDevGradle或者是NeoGradle)点击`Use this template`(使用此模版)然后将新创建的仓库clone到你的电脑上。

	译：选择`Use this template`后选择`Create a new repository`(创建新仓库)，进入了创建仓库的界面，填写仓库名后创建仓库。然后把你刚创建的仓库clone下来。


* 你也可以选择下载仓库的ZIP(点Code下面的->Download ZIP)并解压它。

打开你的IDE并导入gradle工程，Eclipse和IDEA会为你自动导入。如果你的IDE并不会帮你导入，你也可以在终端输入gradlew实现。

	译：国内gradle下载慢的话，打开gradle/wrapper/gradle-wrapper.properties文件修改distributionUrl为国内镜像
	一下是一些国内的gradle镜像地址：
	腾讯
	https://mirrors.cloud.tencent.com/gradle/
	阿里
	https://mirrors.aliyun.com/macports/distfiles/gradle/ 

	
* 在你第一次执行时，Gradle将会下载NeoForge的全部依赖，下载mc本体并反编译，这可能要花一些时间(约1h，取决于你的电脑性能和网络)

		译：如果中途失败，可以尝试删除.gradle文件夹(windows c:/User/<你的用户名>/.gradle macos和linux ~/Users/<你的用户名>/.gradle)然后重新导入.

* 当你修改Gradle相关文件后，需要Gradle重新载入，可以使用ide上面的Reload Gradle按钮，或是在终端中再次输入gradlew。

---

## 定制你的mod信息

许多mod的基本属性可以在 `gradle.properties` 文件中修改。像是模组名称，版本。想了解详细信息，可以看 `gradle.properties` 上的注释，或者是 [gradle.properties 文档]()。

如果你想修改构建过程之外的部份，你需要编辑 `build.gradle`。NeoGradle 即 NeoForge的Gradle插件提供了一些了配置选项，其中一些以解释以注释的形式标记在 `build.gradle` 中。想要完整文档，请查看NeoGradle documentation.

__警告__
除非你知道你在做什么，否则不要编辑build.gradle 和 settings.gradle，所有的基础属性都可以通过gradle.properties设置。

---

## 构建并测试你的mod

运行gradlew build。这将在build/libs中输出一个名为`<archivesBaseName>-<version>.jar`的文件。`<archivesBaseName>`和`<version>`是`build.gradle`设置的属性，默认为`mod_id`和`mod_version`的值分别对应于`gradle.properties`文件中的`mod_id`和`mod_version`属性。如果你愿意，你可以在`build.gradle`中修改它们。输出的jar文件可以放到mods文件夹下，或者是直接上传到模组发布平台上。

在测试环境中运行你的mod，你可以使用生成的运行配置，或者使用关联的任务（例如gradlew runClient）。这将从相应的运行目录中启动Minecraft（例如runs/client或runs/server），并附带任何指定的源集。MDK的默认版本包括主源集，因此任何在src/main/java中编写的代码都会被应用。

## 服务端测试

如果你正在运行一个专用服务器，无论是通过运行配置还是gradlew runServer，服务器都会立即关闭。你需要通过在运行目录中编辑eula.txt文件来接受Minecraft的EULA。

一旦接受，服务器将加载并变为可用，在localhost（或127.0.0.1）上。但是，你将仍然无法加入，因为服务器将默认使用在线模式，该模式需要身份验证（Dev玩家没有）。要解决这个问题，停止你的服务器，并在server.properties文件中设置online-mode属性为false。现在，重新启动服务器就可以正常链接了。

提示
你应该始终在服务器环境中测试你的mod。也包括只在客户端使用的模组，因为它们不应该在服务器上加载任何东西。