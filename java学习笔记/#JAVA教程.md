# JAVA教程



## Java 基础知识

- JDK = JRE + Java开发工具（如编译工具javac.exe）

- JRE = JVM + **核心类库**

- Java核心类库：Java自带很多实用的包，这些包中定义了很多类库

- 环境变量配置作用：为dos在任意目录，都可以直接使用javac和java命令

- 环境变量配置方法：

  1. 此电脑->属性->高级系统设置->环境变量->设置JAVA_HOME = 指向JDK安装的主目录`D:\JDK8\jdk8`

     /*这里变量是用户变量 如naruto的用户变量：意思是对当前用户生效的环境变量，而系统变量是对所有用户都生效的环境变量*/

  2. 也是在环境变量中找到 path，编辑path变量，添加`%JAVA_HOME%\bin`

     /*这里的%JAVA_HOME%相当于D：\JDK8\jdk8这个路径，用JAVA_HOME是为了后面如果要修改，可以直接修改JAVA_HOME这个变量的路径指向而不是直接修改路径*/

- Java代码编写步骤

  1. 编写代码
  2. javac 编译 ，得到对应的`.class`字节码文件
  3. java 运行 ，本质是将 `.class`文件加载到 JVM 中运行

 ## Java快速入门--hello world

+ hello world 的编译 在cmd中用javac hello.java来编译

- 如果加了中文注释，有可能编译失败，因为格式对不上，在cmd中的属性看使用的是GBK格式，在sublime的file里将save with encoding改为GBK保存之后，即可编译成功

+ cmd中 在编译之后，用java hello 即可运行，不要用java hello.class这样会找不到类，因为java后面就是类名

- cmd使用技巧，上键可以直接调用上一个指令，Tab是快速补全

  

## Java执行流程

- .java文件 通过javac编译生成 .class文件**（字节码文件）**
- 通过java将.class文件装载到**JVM虚拟机**运行文件



## Java开发细节

- java源文件以.java为拓展名，基本组成部分是**类（class）**如hello类

- Java应用程序的执行入口是main（）方法书写格式是

  ```java
  public static void main(String [] args){
      ···
  }
  ```

- 一个源文件最多只能有==一个public类== 若一个类里面有多个类，编译源文件之后这几个类都会被编译成对应的class文件

- 源文件名必须和public类的类名一致（这也是为什么public类只能有一个）

- public类只能有一个，但其他的类不做限制

- **可以将main方法写进非public类中，然后指定运行非public类，这样入口方法就是非public的main方法**

  ```java
  public class Hello{
      public static void main(String [] args){
          System.out.println("hello world");
      }
  }
  class Dog{
      public static void main(String [] args){
          System.out.println("hello dog");
      }
  }
  class Tiger{
     public static void main(String [] args){
          System.out.println("hello tiger");
      }
  }
  ```

  **在cmd中编译源文件之后会形成三个.class文件 分别是Hello.class/Dog.class/Tiger.class**

  **下面可以运行三个主方法**

  1. `java Hello `    输出 `hello world`
  2. `java Dog`输出`hello dog`
  3. `java Tiger`输出`hello tiger`

- **注意不能在去掉main方法就打印，会报错**

  ```java
  class Dog{
      System.out.println("hello dog");
  }
  //这样是绝对错误的！！！
  ```



## Java转义字符

- ctrl+/是多行注释的快捷键

- Tab可以快速补全cmd指令，用法就是：输入javac Change 按下Tab 直接补全为 javac ChangeChar.java

