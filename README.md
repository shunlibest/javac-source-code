# javac-source-code
本项目是从openjdk官网(http://hg.openjdk.java.net/jdk8/jdk8/langtools/ )下载的项目.
把源码目录的 src/share/classes/com 目录整个拷贝到项目 src 目录下。

## 直接运行
找到 javac 主函数入口，代码在src/com/sun/tools/javac/Main.java目录下

直接运行的话，将会直接输出以下信息，这是因为没有加需要编译的源代码路径；
```
用法: javac <options> <source files>
其中, 可能的选项包括:
  -g                         生成所有调试信息
  -g:none                    不生成任何调试信息
  -g:{lines,vars,source}     只生成某些调试信息
  -nowarn                    不生成任何警告
  -verbose                   输出有关编译器正在执行的操作的消息
  -deprecation               输出使用已过时的 API 的源位置
  -classpath <路径>            指定查找用户类文件和注释处理程序的位置
  -cp <路径>                   指定查找用户类文件和注释处理程序的位置
  -sourcepath <路径>           指定查找输入源文件的位置
  -bootclasspath <路径>        覆盖引导类文件的位置
  -extdirs <目录>              覆盖所安装扩展的位置
  -endorseddirs <目录>         覆盖签名的标准路径的位置
  -proc:{none,only}          控制是否执行注释处理和/或编译。
  -processor <class1>[,<class2>,<class3>...] 要运行的注释处理程序的名称; 绕过默认的搜索进程
  -processorpath <路径>        指定查找注释处理程序的位置
  -parameters                生成元数据以用于方法参数的反射
  -d <目录>                    指定放置生成的类文件的位置
  -s <目录>                    指定放置生成的源文件的位置
  -h <目录>                    指定放置生成的本机标头文件的位置
  -implicit:{none,class}     指定是否为隐式引用文件生成类文件
  -encoding <编码>             指定源文件使用的字符编码
  -source <发行版>              提供与指定发行版的源兼容性
  -target <发行版>              生成特定 VM 版本的类文件
  -profile <配置文件>            请确保使用的 API 在指定的配置文件中可用
  -version                   版本信息
  -help                      输出标准选项的提要
  -A关键字[=值]                  传递给注释处理程序的选项
  -X                         输出非标准选项的提要
  -J<标记>                     直接将 <标记> 传递给运行时系统
  -Werror                    出现警告时终止编译
  @<文件名>                     从文件读取选项和文件名
```
### 添加要编译文件的路径
* 新建一个HelloWorld.java文件，在启动配置的Program arguments里加入 HelloWorld.java 的绝对路径。
  ![image](https://user-images.githubusercontent.com/32166825/147623754-306b2f3d-9f82-411d-b4c2-730bedcf8d6c.png)

* 在这里添加要编译的Java文件绝对路径即可
  ![image](https://user-images.githubusercontent.com/32166825/147623796-59286ae6-f211-4586-978f-e861b0ef2b30.png)

* 再次点击运行，会在 HelloWorld.java 的同级目录生成 HelloWorld.class 文件。

## 再次运行
第一次，我是直接进入到该class的目录下，执行class文件，会输出以下错误
```
➜  Documents java HelloWorld                                          
   错误: 找不到或无法加载主类 HelloWorld
```
搜索了一下，发现进入的路径是有问题，要进入到com/目录的上一级目录，然后再执行，执行的时候，需要加上包名, 这样就成功运行了
```
➜  java java com.shunli.HelloWorld
   hello
```

## 调试
在 Main.java 中打上断点，开始调试以后会发现不管怎么设置，调试都会进入tool.jar，没有走刚刚导入的源码。
所以需要打开 Project Structure 页面（File->Project Structure）， 选中图中 Dependencies 选项卡，把<Moudle source>顺序调整到项目 JDK 的上面：
![20784247-cafb53969f5328b9](https://user-images.githubusercontent.com/32166825/147624488-29aa6c27-6768-431d-b2a7-708c2693253c.jpeg)
或者这种
![image](https://user-images.githubusercontent.com/32166825/147625132-7a5e8424-5dbd-48d0-8d0c-2bf8941d3dd5.png)

这样，我们就可以开心愉快的学习了
