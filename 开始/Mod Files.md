# Mod Files

模组文件负责确定哪些模组被打包到你的JAR中，以及如何显示在“模组”菜单中，以及在游戏中如何加载你的模组。

---

## gradle.properties

gradle.properties文件存储了模组的一些常见属性，如模组id或模组和版本。在构建过程中，Gradle会读取这些文件中的值，并在各种地方链接这些值，如neoforge.mods.toml。这样，您只需要在某个地方更改值，然后就能应用到所有地方。

大部分值的说明都在MDK的gradle.properties文件中进行了注释。

|  属性   | 描述  | 例子 |
|  ----  | ----  | --- |
| org.gradle.jvmargs  | 允许你传递给Gradle的额外JVM参数。用于分配给Gradle更多的/更少的内存。请注意，这是为Gradle本身，而不是Minecraft。 | org.gradle.jvmargs=-Xmx3G |
| org.gradle.daemon  | 当Gradle构建时，是否使用守护进程。 | org.gradle.daemon=false |