- Java常用转义字符

  1. \t：一个制表位，实现对齐的功能**（左对齐）**

     ```java
     System.out.println("北京\t上海\t广州");
     //结果是
     北京	上海	广州
     ```

  2. \n:换行符

     ```java
     System.out.println("jack\nsmith\nmary");
     //输出结果
     jack
     smith
     mary
     ```

  3. \\\：一个\

     ```java
     //System.out.println("D:\javacode") 这里一定会报错，因为\会连着后面的j，要么是变成其他转义字符，要么就是直接报错。
     System.out.println("D:\\javacode");
     //用\\来表示一个\ 这也是为什么磁盘路径是单斜杠，但在代码里写磁盘路径都得用双斜杠，因为两个双斜杠才表示一个单斜杠
     //要是想表是\\双斜杠，就得用\\\\四个斜杠来表示双斜杠
     ```

     

  4. \\"：一个"

     ```java
     System.out.println("我说：“好好学java”");//完全没问题，因为""里面的是中文的“”所以不会有歧义
     输出：我说：“好好学java”
     System.out.println("我说："asdasdasd"");//错误！！，因为""里面的是英文的""起冲突了。
     报错！！
     System.out.println("我说：\"asdasfvs\"");//完全没问题，因为可以用\"表示一个"是字符串一部分
     输出：我说："asdasdasd"
     ```

  5. \\':一个'

     ```java
     System.out.println("我说:\'sadasdasd\'");
     输出：我说'sadasdasd'
     ```

  6. \r:回车**回退到本行第一个字符**

     ```java
     System.out.println("韩顺平教育\r北京");
     输出：北京平教育
     //原因是：先输出韩顺平教育 再回车光标回退到第一个字符 韩，然后输出北京，覆盖了韩顺两个字
     System.out.println("韩顺平教育\r\n北京");
     韩顺平教育
     北京
     ```

     

## Java 易犯错误

- 找不到文件

  问题：当出现**找不到文件**信息，一般是cmd中文件名写错了

- 公共类与文件名不匹配

  问题：当出现**····是公共的**，一般是主类（公共类）与文件名不一致

- 忘记写分号了

  问题：出现提示信息 第几行需要分号



## Java 注释

- 单行注释

- 多行注释：多行注释里面切记不要再加入多行煮熟

  ```java
  /*
  	····
  	/*
      ···
  	*/
  */
  这样会出错！！因为/*表示注释开始，*/表示注释结束，这里嵌套多行注释，再遇到第一个*/就表示注释结束，下面的*/就被孤立，会报错！！
  ```

- 文档注释：

  （注释内容可以被JDK提供的工具javadoc所解析，生成一套用网页文件形式体现的该程序的说明文档）

  - 基本格式

  ```java
  /**
   *@author szd 
   *@version  1.0
  */
  文档注释的固定格式：多行注释的形式，第一行多加一个*，此后注释里每写一行都要加* 然后加@author之类的javadoc标签
  ```

  - 如何生成对应的文档注释

    在cmd中输入

    `javadoc -d 目标文件名（文档注释放在哪里）-xx -yy（生成的javadoc标签）源文件名.java`

    例： `javadoc -d d:\\temp -author -version Comment.java`

    **注意，这里的目标文件 的路径用\\**\

    tips：cmd中的cls是清屏指令

  - 生成实例：打开目标文件夹里的index.html即可看到文档注释

## Java 补充 Typora上传至github

- 在github上创建repository，复制地址
- 打开md文件所在处，右键点击git Bash here（若是在desktop打开的 用cd指令进入md文件所在处）
  1. git clone https://github.com/fsbbts/Java_Note.git 本地与github建立联系
  2. git add *
  3. git commit -m "这里写一些文字说明"
  4. git push -u origin main
- 后续更新
  1. 更新md文件后保存
  2. git add *
  3. git commit -m "文字说明"
  4. git push -u origin main



## Java 代码规范

1. 类，方法用javadoc来写
2. 非javadoc注释，用单行/多行注释，用以给代码维护者看
3. 整体后移：选中之后按Tab
4. 整体前移：选中之后按shift+Tab
5. 运算符和 = 两边多加一个空格
6. 源文件用 utf-8进行编码，这里是因为在DOS系统中有中文字符不得已用GBK，正常都是用utf-8
7. 编码使用：行尾风格/次行风格



## Java DOS命令(不是重点)

**相对路径与绝对路径**

相对路径：从当前目录开始定位，形成一个路径

`..\..\abc2\test200\hello.txt`

绝对路径：从顶级目录d，开始定位，形成一个路径

`d:\abc2\test200\hello.txt`

1. 查看当前目录：`dir`   `dir d:\abc2\test200`
2. 切换根目录 `cd \D c:`
3. 切换到当前目录其他目录下`cd d:\abc2\test200`   `cd ..\..\abc2\test200`
4. 切换到上一级`cd ..`
5. 切换到根目录`cd \`
6. 查看当前目录的所有子目录 `tree d:` `tree d:\abc2`
7. 清屏`cls`
8. 退出DOS `exit`



## Java
